---
title: Verwalten von Hyperkonvergenten Infrastrukturen mit Windows Admin Center
description: Verwalten von Hyperkonvergenten Infrastrukturen mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9ce4381735746ace6358aa2cb30f8b341c576054
ms.sourcegitcommit: e558dda2774345e9ad17ff04b759f68c59d88139
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2019
ms.locfileid: "9262843"
---
# Verwalten von Hyperkonvergenten Infrastrukturen mit Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

## Was ist hyperkonvergente Infrastruktur

Hyperkonvergente Infrastruktur konsolidiert Software-defined Compute, Speicher und Networking in einem Cluster High-End, kostengünstige, bereitstellen und leicht skalierbaren Virtualisierung. Diese Funktion wurde in Windows Server 2016 mit ["Direkte Speicherplätze"](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview), [Software Defined Networking](https://docs.microsoft.com/en-us/windows-server/networking/sdn/software-defined-networking) und [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)eingeführt.

> [!Tip]
> Hyperkonvergente Infrastruktur erwerben möchten? Microsoft empfiehlt diese [Windows Server Software-Defined](https://microsoft.com/wssd) -Lösungen von unseren Partnern. Sie sind entwickelt, zusammengesetzt und überprüft mit unseren Referenzarchitektur, um sicherzustellen, dass Kompatibilität und Zuverlässigkeit, so Sie einrichten erhalten und schnell ausgeführt.

> [!IMPORTANT]
> Einige der in diesem Artikel beschriebenen Features sind nur in Windows Admin Center-Vorschau verfügbar. [Wie erhalte ich diese Version?](http://aka.ms/windowsadmincenter)

## Was ist Windows Admin Center

[Windows Admin Center](../understand/windows-admin-center.md) ist der nächsten Generation Verwaltungstool für Windows Server, der Nachfolger von herkömmlichen "im Feld" Verwaltungstools wie Server Manager. Es ist kostenlos und installiert und ohne Internetzugang verwendet werden können. Sie können Windows Admin Center verwenden, verwalten und Überwachen von hyperkonvergente Infrastruktur mit Windows Server 2016 oder Windows Server 2019.

![Zusammengeführte Cluster-dashboard](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## Wichtige Funktionen

Windows Admin Center für hyperkonvergente Infrastruktur bietet folgende Vorteile:

- **Einheitliche einzelne Bereich-transparente für Compute, Speicher und networking bald.** Zeigen Sie Ihre virtuellen Computer, Host-Servern, Volumes, Laufwerke und mehr auf eine spezielle, konsistente, miteinander verbundenen Benutzeroberfläche.
- **Erstellen und Verwalten von direkte Speicherplätze und Hyper-V virtuelle Computer.** Radikal einfachen Workflows zu erstellen, öffnen, Ändern der Größe und löschen Sie Volumes. Erstellen, starten, herstellen und virtuelle Computer verschieben; und vieles mehr.
- **Leistungsstarke für den gesamten Cluster überwachen.** Das Dashboard Diagramme, Arbeitsspeicher und CPU-Auslastung, Speicherkapazität, IOPS, Durchsatz und Latenz in Echtzeit über alle Server im Cluster mit Warnungen löschen, wenn etwas nicht geeignet ist.
- **Unterstützung für Software-Defined Networking (SDN).** Verwalten und Überwachen von virtuellen Netzwerken, Subnetze, Verbinden von virtuellen Computern mit virtuellen Netzwerken und Überwachen von SDN-Infrastruktur.

Windows Admin Center für hyperkonvergente Infrastruktur ist aktiv von Microsoft entwickelt. Er erhält häufige Updates, die vorhandenen Features verbessern und neue Funktionen hinzugefügt.

## Vorbereitung

Um Ihre Cluster als hyperkonvergente Infrastruktur in Windows Admin Center zu verwalten, es muss Windows Server 2016 oder Windows Server 2019 ausgeführt werden, und Hyper-V und direkte Speicherplätze aktiviert haben. Optional können sie auch Software Defined Networking aktiviert und über Windows Admin Center verwaltet haben.

> [!Tip]
> Windows Admin Center bietet auch eine allgemeine Management-Erfahrung für jedem Cluster mit alle Workloads, verfügbar für Windows Server 2012 und höher. Wenn dies z. B. eine bessere Übereinstimmung, sounds, wenn Sie Windows Admin Center Ihre Cluster hinzufügen, wählen Sie [**Failovercluster**](manage-failover-clusters.md) anstelle von **Hyper-converged Cluster**.

### Vorbereiten des Windows Server 2016-Clusters für Windows Admin Center

Windows Admin Center für hyperkonvergente Infrastruktur hängt von Verwaltung, die APIs hinzugefügt, nachdem Windows Server 2016 veröffentlicht wurde. Bevor Sie Ihre Windows Server 2016-Cluster mit Windows Admin Center verwalten können, müssen Sie diese beiden Schritte ausführen:

1. Stellen Sie sicher, dass jeder Server im Cluster den [2018-05 kumulative Update für WindowsServer 2016 (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723) installiert wurde oder höher. Zum Herunterladen und Installieren dieses Update, wechseln Sie zu **Einstellungen** > **Aktualisieren & Sicherheit** > **Windows Update** und wählen **online nach Updates Suchen von Microsoft Update**.
2. Führen Sie das folgende PowerShell-Cmdlet als Administrator auf dem Cluster:

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> Sie müssen nur einmal, führen Sie das Cmdlet auf allen Servern im Cluster. Sie können in Windows PowerShell lokal ausführen oder mit, dass Credential Security Service Provider (CredSSP) Remote ausführen. Je nach Konfiguration können Sie nicht dieses Cmdlet aus in Windows Admin Center ausführen können.

### Vorbereiten des Windows Server 2019-Clusters für Windows Admin Center

Wenn Ihre Cluster mit Windows Server 2019 ausgeführt wird, sind die oben aufgeführten Schritte nicht erforderlich. Cluster nur bei Windows Admin Center hinzufügen, wie im nächsten Abschnitt beschrieben, und Sie sind startklar!

### Konfigurieren von Software-Defined Networking (Optional) ###

Sie können konfigurieren, dass Ihre hyperkonvergente Infrastruktur mit Windows Server 2016 oder 2019 Software Defined Networking (SDN) mit den folgenden Schritten verwendet:

1. Bereiten Sie die virtuelle Festplatte des Betriebssystems, die das gleiche Betriebssystem ist Sie auf die hyperkonvergente Infrastruktur-Hosts installiert. Dieser VHD wird für alle NC/SLB/GW virtuellen Computer verwendet werden.
2. Herunterladen der Ordner und Dateien unter SDN von Express [https://github.com/Microsoft/SDN/tree/master/SDNExpress](https://github.com/Microsoft/SDN/tree/master/SDNExpress).
3. Vorbereiten einer anderen VM unter Verwendung der Deployment-Konsole. Dieses virtuellen Computers sollte die SDN-Hosts zugreifen können. Darüber hinaus die VM sollten werden ist das RSAT-Hyper-V-Tool installiert.
4. Kopieren Sie das gesamte heruntergeladenen für SDN Express auf der Konsole Bereitstellung VM. Und diesen Ordner **SDNExpress** freigeben. Stellen Sie sicher, dass es sich bei jedem Host den freigegebenen Ordner **SDNExpress** , zugreifen kann, gemäß der Definition in der Konfigurationszeile 8:
```
    \\$env:Computername\SDNExpress
```
5. Kopieren Sie die VHD des Betriebssystems, auf den Ordner für **Images** im Ordner "" **SDNExpress** auf der Konsole Bereitstellung VM.
6. Ändern Sie die SDN Express-Konfiguration mit Ihrer Einrichtung der Entwicklungsumgebung. Schließen Sie die folgenden beiden Schritte, nachdem Sie die SDN Express-Konfiguration basierend auf Ihrer Umgebungsinformationen ändern.
7. Führen Sie PowerShell mit Administratorrechte zum Bereitstellen von SDN:

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose 
```

Die Bereitstellung dauert ca. 30 bis 45 Minuten.

## Erste Schritte

Nachdem Ihre hyperkonvergente Infrastruktur bereitgestellt wird, können Sie es mithilfe von Windows Admin Center verwalten.

### Installieren von Windows Admin Center

Wenn Sie nicht bereits geschehen, herunterladen und Installieren von Windows Admin Center. Die schnellste Möglichkeit, um bis zu erhalten ist und ausgeführt wird, auf Ihrem Windows 10-Computer installieren und Ihre Server remote verwalten. Dieser Vorgang dauert weniger als fünf Minuten. [Jetzt herunterladen](https://aka.ms/windowsadmincenter) oder [Weitere Informationen zu anderen Installationsoptionen](../deploy/install.md).

### Zusammengeführte Cluster hinzufügen

Windows Admin Center Ihre Cluster hinzu:

1. Klicken Sie unter alle Verbindungen auf **+ Hinzufügen** .
2. Wählen Sie zum Hinzufügen einer **Hyper-converged Cluster-Verbindung**.
3. Geben Sie den Namen des Clusters und, wenn Sie dazu aufgefordert werden, die Anmeldeinformationen zu verwenden.
4. Klicken Sie auf **Hinzufügen** , um abzuschließen.

Die Verbindungsliste werden Cluster hinzugefügt werden. Klicken Sie auf, um das Dashboard zu starten.

![Fügen Sie zusammengeführte Cluster-Verbindung](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### Hinzufügen von SDN-fähigen zusammengeführte Cluster (Windows Admin Center-Vorschau)

Die neuesten Windows Admin Center – Vorschau unterstützt die Software Defined Networking-Verwaltung für hyperkonvergente Infrastruktur. Die zusammengeführte Cluster-Verbindung ein Netzwerk-Controller-REST-URI hinzufügen, können Sie hyperkonvergente Cluster-Manager zum Verwalten von SDN-Ressourcen und Überwachen von SDN-Infrastruktur.

1. Klicken Sie unter alle Verbindungen auf **+ Hinzufügen** .
2. Wählen Sie zum Hinzufügen einer **Hyper-converged Cluster-Verbindung**.
3. Geben Sie den Namen des Clusters und, wenn Sie dazu aufgefordert werden, die Anmeldeinformationen zu verwenden.
4. Überprüfen Sie **Konfigurieren des Netzwerk-Controllers** , um den Vorgang fortzusetzen.
5. Geben Sie den **URI der Netzwerk-Controller** , und klicken Sie auf **Überprüfen**.
6. Klicken Sie auf **Hinzufügen** , um abzuschließen.

Die Verbindungsliste werden Cluster hinzugefügt werden. Klicken Sie auf, um das Dashboard zu starten.

![Hinzufügen von SDN-fähigen zusammengeführte Cluster-Verbindung](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> SDN-Umgebungen mit Kerberos-Authentifizierung für Northbound Kommunikation werden derzeit nicht unterstützt.

## Häufig gestellte Fragen

### Gibt es Unterschiede bei der Verwaltung von Windows Server 2016 und Windows Server 2019?

Ja Windows Admin Center für hyperkonvergente Infrastruktur empfängt häufige Updates, die die Erfahrung für Windows Server 2016 und Windows Server 2019 zu verbessern. Bestimmte neue Features sind jedoch nur für Windows Server 2019 – z. B. den Umschalter für Datendeduplizierung und-Komprimierung verfügbar.

### Kann ich Windows Admin Center verwenden, um "direkte Speicherplätze" für andere Anwendungsfälle (nicht hyperkonvergenten), z. B. konvergente Scale-Out-Dateiserver (sofs kontaktieren) oder Microsoft SQL Server zu verwalten?

Windows Admin Center für hyperkonvergente Infrastruktur bietet keine Verwaltung oder Überwachungsoptionen speziell für andere Anwendungsfälle von "direkte Speicherplätze" – Es kann keine z. B. Dateifreigaben erstellen. Allerdings funktionieren die Dashboard und Core-Features, z. B. Erstellen von Volumes oder Ersetzen von Laufwerken für alle Storage Spaces Direct-Cluster.

### Was ist der Unterschied zwischen einem Failovercluster und einem hyperkonvergenten Cluster?

Der Begriff "hyperkonvergenten" bezieht sich zum Ausführen von Hyper-V und direkte Speicherplätze auf die gleiche Cluster im Allgemeinen Servern zum Virtualisieren von Compute und Speicher-Ressourcen. Im Kontext von Windows Admin Center beim Anklicken **+ Hinzufügen** aus der Verbindungsliste können Sie wählen zwischen einer **Failovercluster-Verbindung** oder eine **Hyper-converged Cluster-Verbindung**hinzufügen:

- Die **Failovercluster-Verbindung** ist der Nachfolger von den Failovercluster-Manager-desktop-app. Es bietet eine vertraute, universell einsetzbare Verwaltungsfunktion für jedem Cluster mit allen Workload, einschließlich Microsoft SQL Server. Es ist für Windows Server 2012 verfügbar und höher.

- Die **Hyper-converged Cluster-Verbindung** ist eine völlig neue Erfahrung, die speziell für direkte Speicherplätze und Hyper-V. Es bietet das Dashboard und betont Diagramme und Warnungen für die Überwachung. Es ist für Windows Server 2016 und Windows Server 2019 verfügbar.

### Warum benötige ich das neueste kumulative Update für Windows Server 2016?

Windows Admin Center für hyperkonvergente Infrastruktur hängt von Verwaltung, die APIs entwickelt, nach der Veröffentlichung von Windows Server 2016 wurde. Diese APIs werden in den [2018-05 kumulative Update für WindowsServer 2016 (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723), ab dem 8 Mai 2018 verfügbar hinzugefügt.

### Wie viel kostet Windows Admin Center?

Windows Admin Center ist ohne zusätzliche Kosten über Windows erhältlich.

Sie können Windows Admin Center (als separater Download verfügbar) mit den gültigen Lizenzen für Windows Server oder Windows 10 ohne zusätzliche Kosten - er unter Windows ergänzende EULA lizenziert.

### Erfordert Windows Admin Center das System Center?

Nein.

### Ist es eine Internetverbindung erforderlich?

Nein.

Obwohl Windows Admin Center leistungsstarke bietet und praktische-Integration in der Microsoft Azure-Cloud, Core-Verwaltung und Überwachung Erfahrung für hyperkonvergente Infrastruktur vollständig ist lokale. Es kann ohne Internetzugang installiert und verwendet werden.

## Was Sie tun können

Wenn Sie noch die ersten Schritte sind, sind hier einige schnelle Lernprogramme, mit denen Sie die hier erfahren Sie, wie Windows Admin Center für hyperkonvergente Infrastruktur ist organisiert und funktioniert. Übung gute Urteil, und achten Sie darauf, dass Sie mit produktionsumgebungen. Diese Videos wurden mit Windows Admin Center Version 1804 und einen Insider Preview-Build von Windows Server 2019 aufgezeichnet.

### Verwalten von "direkte Speicherplätze" volumes

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">So erstellen Sie ein Volume drei-Wege-Spiegelung</a></li>
               <li>(1:17) <a href="https://youtu.be/R72QHudqWpE">So erstellen Sie ein Volume durch Spiegelung beschleunigte Parität</a></li>
               <li>(1:02) <a href="https://youtu.be/j59z7ulohs4">So öffnen Sie ein Volume und Hinzufügen von Dateien</a></li>
               <li>(0:51) <a href="https://youtu.be/PRibTacyKko">Informationen zum Aktivieren der Datendeduplizierung und-Komprimierung</a></li>
               <li>(0:47) <a href="https://youtu.be/hqyBzipBoTI">so erweitern Sie ein Volume</a></li>
               <li>(0:26) <a href="https://youtu.be/DbjF8r2F6Jo">So löschen Sie ein Volume</a></li>
</ul>

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Erstellen Sie Volume drei-Wege-Spiegelung</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/o66etKq70N8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Erstellen Sie Volume durch Spiegelung beschleunigte Parität</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/R72QHudqWpE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Öffnen Sie die Datei und Hinzufügen von Dateien</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/j59z7ulohs4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Aktivieren der Datendeduplizierung und-Komprimierung</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/PRibTacyKko" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Erweitern von Volumes</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/hqyBzipBoTI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Volume löschen</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/DbjF8r2F6Jo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
</table>

### Erstellen eines neuen virtuellen Computers

1. Klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Am oberen Rand der virtuelle Computer-Tool wählen Sie die Registerkarte " **Inventar** ", und klicken Sie dann **neu** , um einen neuen virtuellen Computer zu erstellen.
3. Geben Sie den virtuellen Computer ein, und wählen Sie zwischen virtuelle Computer der Generation 1 und 2.
4. Uou kann dann auswählen, welche Host anfänglich auf dem virtuellen Computer erstellen oder verwenden die empfohlenen Host.
5. Wählen Sie einen Pfad für die Dateien des virtuellen Computers. Wählen Sie ein Volume aus der Dropdown-Liste, oder klicken Sie auf **Durchsuchen** , um einen Ordner mit der Ordnerauswahl auszuwählen. Die VM-Konfigurationsdateien und die virtuelle Festplatte in einen einzelnen Ordner unter gespeichert werden die `\Hyper-V\[virtual machine name]` Pfad des ausgewählten Datenträgers oder Pfad.
6. Wählen Sie die Anzahl der virtuellen Prozessoren, ob Sie die geschachtelte Virtualisierung aktiviert werden soll, Arbeitsspeicher-Einstellungen, Netzwerkadapter, virtuelle Festplatten konfigurieren und auswählen, ob Sie ein Betriebssystem aus einer Bilddatei ISO- oder über das Netzwerk installieren möchten.
7. Klicken Sie auf **Erstellen** , um den virtuellen Computer zu erstellen.
8. Sobald der virtuelle Computer erstellt wird und in der Liste der virtuellen Computer angezeigt, können Sie den virtuellen Computer starten.
9. Sobald der virtuelle Computer gestartet wird, können Sie mit des virtuellen Computers Konsole über VMConnect auf die Installation des Betriebssystems verbinden. Wählen Sie den virtuellen Computer aus der Liste aus, klicken Sie auf **Weitere** > **Verbinden** , um die RDP-Datei herunterzuladen. Öffnen Sie die RDP-Datei, in der Remotedesktopverbindung-app. Da dies mit des virtuellen Computers-Konsole verbunden ist, müssen Sie den Hyper-V-Host-Administrator-Anmeldeinformationen eingeben.

[Erfahren Sie mehr über die Verwaltung virtueller Computer mit Windows Admin Center](manage-virtual-machines.md).

### Anhalten und problemlos einen Server neu starten

1. Wählen Sie auf dem **Dashboard**- **Servern** bei der Navigation auf der linken Seite oder über den Link **Ansicht Servern >** auf der Kachel in der unteren rechten Ecke des Dashboards.
2. Am oberen wechseln Sie auf der Registerkarte " **Inventar** " aus der **Zusammenfassung** .
3. Wählen Sie einen Server, indem Sie auf deren Namen, die **Server** -Detailseite öffnen.
4. Klicken Sie auf **Pause Server zu Wartungszwecken**. Wenn sicher fortgesetzt werden kann, wird dies virtuelle Computer auf andere Servern im Cluster verschieben. Der Server muss Status ausgleichen, während dies geschieht. Wenn Sie möchten, können Sie die virtuellen Computer auf der Seite der **virtuelle Computer > Inventar** verschieben, in denen ihre Hostserver deutlich im Raster angezeigt ansehen. Wenn alle virtuellen Computer verschoben haben, wird den Status des Servers **angehalten**werden.
5. Klicken Sie auf **Verwalten Server** für den Zugriff auf alle pro Server-Verwaltungstools in Windows Admin Center.
6. Klicken Sie auf **neu starten**, dann **Ja**. Sie müssen zurück zur Verbindungsliste ausgelöst werden.
7. Zurück auf das **Dashboard**ist der Server Rot dargestellt, bevor es verfügbar ist.
8. Sobald er wieder verfügbar ist, navigieren Sie erneut die **Server** -Seite, und klicken Sie auf **Fortsetzen Server aus der Wartung** um den Status des Servers auf einfach auf zurückzusetzen. Zeit verschiebt virtuelle Computer zurück – keine Benutzeraktion erforderlich ist.

### Ersetzen Sie ein fehlgeschlagenen Laufwerk

1. Wenn ein Laufwerk fehlschlägt wird eine Benachrichtigung angezeigt, in der obere linke **Warnungen** Bereich des **Dashboards**.
2. Sie können auch auswählen von **Laufwerken** im Navigationsbereich auf der linken Seite oder klicken Sie auf den Link **Ansicht Laufwerke >** auf der Kachel in der unteren rechten Ecke suchen Laufwerke und sehen ihren Status für sich selbst. In der Registerkarte " **Inventar** " unterstützt das Raster sortieren, gruppieren und Schlüsselwort suchen.
3. Klicken Sie über das **Dashboard**auf die Benachrichtigung, um Details, z. B. das Laufwerk physischen Standort anzuzeigen.
4. Um mehr zu erfahren, klicken Sie auf die Verknüpfung **auf Laufwerk wechseln Sie** zur Detailseite **Laufwerk** .
5. Wenn Ihre Hardware unterstützt wird, klicken Sie zum Steuern des Laufwerks Indikator Licht **Licht ein-/ausschalten aktivieren** .
6. "Direkte Speicherplätze" automatisch wird zurückgezogen und evacuates ausgefallenen Laufwerke. Wenn dies der Fall war, der Laufwerkstatus eingestellt ist, und dessen Speicher Kapazität Titelleiste ist leer.
7. Das fehlerhafte Laufwerk, und legen Sie dessen Ersatz.
8. In **> Inventar-Laufwerke**wird das neue Laufwerk angezeigt. Zeitpunkt die Warnung wird gelöscht, Volumes auf OK Status repariert und Speicher wird auf das neue Laufwerk Ausgleich – ist keine Benutzeraktion erforderlich.

### Verwalten von virtuellen Netzwerken (SDN-fähigen HCI Cluster mit Windows Admin Center-Vorschau)

1. Wählen Sie im Navigationsbereich auf der linken Seite **Virtuellen Netzwerken** .
2. Klicken Sie auf **neue** zum Erstellen eines neuen virtuellen Netzwerks und Subnetze, oder wählen Sie ein vorhandenes virtuelles Netzwerk, und klicken Sie auf **Einstellungen** , um seine Konfiguration zu ändern.
3. Klicken Sie auf ein vorhandenes virtuelles Netzwerk zum Anzeigen von VM-Verbindungen mit virtuellen Netzwerks Subnetze und Zugriffssteuerungslisten auf virtuellen Netzwerks Subnetze angewendet.

![Verwalten von virtuellen Netzwerken](../media/manage-hyper-converged/manage-virtual-networks.png)

### Verbinden Sie einen virtuellen Computer mit einem virtuellen Netzwerk (SDN-fähigen HCI Cluster mit Windows Admin Center-Vorschau)

1. Auswählen von **virtuellen Computern** im Navigationsbereich auf der linken Seite.
2. Wählen Sie einen vorhandenen virtuellen Computer > klicken Sie auf **Einstellungen** > öffnen Sie die Registerkarte " **Netzwerke** " unter " **Einstellungen"**.
3. Konfigurieren Sie die Felder **Virtuelles Netzwerk** und **Virtuellen Subnetz** , um den virtuellen Computer mit einem virtuellen Netzwerk herzustellen.

Sie können auch das virtuelle Netzwerk konfigurieren, beim Erstellen eines virtuellen Computers.

![Verbinden Sie einen virtuellen Computer mit einem virtuellen Netzwerk](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### Überwachen der Infrastruktur Software Defined Networking (SDN-fähigen HCI Cluster mit Windows Admin Center-Vorschau)

1. Wählen Sie im Navigationsbereich auf der linken Seite **SDN überwachen** .
2. Anzeigen von detaillierten Informationen über die Integrität der Netzwerkcontroller, Softwarelastenausgleich,-Gateways, und Ihre virtuellen Gateway-Pool, öffentliche und Private IP-Pool-Verwendung und SDN-Host-Status überwachen.

![Monitor SDN-Infrastruktur](../media/manage-hyper-converged/sdn-monitoring.png)

## Feedback

Es geht um die Ihr Feedback! Der wichtigste Vorteil von häufige Updates ist zu hören, was funktioniert und was verbessert werden muss. Hier sind einige Möglichkeiten, um uns mitzuteilen, was Sie denken:

- [Übermitteln Sie und stimmen Sie für Feature-Anforderungen für UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Verknüpfen Sie das Windows Admin Center-Forum von Microsoft Tech-Community](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- Tweet zu `@servermgmt`

### Weitere Informationen:

- [Windows Admin Center](../understand/windows-admin-center.md)
- [Speicherplätze DAS](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
- [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)
- [Software-Defined Networking](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)
