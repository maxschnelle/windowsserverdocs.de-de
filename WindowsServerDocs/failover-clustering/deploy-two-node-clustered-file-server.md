---
title: Bereitstellen eines Cluster Dateiservers mit zwei Knoten
description: In diesem Artikel wird das Erstellen eines Dateiserver Clusters mit zwei Knoten beschrieben.
manager: eldenc
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 02/01/2019
ms.openlocfilehash: 56130833ca2c3de8752fb79f5acdf30a1fafae2f
ms.sourcegitcommit: 67a486b4fb3937a457eb00d21a2e33b753489fd8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88149554"
---
# <a name="deploying-a-two-node-clustered-file-server"></a>Bereitstellen eines Cluster Dateiservers mit zwei Knoten

> Gilt für: Windows Server 2019, Windows Server 2016

Ein Failovercluster besteht aus einer Gruppe von unabhängigen Computern, die miteinander interagieren und somit die Verfügbarkeit von Anwendungen und Diensten erhöhen. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn auf einem der Clusterknoten ein Fehler auftritt, werden seine Aufgaben sofort auf einen anderen Knoten übertragen. Dies wird als Failover bezeichnet. So ergeben sich für die Benutzer nur minimale Unterbrechungen des Betriebs.

In dieser Anleitung werden die Schritte zum Installieren und Konfigurieren eines allgemeinen Dateiserver-Failoverclusters mit zwei Knoten beschrieben. Wenn Sie die Konfiguration in dieser Anleitung erstellen, können Sie sich über Failovercluster informieren und sich mit der Snap-in-Schnittstelle für Failoverclusterverwaltung in Windows Server 2019 oder Windows Server 2016 vertraut machen.

## <a name="overview-for-a-two-node-file-server-cluster"></a>Übersicht über einen Dateiservercluster mit zwei Knoten

Server in einem Failovercluster können in einer Vielzahl von Rollen eingesetzt werden, einschließlich der Rollen von Dateiserver, Hyper-V-Server oder Datenbankserver. Sie können Hochverfügbarkeit für eine Vielzahl anderer Dienste und Anwendungen bereitstellen. In dieser Anleitung wird die Konfiguration eines Dateiserverclusters mit zwei Knoten beschrieben.

Ein Failovercluster enthält normalerweise eine Speichereinheit, die mit allen Servern im Cluster physisch verbunden ist, obwohl auf jedes Volume im Speicher immer nur von je einem Server zugegriffen wird. Im folgenden Diagramm finden Sie einen Failovercluster mit zwei Knoten, der an mit einer Speichereinheit verbunden ist.

![Cluster mit zwei Knoten](media/Cluster-File-Server/Cluster-FS-Overview.png)

Die für die Knoten eines Clusters offen gelegten Speichervolumes oder logischen Gerätenummern (Logical Unit Numbers, LUNs) müssen für andere Server, einschließlich der Server in einem anderen Cluster, nicht offen gelegt werden. Dies wird im folgenden Diagramm veranschaulicht.

![LUNs im Speicher](media/Cluster-File-Server/Cluster-FS-LUNs.png)

Beachten Sie, dass im Sinne einer optimalen Serververfügbarkeit bewährte Methoden der Serververwaltung zu befolgen, z. B. das sorgfältige Verwalten der physischen Umgebung der Server, das Testen von Softwareänderungen vor der vollständigen Implementierung und das gründliche Nachverfolgen von Softwareupdates und Konfigurationsänderungen auf allen geclusterten Servern.

Das folgende Szenario beschreibt, wie ein Dateiserver-Failovercluster konfiguriert werden kann. Die Dateien, die freigegeben werden sollen, befinden sich auf der Clusterspeichereinheit, und jeder Clusterserver kann als der Dateiserver fungieren, der diese freigibt.

## <a name="shared-folders-in-a-failover-cluster"></a>Freigegebene Ordner in einem Failovercluster

In der folgenden Liste werden die Konfigurationsfunktionen für freigegebene Ordner beschrieben, die in Failoverclustering integriert sind:

- Die Anzeige ist auf freigegebene Clusterordner beschränkt (keine Vermischung mit nicht gruppierten freigegebenen Ordnern): Wenn ein Benutzer freigegebene Ordner durch Angabe des Pfads eines gruppierten Dateiservers anzeigt, enthält die Anzeige nur die freigegebenen Ordner, die Teil der jeweiligen Dateiserver Rolle sind. Nicht gruppierte freigegebene Ordner werden ausgeschlossen, und es wird ein Teil von separaten Dateiserver Rollen verwendet, die sich auf einem Cluster Knoten befinden.

- Zugriffs basierte Enumeration: Sie können die Zugriffs basierte Enumeration verwenden, um einen angegebenen Ordner in der Benutzeransicht auszublenden. Anstatt den Ordner für den Benutzer anzuzeigen, ihn jedoch nicht darauf zugreifen zu lassen, können Sie den Ordner einfach ganz ausblenden. Sie können die Zugriffs basierte Enumeration für einen geclusterten freigegebenen Ordner auf die gleiche Weise wie für einen nicht gruppierten freigegebenen Ordner konfigurieren.

