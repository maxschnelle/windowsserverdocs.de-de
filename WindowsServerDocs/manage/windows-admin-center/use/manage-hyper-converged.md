---
title: Verwalten von Hyper-konvergiert-Infrastruktur mit Windows Admin Center
description: Verwalten von Hyperkonvergenten Infrastruktur mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fe00072932d9c7f283ebd887a5292ac9a9d0e37f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446029"
---
# <a name="manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Verwalten von Hyper-konvergiert-Infrastruktur mit Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

## <a name="what-is-hyper-converged-infrastructure"></a>Was ist Hyper-Converged Infrastruktur

Zusammengeführte Infrastruktur konsolidiert softwaredefinierte COMPUTE-, Speicher- und Netzwerkressourcen in einem Cluster zu hoch leistungsfähige, kostengünstige und einfach skalierbare Virtualisierung. Diese Funktion wurde in Windows Server 2016 mit eingeführt ["direkte Speicherplätze"](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview), [Software Defined Networking](https://docs.microsoft.com/en-us/windows-server/networking/sdn/software-defined-networking) und [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server).

> [!Tip]
> Suche nach Hyper-Converged Infrastruktur? Microsoft empfiehlt diese [Windows Server-Software-Defined](https://microsoft.com/wssd) Lösungen unserer Partner. Sie werden entworfen, zusammengesetzt und für unsere Referenzarchitektur, um sicherzustellen, dass Kompatibilität und Zuverlässigkeit, damit Sie Sie nutzen und schnell überprüft.

> [!IMPORTANT]
> Einige der in diesem Artikel beschriebenen Features sind nur in Windows Admin Center Preview verfügbar. [Wie erhalte ich diese Version?](http://aka.ms/windowsadmincenter)

## <a name="what-is-windows-admin-center"></a>Was ist Windows Admin Center

[Windows Admin Center](../understand/windows-admin-center.md) ist das Verwaltungstool der nächsten Generation für Windows Server, der Nachfolger von herkömmlichen "in-Box" Tools wie Server-Manager. Es ist kostenlos und installiert und ohne Internetverbindung verwendet werden kann. Sie können Windows Admin Center verwenden, verwalten und Überwachen von Hyper-Converged-Infrastruktur, die unter Windows Server 2016 oder Windows Server-2019.

![Hyperkonvergente Cluster-dashboard](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## <a name="key-features"></a>Hauptmerkmale

Der Windows Admin Center für Hyper-Converged Infrastruktur bietet folgende Vorteile:

- **Einheitliche einzelnen Bereich – transparente für Computing, Speicherung und demnächst Netzwerk.** Zeigen Sie Ihre virtuellen Computer, Host-Server, Volumes, Laufwerke und mehr in eine speziell entwickelte, konsistente, miteinander verbundene Erfahrung zu bieten.
- **Erstellen und Verwalten von Speicherplätzen und Hyper-V-VMs.** Einfachste Workflows zu erstellen, öffnen, ändern Sie die Größe und Löschen von Volumes; Erstellen, starten, Herstellen einer Verbindung mit und Verschieben von virtuellen Computern; und vieles mehr.
- **Leistungsstarke für den gesamten Cluster überwachen.** Das Dashboard zu Diagrammen, Arbeitsspeicher und CPU-Auslastung, Speicherkapazität, IOPS, Durchsatz und Latenz in Echtzeit auf jedem Server im Cluster mit Warnungen deaktivieren, wenn etwas nicht geeignet ist.
- **Unterstützung für Software-Defined Networking (SDN).** Verwalten und überwachen virtueller Netzwerke, Subnetze, virtuelle Maschinen mit virtuellen Netzwerken verbinden und Überwachen von SDN-Infrastruktur.

Windows Admin Center für Hyper-Converged Infrastruktur wird von Microsoft aktiv entwickelt wird. Er empfängt die häufige Updates, die vorhandene Funktionen zu verbessern und neue Funktionen hinzuzufügen.

## <a name="before-you-start"></a>Bevor Sie beginnen

Um Ihren Cluster als Hyper-Converged-Infrastruktur in Windows Admin Center verwalten zu können, muss Windows Server 2016 oder Windows Server-2019 ausgeführt werden, und Hyper-V- und "direkte Speicherplätze" aktiviert haben. Optional können sie auch Software Defined Networking, aktiviert und über Windows Admin Center verwaltet haben.

> [!Tip]
> Darüber hinaus bietet Windows Admin Center, eine allgemeine verwaltungsumgebung für alle Cluster unterstützen jede Workload, verfügbar für Windows Server 2012 und höher. Wählen Sie diese, wenn Sie Ihren Cluster Windows Admin Center hinzufügen besser geeignet scheint, [ **Failovercluster** ](manage-failover-clusters.md) anstelle von **Hyper-Converged Cluster**.

### <a name="prepare-your-windows-server-2016-cluster-for-windows-admin-center"></a>Vorbereiten Sie Ihres Windows Server 2016-Clusters für Windows Admin Center

Windows Admin Center für Hyper-Converged Infrastruktur hängt von Verwaltung, die APIs hinzugefügt, nachdem Windows Server 2016 veröffentlicht wurde. Bevor Sie Ihren Windows Server 2016-Cluster mit Windows Admin Center verwalten können, müssen Sie diese beiden Schritte ausführen:

1. Stellen Sie sicher, dass alle Server im Cluster installiert hat die [2018-05 Kumulatives Update für WindowsServer 2016 (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723) oder höher. Wechseln Sie zum Herunterladen und installieren Sie dieses Update, um **Einstellungen** > **Update und Sicherheit** > **Windows Update** , und wählen Sie  **Online nach Updates von Microsoft Update suchen**.
2. Führen Sie das folgende PowerShell-Cmdlet als Administrator an, auf dem Cluster:

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> Sie müssen nur einmal, führen Sie das Cmdlet auf einem beliebigen Server im Cluster. Sie können in Windows PowerShell lokal ausführen, oder verwenden Credential Security Service Provider (CredSSP) an einem Remotestandort ausgeführt. Abhängig von Ihrer Konfiguration können Sie dieses Cmdlet aus in Windows Admin Center ausführen möglicherweise nicht.

### <a name="prepare-your-windows-server-2019-cluster-for-windows-admin-center"></a>Vorbereiten Sie Ihres 2019 für Windows Server-Clusters für Windows Admin Center

Wenn Ihr Cluster Windows Server-2019 ausgeführt wird, sind die oben genannten Schritte nicht erforderlich. Fügen dem Cluster nur auf Windows Admin Center, wie im nächsten Abschnitt beschrieben, und Sie sind startklar!

### <a name="configure-software-defined-networking-optional"></a>Konfigurieren von Software-Defined Networking (Optional) ###

Sie können Ihre Hyper-Converged-Infrastruktur, die unter Windows Server 2016 oder 2019, verwenden Sie Software Defined Networking (SDN) mit den folgenden Schritten konfigurieren:

1. Bereiten Sie die virtuelle Festplatte des Betriebssystems die mit dem gleichen Betriebssystem wird Sie auf den Hosts hyperkonvergenten Infrastruktur installiert. Diese virtuelle Festplatte wird für alle NC/SLB/GW-VMs verwendet werden.
2. Laden Sie die Ordner und Dateien unter SDN Express von [ https://github.com/Microsoft/SDN/tree/master/SDNExpress ](https://github.com/Microsoft/SDN/tree/master/SDNExpress).
3. Bereiten Sie vor einem anderen virtuellen Computer mithilfe der Bereitstellungskonsole. Dieser virtuelle Computer sollte die SDN-Hosts zugreifen können. Darüber hinaus werden der virtuellen Computer verfügen die RSAT-Hyper-V-Tools installiert.
4. Kopieren Sie alle Elemente, die Sie in der Bereitstellungskonsole virtuellen Computer für SDN Express heruntergeladen werden soll. Teilen **SDNExpress** Ordner. Stellen Sie sicher, dass jeder Host Zugriff hat auf die **SDNExpress** freigegebenen Netzwerkordner, wie in der konfigurationsdateizeile 8 definiert:
   ```
    \\$env:Computername\SDNExpress
   ```
5. Kopieren Sie die VHD des Betriebssystems an die **Images** Ordner unter der **SDNExpress** Ordner in der Bereitstellungskonsole virtuellen Computer.
6. Ändern Sie die Konfiguration des SDN Express mit Ihrer Umgebung einrichten. Schließen Sie die folgenden beiden Schritte aus, nach dem Ändern der SDN Express-Konfigurations, die auf Grundlage der Umgebungsinformationen.
7. Führen Sie PowerShell mit Admin-Berechtigungen zum Bereitstellen von SDN aus:

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose 
```

Die Bereitstellung dauert ca. 30 bis 45 Minuten.

## <a name="get-started"></a>Beginnen

Nachdem Ihre Infrastruktur Hyper-Converged bereitgestellt wurde, können Sie mithilfe von Windows Admin Center verwalten.

### <a name="install-windows-admin-center"></a>Installieren von Windows Admin Center

Wenn Sie nicht bereits geschehen, herunterladen und installieren Sie Windows Admin Center. Die schnellste Möglichkeit, den Einstieg zu ist und ausgeführt wird, installieren Sie es auf Ihrem Windows 10-Computer und Ihre Server remote verwalten. Dies dauert weniger als fünf Minuten. [Jetzt herunterladen](https://aka.ms/windowsadmincenter) oder [erfahren Sie mehr über andere Installationsoptionen](../deploy/install.md).

### <a name="add-hyper-converged-cluster"></a>Hyperkonvergenten Cluster hinzufügen

So fügen Sie Ihrem Cluster Windows Admin Center hinzu

1. Klicken Sie auf **+ hinzufügen** unter alle Verbindungen.
2. Hinzufügen einer **Hyper-Converged Clusterverbindung**.
3. Geben Sie den Namen des Clusters und, wenn Sie dazu aufgefordert werden, die zu verwendenden Anmeldeinformationen.
4. Klicken Sie auf **hinzufügen** um den Vorgang abzuschließen.

Der Cluster wird der Liste der Verbindungen hinzugefügt werden. Klicken Sie auf, um das Dashboard zu öffnen.

![Verbindung mit einem hyperkonvergenten Cluster hinzufügen](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### <a name="add-sdn-enabled-hyper-converged-cluster-windows-admin-center-preview"></a>Hinzufügen von SDN-fähigen Hyperkonvergenten Cluster (Windows Admin Center-Vorschau)

Die neueste Windows Admin Center Preview unterstützt die Verwaltung Software Defined Networking Hyper-Converged-Infrastruktur. Eine Netzwerk-Controller-REST-URI Ihrer Hyperkonvergente Cluster-Verbindung hinzufügen, können Sie hyperkonvergente Cluster-Manager verwenden, um Ihre SDN-Ressourcen verwalten und Überwachen von SDN-Infrastruktur.

1. Klicken Sie auf **+ hinzufügen** unter alle Verbindungen.
2. Hinzufügen einer **Hyper-Converged Clusterverbindung**.
3. Geben Sie den Namen des Clusters und, wenn Sie dazu aufgefordert werden, die zu verwendenden Anmeldeinformationen.
4. Überprüfen Sie **konfigurieren Sie den Netzwerkcontroller** um den Vorgang fortzusetzen.
5. Geben Sie die **Network Controller URI** , und klicken Sie auf **überprüfen**.
6. Klicken Sie auf **hinzufügen** um den Vorgang abzuschließen.

Der Cluster wird der Liste der Verbindungen hinzugefügt werden. Klicken Sie auf, um das Dashboard zu öffnen.

![SDN-fähigen hyperkonvergenten Cluster-Verbindung hinzufügen](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> SDN-Umgebungen mit Kerberos-Authentifizierung für die Northbound-Kommunikation werden derzeit nicht unterstützt.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="are-there-differences-between-managing-windows-server-2016-and-windows-server-2019"></a>Gibt es Unterschiede zwischen der Verwaltung von Windows Server 2016 und Windows Server-2019?

Ja. Windows Admin Center für Hyper-Converged Infrastruktur empfängt die häufige Updates, die die Erfahrung für Windows Server 2016 und Windows Server-2019 zu verbessern. Allerdings sind bestimmte neuen Funktionen nur verfügbar für Windows Server 2019 – z. B. mit dem Umschalter für Deduplizierung und Komprimierung.

### <a name="can-i-use-windows-admin-center-to-manage-storage-spaces-direct-for-other-use-cases-not-hyper-converged-such-as-converged-scale-out-file-server-sofs-or-microsoft-sql-server"></a>Kann ich Windows Admin Center verwenden, um "direkte Speicherplätze" für andere Anwendungsfälle (nicht hyper-konvergiert), z. B. zusammengeführte Dateiserver mit horizontaler (Skalierung SoFS) oder Microsoft SQL Server zu verwalten?

Windows Admin Center für Hyper-Converged Infrastruktur bietet keine Verwaltung oder Überwachungsoptionen speziell für andere Anwendungsfälle von "direkte Speicherplätze" – z. B. sie keine Dateifreigaben erstellen. Allerdings funktionieren die Dashboards und Core-Features, wie z. B. das Erstellen von Volumes oder Laufwerke, und Ersetzen Sie dabei für alle Cluster "direkte Speicherplätze".

### <a name="whats-the-difference-between-a-failover-cluster-and-a-hyper-converged-cluster"></a>Was ist der Unterschied zwischen einem Failovercluster und einem Hyper-Converged Cluster?

Im Allgemeinen gruppiert der Begriff bezieht sich mit der "hyperkonvergent" für die Ausführung von Hyper-V- und "direkte Speicherplätze" auf dem gleichen Server zum Virtualisieren von COMPUTE-und Speicherressourcen. Im Kontext des Windows Admin Center, wenn Sie auf **+ hinzufügen** aus der Verbindungsliste können Sie zwischen dem Hinzufügen einer **Failover Cluster-Verbindung** oder **Hyper-Converged-Cluster Verbindung**:

- Die **Failover Cluster-Verbindung** ist der Nachfolger von der Failovercluster-Manager-desktop-app. Es bietet eine vertraute und allgemeine Verwaltungsoberfläche, für alle Cluster, die jede Workload, einschließlich Microsoft SQL Server unterstützen. Es ist für Windows Server 2012 und höher verfügbar.

- Die **Hyper-Converged Clusterverbindung** ist eine völlig neue Erfahrung für "direkte Speicherplätze" und Hyper-V zugeschnitten. Es bietet das Dashboard und betont Diagramme und Warnungen für die Überwachung. Es ist für Windows Server 2016 und Windows Server-2019 verfügbar.

### <a name="why-do-i-need-the-latest-cumulative-update-for-windows-server-2016"></a>Warum benötige ich das neueste kumulative Update für Windows Server 2016?

Windows Admin Center für Hyper-Converged Infrastruktur hängt von Verwaltung, die APIs entwickelt, da Windows Server 2016 veröffentlicht wurde. Diese APIs werden hinzugefügt, der [2018-05 Kumulatives Update für WindowsServer 2016 (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723), ab dem 8. Mai 2018 verfügbar.

### <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Wie viel kostet Windows Admin Center?

Windows Admin Center ist ohne zusätzliche Kosten über Windows erhältlich.

Sie können Windows Admin Center (als separater Download verfügbar) mit gültiger Lizenzen von Windows Server oder Windows 10 ohne zusätzliche Kosten verwenden – er lizenziert unter ein ergänzender EULA für Windows.

### <a name="does-windows-admin-center-require-system-center"></a>Erfordert Windows Admin Center das System Center?

Nein.

### <a name="does-it-require-an-internet-connection"></a>Ist es erforderlich, dass eine Internetverbindung?

Nein.

Obwohl Windows Admin Center leistungsstarke bietet und praktische-Integration mit der Microsoft Azure-Cloud, die zentrale Verwaltung und überwachungsoberfläche für Hyper-Converged Infrastruktur vollständig lokal. Sie können installiert werden und ohne Internetverbindung verwendet werden.

## <a name="things-to-try"></a>Versuchen Folgendes

Wenn Sie zum Einstieg, sind hier einige schnellen Lernprogrammen für den erfahren, wie Windows Admin Center für Hyper-Converged Infrastruktur organisiert ist und funktioniert. Übung Menschenverstand, und achten Sie darauf, dass Sie mit der Produktion eingesetzten Umgebungen. Diese Videos wurden mit Windows Admin Center-Version 1804 und ein Insider Preview-Build von Windows Server-2019 aufgezeichnet.

### <a name="manage-storage-spaces-direct-volumes"></a>Verwalten von Volumes mit "direkte Speicherplätze"

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">Gewusst wie: Erstellen eines Volumes drei-Wege-Spiegelung</a></li>
               <li>(1:17) <a href="https://youtu.be/R72QHudqWpE">Gewusst wie: Erstellen Sie ein Volume Parität Mirror-Beschleunigung</a></li>
               <li>(1:02) <a href="https://youtu.be/j59z7ulohs4">So öffnen Sie ein Volume und Hinzufügen von Dateien</a></li>
               <li>(0:51) <a href="https://youtu.be/PRibTacyKko">Deduplizierung und Komprimierung aktivieren</a></li>
               <li>(0:47) <a href="https://youtu.be/hqyBzipBoTI">Gewusst wie: Erweitern eines Volumes</a></li>
               <li>(0:26) <a href="https://youtu.be/DbjF8r2F6Jo">Vorgehensweise: Löschen ein Volumes</a></li>
</ul>

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Erstellen Sie Volumes, die drei-Wege-Spiegelung</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/o66etKq70N8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Erstellen Sie Volume Parität Mirror-Beschleunigung</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/R72QHudqWpE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Öffnen Sie die Datei und Hinzufügen von Dateien</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/j59z7ulohs4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Aktivieren Sie Deduplizierung und Komprimierung</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/PRibTacyKko" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Erweitern von Volumes</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/hqyBzipBoTI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Löschen von volume</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/DbjF8r2F6Jo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
</table>

### <a name="create-a-new-virtual-machine"></a>Erstellen eines neuen virtuellen Computers

1. Klicken Sie auf die **VMs** Tool im Navigationsbereich mit der linken Seite.
2. Wählen Sie am Anfang des VM-Tools, die **Inventur** Registerkarte, und klicken Sie dann **neu** um einen neuen virtuellen Computer zu erstellen.
3. Geben Sie den virtuellen Computer ein, und wählen Sie zwischen virtuellen Computern der Generation 1 und 2.
4. So kann dann auswählen, welcher Host zum anfänglich auf dem virtuellen Computer erstellen oder verwenden Sie die empfohlenen Host.
5. Wählen Sie einen Pfad für die Dateien der virtuellen Maschine. Wählen Sie ein Volume aus der Dropdownliste aus, oder klicken Sie auf **Durchsuchen** um einen Ordner, die über die Ordnerauswahl auszuwählen. Die Konfigurationsdateien der virtuellen Computer und die VHD-Datei werden gespeichert in einem einzigen Ordner unter dem `\Hyper-V\[virtual machine name]` Pfad des ausgewählten Volumes oder der Pfad.
6. Wählen Sie die Anzahl virtueller Prozessoren, ob Sie die geschachtelte Virtualisierung aktiviert werden soll, konfigurieren Einstellungen für den Arbeitsspeicher, Netzwerkadapter, virtuelle Festplatten und auswählen, ob ein Betriebssystem von einer ISO-Abbilddatei oder vom Netzwerk installiert werden soll.
7. Klicken Sie auf **Erstellen**, um die virtuelle Maschine zu erstellen.
8. Nachdem Sie den virtuellen Computer erstellt und wird in der Liste der virtuellen Computer angezeigt, können Sie den virtuellen Computer starten.
9. Nachdem der virtuelle Computer gestartet wurde, können Sie mit der VM Konsole über das VMConnect zum Installieren des Betriebssystems verbinden. Wählen Sie den virtuellen Computer aus der Liste aus, klicken Sie auf **weitere** > **Connect** zum Herunterladen der RDP-Datei. Öffnen Sie die RDP-Datei, in der app für die Remotedesktopverbindung. Da dies in der VM Konsole verbunden ist, müssen Sie den Hyper-V-Host-Administratoranmeldeinformationen einzugeben.

[Erfahren Sie mehr über die Verwaltung virtueller Computer mit Windows Admin Center](manage-virtual-machines.md).

### <a name="pause-and-safely-restart-a-server"></a>Halten Sie an und Neustarten Sie sicher auf einen server

1. Von der **Dashboard**Option **Server** im Navigationsbereich auf der linken Seite oder durch Klicken auf die **Server anzeigen >** Link auf der Kachel in der unteren rechten Ecke des Dashboards .
2. Wechseln Sie im oberen Bereich von **Zusammenfassung** auf die **Inventur** Registerkarte.
3. Wählen Sie einen Server, indem Sie auf den Namen in das Öffnen der **Server** Detailseite.
4. Klicken Sie auf **Anhalten eines Servers für die Wartung**. Wenn fortgesetzt werden kann, wird dadurch virtuellen Maschinen auf andere Server im Cluster verschoben. Der Server wird sein Status zu leeren, während dieses Vorgangs. Wenn Sie möchten, können Sie sehen Sie sich die virtuellen Computer weiter die **virtuelle Computer > Inventar** Seite, in dem ihre Hostserver eindeutig im Raster angezeigt wird. Wenn alle virtuellen Computer verschoben haben, wird der Status des Servers **angehalten**.
5. Klicken Sie auf **-Server verwalten** auf alle pro-Server-Verwaltungstools in Windows Admin Center zugreifen.
6. Klicken Sie auf **Neustart**, klicken Sie dann **Ja**. Sie werden zurück in die Verbindungsliste initiiert werden soll.
7. Auf der **Dashboard**, der Server ist rot, wenn dieser ausgefallen ist.
8. Sobald sie sich sichern ist, navigieren Sie erneut die **Server** Seite, und klicken Sie auf **Resume-Server von Wartung** an einfach immer den Status des Servers fest. In der Zeit werden virtuelle Computer zurück – verschoben keine Handlung des Benutzers erforderlich ist.

### <a name="replace-a-failed-drive"></a>Ersetzen Sie einen fehlerhaften Datenträger

1. Wenn ein Laufwerk ausfällt, wird eine Benachrichtigung angezeigt, in der oberen linken Ecke **Warnungen** Teil der **Dashboard**.
2. Sie können auch auswählen, **Laufwerke** aus dem Navigationsbereich auf der linken Seite oder klicken Sie auf die **Ansicht Laufwerke >** Link auf der Kachel in der unteren rechten Ecke, durchsuchen die Laufwerke und deren Status selbst ermitteln. In der **Inventur** Registerkarte Raster unterstützt die Sortierung, Gruppierung und Schlüsselwortsuche.
3. Von der **Dashboard**, klicken Sie auf die Warnung aus, um Details wie den physischen Speicherort des Laufwerks anzuzeigen.
4. Informieren, klicken Sie auf die **wechseln Sie zu Laufwerk** Verknüpfung zu den **Laufwerk** Detailseite.
5. Wenn Ihre Hardware unterstützt wird, können Sie klicken **Licht zu aktivieren/deaktivieren von** Leuchte des Laufwerks zu steuern.
6. "Direkte Speicherplätze" automatisch abkoppelt, trifft und fehlerhafte Laufwerke verschoben. Wenn dies der Fall, der Laufwerkstatus ist veraltet, und die Speicher-Kapazitätsbalken ist leer.
7. Entfernen Sie den fehlerhaften Datenträger aus, und legen Sie als Ersatz.
8. In **Laufwerke > Inventory**, wird das neue Laufwerk angezeigt. In-Time die Warnung wird gelöscht, Volumes werden zurück an den Status OK, reparieren und Speicher wird auf das neue Laufwerk ausgleichen: ist keine Benutzeraktion erforderlich.

### <a name="manage-virtual-networks-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>Verwalten von virtuellen Netzwerken (SDN-fähigen HCI-Cluster unter Verwendung von Windows Admin Center Preview)

1. Wählen Sie **virtuelle Netzwerke** im Navigationsbereich auf der linken Seite.
2. Klicken Sie auf **neu** , erstellen Sie ein neues virtuelles Netzwerk und Subnetze, oder wählen Sie ein vorhandenes virtuelles Netzwerk aus, und klicken Sie auf **Einstellungen** seine Konfiguration zu ändern.
3. Klicken Sie auf ein vorhandenes virtuelles Netzwerk zum Anzeigen von VM-Verbindungen mit den Subnetzen des virtuellen Netzwerks und access Control Lists, die auf Subnetzen in virtuellen Netzwerken angewendet.

![Verwalten von virtuellen Netzwerken](../media/manage-hyper-converged/manage-virtual-networks.png)

### <a name="connect-a-virtual-machine-to-a-virtual-network-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>Verbinden Sie virtueller Computer mit einem virtuellen Netzwerk (SDN-fähigen HCI-Cluster unter Verwendung von Windows Admin Center Preview)

1. Wählen Sie **VMs** im Navigationsbereich auf der linken Seite.
2. Wählen Sie einen vorhandenen virtuellen Computer > Klicken Sie auf **Einstellungen** > Öffnen die **Netzwerke** Registerkarte **Einstellungen**.
3. Konfigurieren der **Virtual Network** und **virtuelle Subnetz** Felder für den virtuellen Computer mit einem virtuellen Netzwerk zu verbinden.

Sie können auch das virtuelle Netzwerk konfigurieren, beim Erstellen eines virtuellen Computers.

![Herstellen einer Verbindung eines virtuellen Netzwerks mit einem virtuellen Computer](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### <a name="monitor-software-defined-networking-infrastructure-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>Überwachen der Infrastruktur Software Defined Networking (SDN-fähigen HCI-Cluster unter Verwendung von Windows Admin Center Preview)

1. Wählen Sie **SDN Überwachung** im Navigationsbereich auf der linken Seite.
2. Zeigen Sie ausführliche Informationen über die Integrität des virtuellen Gateways Netzwerkcontroller, Softwarelastenausgleich, und überwachen Sie virtuelle Gatewaypool, öffentliche und Private IP-Pool-Nutzung und Status der SDN-Hosts zu.

![Überwachen von SDN-Infrastruktur](../media/manage-hyper-converged/sdn-monitoring.png)

## <a name="feedback"></a>Feedback senden

Alles dreht sich Ihr Feedback! Der wichtigste Vorteil von häufige Updates ist, erfahren Sie, was funktioniert und was verbessert werden muss. Hier sind einige Möglichkeiten, um uns mitzuteilen, was Sie denken:

- [Übermitteln und Abstimmen für featureanforderungen auf UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Das Windows Admin Center-Forum auf Microsoft Tech Community beitreten](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- Zum Tweet `@servermgmt`

### <a name="see-also"></a>Siehe auch

- [Windows Admin Center](../understand/windows-admin-center.md)
- [Direkte Speicherplätze](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
- [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)
- [Software-Defined Networking](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)
