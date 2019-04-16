---
title: Erstellen eines Failoverclusters
description: So erstellen Sie einen Failovercluster für Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f919e69488c4f2272ddd07e535ba4e2248ddf79c
ms.sourcegitcommit: 5cbaca9685720f11d896c4ca167c86e74c032feb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2018
ms.locfileid: "6068978"
---
# Erstellen eines Failoverclusters

>Gilt für: Windows Server 2012 R2, WindowsServer 2012, WindowsServer 2016

Dieses Thema zeigt, wie auf einen Failovercluster zu erstellen, indem Sie mit dem Failovercluster-Manager-Snap-in oder Windows PowerShell. Das Thema umfasst typischerweise, wo Computerobjekte für den Cluster und seine zugeordneten clusterrollen in Active Directory-Domänendiensten (AD DS) erstellt werden. Wenn Sie einen "direkte Speicherplätze" Cluster bereitstellen, finden Sie stattdessen unter [Bereitstellen von "direkte Speicherplätze"](../storage/storage-spaces/deploy-storage-spaces-direct.md).

Sie können auch einen Cluster Active Directory getrennt bereitstellen. Diese Methode der Bereitstellung können Sie zum Erstellen eines Failoverclusters ohne Berechtigungen zum Erstellen von Computerobjekten in AD DS oder der Notwendigkeit, den Computer anzufordern, die Objekte in AD DS vorbereitet sind. Diese Option ist nur über Windows PowerShell verfügbar und wird nur für bestimmte Szenarien empfohlen. Weitere Informationen finden Sie unter [einem Cluster Active Directory-Detached bereitstellen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

#### Prüfliste: Erstellen eines Failoverclusters

|Status|Aufgabe|Referenz|
|:---:|---|---|
|☐|Überprüfen Sie die erforderlichen Komponenten|[Überprüfen Sie die erforderlichen Komponenten](#verify-the-prerequisites)|
|☐|Installieren Sie die Failover-Clusterunterstützung auf jedem Server, die Sie als Clusterknoten hinzufügen möchten|[Installieren Sie die Failover-Clusterunterstützung](#install-the-failover-clustering-feature)|
|☐|Führen Sie zum Überprüfen der Konfigurations der Clusterüberprüfungs-Assistenten|[Überprüfen der Konfigurations](#validate-the-configuration)|
|☐|Führen Sie den Assistenten zum Erstellen von Cluster um Failovercluster zu erstellen.|[Erstellen Sie den Failovercluster](#create-the-failover-cluster)|
|☐|Erstellen von clusterrollen zu-Cluster-Arbeitslasten|[Erstellen von clusterrollen](#create-clustered-roles)|

## Überprüfen Sie die erforderlichen Komponenten

Bevor Sie beginnen, vergewissern Sie sich die folgenden Voraussetzungen:

- Stellen Sie sicher, dass auf allen Servern, die Sie als Knoten im Cluster hinzufügen möchten die gleiche Version von Windows Server ausgeführt werden.
- Überprüfen Sie die hardwareanforderungen, um sicherzustellen, dass die Konfiguration unterstützt wird. Weitere Informationen finden Sie unter [Failover-Clusterunterstützung Hardwareanforderungen und Speicheroptionen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj612869(v%3dws.11)). Wenn Sie einen "direkte Speicherplätze"-Cluster erstellen, finden Sie unter ["direkte Speicherplätze" hardwareanforderungen](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md).
- Um Speicher im Cluster während der Erstellung des Clusters hinzuzufügen, stellen Sie sicher, dass alle Server den Speicher zugreifen können. (Sie können auch Speicher im Cluster hinzufügen, nach der Erstellung des Clusters.)
- Stellen Sie sicher, dass alle Server, die Sie als Knoten im Cluster hinzufügen möchten mit derselben Active Directory-Domäne verknüpft sind.
- (Optional) Erstellen Sie eine Organisationseinheit (OE), und Verschieben der Computerkonten für Server, die Sie als Clusterknoten in die Organisationseinheit hinzufügen möchten. Als bewährte Methode empfehlen wir, dass Sie in ihrer eigenen Organisationseinheit in AD DS Failoverclustern platzieren. Dadurch können Sie besser steuern, welche Einstellungen für Gruppenrichtlinien oder Sicherheitsvorlagen Clusterknoten auswirken. Durch das Isolieren von Clustern in ihrer eigenen Organisationseinheit, können sie vor dem versehentlichen Löschen von Computerobjekten Cluster verhindert.

Überprüfen Sie darüber hinaus die folgenden kontoanforderungen:

- Stellen Sie sicher, dass das Konto, das Sie zum Erstellen des Clusters verwenden möchten, ein Domänenbenutzer ist, der über Administratorrechte auf allen Servern hat, die Sie als Knoten im Cluster hinzufügen möchten.
- Stellen Sie sicher, dass eine der folgenden "true" ist:
    - Der Benutzer, der den Cluster erstellt, hat die Berechtigung **Computerobjekte erstellen** , auf die Organisationseinheit oder den Container, in dem der Server, auf denen das Cluster bilden werden eingefügt.
    - Wenn der Benutzer keinen die Berechtigung **Computerobjekte erstellen** , bitten Sie einen Domänenadministrator zum Vorbereiten einer Cluster-Computerobjekt für den Cluster. Weitere Informationen finden Sie unter [Prestage Cluster Computer Objects in Active Directory Domain Services](prestage-cluster-adds.md).

>[!NOTE]
>Diese Anforderung gilt nicht, wenn Sie ein Active Directory-getrennt-Cluster in Windows Server 2012 R2 erstellen möchten. Weitere Informationen finden Sie unter [einem Cluster Active Directory-Detached bereitstellen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

## Installieren Sie die Failover-Clusterunterstützung

Sie müssen die Failover-Clusterunterstützung auf jedem Server installieren, die Sie als ein Failover Cluster-Knoten hinzufügen möchten.

### Installieren Sie die Failover-Clusterunterstützung

1. Starten Sie den Server-Manager.
2. Wählen Sie im Menü **Verwalten** **Rollen und Features hinzufügen**.
3. Wählen Sie auf der Seite **Vorbereitung** **Weiter**.
4. Klicken Sie auf der Seite **Installationstyp auswählen** **rollenbasierte oder featurebasierte Installation**wählen Sie, und wählen Sie dann **Weiter**.
5. Wählen Sie den Server, in denen Sie das Feature installieren möchten, und wählen Sie dann **Weiter**, auf der Seite **Zielserver auswählen** .
6. Wählen Sie auf der Seite " **Serverrollen auswählen** " **Weiter**.
7. Aktivieren Sie das Kontrollkästchen **Failover-Clusterunterstützung** , auf der Seite **Features auswählen** .
8. Um die Failover Cluster-Verwaltungstools zu installieren, wählen Sie **Features hinzufügen**, und wählen Sie dann **Weiter**.
9. Wählen Sie auf der Seite " **Installationsauswahl bestätigen** " **Installieren**.
<br>Ein Neustart des Servers ist nicht erforderlich, damit die Failover-Clusterunterstützung.

10. Wenn die Installation abgeschlossen ist, wählen Sie **Schließen**.
11. Wiederholen Sie diesen Vorgang auf jedem Server, die Sie als ein Failover Cluster-Knoten hinzufügen möchten.

>[!NOTE]
>Nach der Installation der Failoverclustering-Funktion wird empfohlen, dass Sie die neuesten Updates von Windows Update anwenden. Darüber hinaus für einen Windows Server 2012-basierte Failovercluster, lesen Sie den Microsoft-Support-Artikel [Recommended Hotfixes und Updates für Windows Server 2012-basierten Failover Cluster](https://support.microsoft.com/help/2784261/recommended-hotfixes-and-updates-for-windows-server-2012-based-failove) , und installieren Sie alle Updates, die angewendet werden.

## Überprüfen der Konfigurations

Bevor Sie den Failovercluster erstellen, wird dringend empfohlen, dass Sie die Konfiguration überprüfen, um sicherzustellen, dass die Hardware und die hardwareeinstellungen mit Failover-Clusterunterstützung kompatibel sind. Microsoft unterstützt eine Clusterlösung nur dann, wenn die gesamte Konfiguration alle ist die Überprüfung erfolgreich Tests und die gesamte Hardware für die Version von Windows Server zertifiziert wurde, die die Clusterknoten ausgeführt werden.

>[!NOTE]
>Sie müssen mindestens zwei Knoten alle Tests ausgeführt haben. Wenn Sie nur einen Knoten haben, werden viele der kritischen Speichertests nicht ausgeführt.

### Führen Sie Clustervalidierungstests

1. Starten Sie auf einem Computer mit dem Failover Cluster-Verwaltungstools aus der Remoteserver-Verwaltungstools installiert, oder auf einem Server, auf dem die Failover-Clusterunterstützung installiert, Failovercluster-Manager. Zu diesem Zweck auf einem Server starten Sie Server-Manager, und wählen Sie dann auf das Menü " **Extras** " **Failovercluster-Manager**.
2. Wählen Sie klicken Sie im **Failovercluster-Manager** unter **Verwaltung** **Konfiguration überprüfen**.
3. Wählen Sie auf der Seite " **Vorbereitung** " **Weiter**.
4. Geben Sie auf der Seite **Server auswählen oder einen Cluster** in das Feld **Geben Sie den Namen** den NetBIOS-Namen oder der vollqualifizierte Domänenname des Servers, den Sie als ein Failover Cluster-Knoten hinzufügen möchten, und wählen Sie dann **Hinzufügen**. Wiederholen Sie diesen Schritt für jeden Server, den Sie hinzufügen möchten. Um mehrere Server gleichzeitig hinzuzufügen, trennen Sie die Namen durch ein Komma oder durch ein Semikolon. Geben Sie z. B. die Namen im Format *server1.contoso.com, server2.contoso.com*. Wenn Sie fertig sind, wählen Sie **Weiter**.
5. Wählen Sie auf der Seite **Testen Optionen** , **Führen Sie alle Tests aus (empfohlen)**, und wählen Sie dann **Weiter**.
6. Wählen Sie auf der Seite " **Bestätigung** " **Weiter**.

    Die Seite "Überprüfung" zeigt den Status der ausgeführten Tests.
7. Führen Sie eine der folgenden Schritte aus, auf der Seite " **Zusammenfassung** ":
    
      - Die Ergebnisse angeben, dass der Test erfolgreich abgeschlossen und die Konfiguration sich für Failoverclustering eignet und Sie den Cluster sofort erstellen möchten, stellen Sie sicher, dass das Kontrollkästchen **Erstellen des Clusters jetzt mithilfe der überprüften Knoten** ausgewählt ist, und klicken Sie dann Wählen Sie **Fertig stellen**. Fahren Sie mit Schritt 4 des Verfahrens [Erstellen Failovercluster](#create-the-failover-cluster) .
      - Die Ergebnisse angeben, dass Warnungen oder Fehlern wurden, wählen Sie **Bericht anzeigen** , um die Details anzuzeigen und zu ermitteln, welche Probleme behoben werden müssen. Bewusst, dass eine Warnung für einen bestimmten Überprüfungstest gibt an, dass dieser Aspekt der Failovercluster unterstützt werden, aber die empfohlenen bewährten Methoden möglicherweise nicht erfüllen.
        
        >[!NOTE]
        >Wenn Sie eine Warnung für den Test überprüft Storage Spaces permanente Reservierung erhalten, finden Sie im Blogbeitrag [Windows-Failovercluster Validierung Warnung weist darauf hin, dass der Datenträger nicht die permanente Reservierung für "Speicherplätze" unterstützen](https://blogs.msdn.microsoft.com/clustering/2013/05/24/validate-storage-spaces-persistent-reservation-test-results-with-warning/) Weitere Informationen.

Weitere Informationen zu Hardware Validierungstests finden Sie unter [Überprüfen der Hardware für einen Failovercluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>).

## Erstellen Sie den Failovercluster

Um diesen Schritt abgeschlossen haben, stellen Sie sicher, dass das Benutzerkonto, dem Sie als Anmelden die Anforderungen erfüllt, die im Abschnitt [Überprüfen Sie die erforderlichen Komponenten](#verify-the-prerequisites) in diesem Thema beschrieben werden.

1. Starten Sie den Server-Manager.
2. Wählen Sie auf das Menü " **Extras** " **Failovercluster-Manager**.
3. Klicken Sie im **Failovercluster-Manager** unter **Management**wählen Sie **Cluster zu erstellen**.
    
    Der Assistent zum Erstellen eines Clusters wird geöffnet.
4. Wählen Sie auf der Seite " **Vorbereitung** " **Weiter**.
5. Wenn die Seite " **Server auswählen** " angezeigt, in das Feld **Geben Sie den Namen wird** Geben Sie den NetBIOS-Namen oder der vollqualifizierte Domänenname des Servers, den Sie als ein Failover Cluster-Knoten hinzufügen möchten, und wählen Sie dann **Hinzufügen**. Wiederholen Sie diesen Schritt für jeden Server, den Sie hinzufügen möchten. Um mehrere Server gleichzeitig hinzuzufügen, trennen Sie die Namen durch ein Komma oder ein Semikolon. Geben Sie z. B. die Namen in das Format *server1.contoso.com; server2.contoso.com*. Wenn Sie fertig sind, wählen Sie **Weiter**.
    
    >[!NOTE]
    >Wenn Sie unmittelbar nach der Ausführung der Überprüfung in der [Überprüfung Konfigurationsvorgang](#validate-the-configuration)Erstellen des Clusters ausgewählt haben, sehen Sie nicht die Seite " **Server auswählen** ". Die Knoten, die überprüft wurden, werden automatisch der Assistent zum Erstellen von Cluster hinzugefügt, damit Sie nicht erneut eingeben verfügen.
6. Wenn Sie zuvor Überprüfung übersprungen, wird der Seite " **Warnung Validierung** " angezeigt. Es wird dringend empfohlen, dass Sie die Cluster-Überprüfung ausführen. Nur von Clustern, die alle Validierungstests werden von Microsoft unterstützt. Um die Überprüfungstests aus auszuführen, wählen Sie **Ja**, und wählen Sie dann **Weiter**. Führen Sie die Konfiguration Assistenten zum Überprüfen einer gemäß [Überprüfen der Konfiguration](#validate-the-configuration).
7. Führen Sie auf der Seite " **Zugriffspunkt zum Verwalten des Clusters** " folgende Schritte aus:
    
    1. Geben Sie den Namen, den Sie zum Verwalten des Clusters verwenden möchten, klicken Sie im **Clusternamen** . Bevor Sie die folgende Informationen überprüfen dazu:
        
          - Dieser Name wird während der Erstellung des Clusters als das Cluster Computerobjekt (auch bekannt als *Namen Clusterobjekts* oder *Clusternamenobjekt*) in AD DS registriert. Wenn Sie einen NetBIOS-Namen für den Cluster angeben, wird das Clusternamenobjekt am selben Speicherort erstellt, in denen die Computerobjekte für den Clusterknoten befinden. Dies kann entweder den Standardcontainer Computer oder eine OU sein.
          - Um einen anderen Speicherort für das Clusternamenobjekt anzugeben, können Sie den distinguished Name des eine OU im **Cluster Name** eingeben. Z. B.: *CN = ClusterName, OU = Clustern, DC = Contoso, DC = com*.
          - Wenn ein Domänenadministrator das Clusternamenobjekt in einer anderen Organisationseinheit als, in denen die Clusterknoten befinden vorbereitet wurde, geben Sie den definierten Namen, den als Domänenadministrator bereitstellt.
    2. Wenn der Server keinen Netzwerkadapter verfügt, der Verwendung von DHCP konfiguriert ist, müssen Sie mindestens eine statische IP-Adressen für den Failovercluster konfigurieren. Aktivieren Sie das Kontrollkästchen neben jedem Netzwerk, die Sie zur Clusterverwaltung von verwenden möchten. Wählen Sie das Feld " **Adresse** " neben einem ausgewählten Netzwerk, und geben Sie die IP-Adresse, die Sie zum Cluster zuweisen möchten. Diese IP-Adresse (oder Adressen) werden mit den Namen des Clusters im Domain Name System (DNS) verknüpft werden.
    3. Wenn Sie fertig sind, wählen Sie **Weiter**.
8. Überprüfen Sie die Einstellungen, auf der Seite " **Bestätigung** ". Standardmäßig ist das Kontrollkästchen **alle geeigneten Speicher zum Cluster hinzufügen,** aktiviert. Deaktivieren Sie dieses Kontrollkästchen, wenn Sie eine der folgenden Aktionen durchführen möchten:
    
      - Möchten Sie Speicher später konfigurieren.
      - Gruppierte Speicherplätze über Failovercluster-Manager oder über die Failover-Clusterunterstützung Windows PowerShell-Cmdlets zu erstellen, und haben noch nicht erstellt "Speicherplätze" in Datei- und Speicherdienste werden soll. Weitere Informationen finden Sie unter [Gruppierter Speicherplätze bereitstellen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>).
9. Wählen Sie **als Nächstes** Failovercluster zu erstellen.
10. Vergewissern Sie sich auf der Seite " **Zusammenfassung** ", dass der Failovercluster erfolgreich erstellt wurde. Falls Warnungen oder Fehler aufgeführt sind, zeigen Sie die Zusammenfassung Ausgabe, oder wählen Sie **Bericht anzeigen** , um den vollständigen Bericht anzuzeigen. Wählen Sie **Fertig stellen**.
11. Um zu bestätigen, dass der Cluster erstellt wurde, stellen Sie sicher, dass der Clustername unter **Failovercluster-Manager** in der Navigationsstruktur aufgeführt ist. Sie können den Namen des Clusters erweitern und wählen Sie dann Elemente unter **Knoten**, **Speicher** oder **Netzwerke** , um die zugeordneten Ressourcen anzuzeigen.
    
    Bewusst, dass es einige Zeit für den Clusternamen erfolgreich in DNS replizieren dauern kann. Nach dem erfolgreichen DNS-Registrierung und Replikation Wenn Sie **Alle Server** im Server-Manager auswählen sollten den Namen des Clusters als Server mit dem Status **Verwaltbarkeit** **Online**aufgeführt werden.

Nach der Erstellung des Clusters möglich Dinge wie z. B. Cluster Quorumkonfiguration überprüfen und optional erstellen (Cluster Shared Volumes, CSV). Weitere Informationen finden Sie unter [Understanding Quorums in "direkte Speicherplätze"](../storage/storage-spaces/understand-quorum.md) und [Verwenden freigegebener Clustervolumes in einem Failovercluster](failover-cluster-csvs.md).

## Erstellen von clusterrollen

Nachdem Sie den Failovercluster erstellt haben, können Sie clusterrollen zu-Cluster-Arbeitslasten erstellen.

>[!NOTE]
>Für clusterrollen, die einen Clientzugriffspunkt erfordern, wird ein Objekt des virtuellen Computers (VCO) in AD DS erstellt. Standardmäßig werden alle virtuellen Computerobjekte für den Cluster in der gleichen Container oder Organisationseinheit als das Clusternamenobjekt erstellt. Bewusst, dass nach der Erstellung eines Clusters das Clusternamenobjekt an einer beliebigen OE verschieben können.

Hier wird beschrieben, wie eine gruppierte Rolle erstellen:

1. Verwenden Sie Server-Manager oder Windows PowerShell zum Installieren der Rolle oder Feature, das für einen Clusterrolle auf jedem Failover Cluster-Knoten erforderlich ist. Z. B. Wenn Sie einen gruppierten Dateiserver erstellen möchten, installieren Sie die Rolle "Dateiserver" auf allen Clusterknoten.
    
    Die folgende Tabelle zeigt die clusterrollen, die Sie in den Assistenten für hohe Verfügbarkeit und die zugehörigen Server-Rolle oder Feature, das Sie als Voraussetzung installiert werden müssen, konfigurieren können.
    
    <table>
    <thead>
    <tr class="header">
    <th>Clusterrolle</th>
    <th>Rolle oder Feature Voraussetzung</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>DFS-Namespace-Server</td>
    <td>DFS-Namespaces (Teil der Rolle "Dateiserver")</td>
    </tr>
    <tr class="even">
    <td>DHCP-Server</td>
    <td>DHCP-Serverrolle</td>
    </tr>
    <tr class="odd">
    <td>Distributed Transaction Coordinator (DTC)</td>
    <td>Keine</td>
    </tr>
    <tr class="even">
    <td>Dateiserver</td>
    <td>Dateiserverrolle</td>
    </tr>
    <tr class="odd">
    <td>Allgemeine Anwendung</td>
    <td>Nicht zutreffend</td>
    </tr>
    <tr class="even">
    <td>Allgemeine Skripts</td>
    <td>Nicht zutreffend</td>
    </tr>
    <tr class="odd">
    <td>Allgemeiner Dienst</td>
    <td>Nicht zutreffend</td>
    </tr>
    <tr class="even">
    <td>Hyper-V-Replikat Broker</td>
    <td>Hyper-V-Rolle</td>
    </tr>
    <tr class="odd">
    <td>iSCSI Target Server</td>
    <td>iSCSI-Zielserver (Teil der Rolle "Dateiserver")</td>
    </tr>
    <tr class="even">
    <td>iSNS-Server</td>
    <td>iSNS-Serverdienst feature</td>
    </tr>
    <tr class="odd">
    <td>Message Queuing</td>
    <td>Message Queuing-Dienste feature</td>
    </tr>
    <tr class="even">
    <td>Andere Server</td>
    <td>Keine</td>
    </tr>
    <tr class="odd">
    <td>Virtuellen Computer</td>
    <td>Hyper-V-Rolle</td>
    </tr>
    <tr class="even">
    <td>WINS-Server</td>
    <td>WINS-Server-feature</td>
    </tr>
    </tbody>
    </table>
2. Im Failovercluster-Manager, erweitern Sie den Namen des Clusters, mit der rechten Maustaste **Rollen**und wählen Sie dann die **Rolle konfigurieren**.
3. Führen Sie die Schritte im Assistenten zum Erstellen der Clusterrolle hohe Verfügbarkeit.
4. Um sicherzustellen, dass der Clusterrolle, klicken Sie im Bereich **Rollen erstellt wurde** stellen Sie sicher, dass die Rolle Status **ausgeführt**hat. Bereich Rollen gibt auch dem Besitzerknoten an. Zum Testen des Failovers rechten Maustaste auf die Rolle, zeigen Sie auf **Verschieben**, und wählen Sie dann den **Knoten auswählen**. Wählen Sie in das Dialogfeld **Gruppierten Rolle verschieben** den gewünschten Clusterknoten, und wählen Sie dann auf **OK**. In der Spalte **Besitzerknoten** stellen Sie sicher, dass der Knoten "Besitzer" geändert.

## Erstellen eines Failoverclusters mithilfe von Windows PowerShell

Die folgenden Windows PowerShell-Cmdlets führen die gleichen Funktionen wie die oben beschriebenen in diesem Thema. Geben Sie jedes Cmdlet in einer einzelnen Zeile, obwohl sie umbrochen über mehrere Zeilen erscheint aufgrund der Formatierung von Einschränkungen.

>[!NOTE]
>Sie müssen Windows PowerShell verwenden, um ein Active Directory-abgetrennter Cluster in Windows Server 2012 R2 zu erstellen. Informationen zur Syntax finden Sie unter [einem Cluster Active Directory-Detached bereitstellen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11)).

Im folgende Beispiel wird die Failover-Clusterunterstützung installiert.

```PowerShell
Install-WindowsFeature –Name Failover-Clustering –IncludeManagementTools
```

Das folgende Beispiel führt alle Clustervalidierungstests auf Computern, die *Server1* und *Server2*benannt sind.

```PowerShell
Test-Cluster –Node Server1, Server2
```

>[!NOTE]
>Das Cmdlet " **Test-Cluster** " gibt die Ergebnisse in eine Protokolldatei in das aktuelle Arbeitsverzeichnis. Zum Beispiel: C:\Users\ < Benutzername > \AppData\Local\Temp.

Das folgende Beispiel erstellt einen Failovercluster mit der Bezeichnung *MeinCluster* mit Knoten *Server1* und *Server2*, weist die statische IP-Adresse *192.168.1.12*und Failovercluster alle geeigneten Speicher hinzugefügt.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12
```

Das folgende Beispiel erstellt den gleichen Failovercluster wie im vorherigen Beispiel, aber es keinen geeigneten Speicher zum Failovercluster hinzufügt.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12 -NoStorage
```

Das folgende Beispiel erstellt einen Cluster mit dem Namen *MeinCluster* im *Cluster* OU der Domäne *"contoso.com"*.

```PowerShell
New-Cluster -Name CN=MyCluster,OU=Cluster,DC=Contoso,DC=com -Node Server1, Server2
```

Beispiele zur Verwendung von clusterrollen hinzufügen finden Sie unter Themen, z. B. [Add-ClusterFileServerRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clusterfileserverrole?view=win10-ps) und [Add-ClusterGenericApplicationRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergenericapplicationrole?view=win10-ps).

## Weitere Informationen

  - [Failoverclustering](failover-clustering.md)
  - [Bereitstellen eines Hyper-V-Clusters](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj863389(v%3dws.11)>)
  - [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831349(v%3dws.11)>)
  - [Bereitstellen eines Active Directory-getrennt Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))
  - [Hohe Verfügbarkeit durch Gastclustering](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)
  - [Clusterfähiges Aktualisieren](cluster-aware-updating.md)
  - [Neuen Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/new-cluster?view=win10-ps)
  - [Test-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)