- Offline Zugriff: Sie können den Offline Zugriff (Caching) für einen geclusterten freigegebenen Ordner auf die gleiche Weise wie für einen nicht gruppierten freigegebenen Ordner konfigurieren.

- Geclusterte Datenträger werden immer als Teil des Clusters erkannt: unabhängig davon, ob Sie die Failoverclusterschnittstelle, Windows-Explorer oder das Freigabe-und Speicher Verwaltungs-Snap-in verwenden, erkennt Windows, ob ein Datenträger als im Cluster Speicher festgelegt wurde. Wenn ein solcher Datenträger bereits in der Failoverclusterverwaltung als Teil eines Cluster Dateiservers konfiguriert wurde, können Sie mithilfe einer der oben erwähnten Schnittstellen eine Freigabe auf dem Datenträger erstellen. Wenn der Datenträger nicht als Teil eines Clusterdateiservers konfiguriert wurde, ist es nicht möglich, versehentlich eine Freigabe darauf zu erstellen. Stattdessen gibt eine Fehlermeldung an, dass der Datenträger zuerst als Teil eines Clusterdateiservers konfiguriert werden muss, bevor er freigegeben werden kann.

- Integration von Services for Network File System: die Rolle "Datei Server" in Windows Server umfasst den optionalen Rollen Dienst "Dienste für NFS (Network File System)". Durch Installieren des Rollendiensts und Konfigurieren von freigegebenen Ordner mit Diensten für NFS können Sie einen Clusterdateiserver erstellen, der UNIX-basierte Clients unterstützt.

## <a name="requirements-for-a-two-node-failover-cluster"></a>Anforderungen für einen Failovercluster mit zwei Knoten

Damit ein Failovercluster in Windows Server 2016 oder Windows Server 2019 als offiziell unterstützte Lösung von Microsoft angesehen wird, muss die Lösung die folgenden Kriterien erfüllen.

