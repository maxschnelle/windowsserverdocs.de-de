---
title: Bereitstellen eines gruppierten Dateiservers mit zwei Knoten
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/01/2019
description: Dieser Artikel beschreibt das Erstellen eines dateiserverclusters mit zwei Knoten
ms.openlocfilehash: fbfde60f60df64514a6a0f514cbabd005544af84
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846411"
---
# <a name="deploying-a-two-node-clustered-file-server"></a>Bereitstellen eines gruppierten Dateiservers mit zwei Knoten

> Gilt für: Windows Server 2019, Windows Server 2016

Ein Failovercluster besteht aus einer Gruppe von unabhängigen Computern, die miteinander interagieren und somit die Verfügbarkeit von Anwendungen und Diensten erhöhen. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn auf einem der Clusterknoten ein Fehler auftritt, werden seine Aufgaben sofort auf einen anderen Knoten übertragen. Dies wird als Failover bezeichnet. So ergeben sich für die Benutzer nur minimale Unterbrechungen des Betriebs.

Dieses Handbuch beschreibt die Schritte zum Installieren und konfigurieren einen allgemeiner Dateiserver-Failovercluster, der über zwei Knoten verfügt. Durch die Konfiguration in dieser Anleitung erstellt haben, können mehr über Failovercluster erfahren und machen Sie sich mit den Failovercluster-Verwaltungs-Snap-in-Schnittstelle in Windows Server-2019 oder Windows Server 2016.

## <a name="overview-for-a-two-node-file-server-cluster"></a>Übersicht über einen Dateiservercluster mit zwei Knoten

Server in einem Failovercluster können in einer Vielzahl von Rollen, einschließlich der Rollen der Scale-Out File Server, Hyper-V-Server oder Datenbank-Server fungieren, und es können hohe Verfügbarkeit für eine Vielzahl von anderen Diensten und Anwendungen bereitstellen. In dieser Anleitung wird die Konfiguration eines Dateiserverclusters mit zwei Knoten beschrieben.

Ein Failovercluster enthält normalerweise eine Speichereinheit, die mit allen Servern im Cluster physisch verbunden ist, obwohl auf jedes Volume im Speicher immer nur von je einem Server zugegriffen wird. Im folgenden Diagramm finden Sie einen Failovercluster mit zwei Knoten, der an mit einer Speichereinheit verbunden ist.

![Cluster mit zwei Knoten](media\Cluster-File-Server\Cluster-FS-Overview.png)

Die für die Knoten eines Clusters offen gelegten Speichervolumes oder logischen Gerätenummern (Logical Unit Numbers, LUNs) müssen für andere Server, einschließlich der Server in einem anderen Cluster, nicht offen gelegt werden. Dies wird im folgenden Diagramm veranschaulicht.

![LUNs im Speicher](media\Cluster-File-Server\Cluster-FS-LUNs.png)

Beachten Sie, dass im Sinne einer optimalen Serververfügbarkeit bewährte Methoden der Serververwaltung zu befolgen, z. B. das sorgfältige Verwalten der physischen Umgebung der Server, das Testen von Softwareänderungen vor der vollständigen Implementierung und das gründliche Nachverfolgen von Softwareupdates und Konfigurationsänderungen auf allen geclusterten Servern.

Das folgende Szenario beschreibt, wie ein Dateiserver-Failovercluster konfiguriert werden kann. Die Dateien, die freigegeben werden sollen, befinden sich auf der Clusterspeichereinheit, und jeder Clusterserver kann als der Dateiserver fungieren, der diese freigibt.

## <a name="shared-folders-in-a-failover-cluster"></a>Freigegebene Ordner in einem Failovercluster

Die folgende Liste beschreibt die freigegebenen Ordner Funktionen, die in das Failoverclustering integriert ist:

- Anzeige ist auf nur gruppierte freigegebene Ordner (keine Vermischung mit nicht gruppierten freigegebenen Ordnern) begrenzt: Wenn ein Benutzer freigegebene Ordner durch Angabe des Pfads eines Clusterdateiservers, umfasst die Anzeige nur die freigegebenen Ordner, die Teil der Serverrolle "Datei" sind. Er schließt nicht gruppierte freigegebene Ordner und Freigaben Teil separate Datei-Serverrollen, die auf einem Knoten des Clusters sind.

- -Zugriffsbasierte Aufzählung: Sie können die zugriffsbasierte Aufzählung verwenden, um einen bestimmten Ordner für Benutzer auszublenden. Anstatt den Ordner für den Benutzer anzuzeigen, ihn jedoch nicht darauf zugreifen zu lassen, können Sie den Ordner einfach ganz ausblenden. Sie können die zugriffsbasierte Aufzählung für einen geclusterten freigegebenen Ordner auf die gleiche Weise wie für einen nicht gruppierten freigegebenen Ordner konfigurieren.

