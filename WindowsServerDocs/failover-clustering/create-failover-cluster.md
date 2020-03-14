---
title: Erstellen eines Failoverclusters
description: Erstellen eines Failoverclusters für Windows Server 2012 R2, Windows Server 2012, Windows Server 2016 und Windows Server 2019.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: d85866284272d80727d3fdb21c6e6447bd3ded2f
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322812"
---
# <a name="create-a-failover-cluster"></a>Erstellen eines Failoverclusters

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012

In diesem Thema wird gezeigt, wie ein Failovercluster mithilfe des Failovercluster-Manager-Snap-Ins oder mit Windows PowerShell erstellt wird. Das Thema behandelt eine typische Bereitstellung, bei der Computerobjekte für den Cluster und seine zugehörigen Clusterrollen in Active Directory-Domänendiensten (AD DS) erstellt werden. Wenn Sie einen direkte Speicherplätze Cluster bereitstellen, finden Sie weitere Informationen unter Bereitstellen [direkte Speicherplätze](../storage/storage-spaces/deploy-storage-spaces-direct.md).

Sie können auch einen Active Directory getrennten Cluster bereitstellen. Mit dieser Bereitstellungsmethode können Sie einen Failovercluster erstellen und benötigen dazu nicht die Berechtigungen zum Erstellen von Computerobjekten in AD DS. Außerdem müssen Sie nicht die Vorabbereitstellung von Computerobjekten in AD DS anfordern. Diese Option ist nur über Windows PowerShell verfügbar und wird nur für bestimmte Szenarien empfohlen. Weitere Informationen finden Sie unter [Bereitstellen eines von Active Directory getrennten Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

#### <a name="checklist-create-a-failover-cluster"></a>Prüfliste: Erstellen eines Failoverclusters

| Status | Aufgabe | Verweis |
| ---    | ---  | ---       |
| ☐    | Überprüfen der Voraussetzungen | [Überprüfen der Voraussetzungen](#verify-the-prerequisites) |
| ☐    | Installieren Sie das Failoverclusteringfeature auf jedem Server, den Sie als Clusterknoten hinzufügen möchten. | [Installieren des Failoverclustering-Features](#install-the-failover-clustering-feature) |
| ☐    | Ausführen des Clusterüberprüfungs-Assistenten zum Überprüfen der Konfiguration | [Überprüfen der Konfiguration](#validate-the-configuration) |
| ☐ | Ausführen des Clustererstellungs-Assistenten zum Erstellen des Failoverclusters | [Erstellen des Failoverclusters](#create-the-failover-cluster) |
| ☐ | Erstellen von Clusterrollen zum Hosten der Clusterarbeitsauslastung | [Erstellen von Cluster Rollen](#create-clustered-roles) |

## <a name="verify-the-prerequisites"></a>Überprüfen der Voraussetzungen

Bevor Sie beginnen, überprüfen Sie die folgenden Voraussetzungen:

- Stellen Sie sicher, dass alle Server, die Sie als Clusterknoten hinzufügen möchten, dieselbe Version von Windows Server ausführen.
- Überprüfen Sie die Hardwareanforderungen, um sicherzustellen, dass Ihre Konfiguration unterstützt wird. Weitere Informationen finden Sie unter [Hardwareanforderungen und Speicheroptionen für Failovercluster](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj612869(v%3dws.11)). Wenn Sie einen direkte Speicherplätze Cluster erstellen, finden Sie unter [direkte Speicherplätze Hardwareanforderungen](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md)Weitere Informationen.
- Um Cluster Speicher während der Cluster Erstellung hinzuzufügen, stellen Sie sicher, dass alle Server auf den Speicher zugreifen können. (Sie können Clusterspeicher auch nach der Erstellung des Clusters hinzufügen.)
- Stellen Sie sicher, dass alle Server, die Sie als Clusterknoten hinzufügen möchten, derselben Active Directory-Domäne angehören.
- (Optional) Erstellen Sie eine Organisationseinheit (OU), und verschieben Sie die Computerkonten für die Server, die Sie als Clusterknoten hinzufügen möchten, in die Organisationseinheit. Als bewährte Methode wird empfohlen, dass Sie Failovercluster in ihren eigenen Organisationseinheiten in AD DS bereitstellen. Auf diese Weise können Sie besser kontrollieren, welche Gruppenrichtlinieneinstellungen oder Sicherheitsvorlageneinstellungen die Clusterknoten beeinflussen. Das Isolieren der Cluster in eigenen Organisationseinheiten schützt zudem vor dem versehentlichen Löschen von Clustercomputerobjekten.

Überprüfen Sie zusätzlich die folgenden Kontoanforderungen:

- Stellen Sie sicher, dass das Konto, das Sie zum Erstellen des Clusters verwenden möchten, einem Domänenbenutzer entspricht, der auf allen Servern, die Sie als Clusterknoten hinzufügen möchten, über Administratorrechte verfügt.
- Stellen Sie sicher, dass eine der folgenden Optionen zutrifft:
    - Der Benutzer, der die Cluster erstellt, verfügt für die Organisationseinheit oder den Container, in dem sich die Server befinden, die den Cluster bilden, über die Berechtigung **Computerobjekte erstellen**.
    - Wenn der Benutzer nicht über die Berechtigung **Computerobjekte erstellen** verfügt, bitten Sie einen Domänenadministrator, ein Clustercomputerobjekt für den Cluster vorab bereitzustellen. Weitere Informationen finden Sie unter [Vorabbereitstellen von Clustercomputerobjekten in Active Directory-Domänendiensten](prestage-cluster-adds.md).

> [!NOTE]
> Diese Anforderung trifft nicht zu, wenn Sie einen Active Directory getrennten Cluster in Windows Server 2012 R2 erstellen möchten. Weitere Informationen finden Sie unter [Bereitstellen eines von Active Directory getrennten Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

## <a name="install-the-failover-clustering-feature"></a>Installieren des Failoverclusteringfeatures

Sie müssen das Failoverclusteringfeature auf jedem Server installieren, den Sie als Failoverclusterknoten hinzufügen möchten.

### <a name="install-the-failover-clustering-feature"></a>Installieren des Failoverclusteringfeatures

1. Starten Sie den Server-Manager.
2. Wählen Sie im Menü **Verwalten** die Option **Rollen und Features hinzufügen**aus.
3. Wählen Sie **auf der Seite** Vorbereitung die Option **weiter**aus.
4. Wählen Sie auf der Seite **Installationstyp auswählen** die Option **rollenbasierte oder featurebasierte Installation**aus, und klicken Sie dann auf **weiter**.
5. Wählen Sie auf der Seite **Zielserver auswählen** den Server aus, auf dem Sie das Feature installieren möchten, und klicken Sie dann auf **weiter**.
6. Wählen Sie **Weiter** auf der Seite **Serverrollen auswählen** aus.
7. Aktivieren Sie auf der Seite **Features auswählen** das Kontrollkästchen **Failoverclustering**.
8. Wählen Sie zum Installieren der Failovercluster-Verwaltungs Tools **Features hinzufügen**aus, und klicken Sie dann auf **weiter**.
9. Wählen Sie auf der Seite **Installations Auswahl bestätigen** die Option **Installieren**aus.
<br>Ein Neustart des Servers ist für das Failoverclusteringfeature nicht erforderlich.

10. Wenn die Installation abgeschlossen ist, wählen Sie **Schließen**aus.
11. Wiederholen Sie diesen Vorgang auf jedem Server, den Sie als Failoverclusterknoten hinzufügen möchten.

> [!NOTE]
> Es wird empfohlen, dass Sie nach der Installation des Failoverclusteringfeatures die neuesten Updates von Windows Update anwenden. Lesen Sie außerdem für einen Windows Server 2012-basierten Failovercluster die [empfohlenen Hotfixes und Updates für Windows Server 2012-basierte Failovercluster](https://support.microsoft.com/help/2784261/recommended-hotfixes-and-updates-for-windows-server-2012-based-failove) Microsoft-Support Artikel, und installieren Sie alle Updates, die angewendet werden.

## <a name="validate-the-configuration"></a>Überprüfen der Konfiguration

Vor der Erstellung des Failovercluster wird dringend empfohlen, dass Sie die Konfiguration überprüfen, um sicherzustellen, dass die Hardware und die Hardwareeinstellungen mit dem Failoverclustering kompatibel sind. Microsoft unterstützt eine Clusterlösung nur, wenn die gesamte Konfiguration die Validierungstests besteht und die gesamte Hardware für die Version von Windows Server zertifiziert ist, die auf den Clusterknoten ausgeführt wird.

> [!NOTE]
> Sie müssen mindestens zwei Knoten besitzen, um alle Tests ausführen zu können. Viele wichtige Speichertests können nicht ausgeführt werden, wenn nur ein Knoten verfügbar ist.

### <a name="run-cluster-validation-tests"></a>Ausführen von Cluster Validierungstests

1. Starten Sie den Failovercluster-Manager auf einem Computer, auf dem die Verwaltungstools für Failovercluster über die Remoteserver-Verwaltungstools installiert wurden, oder auf einem Server, auf dem Sie das Failoverclusteringfeature installiert haben. Um dies auf einem Server zu erreichen, starten Sie Server-Manager, und wählen Sie dann **im Menü Extras** die Option **Failovercluster-Manager**aus.
2. Klicken Sie im **Failovercluster-Manager** Bereich unter **Verwaltung**auf **Konfiguration**überprüfen.
3. Wählen Sie **auf der Seite** Vorbereitung die Option **weiter**aus.
4. Geben Sie auf der Seite **Server oder Cluster auswählen** in das Feld **Name eingeben** den NetBIOS-Namen oder den voll qualifizierten Domänen Namen eines Servers ein, den Sie als Failoverclusterknoten hinzufügen möchten, und klicken Sie dann auf **Hinzufügen**. Wiederholen Sie diesen Schritt für alle weiteren Server, die Sie hinzufügen möchten. Wenn Sie mehrere Server gleichzeitig hinzufügen möchten, trennen Sie die Namen durch ein Komma oder Semikolon. Geben Sie z. b. die Namen im Format `server1.contoso.com, server2.contoso.com`ein. Wenn Sie fertig sind, wählen Sie **weiter**aus.
5. Wählen Sie auf der Seite **Test Optionen die Option** **alle Tests ausführen (empfohlen)** aus, und klicken Sie dann auf **weiter**.
6. Wählen Sie auf der Seite **Bestätigung** die Option **weiter**aus.

    Auf der Seite zur Ausführung der Überprüfung wird der Status der aktiven Tests angezeigt.
7. Führen Sie auf der Seite **Zusammenfassung** eine der folgenden Aktionen aus:
    
      - Wenn die Ergebnisse auf eine erfolgreiche Ausführung der Tests hinweisen und die Konfiguration für das Clustering geeignet ist und Sie den Cluster sofort erstellen möchten, stellen Sie sicher, dass das Kontrollkästchen **Cluster jetzt mit den überprüften Knoten erstellen** aktiviert ist, und klicken Sie dann auf **Fertig**stellen. Fahren Sie dann mit Schritt 4 des Verfahrens [Erstellen des Failoverclusters](#create-the-failover-cluster) fort.
      - Wenn die Ergebnisse darauf hindeuten, dass Warnungen oder Fehler aufgetreten sind, wählen Sie **Bericht anzeigen** aus, um die Details anzuzeigen und zu ermitteln, welche Probleme korrigiert werden müssen. Beachten Sie, dass eine Warnung für einen bestimmten Validierungstest darauf hinweist, dass dieser Aspekt des Failoverclusters zwar unterstützt werden kann, er aber möglicherweise nicht den empfohlenen bewährten Methoden entspricht.
        
        > [!NOTE]
        > Wenn Sie eine Warnung für den Test "Permanente Reservierung für Speicherplatz überprüfen" erhalten, finden Sie weitere Informationen im Blogbeitrag [Windows Failover Cluster validation warning indicates your disks don't support the persistent reservations for Storage Spaces](https://blogs.msdn.microsoft.com/clustering/2013/05/24/validate-storage-spaces-persistent-reservation-test-results-with-warning/) .

Weitere Informationen zu Hardwarevalidierungstests finden Sie unter [Überprüfen der Hardware für einen Failovercluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>).

## <a name="create-the-failover-cluster"></a>Erstellen des Failoverclusters

Stellen Sie zum Abschließen dieses Schritts sicher, dass das Benutzerkonto, mit dem Sie sich anmelden, den im Abschnitt [Überprüfen der Voraussetzungen](#verify-the-prerequisites) dieses Themas angegebenen Anforderungen entspricht.

1. Starten Sie den Server-Manager.
2. Wählen Sie **im Menü Extras** die Option **Failovercluster-Manager**aus.
3. Klicken Sie im **Failovercluster-Manager** Bereich unter **Verwaltung**auf **Cluster erstellen**.
    
    Der Clustererstellungs-Assistent wird geöffnet.
4. Wählen Sie **auf der Seite** Vorbereitung die Option **weiter**aus.
5. Wenn die Seite **Server auswählen** angezeigt wird, geben Sie in das Feld **Name eingeben** den NetBIOS-Namen oder den voll qualifizierten Domänen Namen eines Servers ein, den Sie als Failoverclusterknoten hinzufügen möchten, und klicken Sie dann auf **Hinzufügen**. Wiederholen Sie diesen Schritt für alle weiteren Server, die Sie hinzufügen möchten. Wenn Sie mehrere Server gleichzeitig hinzufügen möchten, trennen Sie die Namen durch ein Komma oder Semikolon. Geben Sie die Namen z. B. im Format *server1.contoso.com; server2.contoso.com* ein. Wenn Sie fertig sind, wählen Sie **weiter**aus.
    
    > [!NOTE]
    > Wenn Sie den Cluster sofort nach dem Ausführen der Überprüfung im [Konfigurations Überprüfungsverfahren](#validate-the-configuration)erstellt haben, wird die Seite **Server auswählen** nicht angezeigt. Die überprüften Knoten werden automatisch zum Clustererstellungs-Assistenten hinzugefügt, damit Sie diese nicht erneut eingeben müssen.
6. Wenn Sie die Validierung zuvor übersprungen haben, wird eine Seite mit einer **Validierungswarnung** angezeigt. Es wird dringend empfohlen, die Clustervalidierung auszuführen. Nur Cluster, die alle Validierungstests bestehen, werden von Microsoft unterstützt. Um die Validierungstests auszuführen, wählen Sie **Ja**aus, und klicken Sie dann auf **weiter**. Führen Sie den Konfigurationsüberprüfungs-Assistenten wie unter Überprüfen [der Konfiguration](#validate-the-configuration)beschrieben aus.
7. Gehen Sie auf der Seite **Zugriffspunkt für die Clusterverwaltung** wie folgt vor:
    
    1. Geben Sie in das Feld **Clustername** den Namen ein, über den Sie den Cluster verwalten möchten. Überprüfen Sie zuvor die folgenden Informationen:
        
          - Während der Clustererstellung wird dieser Name als Clustercomputerobjekt (auch als *Clusternamenobjekt* oder *CNO*bezeichnet) in AD DS registriert. Wenn Sie einen NetBIOS-Namen für den Cluster angeben, wird das Clustercomputerobjekt (CNO) am gleichen Speicherort erstellt, an dem sich die Computerobjekte für die Clusterknoten befinden. Hierbei kann es sich um den Standardcontainer des Computers oder um eine Organisationseinheit (OU) handeln.
          - Wenn Sie einen anderen Speicherort für das CNO angeben möchten, können Sie den Distinguished Name einer Organisationseinheit im Feld **Clustername** eingeben. Zum Beispiel: *CN=ClusterName, OU=Clusters, DC=Contoso, DC=com*.
          - Wenn ein Domänenadministrator das CNO in einer anderen Organisationseinheit vorab bereitgestellt hat, in der sich die Clusterknoten nicht befinden, geben Sie den Distinguished Name an, der vom Domänenadministrator bereitgestellt wird.
    2. Wenn der Server nicht über einen für DHCP konfigurierten Netzwerkadapter verfügt, müssen Sie mindestens eine statische IP-Adresse für den Failovercluster konfigurieren. Aktivieren Sie das Kontrollkästchen neben den jeweiligen Netzwerkadaptern, die Sie für die Clusterverwaltung verwenden möchten. Wählen Sie das Feld **Adresse** neben einem ausgewählten Netzwerk aus, und geben Sie dann die IP-Adresse ein, die Sie dem Cluster zuweisen möchten. Diese IP-Adresse (oder Adressen) wird dem Clusternamen im Domain Name System zugeordnet.
    
      >[!NOTE]
      > Wenn Sie Windows Server 2019 verwenden, haben Sie die Möglichkeit, einen verteilten Netzwerknamen für den Cluster zu verwenden. Ein verteilter Netzwerkname verwendet die IP-Adressen der Mitglieds Server, anstatt eine dedizierte IP-Adresse für den Cluster zu erfordern. Standardmäßig wird von Windows ein verteilter Netzwerkname verwendet, wenn erkannt wird, dass Sie den Cluster in Azure erstellen (sodass Sie keinen internen Lastenausgleich für den Cluster erstellen müssen) oder eine normale statische oder IP-Adresse, wenn Sie lokal ausgeführt werden. Weitere Informationen finden Sie unter [Name des verteilten Netzwerks](https://blogs.windows.com/windowsexperience/2018/08/14/announcing-windows-server-2019-insider-preview-build-17733/#W0YAxO8BfwBRbkzG.97).
    
    3. Wenn Sie fertig sind, wählen Sie **weiter**aus.
8. Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen. Das Kontrollkästchen **Der gesamte geeignete Speicher soll dem Cluster hinzugefügt werden** ist standardmäßig aktiviert. Deaktivieren Sie dieses Kontrollkästchen, wenn Sie eine der folgenden Optionen ausführen möchten:
    
      - Sie möchten den Speicher später konfigurieren.
      - Sie planen die Erstellung von Clusterspeicherplätzen über den Failovercluster-Manager oder mithilfe von Windows PowerShell-Cmdlets für Failoverclustering und haben bisher keine Speicherplätze in den Datei- und Speicherdiensten erstellt. Weitere Informationen finden Sie unter [Bereitstellen von Clusterspeicherplätzen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>).
9. Wählen Sie **weiter** aus, um den Failovercluster zu erstellen.
10. Bestätigen Sie auf der Seite **Zusammenfassung** die erfolgreiche Erstellung des Failoverclusters. Wenn Warnungen oder Fehler aufgetreten sind, zeigen Sie die Ausgabe der Zusammenfassung an, oder wählen Sie **Bericht anzeigen** aus, um den vollständigen Bericht anzuzeigen. Wählen Sie **Fertig stellen** aus.
11. Überprüfen Sie, ob der Clustername in der Navigationsstruktur unter **Failovercluster-Manager** aufgeführt ist, um die Erstellung des Clusters zu bestätigen. Sie können den Cluster Namen erweitern und dann unter **Knoten**, **Speicher** oder **Netzwerke** Elemente auswählen, um die zugeordneten Ressourcen anzuzeigen.
    
    Beachten Sie, dass es einen Moment dauern kann, bevor der Clustername im DNS erfolgreich repliziert wird. Wenn Sie nach der erfolgreichen DNS-Registrierung und-Replikation **alle Server** in Server-Manager ausgewählt haben, sollte der Cluster Name als Server mit dem **verwaltbarkeitsstatus** **Online**aufgeführt werden.

Nach der Erstellung des Clusters können Sie z. B. die Clusterquorumkonfiguration überprüfen und optional freigegebene Clustervolumes (CSV) erstellen. Weitere Informationen finden Sie Untergrund Legendes zu [Quorums in direkte Speicherplätze](../storage/storage-spaces/understand-quorum.md) und [Verwenden von freigegebenen Clustervolumes in einem Failovercluster](failover-cluster-csvs.md).

## <a name="create-clustered-roles"></a>Erstellen von Clusterrollen

Nachdem Sie den Failovercluster erstellt haben, können Sie Clusterrollen zum Hosten der Clusterarbeitsauslastung erstellen.

>[!NOTE]
>Für Clusterrollen, die einen Clientzugriffspunkt erfordern, wird ein virtuelles Computerobjekt (Virtual Computer Object, VCO) in AD DS erstellt. Standardmäßig werden alle virtuellen Computerobjekte für den Cluster in demselben Container oder in derselben Organisationseinheit wie das CNO erstellt. Beachten Sie, dass Sie das CNO nach der Erstellung eines Clusters in eine beliebige Organisationseinheit verschieben können.

So erstellen Sie eine Cluster Rolle:

1. Installieren Sie die Rolle oder das Feature, die bzw. das für eine Clusterrolle erforderlich ist, mit dem Server-Manager oder Windows PowerShell auf jeden Failoverclusterknoten. Wenn Sie z. B. einen Clusterdateiserver erstellen möchten, installieren Sie die Rolle "Dateiserver" auf allen Clusterknoten.
    
    In der folgenden Tabelle werden die Clusterrollen, die Sie im Assistenten für hohe Verfügbarkeit konfigurieren sowie die zugehörige Serverrolle oder das Feature angezeigt, die Sie als Voraussetzung installieren müssen.

   | Clusterrolle  | Vorausgesetzte(s) Rolle oder Feature  |
   | ---------       | ---------                    |
   | Namespace Server     |   Namespaces (Teil der Datei Server Rolle)       |
   | DFS-Namespaceserver     |  DHCP-Serverrolle       |
   | Distributed Transaction Coordinator (DTC)     | Keine        |
   | Dateiserver     |  Dateiserverrolle       |
   | Generische Anwendung     |  Nicht verfügbar       |
   | Generisches Skript     |   Nicht verfügbar      |
   | Generischer Dienst     |   Nicht verfügbar      |
   | Hyper-V-Replikatbroker     |   Hyper-V-Rolle      |
   | iSCSI-Zielserver     |    iSCSI-Zielserver (Teil der Dateiserverrolle)     |
   | iSNS-Server     |  iSNS-Serverdienstfeature       |
   | Message Queuing     |  Message Queuing-Dienstfeature       |
   | Anderer Server     |  Keine       |
   | Virtuelle Maschine     |  Hyper-V-Rolle       |
   | WINS-Server     |   WINS-Server-Feature      |

2. Erweitern Sie in Failovercluster-Manager den Cluster Namen, klicken Sie mit der rechten Maustaste auf **Rollen**, und wählen Sie dann **Rolle konfigurieren**aus.
3. Folgen Sie den Schritten im Assistenten für hohe Verfügbarkeit, um die Clusterrolle zu erstellen.
4. Stellen Sie im Bereich **Rollen** sicher, dass die Rolle den Status **Wird ausgeführt** aufweist, um die Erstellung der Clusterrolle zu überprüfen. Im Bereich "Rollen" wird auch der Besitzerknoten angezeigt. Um das Failover zu testen, klicken Sie mit der rechten Maustaste auf die Rolle, zeigen Sie auf **verschieben**, und wählen Sie dann **Knoten auswählen**. Wählen Sie im Dialogfeld **Cluster Rolle verschieben** den gewünschten Cluster Knoten aus, und klicken Sie dann auf **OK**. Überprüfen Sie in der Spalte **Besitzerknoten**, ob der Besitzerknoten geändert wurde.

## <a name="create-a-failover-cluster-by-using-windows-powershell"></a>Erstellen eines Failoverclusters mithilfe von Windows PowerShell

Die folgenden Windows PowerShell-Cmdlets führen dieselben Funktionen aus wie die vorherigen Prozeduren in diesem Thema. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

> [!NOTE]
> Sie müssen Windows PowerShell verwenden, um einen Active Directory getrennten Cluster in Windows Server 2012 R2 zu erstellen. Weitere Informationen zur Syntax finden Sie unter [Bereitstellen eines von Active Directory getrennten Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

Im folgenden Beispiel wird das Failoverclusteringfeature installiert.

```PowerShell
Install-WindowsFeature –Name Failover-Clustering –IncludeManagementTools
```

Im folgenden Beispiel werden alle Clustervalidierungstests auf den Computern *Server1* und *Server2* ausgeführt.

```PowerShell
Test-Cluster –Node Server1, Server2
```

> [!NOTE]
> Das **Test-Cluster-** Cmdlet gibt die Ergebnisse in eine Protokolldatei im aktuellen Arbeitsverzeichnis aus. Beispiel: c:\Users\<username > \AppData\Local\Temp.

Im folgenden Beispiel wird ein Failovercluster namens *MyCluster* mit den Knoten *Server1* und *Server2* erstellt, die statische IP-Adresse *192.168.1.12* zugewiesen und der gesamte geeignete Speicher zum Failovercluster hinzugefügt.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12
```

Im folgenden Beispiel wird derselbe Failovercluster wie im vorherigen Beispiel erstellt, aber nicht der geeignete Speicher zum Failovercluster hinzugefügt.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12 -NoStorage
```

Im folgenden Beispiel wird der Cluster *MyCluster* in der Organisationseinheit *Cluster* der Domäne *Contoso.com* erstellt.

```PowerShell
New-Cluster -Name CN=MyCluster,OU=Cluster,DC=Contoso,DC=com -Node Server1, Server2
```

Beispiele zum Hinzufügen von Clusterrollen finden Sie in Themen wie z. B. [Add-ClusterFileServerRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clusterfileserverrole?view=win10-ps) und [Add-ClusterGenericApplicationRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergenericapplicationrole?view=win10-ps).

## <a name="more-information"></a>Weitere Informationen

  - [Failoverclustering](failover-clustering.md)
  - [Bereitstellen eines Hyper-V-Clusters](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj863389(v%3dws.11)>)
  - [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831349(v%3dws.11)>)
  - [Bereitstellen eines Active Directory getrennten Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))
  - [Verwenden von Gastclustering für hohe Verfügbarkeit](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)
  - [Clusterfähiges Aktualisieren](cluster-aware-updating.md)
  - [Neu-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/new-cluster?view=win10-ps)
  - [Test-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)