- Alle Hardware- und Softwarekomponenten müssen die Qualifikationen für das entsprechende Logo erfüllen. Für Windows Server 2016 ist dies das Logo "Certified for Windows Server 2016". Für Windows Server 2019 ist dies das Logo "Certified for Windows Server 2019". Weitere Informationen dazu, welche Hardware-und Softwaresysteme zertifiziert wurden, finden Sie auf der Microsoft [Windows Server-Katalog](https://www.windowsservercatalog.com/default.aspx) Website.

- Die vollständig konfigurierte Lösung (Server, Netzwerk und Speicher) muss alle Tests im Validierungs-Assistenten bestehen, der Teil des Failovercluster-Snap-Ins ist.

Für einen Failovercluster mit zwei Knoten ist Folgendes erforderlich:

- **Server:** Es wird empfohlen, übereinstimmende Computer mit denselben oder ähnlichen Komponenten zu verwenden.  Auf den Servern für einen Failovercluster mit zwei Knoten muss die gleiche Version von Windows Server ausgeführt werden. Sie sollten auch die gleichen Software Updates (Patches) enthalten.

- **Netzwerkadapter und Kabel:** Die Netzwerkhardware muss wie andere Komponenten in der Failoverclusterlösung mit Windows Server 2016 oder Windows Server 2019 kompatibel sein. Wenn Sie iSCSI verwenden, müssen die Netzwerkadapter entweder für die Netzwerkkommunikation oder für iSCSI, nicht jedoch für beides dediziert sein. Vermeiden Sie in der Netzwerkinfrastruktur, über die die Clusterknoten verbunden sind, die Verwendung von Komponenten, deren Ausfall einen Ausfall des Gesamtsystems zur Folge hätte. Es gibt mehrere Methoden, dies zu erreichen. Sie können die Clusterknoten durch mehrere unterschiedliche Netzwerke verbinden. Zudem können Sie die Clusterknoten mit einem Netzwerk verbinden, das aus Netzwerkadapterteams, redundanten Switches, redundanten Routern oder ähnlicher Hardware besteht, die einzelne Fehlerpunkte beseitigt.

   > [!NOTE]
   > Wenn die Cluster Knoten mit einem einzelnen Netzwerk verbunden sind, übergibt das Netzwerk die Redundanz Anforderung im Konfigurationsüberprüfungs-Assistenten.  Der Bericht enthält jedoch eine Warnung, dass das Netzwerk keine Single Point of Failure haben sollte.

- **Geräte Controller oder geeignete Adapter für den Speicher:**
    - **Serielle angehängte SCSI-oder-Fibre Channel:** Wenn Sie Serial Attached SCSI oder Fibre Channel verwenden, sollten alle Komponenten des Speicher Stapels auf allen Cluster Servern identisch sein. Es ist erforderlich, dass die Multipfad-e/a (MPIO)-Software und DSM-Softwarekomponenten (Device Specific Module) identisch sind.  Es wird empfohlen, identische Massenspeichergerätecontroller zu verwenden, d. h. Hostbusadapter (HBA), HBA-Treiber und HBA-Firmware. Wenn Sie unterschiedliche HBAs verwenden, sollten Sie gemeinsam mit dem Speicheranbieter überprüfen, ob die unterstützten oder empfohlenen Konfigurationen eingehalten werden.
    - **iSCSI:** Wenn Sie iSCSI verwenden, muss jeder Cluster Server über mindestens einen Netzwerkadapter oder Hostbus Adapter verfügen, der für den iSCSI-Speicher reserviert ist. Das Netzwerk, das Sie für iSCSI verwenden, kann nicht für die Netzwerkkommunikation verwendet werden. Die zum Herstellen von Verbindungen mit dem iSCSI-Speicherziel verwendeten Netzwerkadapter müssen für alle Clusterserver identisch sein, und es empfiehlt sich, Gigabit Ethernet oder höher zu verwenden.

- **Speicher:** Sie müssen freigegebenen Speicher verwenden, der für Windows Server 2016 oder Windows Server 2019 zertifiziert ist.

    Bei einem Failovercluster mit zwei Knoten sollte der Speicher mindestens zwei separate Volumes (LUNs) enthalten, wenn ein Zeugen Datenträger für das Quorum verwendet wird. Bei einem Zeugendatenträger handelt es sich um einen Datenträger im Clusterspeicher, auf dem eine Kopie der Clusterkonfigurationsdatenbank gespeichert ist. Bei diesem Beispiel für einen Cluster mit zwei Knoten ist die Quorum Konfiguration Knoten-und Datenträger Mehrheit. Knoten- und Datenträgermehrheit bedeutet, dass die Knoten und der Zeugendatenträger jeweils Kopien der Clusterkonfiguration enthalten. Der Cluster besitzt das Quorum, solange die Mehrheit dieser Kopien (zwei von drei) verfügbar ist. Das andere Volume (LUN) enthält die Dateien, die für die Benutzer freigegeben werden.

    Die Speicheranforderungen beinhalten Folgendes:

    - Um die systemeigene, im Failoverclustering enthaltene Datenträgerunterstützung verwenden zu können, müssen anstelle von dynamischen Datenträgern Basisdatenträger verwendet werden.
    - Die Formatierung als NTFS-Partitionen wird empfohlen (die Partition des Zeugendatenträgers muss NTFS-formatiert sein).
    - Als Partitionsstil des Datenträgers können Sie entweder MBR (Master Boot Record) oder GPT (GUID-Partitionstabelle) verwenden.
    - Der Speicher muss ordnungsgemäß auf bestimmte SCSI-Befehle Antworten. der Speicher muss dem Standard entsprechen, der als SCSI Primary Commands-3 (SPC-3) bezeichnet wird. Insbesondere muss der Speicher permanente Reservierungen unterstützen, wie im SPC-3-Standard angegeben.
    -  Der für den Speicher verwendete Miniporttreiber muss mit dem StorPort-Speichertreiber von Microsoft kompatibel sein.

## <a name="deploying-storage-area-networks-with-failover-clusters"></a>Bereitstellen von SANs (Storage Area Networks) mit Failoverclustern

Beim Bereitstellen einer Storage Area Network (San) mit einem Failovercluster sollten die folgenden Richtlinien beachtet werden.

- **Bestätigen Sie die Zertifizierung des Speichers:** Bestätigen Sie mithilfe der [Windows Server-Katalog](https://www.windowsservercatalog.com/default.aspx) Website, dass der Speicher des Anbieters, einschließlich der Treiber, Firmware und Software, für Windows Server 2016 oder Windows Server 2019 zertifiziert ist.

- **Isolieren Sie Speichergeräte, einen Cluster pro Gerät:** Server aus unterschiedlichen Clustern dürfen nicht auf dieselben Speichergeräte zugreifen können. In den meisten Fällen sollte eine LUN, die für einen Satz von Clusterservern verwendet wird, durch LUN-Maskierung oder -Zoneneinteilung von allen anderen Servern isoliert werden.

- **Verwenden Sie ggf. Multipfad-e/a-Software:** In einer hoch verfügbaren speicherfabric können Sie mithilfe von Multipfad-e/a-Software Failovercluster mit mehreren Hostbus Adaptern bereitstellen. Auf diese Weise erhalten Sie den höchsten Grad an Redundanz und Verfügbarkeit. Die Multipfadlösung muss auf Microsoft Multipfad-e/a (MPIO) basieren. Der Speicherhardware Hersteller kann ein Geräte spezifisches MPIO-Modul (DSM) für die Hardware bereitstellen, obwohl Windows Server 2016 und Windows Server 2019 mindestens eine DSMs als Teil des Betriebssystems enthalten.

## <a name="network-infrastructure-and-domain-account-requirements"></a>Anforderungen an die Netzwerkinfrastruktur und das Domänenkonto

Für einen Failovercluster mit zwei Knoten benötigen Sie die folgende Netzwerkinfrastruktur und ein Administratorkonto mit den folgenden Domänenberechtigungen:

- **Netzwerkeinstellungen und IP-Adressen:** Wenn Sie für ein Netzwerk identische Netzwerkadapter verwenden, verwenden Sie auch identische Kommunikationseinstellungen auf diesen Adaptern (z. b. Geschwindigkeit, Duplex Modus, Fluss Steuerung und Medientyp). Vergleichen Sie zudem die Einstellungen zwischen dem Netzwerkadapter und dem Switch, zu dem eine Verbindung hergestellt wird, und stellen Sie sicher, dass die Einstellungen nicht miteinander in Konflikt stehen.

    Wenn Sie über private Netzwerke verfügen, die nicht an die übrige Netzwerkinfrastruktur weitergeleitet werden, muss sichergestellt werden, dass jedes dieser privaten Netzwerke ein eindeutiges Subnetz verwendet. Dies ist auch dann erforderlich, wenn jeder Netzwerkadapter über eine eindeutige IP-Adresse verfügt. Wenn Sie beispielsweise in einer Zentrale mit einem physischen Netzwerk über einen Clusterknoten und in einer Filiale mit einem separaten physischen Netzwerk über einen weiteren Knoten verfügen, sollte 10.0.0.0/24 selbst dann nicht für beide Netzwerke angegeben werden, wenn Sie jedem Adapter eine eindeutige IP-Adresse zuweisen.

    Weitere Informationen zu den Netzwerkadaptern finden Sie weiter oben in dieser Anleitung unter Hardwareanforderungen für einen Failovercluster mit zwei Knoten.

- **DNS:** Die Server im Cluster müssen für die Namensauflösung Domain Name System (DNS) verwenden. Das Protokoll für das dynamische DNS-Update kann verwendet werden.

- **Domänen Rolle:** Alle Server im Cluster müssen sich in derselben Active Directory Domäne befinden. Als bewährte Methode sollten alle geclusterten Server über dieselbe Domänenrolle verfügen (entweder Mitgliedsserver oder Domänencontroller). Die empfohlene Rolle ist Mitgliedsserver.

- **Domänen Controller:** Es wird empfohlen, dass die geclusterten Server Mitglied Server sind. Ist dies der Fall, benötigen Sie einen zusätzlichen Server, der in der Domäne, die den Failovercluster enthält, als Domänencontroller fungiert.

- **Clients:** Bei Bedarf können Sie einen oder mehrere vernetzte Clients mit dem Failovercluster verbinden, den Sie erstellen, und die Auswirkung auf einen Client beobachten, wenn Sie den Cluster Dateiserver von einem Cluster Knoten zum anderen verschieben oder einen Failover ausführen.

- **Konto zum Verwalten des Clusters:** Wenn Sie zum ersten Mal einen Cluster erstellen oder diesem Server hinzufügen, müssen Sie bei der Domäne mit einem Konto angemeldet sein, das über Administratorrechte und Berechtigungen für alle Server in diesem Cluster verfügt. Dabei muss es sich nicht unbedingt um ein Domänenadministratorenkonto handeln. Es kann auch ein Domänenbenutzerkonto verwendet werden, das der Gruppe "Administratoren" für die einzelnen Clusterserver angehört. Wenn es sich bei dem Konto nicht um ein Domänen-Admins-Konto handelt, muss dem Konto (oder der Gruppe, der das Konto angehört) außerdem die Berechtigung zum **Erstellen von Computer Objekten** und zum **Lesen aller Eigenschaften** in der Domänen Organisationseinheit (OE) erteilt werden, in der sich das Konto befindet.

## <a name="steps-for-installing-a-two-node-file-server-cluster"></a>Schritte zum Installieren eines Dateiserverclusters mit zwei Knoten

Sie müssen die folgenden Schritte ausführen, um einen Dateiserver-Failovercluster mit zwei Knoten zu installieren.

Schritt 1: Verbinden der Cluster Server mit den Netzwerken und dem Speicher

Schritt 2: Installieren des Failoverclusterfeatures

Schritt 3: Überprüfen der Cluster Konfiguration

Schritt 4: Erstellen des Clusters

Wenn Sie die Clusterknoten bereits installiert haben und einen Dateiserver-Failovercluster konfigurieren möchten, finden Sie weiter unten in dieser Anleitung weitere Informationen unter Schritte zum Konfigurieren eines Dateiserverclusters mit zwei Knoten.

### <a name="step-1-connect-the-cluster-servers-to-the-networks-and-storage"></a>Schritt 1: Verbinden der Cluster Server mit den Netzwerken und dem Speicher

Vermeiden Sie in einem Failoverclusternetzwerk einzelne Fehlerpunkte. Es gibt mehrere Methoden, dies zu erreichen. Sie können die Clusterknoten durch mehrere unterschiedliche Netzwerke verbinden. Alternativ können Sie die Clusterknoten mit einem Netzwerk verbinden, das aus kombinierten Netzwerkadaptern, redundanten Switches, redundanten Routern oder ähnlicher Hardware besteht, die einzelne Fehlerpunkte ausschließt (Wenn Sie ein Netzwerk für iSCSI verwenden, müssen Sie dieses Netzwerk zusätzlich zu den anderen Netzwerken einrichten).

Für einen Dateiservercluster mit zwei Knoten müssen Sie mindestens zwei Volumes (LUNs) verfügbar machen, wenn Sie die Server mit dem Clusterspeicher verbinden. Für gründliche Tests der Konfiguration können Sie bei Bedarf zusätzliche Volumes verfügbar machen. Die Clustervolumes dürfen nicht für Server verfügbar gemacht werden, die sich nicht im Cluster befinden.

#### <a name="to-connect-the-cluster-servers-to-the-networks-and-storage"></a>So verbinden Sie den Clusterserver mit den Netzwerken und dem Speicher

1. Lesen Sie die Details zu Netzwerken unter Hardware Anforderungen für einen Failovercluster mit zwei Knoten und Netzwerkinfrastruktur-und Domänen Kontoanforderungen für einen Failovercluster mit zwei Knoten weiter oben in dieser Anleitung.

2. Verbinden und konfigurieren Sie die Netzwerke, die die Server im Cluster verwenden.

3. Wenn die Testkonfiguration Clients oder einen nicht geclusterten Domänencontroller umfasst, stellen Sie sicher, dass diese Computer über mindestens ein Netzwerk eine Verbindung mit den geclusterten Servern herstellen können.

4. Befolgen Sie die Anweisungen des Herstellers zum physischen Verbinden der Server mit dem Speicher.

5. Stellen Sie sicher, dass die Datenträger (LUNs), die Sie im Cluster verwenden möchten, für die zu gruppierenden Server (und zwar ausschließlich für diese Server) bereitgestellt wurden. Sie können Datenträger oder LUNs mit einer der folgenden Schnittstellen verfügbar machen:

    - Die Schnittstelle, die vom Hersteller des Speichers bereitgestellt wird

    - Wenn Sie iSCSI verwenden, eine entsprechende iSCSI-Schnittstelle

6. Wenn Sie Software erworben haben, mit der das Format oder die Funktion des Datenträgers gesteuert wird, befolgen Sie die Anweisungen des Herstellers, um zu erfahren, wie Sie diese Software mit Windows Server verwenden.

7. Klicken Sie auf einem der in den Cluster einzuschließenden Server nacheinander auf Start, Verwaltung, Computerverwaltung und Datenträgerverwaltung. (Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.) Vergewissern Sie sich unter Datenträgerverwaltung, dass die Cluster Datenträger sichtbar sind.

8. Wenn Sie ein Speichervolume mit mehr als zwei Terabyte erstellen möchten und Sie zum Steuern des Datenträgerformats die Windows-Benutzeroberfläche verwenden, konvertieren Sie diesen Datenträger in den Partitionstyp GPT (GUID-Partitionstabelle). Sichern Sie hierzu alle Daten auf dem Datenträger, löschen Sie alle Volumes auf dem Datenträger, klicken Sie in der Datenträgerverwaltung mit der rechten Maustaste auf den Datenträger (nicht jedoch auf eine Partition), und klicken Sie auf In GPT-Datenträger konvertieren.  Für Volumes mit weniger als zwei Terabyte können Sie statt GPT den Partitionstyp MBR (Master Boot Record) verwenden.

9. Überprüfen Sie das Format aller verfügbar gemachten Volumes bzw. LUNs. Es wird empfohlen, als Format NTFS zu verwenden (für den Zeugendatenträger muss NTFS verwendet werden).

### <a name="step-2-install-the-file-server-role-and-failover-cluster-feature"></a>Schritt 2: Installieren der Dateiserver Rolle und des Failoverclusterfeatures

In diesem Schritt werden die Dateiserver Rolle und das Failoverclusterfeature installiert. Auf beiden Servern muss entweder Windows Server 2016 oder Windows Server 2019 ausgeführt werden.

#### <a name="using-server-manager"></a>Verwenden von Server-Manager

1. Öffnen Sie **Server-Manager** , und wählen Sie in der Dropdown-Dropdown- **Verwaltung** **Rollen und Features hinzufügen**.

   ![Hinzufügen eines Features](media/Cluster-File-Server/Cluster-FS-Add-Feature.png)

2. Wenn das Fenster **vor dem Beginn** geöffnet wird, wählen Sie **weiter**aus.

3. Wählen Sie für **Installationstyp**die Option **rollenbasierte oder featurebasierte Installation** und **dann weiter**aus.

4. Stellen Sie sicher, dass **Server aus dem Server Pool auswählen** ausgewählt ist, der Name des Computers hervorgehoben ist und **dann weiter**.

5. Öffnen Sie für die Server Rolle in der Liste der Rollen die **Dateidienste**, und wählen Sie dann **Datei Server**und **weiter**aus.

   ![Add Role](media/Cluster-File-Server/Cluster-FS-Add-FS-Role-1.png)

6. Wählen Sie für die Features in der Liste der Features **Failoverclustering**aus.  Ein Popup Dialogfeld wird angezeigt, in dem die zu installierende Verwaltungs Tools aufgelistet sind.  Behalten Sie alle ausgewählten Optionen bei, wählen Sie **Features hinzufügen** und **weiter**aus.

   ![Hinzufügen eines Features](media/Cluster-File-Server/Cluster-FS-Add-WSFC-1.png)

7. Wählen Sie auf der Seite Bestätigung die Option Installieren aus.

8. Nachdem die Installation abgeschlossen ist, starten Sie den Computer neu.

9. Wiederholen Sie die Schritte auf dem zweiten Computer.

#### <a name="using-powershell"></a>PowerShell

1. Öffnen Sie eine administrative PowerShell-Sitzung, indem Sie mit der rechten Maustaste auf die Schaltfläche Start klicken und dann **Windows PowerShell (admin)** auswählen.
2. Um die Datei Server Rolle zu installieren, führen Sie den folgenden Befehl aus:

    ```PowerShell
    Install-WindowsFeature -Name FS-FileServer
    ```

3. Führen Sie den folgenden Befehl aus, um das Failoverclustering-Feature und seine Verwaltungs Tools zu installieren:

    ```PowerShell
    Install-WindowsFeature -Name Failover-Clustering -IncludeManagementTools
    ```

4. Sobald Sie abgeschlossen sind, können Sie mit den folgenden Befehlen überprüfen, ob Sie installiert sind:

    ```PowerShell
    Get-WindowsFeature -Name FS-FileServer
    Get-WindowsFeature -Name Failover-Clustering
    ```

5. Wenn Sie überprüft haben, starten Sie den Computer mit dem folgenden Befehl neu:

    ```PowerShell
    Restart-Computer
    ```

6. Wiederholen Sie die Schritte auf dem zweiten Server.

### <a name="step-3-validate-the-cluster-configuration"></a>Schritt 3: Überprüfen der Cluster Konfiguration

Es wird dringend empfohlen, vor dem Erstellen eines Clusters die Konfiguration zu überprüfen. Anhand der Überprüfung können Sie sicherstellen, dass die Konfiguration der Server, Netzwerke und Speicher eine Reihe bestimmter Anforderungen für Failovercluster erfüllt.

#### <a name="using-failover-cluster-manager"></a>Verwenden des Failovercluster-Managers

1. Wählen Sie in **Server-Manager**das Dropdown- **Tool** aus, und wählen Sie **Failovercluster-Manager**aus.

2. Wechseln Sie in **Failovercluster-Manager**zur mittleren Spalte unter **Verwaltung** , und klicken Sie auf **Konfiguration**überprüfen.

3. Wenn das Fenster **vor dem Beginn** geöffnet wird, wählen Sie **weiter**aus.

4. Fügen Sie im Fenster **Server oder Cluster auswählen** die Namen der beiden Computer hinzu, die die Knoten des Clusters sein werden.  Wenn die Namen z. b. Node1 und Node2 lauten, geben Sie den Namen ein, und wählen Sie **Hinzufügen**aus.  Sie können auch auf die Schaltfläche **Durchsuchen** klicken, um Active Directory nach den Namen zu suchen.  Wenn beide unter **ausgewählte Server**aufgeführt sind, wählen Sie **weiter**aus.

5. Wählen Sie im Fenster **Test Optionen die Option** **alle Tests ausführen (empfohlen)** und **weiter**aus.

6. Auf der **Bestätigungs** Seite erhalten Sie die Liste aller Tests, die überprüft werden.  Wählen Sie **weiter** aus, und die Tests werden gestartet.

7. Nach Abschluss des Vorgangs wird die Seite **Zusammenfassung** angezeigt, nachdem die Tests ausgeführt wurden. Um Hilfethemen anzuzeigen, die Ihnen bei der Interpretation der Ergebnisse helfen, klicken Sie auf **Weitere Informationen über Clustervalidierungstests**.

8. Klicken Sie auf der Seite Zusammenfassung auf Bericht anzeigen, und lesen Sie die Testergebnisse. Nehmen Sie erforderliche Änderungen an der Konfiguration vor, und führen Sie die Tests erneut aus. <br>Informationen zum Anzeigen der Ergebnisse der Tests, nachdem Sie den Assistenten geschlossen haben, finden Sie unter *systemroot\cluster\reports\validation Report Date und time.html*.

9. Um Hilfethemen zur Clustervalidierung nach dem Schließen des Assistenten anzuzeigen, klicken Sie in der Failovercluster-Verwaltung auf Hilfe, Hilfethemen und auf die Registerkarte Inhalt. Erweitern Sie den Inhalt für die Failoverclusterhilfe, und klicken Sie auf Überprüfen einer Failoverclusterkonfiguration.

#### <a name="using-powershell"></a>PowerShell

1. Öffnen Sie eine administrative PowerShell-Sitzung, indem Sie mit der rechten Maustaste auf die Schaltfläche Start klicken und dann **Windows PowerShell (admin)** auswählen.

2. Führen Sie den folgenden Befehl aus, um die Computer (z. b. die Computernamen Node1 und Node2) für das Failoverclustering zu überprüfen:

    ```PowerShell
    Test-Cluster -Node "NODE1","NODE2"
    ```
4. Wenn Sie die Ergebnisse der Tests anzeigen möchten, nachdem Sie den Assistenten geschlossen haben, lesen Sie die angegebene Datei (in systemroot\cluster\reports) \) , nehmen Sie dann alle erforderlichen Änderungen an der Konfiguration vor, und führen Sie die Tests erneut aus.

Weitere Informationen finden Sie unter [Validieren einer Failoverclusterkonfiguration](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v=ws.11)).