- Offline-Zugriff: Sie können den Offlinezugriff (Zwischenspeichern) für einen geclusterten freigegebenen Ordner auf die gleiche Weise wie für nicht geclusterte freigegebene Ordner konfigurieren.

- Geclusterte Datenträger werden immer als Teil des Clusters erkannt: Unabhängig davon, ob Sie die failoverclusterschnittstelle, Windows-Explorer oder das Freigabe- und Speicherverwaltung-Snap-in, erkennt Windows an, ob ein Datenträger als in den Clusterspeicher festgelegt wurde. Wenn solch ein Datenträger bereits im Failovercluster-Verwaltung als Teil eines Clusterdateiservers konfiguriert wurde, klicken Sie dann können eine der zuvor erwähnten Schnittstellen Sie um eine Freigabe auf dem Datenträger zu erstellen. Wenn der Datenträger nicht als Teil eines Clusterdateiservers konfiguriert wurde, ist es nicht möglich, versehentlich eine Freigabe darauf zu erstellen. Stattdessen gibt eine Fehlermeldung an, dass der Datenträger zuerst als Teil eines Clusterdateiservers konfiguriert werden muss, bevor er freigegeben werden kann.

- Die Integration von Diensten für NFS: Die Rolle "Dateiserver" in Windows Server enthält den optionalen Rollendienst, der Dienste für Network File System (NFS) aufgerufen. Durch Installieren des Rollendiensts und Konfigurieren von freigegebenen Ordner mit Diensten für NFS können Sie einen Clusterdateiserver erstellen, der UNIX-basierte Clients unterstützt.

## <a name="requirements-for-a-two-node-failover-cluster"></a>Anforderungen für einen Failovercluster mit zwei Knoten

Für einen Failovercluster in Windows Server 2016 oder Windows Server-2019 von Microsoft eine offiziell unterstützte Lösung berücksichtigt werden muss die Lösung die folgenden Kriterien erfüllen.

