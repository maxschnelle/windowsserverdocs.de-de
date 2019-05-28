---
title: Erstellen eines Failoverclusters
description: 'Vorgehensweise: erstellen ein Failoverclusters für Windows Server 2012 R2, Windows Server 2012, Windows Server 2016 und Windows Server-2019.'
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4122375a48cae17e5f3ebcd7e9f3ce1fad28a105
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222490"
---
# <a name="create-a-failover-cluster"></a>Erstellen eines Failoverclusters

>Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2 und WindowsServer 2012

In diesem Thema wird gezeigt, wie ein Failovercluster mithilfe des Failovercluster-Manager-Snap-Ins oder mit Windows PowerShell erstellt wird. Das Thema behandelt eine typische Bereitstellung, bei der Computerobjekte für den Cluster und seine zugehörigen Clusterrollen in Active Directory-Domänendiensten (AD DS) erstellt werden. Wenn Sie einen "direkte Speicherplätze"-Cluster bereitstellen, finden Sie stattdessen unter [Bereitstellen von "direkte Speicherplätze"](../storage/storage-spaces/deploy-storage-spaces-direct.md).

Sie können auch einen Active Directory getrennten Cluster bereitstellen. Mit dieser Bereitstellungsmethode können Sie einen Failovercluster erstellen und benötigen dazu nicht die Berechtigungen zum Erstellen von Computerobjekten in AD DS. Außerdem müssen Sie nicht die Vorabbereitstellung von Computerobjekten in AD DS anfordern. Diese Option ist nur über Windows PowerShell verfügbar und wird nur für bestimmte Szenarien empfohlen. Weitere Informationen finden Sie unter [Bereitstellen eines von Active Directory getrennten Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

#### <a name="checklist-create-a-failover-cluster"></a>Prüfliste: Erstellen eines Failoverclusters

|Status|Aufgabe|Referenz|
|:---:|---|---|
|☐|Überprüfen der Voraussetzungen|[Überprüfen der Voraussetzungen](#verify-the-prerequisites)|
|☐|Installieren Sie das Failoverclusteringfeature auf jedem Server, den Sie als Clusterknoten hinzufügen möchten.|[Installieren Sie das Feature "Failoverclustering"](#install-the-failover-clustering-feature)|
|☐|Ausführen des Clusterüberprüfungs-Assistenten zum Überprüfen der Konfiguration|[Überprüfen der Konfiguration](#validate-the-configuration)|
|☐|Ausführen des Clustererstellungs-Assistenten zum Erstellen des Failoverclusters|[Erstellen des Failoverclusters](#create-the-failover-cluster)|
|☐|Erstellen von Clusterrollen zum Hosten der Clusterarbeitsauslastung|[Erstellen von clusterrollen](#create-clustered-roles)|

## <a name="verify-the-prerequisites"></a>Überprüfen der Voraussetzungen

Bevor Sie beginnen, überprüfen Sie die folgenden Voraussetzungen:

- Stellen Sie sicher, dass alle Server, die Sie als Clusterknoten hinzufügen möchten, dieselbe Version von Windows Server ausführen.
- Überprüfen Sie die Hardwareanforderungen, um sicherzustellen, dass Ihre Konfiguration unterstützt wird. Weitere Informationen finden Sie unter [Hardwareanforderungen und Speicheroptionen für Failovercluster](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj612869(v%3dws.11)). Wenn Sie einen "direkte Speicherplätze"-Cluster erstellen, finden Sie unter ["direkte Speicherplätze" hardwareanforderungen](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md).
- Um während der Clustererstellung Clusterspeicher hinzufügen möchten, stellen Sie sicher, dass alle Server auf den Speicher zugreifen können. (Sie können Clusterspeicher auch nach der Erstellung des Clusters hinzufügen.)
- Stellen Sie sicher, dass alle Server, die Sie als Clusterknoten hinzufügen möchten, derselben Active Directory-Domäne angehören.
- (Optional) Erstellen Sie eine Organisationseinheit (OU), und verschieben Sie die Computerkonten für die Server, die Sie als Clusterknoten hinzufügen möchten, in die Organisationseinheit. Als bewährte Methode wird empfohlen, dass Sie Failovercluster in ihren eigenen Organisationseinheiten in AD DS bereitstellen. Auf diese Weise können Sie besser kontrollieren, welche Gruppenrichtlinieneinstellungen oder Sicherheitsvorlageneinstellungen die Clusterknoten beeinflussen. Das Isolieren der Cluster in eigenen Organisationseinheiten schützt zudem vor dem versehentlichen Löschen von Clustercomputerobjekten.

Überprüfen Sie zusätzlich die folgenden Kontoanforderungen:

- Stellen Sie sicher, dass das Konto, das Sie zum Erstellen des Clusters verwenden möchten, einem Domänenbenutzer entspricht, der auf allen Servern, die Sie als Clusterknoten hinzufügen möchten, über Administratorrechte verfügt.
- Stellen Sie sicher, dass eine der folgenden Optionen zutrifft:
    - Der Benutzer, der die Cluster erstellt, verfügt für die Organisationseinheit oder den Container, in dem sich die Server befinden, die den Cluster bilden, über die Berechtigung **Computerobjekte erstellen** .
    - Wenn der Benutzer nicht über die Berechtigung **Computerobjekte erstellen** verfügt, bitten Sie einen Domänenadministrator, ein Clustercomputerobjekt für den Cluster vorab bereitzustellen. Weitere Informationen finden Sie unter [Vorabbereitstellen von Clustercomputerobjekten in Active Directory-Domänendiensten](prestage-cluster-adds.md).

>[!NOTE]
>Diese Anforderung gilt nicht, wenn Sie einen Active Directory getrennten Cluster in Windows Server 2012 R2 erstellen möchten. Weitere Informationen finden Sie unter [Bereitstellen eines von Active Directory getrennten Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

## <a name="install-the-failover-clustering-feature"></a>Installieren des Failoverclusteringfeatures

Sie müssen das Failoverclusteringfeature auf jedem Server installieren, den Sie als Failoverclusterknoten hinzufügen möchten.

### <a name="install-the-failover-clustering-feature"></a>Installieren des Failoverclusteringfeatures

1. Starten Sie den Server-Manager.
2. Auf der **verwalten** , wählen Sie im Menü **Hinzufügen von Rollen und Features**.
3. Auf der **vor dem Beginn** Seite **Weiter**.
4. Auf der **Installationstyp** Seite **rollenbasierte oder featurebasierte Installation**, und wählen Sie dann **Weiter**.
5. Auf der **Zielserver auswählen** Seite, wählen Sie den Server, in dem Sie die Funktion installieren, und wählen Sie dann möchten **Weiter**.
6. Auf der **Serverrollen auswählen** Seite **Weiter**.
7. Aktivieren Sie auf der Seite **Features auswählen** das Kontrollkästchen **Failoverclustering**.
8. Wählen Sie zum Installieren der Verwaltungstools für Failovercluster **Features hinzufügen**, und wählen Sie dann **Weiter**.
9. Auf der **Installationsauswahl bestätigen** Seite **installieren**.
<br>Ein Neustart des Servers ist für das Failoverclusteringfeature nicht erforderlich.

10. Wenn die Installation abgeschlossen ist, wählen Sie **schließen**.
11. Wiederholen Sie diesen Vorgang auf jedem Server, den Sie als Failoverclusterknoten hinzufügen möchten.

>[!NOTE]
>Es wird empfohlen, dass Sie nach der Installation des Failoverclusteringfeatures die neuesten Updates von Windows Update anwenden. Lesen Sie auch für einen Windows Server 2012-basierte Failovercluster die [empfohlene Hotfixes und Updates für Windows Server 2012-basierte Failovercluster](https://support.microsoft.com/help/2784261/recommended-hotfixes-and-updates-for-windows-server-2012-based-failove) Microsoft-Support-Artikel, und installieren Sie alle entsprechenden Updates.

## <a name="validate-the-configuration"></a>Überprüfen der Konfiguration

Vor der Erstellung des Failovercluster wird dringend empfohlen, dass Sie die Konfiguration überprüfen, um sicherzustellen, dass die Hardware und die Hardwareeinstellungen mit dem Failoverclustering kompatibel sind. Microsoft unterstützt eine Clusterlösung nur, wenn die gesamte Konfiguration die Validierungstests besteht und die gesamte Hardware für die Version von Windows Server zertifiziert ist, die auf den Clusterknoten ausgeführt wird.

>[!NOTE]
>Sie müssen mindestens zwei Knoten besitzen, um alle Tests ausführen zu können. Viele wichtige Speichertests können nicht ausgeführt werden, wenn nur ein Knoten verfügbar ist.

### <a name="run-cluster-validation-tests"></a>Tests zur Clusterüberprüfung ausführen

1. Starten Sie den Failovercluster-Manager auf einem Computer, auf dem die Verwaltungstools für Failovercluster über die Remoteserver-Verwaltungstools installiert wurden, oder auf einem Server, auf dem Sie das Failoverclusteringfeature installiert haben. Starten Sie dazu auf einem Server, Server-Manager, und klicken Sie dann auf die **Tools** , wählen Sie im Menü **Failovercluster-Manager**.
2. In der **Failovercluster-Manager** Bereich unter **Management**Option **Konfiguration überprüfen**.
3. Auf der **Vorbemerkungen** Seite **Weiter**.
4. Auf der **Server auswählen oder in einem Cluster** auf der Seite die **Geben Sie den Namen** Feld Geben Sie den NetBIOS-Namen oder den vollqualifizierten Domänennamen eines Servers, den Sie als Failoverclusterknoten hinzufügen möchten, und wählen Sie dann auf **Hinzufügen**. Wiederholen Sie diesen Schritt für alle weiteren Server, die Sie hinzufügen möchten. Wenn Sie mehrere Server gleichzeitig hinzufügen möchten, trennen Sie die Namen durch ein Komma oder Semikolon. Geben Sie die Namen z. B. im Format *server1.contoso.com, server2.contoso.com* ein. Wenn Sie fertig sind, wählen Sie **Weiter**.
5. Auf der **Testoptionen** Seite **alle Tests ausführen (empfohlen)** , und wählen Sie dann **Weiter**.
6. Auf der **Bestätigung** Seite **Weiter**.

    Auf der Seite zur Ausführung der Überprüfung wird der Status der aktiven Tests angezeigt.
7. Führen Sie auf der Seite **Zusammenfassung** eine der folgenden Aktionen aus:
    
      - Wenn die Ergebnisse auf, dass die Tests erfolgreich abgeschlossen und die Konfiguration für clustering geeignet ist, und Sie den Cluster sofort erstellen möchten, stellen sicher, dass die **Cluster jetzt unter Verwendung der überprüften Knoten erstellen** überprüfen Feld ausgewählt ist, und wählen Sie dann **Fertig stellen**. Fahren Sie dann mit Schritt 4 des Verfahrens [Erstellen des Failoverclusters](#create-the-failover-cluster) fort.
      - Wenn die Ergebnisse auf Warnungen oder Fehler aufgetreten sind, wählen Sie **View-Bericht** um die Details anzuzeigen und zu bestimmen, welche Probleme behoben werden müssen. Beachten Sie, dass eine Warnung für einen bestimmten Validierungstest darauf hinweist, dass dieser Aspekt des Failoverclusters zwar unterstützt werden kann, er aber möglicherweise nicht den empfohlenen bewährten Methoden entspricht.
        
        >[!NOTE]
        >Wenn Sie eine Warnung für den Test "Permanente Reservierung für Speicherplatz überprüfen" erhalten, finden Sie weitere Informationen im Blogbeitrag [Windows Failover Cluster validation warning indicates your disks don't support the persistent reservations for Storage Spaces](https://blogs.msdn.microsoft.com/clustering/2013/05/24/validate-storage-spaces-persistent-reservation-test-results-with-warning/) .

Weitere Informationen zu Hardwareüberprüfungstests finden Sie unter [Validate Hardware for a Failover Cluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>).

## <a name="create-the-failover-cluster"></a>Erstellen des Failoverclusters

Stellen Sie zum Abschließen dieses Schritts sicher, dass das Benutzerkonto, mit dem Sie sich anmelden, den im Abschnitt [Überprüfen der Voraussetzungen](#verify-the-prerequisites) dieses Themas angegebenen Anforderungen entspricht.

1. Starten Sie den Server-Manager.
2. Auf der **Tools** , wählen Sie im Menü **Failovercluster-Manager**.
3. In der **Failovercluster-Manager** Bereich unter **Management**Option **Clustererstellungs**.
    
    Der Clustererstellungs-Assistent wird geöffnet.
4. Auf der **Vorbemerkungen** Seite **Weiter**.
5. Wenn die **Server auswählen** Seite angezeigt wird, in der **Geben Sie den Namen** Feld Geben Sie den NetBIOS-Namen oder den vollqualifizierten Domänennamen eines Servers, den Sie als Failoverclusterknoten hinzufügen möchten, und wählen Sie dann auf **Hinzufügen**. Wiederholen Sie diesen Schritt für alle weiteren Server, die Sie hinzufügen möchten. Wenn Sie mehrere Server gleichzeitig hinzufügen möchten, trennen Sie die Namen durch ein Komma oder Semikolon. Geben Sie die Namen z. B. im Format *server1.contoso.com; server2.contoso.com*ein. Wenn Sie fertig sind, wählen Sie **Weiter**.
    
    >[!NOTE]
    >Wenn Sie ausgewählt, zum Erstellen des Clusters haben, sofort nach dem Ausführen der Validierung der [Prozedur überprüft Configuration](#validate-the-configuration), nicht angezeigt wird der **Server auswählen** Seite. Die überprüften Knoten werden automatisch zum Clustererstellungs-Assistenten hinzugefügt, damit Sie diese nicht erneut eingeben müssen.
6. Wenn Sie die Validierung zuvor übersprungen haben, wird eine Seite mit einer **Validierungswarnung** angezeigt. Es wird dringend empfohlen, die Clustervalidierung auszuführen. Nur Cluster, die alle Validierungstests bestehen, werden von Microsoft unterstützt. Wählen Sie zum Ausführen der Validierungstests **Ja**, und wählen Sie dann **Weiter**. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, wie in beschrieben [Überprüfen der Konfiguration](#validate-the-configuration).
7. Gehen Sie auf der Seite **Zugriffspunkt für die Clusterverwaltung** wie folgt vor:
    
    1. Geben Sie in das Feld **Clustername** den Namen ein, über den Sie den Cluster verwalten möchten. Überprüfen Sie zuvor die folgenden Informationen:
        
          - Während der Clustererstellung wird dieser Name als Clustercomputerobjekt (auch als *Clusternamenobjekt* oder *CNO*bezeichnet) in AD DS registriert. Wenn Sie einen NetBIOS-Namen für den Cluster angeben, wird das Clustercomputerobjekt (CNO) am gleichen Speicherort erstellt, an dem sich die Computerobjekte für die Clusterknoten befinden. Hierbei kann es sich um den Standardcontainer des Computers oder um eine Organisationseinheit (OU) handeln.
          - Wenn Sie einen anderen Speicherort für das CNO angeben möchten, können Sie den Distinguished Name einer Organisationseinheit im Feld **Clustername** eingeben. Zum Beispiel: *CN=ClusterName, OU=Clusters, DC=Contoso, DC=com*.
          - Wenn ein Domänenadministrator das CNO in einer anderen Organisationseinheit vorab bereitgestellt hat, in der sich die Clusterknoten nicht befinden, geben Sie den Distinguished Name an, der vom Domänenadministrator bereitgestellt wird.
    2. Wenn der Server nicht über einen für DHCP konfigurierten Netzwerkadapter verfügt, müssen Sie mindestens eine statische IP-Adresse für den Failovercluster konfigurieren. Aktivieren Sie das Kontrollkästchen neben den jeweiligen Netzwerkadaptern, die Sie für die Clusterverwaltung verwenden möchten. Wählen Sie die **Adresse** Feld neben einem ausgewählten Netzwerk aus, und geben Sie dann die IP-Adresse, die Sie dem Cluster zuweisen möchten. Diese IP-Adresse (oder Adressen) wird dem Clusternamen im Domain Name System zugeordnet.
    3. Wenn Sie fertig sind, wählen Sie **Weiter**.
8. Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen. Das Kontrollkästchen **Der gesamte geeignete Speicher soll dem Cluster hinzugefügt werden** ist standardmäßig aktiviert. Deaktivieren Sie dieses Kontrollkästchen, wenn Sie eine der folgenden Optionen ausführen möchten:
    
      - Sie möchten den Speicher später konfigurieren.
      - Sie planen die Erstellung von Clusterspeicherplätzen über den Failovercluster-Manager oder mithilfe von Windows PowerShell-Cmdlets für Failoverclustering und haben bisher keine Speicherplätze in den Datei- und Speicherdiensten erstellt. Weitere Informationen finden Sie unter [Deploy Clustered Storage Spaces](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>).
9. Wählen Sie **Weiter** zum Erstellen des Failoverclusters.
10. Bestätigen Sie auf der Seite **Zusammenfassung** die erfolgreiche Erstellung des Failoverclusters. Gäbe es keine Warnungen oder Fehler, zeigen Sie die Ausgabe: Zusammenfassung oder wählen Sie **View-Bericht** auf den vollständigen Bericht anzuzeigen. Wählen Sie **Fertig stellen**.
11. Überprüfen Sie, ob der Clustername in der Navigationsstruktur unter **Failovercluster-Manager** aufgeführt ist, um die Erstellung des Clusters zu bestätigen. Sie können den Clusternamen erweitern und wählen Sie dann die Elemente unter **Knoten**, **Storage** oder **Netzwerke** um die zugehörigen Ressourcen anzuzeigen.
    
    Beachten Sie, dass es einen Moment dauern kann, bevor der Clustername im DNS erfolgreich repliziert wird. Nach der erfolgreichen DNS-Registrierung und die Replikation, wenn Sie die Option **alle Server** im Server-Manager der Clustername aufgeführt werden als Server mit einem **Verwaltbarkeit** Status **Online** .

Nach der Erstellung des Clusters können Sie z. B. die Clusterquorumkonfiguration überprüfen und optional freigegebene Clustervolumes (CSV) erstellen. Weitere Informationen finden Sie unter [Understanding Quorum in "direkte Speicherplätze"](../storage/storage-spaces/understand-quorum.md) und [Use Cluster Shared Volumes in einem Failovercluster](failover-cluster-csvs.md).

## <a name="create-clustered-roles"></a>Erstellen von Clusterrollen

Nachdem Sie den Failovercluster erstellt haben, können Sie Clusterrollen zum Hosten der Clusterarbeitsauslastung erstellen.

>[!NOTE]
>Für Clusterrollen, die einen Clientzugriffspunkt erfordern, wird ein virtuelles Computerobjekt (Virtual Computer Object, VCO) in AD DS erstellt. Standardmäßig werden alle virtuellen Computerobjekte für den Cluster in demselben Container oder in derselben Organisationseinheit wie das CNO erstellt. Beachten Sie, dass Sie das CNO nach der Erstellung eines Clusters in eine beliebige Organisationseinheit verschieben können.

Hier wird eine Clusterrolle zu erstellen:

1. Installieren Sie die Rolle oder das Feature, die bzw. das für eine Clusterrolle erforderlich ist, mit dem Server-Manager oder Windows PowerShell auf jeden Failoverclusterknoten. Wenn Sie z. B. einen Clusterdateiserver erstellen möchten, installieren Sie die Rolle "Dateiserver" auf allen Clusterknoten.
    
    In der folgenden Tabelle werden die Clusterrollen, die Sie im Assistenten für hohe Verfügbarkeit konfigurieren sowie die zugehörige Serverrolle oder das Feature angezeigt, die Sie als Voraussetzung installieren müssen.
    

|Clusterrolle  |Vorausgesetzte(s) Rolle oder Feature  |
|---------|---------|
|Namespace-Server     |   Namespaces (Teil der Rolle "Dateiserver")       |
|DFS-Namespaceserver     |  DHCP-Serverrolle       |
|Distributed Transaction Coordinator (DTC)     | Keine        |
|Dateiserver     |  Dateiserverrolle       |
|Allgemeine Anwendung     |  Nicht verfügbar       |
|Allgemeines Skript     |   Nicht verfügbar      |
|Allgemeiner Dienst     |   Nicht verfügbar      |
|Hyper-V-Replikatbroker     |   Hyper-V-Rolle      |
|iSCSI-Zielserver     |    iSCSI-Zielserver (Teil der Dateiserverrolle)     |
|iSNS-Server     |  iSNS-Serverdienstfeature       |
|Message Queuing     |  Message Queuing-Dienstfeature       |
|Anderer Server     |  Keine       |
|Virtueller Computer     |  Hyper-V-Rolle       |
|WINS-Server     |   WINS-Server-Feature      |

2. Im Failovercluster-Manager, erweitern Sie den Clusternamen, mit der rechten Maustaste **Rollen**, und wählen Sie dann **Rolle konfigurieren**.
3. Folgen Sie den Schritten im Assistenten für hohe Verfügbarkeit, um die Clusterrolle zu erstellen.
4. Stellen Sie im Bereich **Rollen** sicher, dass die Rolle den Status **Wird ausgeführt**aufweist, um die Erstellung der Clusterrolle zu überprüfen. Im Bereich "Rollen" wird auch der Besitzerknoten angezeigt. Um einen Failovertest durchzuführen, mit der rechten Maustaste in der Rolle, zeigen Sie auf **verschieben**, und wählen Sie dann **Knoten auswählen**. In der **Clusterrolle verschieben** Dialogfeld Wählen Sie den gewünschten Clusterknoten, und wählen Sie dann **OK**. Überprüfen Sie in der Spalte **Besitzerknoten** , ob der Besitzerknoten geändert wurde.

## <a name="create-a-failover-cluster-by-using-windows-powershell"></a>Erstellen eines Failoverclusters mithilfe von Windows PowerShell

Die folgenden Windows PowerShell-Cmdlets führen die gleichen Funktionen wie das vorhergehenden Verfahren in diesem Thema. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

>[!NOTE]
>Sie müssen Windows PowerShell verwenden, um einen Active Directory getrennten Cluster in Windows Server 2012 R2 zu erstellen. Informationen zur Syntax finden Sie unter [Deploy an Active Directory-Detached Cluster](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

Im folgenden Beispiel wird das Failoverclusteringfeature installiert.

```PowerShell
Install-WindowsFeature –Name Failover-Clustering –IncludeManagementTools
```

Im folgenden Beispiel werden alle Clustervalidierungstests auf den Computern *Server1* und *Server2*ausgeführt.

```PowerShell
Test-Cluster –Node Server1, Server2
```

>[!NOTE]
>Die **Test-Cluster** Cmdlet gibt die Ergebnisse in eine Protokolldatei im aktuellen Arbeitsverzeichnis. Zum Beispiel: C:\Users\<Username > \AppData\Local\Temp.

Im folgenden Beispiel wird ein Failovercluster namens *MyCluster* mit den Knoten *Server1* und *Server2*erstellt, die statische IP-Adresse *192.168.1.12*zugewiesen und der gesamte geeignete Speicher zum Failovercluster hinzugefügt.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12
```

Im folgenden Beispiel wird derselbe Failovercluster wie im vorherigen Beispiel erstellt, aber nicht der geeignete Speicher zum Failovercluster hinzugefügt.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12 -NoStorage
```

Im folgenden Beispiel wird der Cluster *MyCluster* in der Organisationseinheit *Cluster* der Domäne *Contoso.com*erstellt.

```PowerShell
New-Cluster -Name CN=MyCluster,OU=Cluster,DC=Contoso,DC=com -Node Server1, Server2
```

Beispiele zum Hinzufügen von Clusterrollen finden Sie in Themen wie z. B. [Add-ClusterFileServerRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clusterfileserverrole?view=win10-ps) und [Add-ClusterGenericApplicationRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergenericapplicationrole?view=win10-ps).

## <a name="more-information"></a>Weitere Informationen

  - [Failoverclustering](failover-clustering.md)
  - [Bereitstellen eines Hyper-V-Clusters](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj863389(v%3dws.11)>)
  - [Server der Dateiserver mit horizontaler Skalierung für Anwendungsdaten](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831349(v%3dws.11)>)
  - [Bereitstellen eines von Active Directory getrennten Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))
  - [Verwenden von Gastclustering für hohe Verfügbarkeit](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)
  - [Clusterfähiges Aktualisieren](cluster-aware-updating.md)
  - [New-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/new-cluster?view=win10-ps)
  - [Test-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)