### <a name="step-4-create-the-cluster"></a>Schritt 4: Erstellen des Clusters

Im folgenden wird ein Cluster aus den Computern und der Konfiguration erstellt, die Sie besitzen.

#### <a name="using-failover-cluster-manager"></a>Verwenden des Failovercluster-Managers

1. Wählen Sie in **Server-Manager**das Dropdown- **Tool** aus, und wählen Sie **Failovercluster-Manager**aus.

2. Wechseln Sie in **Failovercluster-Manager**zur mittleren Spalte unter **Verwaltung** , und klicken Sie auf **Cluster erstellen**.

3. Wenn das Fenster **vor dem Beginn** geöffnet wird, wählen Sie **weiter**aus.

4. Fügen Sie im Fenster **Server auswählen** die Namen der beiden Computer hinzu, die die Knoten des Clusters sein werden.  Wenn die Namen z. b. Node1 und Node2 lauten, geben Sie den Namen ein, und wählen Sie **Hinzufügen**aus.  Sie können auch auf die Schaltfläche **Durchsuchen** klicken, um Active Directory nach den Namen zu suchen.  Wenn beide unter **ausgewählte Server**aufgeführt sind, wählen Sie **weiter**aus.

5. Geben Sie im **Zugriffspunkt für die Verwaltung des Cluster** Fensters den Namen des Clusters ein, den Sie verwenden werden.  Beachten Sie, dass dies nicht der Name ist, den Sie für die Verbindung mit den Dateifreigaben mit verwenden werden.  Dies dient lediglich der Verwaltung des Clusters.

   > [!NOTE]
   > Wenn Sie statische IP-Adressen verwenden, müssen Sie das zu verwendende Netzwerk auswählen und die IP-Adresse eingeben, die für den Cluster Namen verwendet werden soll.  Wenn Sie DHCP für Ihre IP-Adressen verwenden, wird die IP-Adresse automatisch für Sie konfiguriert.