- Alle Hardware- und Softwarekomponenten müssen die Qualifikationen für das entsprechende Logo erfüllen. Für Windows Server 2016 ist dies das Logo "Zertifiziert für WindowsServer 2016". Für Windows Server-2019 ist dies das Logo "Zertifiziert für WindowsServer 2019". Weitere Informationen dazu, welche Hardware und Software-Systeme zertifiziert wurden, finden Sie auf der Microsoft [Windows Server-Katalog](https://www.windowsservercatalog.com/default.aspx) Standort.

- Die vollständig konfigurierte Lösung (Server, Netzwerk und Speicher) muss alle Tests in den überprüfungs-Assistenten bestehen, der den Failovercluster-Snap-ins gehört.

Im folgenden wird für einen Failovercluster mit zwei Knoten benötigt.

- **Server:** Es wird empfohlen, mit einem entsprechenden Computer mit identischen oder ähnlichen Komponenten.  Die Server für einen Failovercluster mit zwei Knoten müssen die gleiche Version von Windows Server ausführen. Sie sollten auch die gleichen Softwareupdates (Patches) haben.

- **Netzwerkadapter und Kabel:** Netzwerkhardware wie andere Komponenten der Failoverclusterlösung muss mit Windows Server 2016 oder Windows Server-2019 kompatibel sein. Wenn Sie iSCSI verwenden, müssen der Netzwerkadapter, Netzwerkkommunikation oder für iSCSI, nicht jedoch für beides verwendet werden. Vermeiden Sie in der Netzwerkinfrastruktur, über die die Clusterknoten verbunden sind, die Verwendung von Komponenten, deren Ausfall einen Ausfall des Gesamtsystems zur Folge hätte. Es gibt mehrere Methoden, dies zu erreichen. Sie können die Clusterknoten durch mehrere unterschiedliche Netzwerke verbinden. Zudem können Sie die Clusterknoten mit einem Netzwerk verbinden, das aus Netzwerkadapterteams, redundanten Switches, redundanten Routern oder ähnlicher Hardware besteht, die einzelne Fehlerpunkte beseitigt.

   > [!NOTE]
   > Wenn die Clusterknoten mit einem Netzwerk verbunden sind, wird das Netzwerk den Konfigurationsüberprüfungs-Assistenten die Redundanz Anforderung übergeben.  Allerdings wird der Bericht enthält eine Warnung, dass das Netzwerk nicht auf eine einzelne Fehlerquelle haben soll.

- **Gerätecontroller oder entsprechende Adapter für Speicher:**
    - **Serial Attached SCSI oder Fibre Channel:** Wenn Sie SAS oder Fibre Channel verwenden, sollten alle Komponenten des Speicherstapels aller geclusterten Server identisch sein. Es ist erforderlich, das Multipfad e/a (MPIO)-Software und die Geräte bestimmten Modul (DSM) Softwarekomponenten, die identisch sein.  Es wird empfohlen, identische Massenspeichergerätecontroller zu verwenden, d. h. Hostbusadapter (HBA), HBA-Treiber und HBA-Firmware. Wenn Sie unterschiedliche HBAs verwenden, sollten Sie gemeinsam mit dem Speicheranbieter überprüfen, ob die unterstützten oder empfohlenen Konfigurationen eingehalten werden.
    - **iSCSI:** Wenn Sie iSCSI verwenden, muss jeder Clusterserver über verfügen, eine oder mehrere Netzwerkadapter oder Hostbusadapter an, die den iSCSI-Speicher zugeordnet sind. Das Netzwerk, das Sie für iSCSI verwenden, kann nicht für die Netzwerkkommunikation verwendet werden. Die zum Herstellen von Verbindungen mit dem iSCSI-Speicherziel verwendeten Netzwerkadapter müssen für alle Clusterserver identisch sein, und es empfiehlt sich, Gigabit Ethernet oder höher zu verwenden.  

- **Speicher:** Sie müssen die freigegebenen Speicher verwenden, der für Windows Server 2016 oder Windows Server-2019 zertifiziert ist.
  
    Für einen Failovercluster mit zwei Knoten sollte der Speicher mindestens zwei separaten Volumes (LUNs) enthalten, wenn einen Zeugendatenträger für ein Quorum zu verwenden. Bei einem Zeugendatenträger handelt es sich um einen Datenträger im Clusterspeicher, auf dem eine Kopie der Clusterkonfigurationsdatenbank gespeichert ist. Cluster mit zwei Knoten in diesem Beispiel wird die Quorumkonfiguration Knoten- und Datenträgermehrheit sein. Knoten- und Datenträgermehrheit bedeutet, dass die Knoten und der Zeugendatenträger jeweils zwei Kopien der Clusterkonfiguration enthalten, und der Cluster besitzt das Quorum, solange die Mehrheit (zwei von drei) diese Kopien sind verfügbar. Das andere Volume (LUN) enthält die Dateien, die für Benutzer freigegeben sind.

    Die Speicheranforderungen beinhalten Folgendes:

    - Um die systemeigene, im Failoverclustering enthaltene Datenträgerunterstützung verwenden zu können, müssen anstelle von dynamischen Datenträgern Basisdatenträger verwendet werden.
    - Die Formatierung als NTFS-Partitionen wird empfohlen (die Partition des Zeugendatenträgers muss NTFS-formatiert sein).
    - Als Partitionsstil des Datenträgers können Sie entweder MBR (Master Boot Record) oder GPT (GUID-Partitionstabelle) verwenden.
    - Der Speicher muss ordnungsgemäß auf bestimmte SCSI-Befehle reagiert. muss der Speicher dem Standard, die SCSI-3 Primary Commands-(SPC-3) wird aufgerufen, entsprechen. Insbesondere muss der Speicher permanente Reservierungen unterstützen, wie im SPC-3-Standard angegeben. 
    -  Der für den Speicher verwendete Miniporttreiber muss mit dem StorPort-Speichertreiber von Microsoft kompatibel sein.

## <a name="deploying-storage-area-networks-with-failover-clusters"></a>Bereitstellen von SANs (Storage Area Networks) mit Failoverclustern

Wenn Sie ein Storage Area Network (SAN) für einen Failovercluster bereitstellen, sollten die folgenden Richtlinien beachtet werden.

- **Bestätigen Sie die Zertifizierung des Speichers:** Mithilfe der [Windows Server-Katalog](https://www.windowsservercatalog.com/default.aspx) Standorts, des Anbieters Speicher, einschließlich Treiber, Firmware und Software, hat eine Zertifizierung für Windows Server 2016 oder Windows Server-2019 zu bestätigen.

- **Isolieren Sie Speichergeräte, ein Cluster pro Gerät:** Server unterschiedlicher Cluster dürfen nicht auf dieselben Speichergeräte zugreifen. In den meisten Fällen sollte eine LUN, die für einen Satz von Clusterservern verwendet wird, durch LUN-Maskierung oder -Zoneneinteilung von allen anderen Servern isoliert werden.

- **Verwenden Sie ggf. Multipfad e/a-Software:** In einem Speicherfabric mit hoher Verfügbarkeit können Sie mit MPIO-Software Failovercluster mit mehreren Hostbusadaptern bereitstellen. Auf diese Weise erhalten Sie den höchsten Grad an Redundanz und Verfügbarkeit. Die multipfadlösung muss auf Microsoft Multipfad-e/a (MPIO) basieren. Die Hardware-Speicheranbieter kann möglicherweise ein MPIO gerätespezifischen Modul (DSM) für die Hardware angeben, obwohl Windows Server 2016 und Windows Server-2019 mindestens ein DSM als Bestandteil des Betriebssystems enthalten.

## <a name="network-infrastructure-and-domain-account-requirements"></a>Anforderungen an die Netzwerkinfrastruktur und das Domänenkonto

Für einen Failovercluster mit zwei Knoten benötigen Sie die folgende Netzwerkinfrastruktur und ein Administratorkonto mit den folgenden Domänenberechtigungen:

- **Netzwerkeinstellungen und IP-Adressen:** Wenn Sie für ein Netzwerk identische Netzwerkadapter verwenden, sollten auch die Kommunikationseinstellungen auf diesen Adaptern identisch sein (z. B. Geschwindigkeit, Duplexmodus, Flusssteuerung und Medientyp). Vergleichen Sie zudem die Einstellungen zwischen dem Netzwerkadapter und dem Switch, zu dem eine Verbindung hergestellt wird, und stellen Sie sicher, dass die Einstellungen nicht miteinander in Konflikt stehen.

    Wenn Sie über private Netzwerke verfügen, die nicht an die übrige Netzwerkinfrastruktur weitergeleitet werden, muss sichergestellt werden, dass jedes dieser privaten Netzwerke ein eindeutiges Subnetz verwendet. Dies ist auch dann erforderlich, wenn jeder Netzwerkadapter über eine eindeutige IP-Adresse verfügt. Wenn Sie beispielsweise in einer Zentrale mit einem physischen Netzwerk über einen Clusterknoten und in einer Filiale mit einem separaten physischen Netzwerk über einen weiteren Knoten verfügen, sollte 10.0.0.0/24 selbst dann nicht für beide Netzwerke angegeben werden, wenn Sie jedem Adapter eine eindeutige IP-Adresse zuweisen.

    Weitere Informationen zu den Netzwerkadaptern finden Sie unter "hardwareanforderungen für einen zwei-Knoten-Failovercluster, in diesem Handbuch".

- **DNS:** Die Server im Cluster müssen für die Namensauflösung DNS (Domain Name System) verwenden. Das Protokoll für das dynamische DNS-Update kann verwendet werden.

- **Domänenrolle:** Alle Server im Cluster müssen sich in der gleichen Active Directory-Domäne befinden. Als bewährte Methode sollten alle geclusterten Server über dieselbe Domänenrolle verfügen (entweder Mitgliedsserver oder Domänencontroller). Die empfohlene Rolle ist Mitgliedsserver.

- **Domänencontroller:** Es wird empfohlen, dass es sich bei den geclusterten Servern um Mitgliedsserver handelt. Ist dies der Fall, benötigen Sie einen zusätzlichen Server, der in der Domäne, die den Failovercluster enthält, als Domänencontroller fungiert.

- **-Clients:** Wenn es für Tests erforderlich ist, können Sie einen oder mehrere vernetzte Clients mit dem Failovercluster verbinden, den Sie erstellen. Beobachten Sie die Auswirkungen auf einen Client, wenn Sie den Clusterdateiserver von einem Clusterknoten zum anderen verschieben bzw. einen Failover ausführen.

- **Konto zum Verwalten des Clusters:** Beim erstmaligen Erstellen eines Clusters oder beim Hinzufügen von Servern zu diesem Cluster, müssen Sie an der Domäne mit einem Konto angemeldet sein, das über Administratorrechte und Berechtigungen für alle Server in diesem Cluster verfügt. Dabei muss es sich nicht unbedingt um ein Domänenadministratorenkonto handeln. Es kann auch ein Domänenbenutzerkonto verwendet werden, das der Gruppe "Administratoren" für die einzelnen Clusterserver angehört. Darüber hinaus ist das Konto kein-Admins-domänenadministratorenkonto, das Konto (oder die Gruppe, die das Konto ein Mitglied ist) muss angegeben werden die **Erstellen von Computerobjekten** und **Lesen aller Eigenschaften** Berechtigungen in der Domäne Organisationseinheit (OU), ist befinden in.

## <a name="steps-for-installing-a-two-node-file-server-cluster"></a>Schritte zum Installieren eines Dateiserverclusters mit zwei Knoten

Sie müssen die folgenden Schritte ausführen, um einen Dateiserver-Failovercluster mit zwei Knoten zu installieren.

Schritt 1: Verbinden der Clusterserver mit den Netzwerken und dem Speicher

Schritt 2: Installieren der Failoverclusterfunktion

Schritt 3: Überprüfen der Clusterkonfiguration

Schritt 4: Erstellen des Clusters

Wenn Sie die Clusterknoten bereits installiert haben und einen Dateiserver-Failovercluster konfigurieren möchten, finden Sie unter Schritten konfigurieren einen zwei-Knoten-Dateiservercluster, weiter unten in diesem Handbuch.

### <a name="step-1-connect-the-cluster-servers-to-the-networks-and-storage"></a>Schritt 1: Verbinden der Clusterserver mit den Netzwerken und dem Speicher

Vermeiden Sie in einem Failoverclusternetzwerk einzelne Fehlerpunkte. Es gibt mehrere Methoden, dies zu erreichen. Sie können die Clusterknoten durch mehrere unterschiedliche Netzwerke verbinden. Alternativ können Sie die Clusterknoten mit einem Netzwerk verbinden, das aus kombinierten Netzwerkadaptern, redundanten Switches, redundanten Routern oder ähnlicher Hardware besteht, die einzelne Fehlerpunkte ausschließt (Wenn Sie ein Netzwerk für iSCSI verwenden, müssen Sie dieses Netzwerk zusätzlich zu den anderen Netzwerken einrichten).

Für einen Dateiservercluster mit zwei Knoten müssen Sie mindestens zwei Volumes (LUNs) verfügbar machen, wenn Sie die Server mit dem Clusterspeicher verbinden. Für gründliche Tests der Konfiguration können Sie bei Bedarf zusätzliche Volumes verfügbar machen. Die Clustervolumes dürfen nicht für Server verfügbar gemacht werden, die sich nicht im Cluster befinden.

#### <a name="to-connect-the-cluster-servers-to-the-networks-and-storage"></a>So verbinden Sie den Clusterserver mit den Netzwerken und dem Speicher

1. Überprüfen Sie die Details zu Netzwerken in hardwareanforderungen für einen Failovercluster mit zwei Knoten und Netzwerk Netzwerkinfrastruktur- und domänenkontenanforderungen für einen zwei-Knoten-Failovercluster, in diesem Handbuch.

2. Verbinden und konfigurieren Sie die Netzwerke, die die Server im Cluster verwenden.

3. Wenn die Testkonfiguration Clients oder einen nicht geclusterten Domänencontroller umfasst, stellen Sie sicher, dass diese Computer über mindestens ein Netzwerk eine Verbindung mit den geclusterten Servern herstellen können.

4. Befolgen Sie die Anweisungen des Herstellers zum physischen Verbinden der Server mit dem Speicher.

5. Stellen Sie sicher, dass die Datenträger (LUNs), die Sie im Cluster verwenden möchten, für die zu gruppierenden Server (und zwar ausschließlich für diese Server) bereitgestellt wurden. Sie können Datenträger oder LUNs mit einer der folgenden Schnittstellen verfügbar machen:

    - Die Schnittstelle, die vom Hersteller des Speichers bereitgestellt wird

    - Wenn Sie iSCSI verwenden, eine entsprechende iSCSI-Schnittstelle

6. Wenn Sie Software erworben haben, die das Format oder die Funktion des Datenträgers gesteuert wird, befolgen Sie die Anweisungen des Anbieters zur Verwendung dieser Software mit Windows Server.

7. Klicken Sie auf einem der Server, die Sie verwenden möchten, gruppieren, klicken Sie auf Start auf Verwaltung, klicken Sie auf ' Computerverwaltung, und klicken Sie dann die Datenträgerverwaltung auf. (Wenn das Dialogfeld "Benutzerkontensteuerung" angezeigt wird, bestätigen Sie, dass die gewünschte Aktion angezeigt wird, was Sie möchten, und klicken Sie dann auf Weiter.) In der Datenträgerverwaltung Vergewissern Sie sich, dass die Clusterdatenträger sichtbar sind.

8. Wenn Sie ein Speichervolume mit mehr als zwei Terabyte erstellen möchten und Sie zum Steuern des Datenträgerformats die Windows-Benutzeroberfläche verwenden, konvertieren Sie diesen Datenträger in den Partitionstyp GPT (GUID-Partitionstabelle). Hierzu, Sichern Sie alle Daten auf dem Datenträger löschen Sie alle Volumes auf dem Datenträger, und klicken Sie dann in der Datenträgerverwaltung mit der rechten Maustaste des Datenträgers (nicht auf eine Partition), und klicken Sie auf GPT-Datenträger konvertieren.  Für Volumes mit weniger als zwei Terabyte können Sie statt GPT den Partitionstyp MBR (Master Boot Record) verwenden.

9. Überprüfen Sie das Format aller verfügbar gemachten Volumes bzw. LUNs. Es wird empfohlen, als Format NTFS zu verwenden (für den Zeugendatenträger muss NTFS verwendet werden).

### <a name="step-2-install-the-file-server-role-and-failover-cluster-feature"></a>Schritt 2: Installieren Sie die Datei Server-Rolle und Failover-Cluster-Funktion

In diesem Schritt wird die Datei Server-Rolle und Failover-Cluster-Funktion installiert werden. Beide Server müssen entweder Windows Server 2016 oder Windows Server-2019 ausgeführt werden.

#### <a name="using-server-manager"></a>Mit dem Server-Manager

1. Open **Server-Manager** und wählen Sie unter den **verwalten** öffnen Sie die Dropdownliste, wählen Sie **Hinzufügen von Rollen und Features**.

   ![Funktion hinzufügen](media\Cluster-File-Server\Cluster-FS-Add-Feature.png)

2. Wenn die **vor dem Beginn** Fenster geöffnet wird, wählen Sie **Weiter**.

3. Für die **Installationstyp**Option **rollenbasierte oder featurebasierte Installation** und **Weiter**.

4. Stellen Sie sicher **wählen Sie einen Server aus dem Serverpool** wird ausgewählt, der Name des Computers wird hervorgehoben, und **Weiter**.

5. Öffnen Sie für die Server-Rolle, aus der Liste der Rollen, **Dateidienste**Option **Dateiserver**, und **Weiter**.

   ![Rolle hinzufügen](media\Cluster-File-Server\Cluster-FS-Add-FS-Role-1.png)

6. Wählen Sie für die Funktionen, aus der Liste der Features, **Failover-Clusterunterstützung**.  Ein Popupdialogfeld zeigt, dass, die Verwaltungstools auch installierenden aufgelistet sind.  Alle beibehalten der ausgewählten Option **Features hinzufügen** und **Weiter**.

   ![Funktion hinzufügen](media\Cluster-File-Server\Cluster-FS-Add-WSFC-1.png)

7. Wählen Sie auf der Seite "Bestätigung" installieren.

8. Nach Abschluss der Installation starten Sie den Computer neu.

9. Wiederholen Sie die Schritte auf dem zweiten Computer ein.

#### <a name="using-powershell"></a>Mithilfe der PowerShell

1. Öffnen Sie eine administrative PowerShell-Sitzung, indem Sie einen Rechtsklick auf die Schaltfläche "Start", und wählen Sie dann **Windows PowerShell (Admin)**.
2. Führen Sie zum Installieren der Rolle für Dateiserver den Befehl ein:

    ```PowerShell
    Install-WindowsFeature -Name FS-FileServer
    ```

3. Um das Feature "Failoverclustering" und die Verwaltungstools zu installieren, führen Sie den Befehl aus:

    ```PowerShell
    Install-WindowsFeature -Name Failover-Clustering -IncludeManagementTools
    ```

4. Wenn sie abgeschlossen haben, können Sie überprüfen, dass sie mit den Befehlen installiert sind:

    ```PowerShell
    Get-WindowsFeature -Name FS-FileServer
    Get-WindowsFeature -Name Failover-Clustering
    ```

5. Nachdem Sie geprüft, ob sie installiert sind, starten Sie den Computer mit dem Befehl neu:

    ```PowerShell
    Restart-Computer
    ```

6. Wiederholen Sie die Schritte auf dem zweiten Server aus.

### <a name="step-3-validate-the-cluster-configuration"></a>Schritt 3: Überprüfen der Clusterkonfiguration

Es wird dringend empfohlen, vor dem Erstellen eines Clusters die Konfiguration zu überprüfen. Anhand der Überprüfung können Sie sicherstellen, dass die Konfiguration der Server, Netzwerke und Speicher eine Reihe bestimmter Anforderungen für Failovercluster erfüllt.

#### <a name="using-failover-cluster-manager"></a>Failovercluster-Manager

1. Von **Server-Manager**, wählen Sie die **Tools** Dropdownliste aus, und wählen Sie **Failovercluster-Manager**.

2. In **Failovercluster-Manager**, fahren Sie mit der mittleren Spalte unter **Management** , und wählen Sie **Konfiguration überprüfen**.

3. Wenn die **vor dem Beginn** Fenster geöffnet wird, wählen Sie **Weiter**.

4. In der **Server auswählen oder in einem Cluster** Fenster in den Namen der zwei Computer, die die Knoten des Clusters hinzufügen.  Beispielsweise wenn die Namen NODE1 und NODE2 sind, geben Sie den Namen, und wählen Sie **hinzufügen**.  Sie können auch die **Durchsuchen** Schaltfläche, um die Active Directory nach den Namen zu suchen.  Sobald beide unter aufgeführten **ausgewählten Servern**, wählen Sie **Weiter**.

5. In der **Testoptionen** wählen Sie im Fenster **alle Tests ausführen (empfohlen)**, und **Weiter**.

6. Auf der **Bestätigung** Seite haben Sie die Auflistung aller Tests überprüft.  Wählen Sie **Weiter** und die Tests beginnen.

7. Nach Abschluss des Vorgangs, der **Zusammenfassung** Seite wird angezeigt, nachdem die Tests ausgeführt. Um Hilfethemen anzuzeigen, die Ihnen bei der Interpretation der Ergebnisse helfen, klicken Sie auf **Weitere Informationen über Clustervalidierungstests**.

8. Klicken Sie auf Bericht anzeigen und Lesen Sie die Testergebnisse, immer noch auf der Seite "Zusammenfassung". Nehmen Sie alle erforderlichen Änderungen in der Konfiguration, und führen Sie die Tests erneut aus. <br>Die Ergebnisse der Tests nach dem Schließen des Assistenten finden Sie unter *SystemRoot\Cluster\Reports\Validation Report Date and time.html*.

9. Zum Anzeigen von Hilfethemen über die clustervalidierung nach des Assistenten auf Failover-Clusterverwaltung schließen klicken Sie auf Hilfe, klicken Sie auf Hilfethemen, klicken Sie auf der Registerkarte "Inhalt", erweitern Sie den Inhalt für die failoverclusterhilfe, und klicken Sie auf die Konfiguration des Failoverclusters überprüfen .

#### <a name="using-powershell"></a>Mithilfe der PowerShell

1. Öffnen Sie eine administrative PowerShell-Sitzung, indem Sie einen Rechtsklick auf die Schaltfläche "Start", und wählen Sie dann **Windows PowerShell (Admin)**.

2. Um die Computer (z. B. Namen der Computer wird von NODE1 und NODE2) für Failover-Clusterunterstützung zu überprüfen, führen Sie den Befehl aus:

    ```PowerShell
    Test-Cluster -Node "NODE1","NODE2"
    ```
4. Die Ergebnisse der Tests nach dem Schließen des Assistenten finden Sie unter der angegebenen Datei (in SystemRoot\Cluster\Reports\), nehmen Sie alle erforderlichen Änderungen in der Konfiguration, und führen Sie die Tests erneut aus.

Weitere Informationen finden Sie unter [Überprüfen einer Failoverclusterkonfiguration](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v=ws.11)).

### <a name="step-4-create-the-cluster"></a>Schritt 4: Erstellen des Clusters

Im folgenden wird ein Cluster erstellt aus der Computer und die Konfiguration, was man.

#### <a name="using-failover-cluster-manager"></a>Failovercluster-Manager

1. Von **Server-Manager**, wählen Sie die **Tools** Dropdownliste aus, und wählen Sie **Failovercluster-Manager**.

2. In **Failovercluster-Manager**, fahren Sie mit der mittleren Spalte unter **Management** , und wählen Sie **Clustererstellungs**.

3. Wenn die **vor dem Beginn** Fenster geöffnet wird, wählen Sie **Weiter**.

4. In der **Server auswählen** Fenster in den Namen der zwei Computer, die die Knoten des Clusters hinzufügen.  Beispielsweise wenn die Namen NODE1 und NODE2 sind, geben Sie den Namen, und wählen Sie **hinzufügen**.  Sie können auch die **Durchsuchen** Schaltfläche, um die Active Directory nach den Namen zu suchen.  Sobald beide unter aufgeführten **ausgewählten Servern**, wählen Sie **Weiter**.

5. In der **Zugriffspunkt zum Verwalten des Clusters** Fenster, geben Sie den Namen des Clusters, die Sie verwenden.  Bitte beachten Sie, dass dies nicht der Name, die Sie für die Verbindung an den Dateifreigaben mit verwenden werden.  Dies ist für den Cluster einfach zu verwalten.

   > [!NOTE]
   > Wenn Sie statische IP-Adressen verwenden, müssen Sie wählen Sie das Netzwerk zu verwenden, und geben Sie die IP-Adresse, die sie für den Namen des Clusters verwenden.  Wenn Sie DHCP für Ihre IP-Adressen verwenden, wird die IP-Adresse automatisch für Sie konfiguriert werden.

6. Wählen Sie **Weiter**.

7. Auf der **Bestätigung** Seite, überprüfen Sie, wie Sie konfiguriert haben, und wählen Sie **Weiter** zum Erstellen des Clusters.

8. Auf der **Zusammenfassung** Seite haben Sie die Konfiguration, die sie erstellt.  Sie können die View-Bericht zum Anzeigen des Berichts, der die Erstellung auswählen.

#### <a name="using-powershell"></a>Mithilfe der PowerShell

1. Öffnen Sie eine administrative PowerShell-Sitzung, indem Sie einen Rechtsklick auf die Schaltfläche "Start", und wählen Sie dann **Windows PowerShell (Admin)**.

2. Führen Sie den folgenden Befehl zum Erstellen des Clusters, wenn Sie statische IP-Adressen verwenden.  Z. B. die Namen der Computer sind NODE1 und NODE2, der Namen des Clusters werden die CLUSTER und die IP-Adresse werden 1.1.1.1.

   ```PowerShell
    New-Cluster -Name CLUSTER -Node "NODE1","NODE2" -StaticAddress 1.1.1.1
   ```

3. Führen Sie den folgenden Befehl zum Erstellen des Clusters, wenn Sie DHCP für IP-Adressen verwenden.  Z. B. die Namen der Computer sind NODE1 und NODE2, und der Namen des Clusters werden die CLUSTER.

   ```PowerShell    
   New-Cluster -Name CLUSTER -Node "NODE1","NODE2"
   ```

### <a name="steps-for-configuring-a-file-server-failover-cluster"></a>Schritte zum Konfigurieren von einem Dateiserver-Failoverclusters

Um eine Dateiserver-Failovercluster zu konfigurieren, führen Sie die folgenden Schritte aus.

1. Von **Server-Manager**, wählen Sie die **Tools** Dropdownliste aus, und wählen Sie **Failovercluster-Manager**.

2. Wenn Failovercluster-Manager geöffnet wird, sollte sie automatisch den Namen des Clusters angezeigt, die Sie erstellt haben.  Wenn dies nicht der Fall ist, wechseln Sie auf der mittleren Spalte unter **Management** , und wählen Sie **Herstellen einer Verbindung mit Cluster**.  Geben Sie den Namen des erstellten Clusters und **OK**.

3. Klicken Sie in der Konsolenstruktur auf den ">" neben den Cluster, den Sie erstellt haben, um die untergeordneten Elemente zu erweitern.

4. Auf der rechten Maustaste **Rollen** , und wählen Sie **Rolle konfigurieren**.

5. Wenn die **vor dem Beginn** Fenster geöffnet wird, wählen Sie **Weiter**.

6. Wählen Sie in der Liste der Rollen, **Dateiserver** und **Weiter**.

7. Wählen Sie für die Dateiservertyp **Dateiserver zur allgemeinen Verwendung** und **Weiter**.<br>Weitere Informationen zu den Scale-Out File Server, finden Sie unter [Scale-Out File Server Overview](sofs-overview.md).

   ![Dateiservertyp](media\Cluster-File-Server\Cluster-FS-File-Server-Type.png)

8. In der **Clientzugriffspunkt** Fenster, geben Sie den Namen des Dateiservers, die Sie verwenden.  Beachten Sie, dass dies nicht der Name des Clusters ist.  Dies ist für die Datei-Freigabe-Konnektivität.  Angenommen, ich möchte, für die Verbindung \\SERVER, würde der Name der eingegebenen SERVER sein.

   > [!NOTE]
   > Wenn Sie statische IP-Adressen verwenden, müssen Sie wählen Sie das Netzwerk zu verwenden, und geben Sie die IP-Adresse, die sie für den Namen des Clusters verwenden.  Wenn Sie DHCP für Ihre IP-Adressen verwenden, wird die IP-Adresse automatisch für Sie konfiguriert werden.

6. Wählen Sie **Weiter**.

7. In der **Speicher auswählen** Fenster, wählen Sie das zusätzliche Laufwerk (kein Zeuge), die Ihre Dateifreigaben erhalten soll und **Weiter**.

8. Auf der **Bestätigung** Seite überprüfen Sie Ihre Konfiguration, und wählen Sie **Weiter**.

9. Auf der **Zusammenfassung** Seite haben Sie die Konfiguration, die sie erstellt.  Sie können die View-Bericht zum Anzeigen des Berichts, der Erstellung des Datei-Server-Rolle auswählen.

10. Klicken Sie unter **Rollen** in der Konsolenstruktur, sehen Sie die neue Rolle, die Sie erstellt haben als den Namen der erstellten aufgeführt.  Mit er hervorgehoben, unter dem **Aktionen** wählen Sie auf der rechten Seite **Hinzufügen einer Freigabe**.

11. Führen Sie über den Assistenten Folgendes eingeben:

    - Typ der Freigabe für die Komponente wird
    - Location-Path wird der Ordner freigegeben werden.
    - Der Name der Freigabe wird eine Verbindung mit
    - Zusätzliche Einstellungen wie z. B. die zugriffsbasierte Aufzählung, Zwischenspeicherung, Verschlüsselung usw.
    - Wenn sie als die Standardwerte werden Dateiberechtigungen Sie auf

12. Auf der **Bestätigung** Seite, überprüfen Sie, wie Sie konfiguriert haben, und wählen Sie **erstellen** Dateiserverfreigabe zu erstellen.

13. Auf der **Ergebnisse** Seite, wählen Sie schließen, wenn es sich um die Freigabe erstellt.  Wenn sie die Freigabe nicht erstellen konnte, wird Sie Fehler entstehen können.

14. Wählen Sie **schließen**.

15. Wiederholen Sie diesen Vorgang für alle zusätzlichen Freigaben ein.