6. Wählen Sie **Weiter** aus.

7. Überprüfen Sie auf der Seite **Bestätigung** , was Sie konfiguriert haben, und klicken Sie auf **weiter** , um den Cluster zu erstellen.

8. Auf der Seite **Zusammenfassung** erhalten Sie die Konfiguration, die Sie erstellt hat.  Sie können Bericht anzeigen auswählen, um den Bericht der Erstellung anzuzeigen.

#### <a name="using-powershell"></a>PowerShell

1. Öffnen Sie eine administrative PowerShell-Sitzung, indem Sie mit der rechten Maustaste auf die Schaltfläche Start klicken und dann **Windows PowerShell (admin)** auswählen.

2. Führen Sie den folgenden Befehl aus, um den Cluster zu erstellen, wenn Sie statische IP-Adressen verwenden.  Die Computernamen sind z. b. Node1 und Node2, der Name des Clusters ist Cluster, und die IP-Adresse lautet 1.1.1.1.

   ```PowerShell
    New-Cluster -Name CLUSTER -Node "NODE1","NODE2" -StaticAddress 1.1.1.1
   ```

3. Führen Sie den folgenden Befehl aus, um den Cluster zu erstellen, wenn Sie DHCP für IP-Adressen verwenden.  Die Computernamen sind z. b. Node1 und Node2, und der Name des Clusters ist Cluster.

   ```PowerShell
   New-Cluster -Name CLUSTER -Node "NODE1","NODE2"
   ```

### <a name="steps-for-configuring-a-file-server-failover-cluster"></a>Schritte zum Konfigurieren eines Dateiserver-Failoverclusters

Führen Sie die folgenden Schritte aus, um einen Dateiserver-Failovercluster zu konfigurieren.

1. Wählen Sie in **Server-Manager**das Dropdown- **Tool** aus, und wählen Sie **Failovercluster-Manager**aus.

2. Wenn Failovercluster-Manager geöffnet wird, sollte der Name des Clusters, den Sie erstellt haben, automatisch angezeigt werden.  Wenn dies nicht der Fall ist, wechseln Sie in der mittleren Spalte unter **Verwaltung** , und wählen Sie **mit Cluster verbinden**aus.  Geben Sie den Namen des Clusters ein, den Sie erstellt haben, und **OK**.

3. Klicken Sie in der Konsolen Struktur neben dem Cluster, den Sie erstellt haben, auf das Zeichen ">", um die darunter liegenden Elemente zu erweitern.

4. Klicken Sie mit der rechten Maustaste auf **Rollen** , und wählen Sie **Rolle konfigurieren**.

5. Wenn das Fenster **vor dem Beginn** geöffnet wird, wählen Sie **weiter**aus.

6. Wählen Sie in der Liste der Rollen **Datei Server** und **dann weiter**aus.

7. Wählen Sie für den Datei Servertyp die Option **Dateiserver zur allgemeinen Verwendung** und **dann weiter**aus.<br>Informationen zu Dateiserver mit horizontaler Skalierung finden Sie unter [Dateiserver mit horizontaler Skalierung Übersicht](sofs-overview.md).

   ![Datei Servertyp](media/Cluster-File-Server/Cluster-FS-File-Server-Type.png)

8. Geben Sie im Fenster **Client Zugriffspunkt** den Namen des Dateiservers ein, den Sie verwenden werden.  Beachten Sie, dass dies nicht der Name des Clusters ist.  Dies gilt für die Verbindung mit der Dateifreigabe.  Wenn Sie z. b. eine Verbindung mit dem Server herstellen möchten \\ , ist der Name "Server".

   > [!NOTE]
   > Wenn Sie statische IP-Adressen verwenden, müssen Sie das zu verwendende Netzwerk auswählen und die IP-Adresse eingeben, die für den Cluster Namen verwendet werden soll.  Wenn Sie DHCP für Ihre IP-Adressen verwenden, wird die IP-Adresse automatisch für Sie konfiguriert.

9. Wählen Sie **Weiter** aus.

10. Wählen Sie im Fenster **Speicher auswählen** das zusätzliche Laufwerk (nicht den Zeugen) aus, das Ihre Freigaben enthalten soll, und klicken Sie auf **weiter**.

11. Überprüfen Sie auf der Seite **Bestätigung** Ihre Konfiguration, und wählen Sie **weiter**aus.

12. Auf der Seite **Zusammenfassung** erhalten Sie die Konfiguration, die Sie erstellt hat.  Sie können Bericht anzeigen auswählen, um den Bericht zur Erstellung der Dateiserver Rolle anzuzeigen.

   > [!NOTE]
   > Wenn die Rolle nicht ordnungsgemäß hinzugefügt oder gestartet wird, verfügt das CNO (Cluster Namen Objekt) möglicherweise nicht über die Berechtigung zum Erstellen von Objekten in Active Directory. Die Datei Server Rolle erfordert ein Computer Objekt mit dem gleichen Namen wie der "Client Zugriffspunkt", der in Schritt 8 bereitgestellt wurde.

13. Unter **Rollen** in der Konsolen Struktur sehen Sie, dass die neu erstellte Rolle als der von Ihnen erstellte Name aufgeführt wird.  Wählen Sie unter dem Bereich **Aktionen** auf der rechten Seite die Option **Freigabe hinzufügen**aus.

14. Führen Sie den Freigabe-Assistenten aus, und geben Sie Folgendes ein:

    - Typ der Freigabe
    - Speicherort/Pfad des freigegebenen Ordners
    - Der Name der Freigabe, mit der Benutzer eine Verbindung herstellen.
    - Weitere Einstellungen, wie z. b. Zugriffs basierte Aufzählung, Caching, Verschlüsselung usw.
    - Berechtigungen auf Dateiebene, wenn Sie nicht die Standardwerte sind

15. Überprüfen Sie auf der Seite **Bestätigung** , was Sie konfiguriert haben, und wählen Sie **Erstellen** aus, um die Dateiserver Freigabe zu erstellen.

16. Wählen Sie auf der Seite **Ergebnisse** die Option schließen aus, wenn die Freigabe erstellt wurde.  Wenn die Freigabe nicht erstellt werden konnte, erhalten Sie die Fehler.

17. Klicken Sie auf **Schließen**.

18. Wiederholen Sie diesen Vorgang für alle weiteren Freigaben.
