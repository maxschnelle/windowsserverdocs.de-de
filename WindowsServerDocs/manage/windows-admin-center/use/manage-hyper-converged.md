---
title: Verwalten der hyperkonvergierten Infrastruktur mit dem Windows Admin Center
description: Verwalten der hyperkonvergierten Infrastruktur mit Windows Admin Center (Project Honolulu)
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 56d953c721fff2218b256fa99d83078485438c0f
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90765971"
---
# <a name="manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Verwalten der hyperkonvergierten Infrastruktur mit dem Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

## <a name="what-is-hyper-converged-infrastructure"></a>Was ist eine hyperkonvergierte Infrastruktur?

Die hyperkonvergierte Infrastruktur konsolidiert softwaredefinierte COMPUTE-, Speicher-und Netzwerk Netzwerke in einem Cluster, um eine leistungsfähige, kostengünstige und leicht skalierbare Virtualisierung bereitzustellen. Diese Funktion wurde in Windows Server 2016 mit [direkte Speicherplätze](../../../storage/storage-spaces/storage-spaces-direct-overview.md), [Software-Defined Networking](../../../networking/sdn/software-defined-networking.md) und [Hyper-V](../../../virtualization/hyper-v/hyper-v-on-windows-server.md)eingeführt.

> [!Tip]
> Sie möchten eine hyperkonvergierte Infrastruktur erwerben? Microsoft empfiehlt von unseren Partnern diese [Software definierten Lösungen von Windows Server](https://microsoft.com/wssd) . Sie wurden in unserer Referenzarchitektur entworfen, zusammengestellt und überprüft, um Kompatibilität und Zuverlässigkeit sicherzustellen, sodass Sie schnell loslegen können.

> [!IMPORTANT]
> Einige der in diesem Artikel beschriebenen Funktionen sind nur in der Vorschauversion des Windows Admin Centers verfügbar. [Gewusst wie diese Version erhalten?](../overview.md)

## <a name="what-is-windows-admin-center"></a>Was ist Windows Admin Center?

[Windows Admin Center](../overview.md) ist das Verwaltungs Tool der nächsten Generation für Windows Server, das Nachfolger für herkömmliche "in-Box"-Tools wie Server-Manager. Es ist kostenlos und kann ohne Internet Verbindung installiert und verwendet werden. Mithilfe des Windows Admin Centers können Sie die hyperkonvergierte Infrastruktur verwalten und überwachen, die unter Windows Server 2016 oder Windows Server 2019 ausgeführt wird.

![Hyperkonvergierte Cluster-Dashboard](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## <a name="key-features"></a>Wichtige Features

Zu den Highlights des Windows Admin Centers für die hyperkonvergierte Infrastruktur gehören:

- **Einheitliche, einfache Umgebung für Compute-, Speicher-und demnächst-Netzwerke.** Zeigen Sie Ihre virtuellen Computer, Host Server, Volumes, Laufwerke und vieles mehr innerhalb eines zweckgebundenen, konsistenten, vernetzten Benutzer Erlebnisses an.
- **Erstellen und verwalten Sie Speicherplätze und virtuelle Hyper-V-Computer.** Grundlegend einfache Workflows zum Erstellen, öffnen, Ändern der Größe und Löschen von Volumes und erstellen, starten, verbinden und Verschieben von virtuellen Maschinen; und vieles mehr.
- **Leistungsstarke Cluster weite Überwachung.** Die Dashboarddiagramme der Arbeitsspeicher-und CPU-Auslastung, Speicherkapazität, IOPS, Durchsatz und Latenz in Echtzeit auf allen Servern im Cluster mit klaren Warnungen, wenn etwas nicht richtig ist.
- **Unterstützung für Software-Defined Networking (SDN).** Verwalten und Überwachen von virtuellen Netzwerken, Subnetzen, verbinden virtueller Computer mit virtuellen Netzwerken und Überwachen der Sdn-Infrastruktur

Das Windows Admin Center für die hyperkonvergierte Infrastruktur wird von Microsoft aktiv entwickelt. Er empfängt häufig Updates, die vorhandene Features verbessern und neue Features hinzufügen.

## <a name="before-you-start"></a>Vorbereitung

Um Ihren Cluster als hyperkonvergierte Infrastruktur im Windows Admin Center zu verwalten, muss Windows Server 2016 oder Windows Server 2019 ausgeführt werden, und Hyper-V und direkte Speicherplätze aktiviert werden. Optional kann die Software auch über das Windows Admin Center aktiviert und verwaltet werden.

> [!Tip]
> Windows Admin Center bietet auch eine allgemeine Verwaltungsfunktion für alle Cluster, die alle Arbeits Auslastungen unterstützen, die für Windows Server 2012 und höher verfügbar sind. Wenn dies eine bessere Anpassung hat, wählen Sie beim Hinzufügen des Clusters zum Windows Admin Center [**Failovercluster**](manage-failover-clusters.md) anstelle des **hyperkonvergierten Clusters**aus.

### <a name="prepare-your-windows-server-2016-cluster-for-windows-admin-center"></a>Vorbereiten des Windows Server 2016-Clusters für Windows Admin Center

Windows Admin Center für hyperkonvergierte Infrastrukturen hängt von den Verwaltungs-APIs ab, die nach der Veröffentlichung von Windows Server 2016 hinzugefügt wurden. Bevor Sie Ihren Windows Server 2016-Cluster mit Windows Admin Center verwalten können, müssen Sie die folgenden beiden Schritte ausführen:

1. Vergewissern Sie sich, dass auf jedem Server im Cluster das [kumulative Update 2018-05 für Windows Server 2016 (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723) oder höher installiert ist. Um dieses Update herunterzuladen und zu installieren, wechseln Sie zu **Einstellungen**  >  **Aktualisieren & Sicherheits**  >  **Windows Update** , und wählen Sie **Online nach Updates suchen aus Microsoft Update aus**.
2. Führen Sie das folgende PowerShell-Cmdlet als Administrator für den Cluster aus:

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> Sie müssen das Cmdlet nur einmal auf einem beliebigen Server im Cluster ausführen. Sie können Sie lokal in Windows PowerShell ausführen oder den Anmelde Informationen-Sicherheits Dienstanbieter (Security Service Provider, kredssp) verwenden, um Sie Remote auszuführen. Abhängig von Ihrer Konfiguration können Sie dieses Cmdlet möglicherweise nicht innerhalb des Windows Admin Centers ausführen.

### <a name="prepare-your-windows-server-2019-cluster-for-windows-admin-center"></a>Vorbereiten des Windows Server 2019-Clusters für Windows Admin Center

Wenn Ihr Cluster Windows Server 2019 ausführt, sind die obigen Schritte nicht erforderlich. Fügen Sie den Cluster dem Windows Admin Center hinzu, wie im nächsten Abschnitt beschrieben, und Sie sind gut unterwegs!

### <a name="configure-software-defined-networking-optional"></a>Konfigurieren von Software-Defined Networking (optional) ###

Sie können Ihre hyperkonvergierte Infrastruktur mit Windows Server 2016 oder 2019 so konfigurieren, dass Sie mit den folgenden Schritten Software-Defined Networking (SDN) verwendet:

1. Bereiten Sie die VHD des Betriebssystems vor, bei dem es sich um das gleiche Betriebssystem handelt, das Sie auf den hyperkonvergierten Infrastruktur Hosts Diese VHD wird für alle virtuellen NC/SLB/GW-VMS verwendet.
2. Laden Sie den gesamten Ordner und die Dateien unter sdn Express von herunter [https://github.com/Microsoft/SDN/tree/master/SDNExpress](https://github.com/Microsoft/SDN/tree/master/SDNExpress) .
3. Bereiten Sie mithilfe der Bereitstellungs Konsole einen anderen virtuellen Computer vor. Diese VM sollte auf die Sdn-Hosts zugreifen können. Außerdem sollte auf dem virtuellen Computer das RSAT-Hyper-V-Tool installiert sein.
4. Kopieren Sie alles, was Sie für Sdn Express heruntergeladen haben, in die VM der Bereitstellungs Und geben Sie diesen Ordner **sdnexpress** frei. Stellen Sie sicher, dass jeder Host auf den freigegebenen **sdnexpress** -Ordner zugreifen kann, wie in der Konfigurationsdatei Zeile 8 definiert:
   ```
    \\$env:Computername\SDNExpress
   ```
5. Kopieren Sie die virtuelle Festplatte des Betriebssystems in den Ordner **Images** im Ordner **sdnexpress** auf der VM der Bereitstellungs Konsole.
6. Ändern Sie die Sdn Express-Konfiguration mit dem Setup Ihrer Umgebung. Führen Sie die folgenden beiden Schritte aus, nachdem Sie die Sdn Express-Konfiguration basierend auf Ihren Umgebungs Informationen geändert haben.
7. Führen Sie PowerShell mit Administrator Berechtigung zum Bereitstellen von Sdn aus:

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose
```

Die Bereitstellung dauert ca. 30 – 45 Minuten.

## <a name="get-started"></a>Erste Schritte

Sobald Ihre hyperkonvergierte Infrastruktur bereitgestellt ist, können Sie Sie mithilfe des Windows Admin Centers verwalten.

### <a name="install-windows-admin-center"></a>Installieren von Windows Admin Center

Wenn Sie dies noch nicht getan haben, müssen Sie Windows Admin Center herunterladen und installieren. Die schnellste Möglichkeit, sich einzurichten, ist die Installation auf Ihrem Windows 10-Computer und die Remote Verwaltung Ihrer Server. Dieser Vorgang dauert weniger als fünf Minuten. [Laden Sie jetzt herunter](../overview.md) , oder [erfahren Sie mehr über andere Installationsoptionen](../deploy/install.md).

### <a name="add-hyper-converged-cluster"></a>Hyperkonvergierten Cluster hinzufügen

So fügen Sie Ihren Cluster zum Windows Admin Center hinzu:

1. Klicken Sie unter alle Verbindungen auf **+ Hinzufügen** .
2. Wählen Sie die Option zum Hinzufügen einer **hyperkonvergierten Cluster Verbindung**aus.
3. Geben Sie den Namen des Clusters und, falls Sie dazu aufgefordert werden, die zu verwendenden Anmelde Informationen ein.
4. Klicken Sie zum Beenden auf **Hinzufügen** .

Der Cluster wird der Verbindungsliste hinzugefügt. Klicken Sie darauf, um das Dashboard zu starten.

![Hyperkonvergierte Cluster Verbindung hinzufügen](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### <a name="add-sdn-enabled-hyper-converged-cluster-windows-admin-center-preview"></a>SDN-aktivierten hyperkonvergierten Cluster hinzufügen (Vorschau des Windows Admin Centers)

Die neueste Windows Admin Center-Vorschauversion unterstützt die Software-Defined Networking-Verwaltung für hyperkonvergierte Infrastrukturen. Durch Hinzufügen eines Netzwerk Controller-Rest-URIs zu ihrer hyperkonvergierten Cluster Verbindung können Sie den hyperkonvergierten Cluster-Manager verwenden, um Ihre Sdn-Ressourcen zu verwalten und die Sdn-Infrastruktur zu überwachen.

1. Klicken Sie unter alle Verbindungen auf **+ Hinzufügen** .
2. Wählen Sie die Option zum Hinzufügen einer **hyperkonvergierten Cluster Verbindung**aus.
3. Geben Sie den Namen des Clusters und, falls Sie dazu aufgefordert werden, die zu verwendenden Anmelde Informationen ein.
4. Aktivieren Sie **Konfigurieren des Netzwerk Controllers** , um fortzufahren.
5. Geben Sie den **Netzwerk Controller-URI** ein, und klicken Sie auf **Validate**
6. Klicken Sie zum Beenden auf **Hinzufügen** .

Der Cluster wird der Verbindungsliste hinzugefügt. Klicken Sie darauf, um das Dashboard zu starten.

![SDN-aktivierte hyperkonvergierte Cluster Verbindung hinzufügen](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> SDN-Umgebungen mit Kerberos-Authentifizierung für die Kommunikation mit Northbound werden zurzeit nicht unterstützt.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="are-there-differences-between-managing-windows-server-2016-and-windows-server-2019"></a>Gibt es Unterschiede zwischen der Verwaltung von Windows Server 2016 und Windows Server 2019?

Ja. Das Windows Admin Center für hyperkonvergierte Infrastrukturen empfängt häufig Updates, die die Leistung von Windows Server 2016 und Windows Server 2019 verbessern. Bestimmte neue Features sind jedoch nur für Windows Server 2019 verfügbar – beispielsweise die UMSCHALT Fläche für Deduplizierung und Komprimierung.

### <a name="can-i-use-windows-admin-center-to-manage-storage-spaces-direct-for-other-use-cases-not-hyper-converged-such-as-converged-scale-out-file-server-sofs-or-microsoft-sql-server"></a>Kann ich das Windows Admin Center verwenden, um direkte Speicherplätze für andere Anwendungsfälle (nicht hyperkonvergiert) zu verwalten, wie z. b. konvergierte Dateiserver mit horizontaler Skalierung (sofs) oder Microsoft SQL Server?

Das Windows Admin Center für hyperkonvergierte Infrastrukturen bietet keine Verwaltungs-oder Überwachungs Optionen speziell für andere Anwendungsfälle von direkte Speicherplätze – beispielsweise kann keine Dateifreigaben erstellt werden. Das Dashboard und die Kernfunktionen, wie das Erstellen von Volumes oder das Austauschen von Laufwerken, funktionieren jedoch für alle direkte Speicherplätze Cluster.

### <a name="whats-the-difference-between-a-failover-cluster-and-a-hyper-converged-cluster"></a>Worin besteht der Unterschied zwischen einem Failovercluster und einem hyperkonvergierten Cluster?

Im Allgemeinen bezieht sich der Begriff "hyperkonvergiert" auf die Ausführung von Hyper-V und direkte Speicherplätze auf denselben gruppierten Servern, um COMPUTE-und Speicherressourcen zu virtualisieren. Wenn Sie im Kontext des Windows Admin Centers in der Liste Verbindungen auf **+ Hinzufügen** klicken, können Sie zwischen dem Hinzufügen einer **failoverclusterverbindung** oder einer **hyperkonvergierten Cluster Verbindung**wählen:

- Die **failoverclusterverbindung** ist der Nachfolger der Failovercluster-Manager Desktop-App. Es bietet eine vertraute allgemeine Verwaltungsfunktion für alle Cluster, die alle Arbeits Auslastungen unterstützen, einschließlich Microsoft SQL Server. Es ist für Windows Server 2012 und höher verfügbar.

- Bei der **hyperkonvergierten Cluster Verbindung** handelt es sich um eine neue, auf direkte Speicherplätze und Hyper-V zugeschnittene Version. Sie konzentriert sich auf das Dashboard und legt den Schwerpunkt auf Diagramme und Benachrichtigungen zur Überwachung. Es ist für Windows Server 2016 und Windows Server 2019 verfügbar.

### <a name="why-do-i-need-the-latest-cumulative-update-for-windows-server-2016"></a>Warum benötige ich das neueste kumulative Update für Windows Server 2016?

Das Windows Admin Center für hyperkonvergierte Infrastrukturen hängt von den Management-APIs ab, die seit der Veröffentlichung von Windows Server 2016 entwickelt wurden. Diese APIs werden im [kumulativen 2018-05-Update für Windows Server 2016 (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)hinzugefügt, das ab dem 8. Mai 2018 verfügbar ist.

### <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Wie viel kostet die Verwendung von Windows Admin Center?

Für Windows Admin Center fallen jenseits der Kosten für Windows keine zusätzlichen Kosten an.

Sie können Windows Admin Center (als separater Download verfügbar) mit den gültigen Lizenzen für Windows Server oder Windows 10 ohne zusätzliche Kosten verwenden – es ist unter einer ergänzenden Windows-EULA (ENDBENUTZER-LIZENZVERTRAG) lizenziert.

### <a name="does-windows-admin-center-require-system-center"></a>Ist System Center für Windows Admin Center erforderlich?

Nein

### <a name="does-it-require-an-internet-connection"></a>Ist eine Internet Verbindung erforderlich?

Nein.

Obwohl das Windows Admin Center eine leistungsstarke und bequeme Integration in die Microsoft Azure Cloud bietet, ist die zentrale Verwaltungs-und Überwachungsumgebung für hyperkonvergierte Infrastrukturen vollständig lokal. Sie kann ohne Internet Verbindung installiert und verwendet werden.

## <a name="things-to-try"></a>Versuchen Sie Folgendes

Wenn Sie gerade erst beginnen, finden Sie hier einige kurze Tutorials, die Ihnen helfen zu erfahren, wie das Windows Admin Center für die hyperkonvergierte Infrastruktur organisiert ist und funktioniert. Führen Sie ein gutes Urteil aus, und seien Sie vorsichtig mit Produktionsumgebungen. Diese Videos wurden mit Windows Admin Center, Version 1804, und einem Insider Preview-Build von Windows Server 2019 aufgezeichnet.

### <a name="manage-storage-spaces-direct-volumes"></a>Verwalten von direkte Speicherplätze Volumes

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">Erstellen eines drei-Wege-Spiegelungs Volumens</a></li>
               <li>(1:17) Vorgehens <a href="https://youtu.be/R72QHudqWpE">Weise beim Erstellen eines Volumes mit Spiegelungs beschleunigter Parität</a></li>
               <li>(1:02) <a href="https://youtu.be/j59z7ulohs4">Öffnen eines Volumes und Hinzufügen von Dateien</a></li>
               <li>(0:51) Vorgehens <a href="https://youtu.be/PRibTacyKko">Weise beim Aktivieren der Deduplizierung und Komprimierung</a></li>
               <li>(0:47) <a href="https://youtu.be/hqyBzipBoTI">Erweitern eines</a> Volumes</li>
               <li>(0:26) <a href="https://youtu.be/DbjF8r2F6Jo">Löschen eines</a> Volumes</li>
</ul>

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Volume erstellen, drei-Wege-Spiegelung</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/o66etKq70N8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Erstellen von Volumes, Spiegel beschleunigter Parität</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/R72QHudqWpE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Volume öffnen und Dateien hinzufügen</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/j59z7ulohs4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Deduplizierung und Komprimierung aktivieren</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/PRibTacyKko" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Volume erweitern</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/hqyBzipBoTI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Volume löschen</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/DbjF8r2F6Jo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
</table>

### <a name="create-a-new-virtual-machine"></a>Erstellen einer neuen VM

1. Klicken Sie im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Wählen Sie am oberen Rand des Virtual Machines Tools die Registerkarte **Inventur** aus, und klicken Sie dann auf **neu** , um einen neuen virtuellen Computer zu erstellen.
3. Geben Sie den Namen des virtuellen Computers ein, und wählen Sie zwischen virtuellen Computern der Generation 1 und 2.
4. Die UOU kann dann auswählen, auf welchem Host der virtuelle Computer anfänglich erstellt werden soll, oder den empfohlenen Host verwenden.
5. Wählen Sie einen Pfad für die Dateien der virtuellen Maschine aus. Wählen Sie ein Volume aus der Dropdown Liste aus, oder klicken Sie auf **Durchsuchen** , um einen Ordner mithilfe der Ordner Auswahl auszuwählen. Die Konfigurationsdateien und virtuellen Festplatten Dateien der virtuellen Maschine werden in einem einzelnen Ordner unter dem `\Hyper-V\[virtual machine name]` Pfad des ausgewählten Volumes oder Pfads gespeichert.
6. Wählen Sie die Anzahl der virtuellen Prozessoren aus, egal ob Sie die aktivierte aktivierte Virtualisierung aktivieren möchten, konfigurieren Sie Arbeitsspeicher Einstellungen, Netzwerkadapter und virtuelle Festplatten, und wählen Sie aus, ob Sie ein Betriebssystem aus einer ISO-Abbild Datei oder aus dem Netzwerk installieren möchten.
7. Klicken Sie auf **Erstellen**, um die virtuelle Maschine zu erstellen.
8. Nachdem der virtuelle Computer erstellt und in der Liste der virtuellen Computer angezeigt wird, können Sie den virtuellen Computer starten.
9. Nachdem der virtuelle Computer gestartet wurde, können Sie über VMConnect eine Verbindung mit der Konsole des virtuellen Computers herstellen, um das Betriebssystem zu installieren. Wählen Sie den virtuellen Computer aus der Liste aus, klicken Sie auf **Weitere**  >  **Verbindung** , um die RDP-Datei herunterzuladen. Öffnen Sie die RDP-Datei in der Remotedesktopverbindung-app. Da diese Verbindung mit der Konsole des virtuellen Computers hergestellt wird, müssen Sie die Administrator Anmelde Informationen für den Hyper-V-Host eingeben.

[Erfahren Sie mehr über die Verwaltung virtueller Computer mit dem Windows Admin Center](manage-virtual-machines.md).

### <a name="pause-and-safely-restart-a-server"></a>Anhalten und sicheres Neustarten eines Servers

1. Wählen Sie im **Dashboard**auf der linken Seite die Option **Server** aus, oder klicken Sie auf den Link **Server >anzeigen **  auf der Kachel in der unteren rechten Ecke des Dashboards.
2. Wechseln Sie am oberen Rand von **Zusammenfassung** zur Registerkarte **Inventur** .
3. Wählen Sie einen Server aus, indem Sie auf den Namen klicken, um die Seite **Server** Detail zu öffnen
4. Klicken Sie **auf Server zur Wartung**anhalten. Wenn es sicher ist, dass der Vorgang fortgesetzt werden kann, werden die virtuellen Maschinen auf andere Server im Cluster verschoben. Der Server wird in diesem Fall in den Status entwässert. Wenn Sie möchten, können Sie sich die virtuellen Computer auf der Seite **virtuelle Computer > Inventur** ansehen, auf der der zugehörige Host Server im Raster eindeutig angezeigt wird. Wenn alle virtuellen Computer verschoben wurden, wird der Serverstatus **angeh**alten.
5. Klicken Sie auf **Server verwalten** , um auf alle Verwaltungs Tools Pro Server im Windows Admin Center zuzugreifen.
6. Klicken Sie auf **neu starten**und dann auf **Ja**. Sie werden zur Verbindungsliste zurückgekehrt.
7. Auf dem **Dashboard**ist der Server rot gefärbt, während er nicht mehr angezeigt wird.
8. Navigieren Sie nach der Wiederaufnahme wieder zur Seite **Server** , und klicken Sie auf **Server von Wartung** fortsetzen, um den Serverstatus auf einfach wieder zu setzen. In der Zeit werden virtuelle Computer wieder zurück – es ist keine Benutzeraktion erforderlich.

### <a name="replace-a-failed-drive"></a>Ersetzen eines fehlgeschlagenen Laufwerks

1. Wenn ein Laufwerk ausfällt, wird im **oberen linken Bereich** des **Dashboards**eine Warnung angezeigt.
2. Alternativ können Sie im Navigationsbereich auf der linken Seite die Option **Laufwerke** auswählen oder auf der Kachel in der rechten unteren Ecke auf den Link **VIEW DRIVES >** (LAUFWERKE ANZEIGEN >) klicken, um die Laufwerke zu durchsuchen und sich über deren Status zu informieren. Auf der Registerkarte **Inventar** unterstützt das Raster das Sortieren, gruppieren und Durchsuchen von Schlüsselwörtern.
3. Klicken Sie im **Dashboard**auf die Warnung, um Details wie den physischen Speicherort des Laufwerks anzuzeigen.
4. Weitere Informationen erhalten Sie, indem Sie auf die Verknüpfung **Go to drive** (Zum Laufwerk) klicken, um zur Detailseite **Laufwerk** zu gelangen.
5. Sofern dies von Ihrer Hardware unterstützt wird, können Sie auf **Turn light on/off** (Licht ein-/ausschalten) klicken, um die Kontrollleuchte des Laufwerks zu steuern.
6. Fehlerhafte Laufwerke werden von „Direkte Speicherplätze“ automatisch außer Betrieb genommen und entfernt. In diesem Fall hat das Laufwerk den Status „Zurückgezogen“, und die Leiste für die Speicherkapazität ist leer.
7. Entfernen Sie das fehlerhafte Laufwerk, und installieren Sie ein Ersatzlaufwerk.
8. Das neue Laufwerk wird unter **Laufwerke > Bestand** angezeigt. Im Laufe der Zeit wird die Warnung entfernt, die Volumes werden repariert und kehren zum Status „OK“ zurück, und der Speicher wird mit dem neuen Laufwerk ausgeglichen – alles ganz ohne Benutzeraktion.

### <a name="manage-virtual-networks-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>Verwalten virtueller Netzwerke (SDN-aktivierte HCI-Cluster mithilfe der Windows Admin Center-Vorschau)

1. Wählen Sie **virtuelle Netzwerke** in der Navigation auf der linken Seite aus.
2. Klicken Sie auf **neu** , um ein neues virtuelles Netzwerk und Subnetze zu erstellen, oder wählen Sie ein vorhandenes virtuelles Netzwerk aus, und klicken Sie auf **Einstellungen** , um die Konfiguration
3. Klicken Sie auf ein vorhandenes virtuelles Netzwerk, um VM-Verbindungen mit den Subnetzen des virtuellen Netzwerks und Zugriffs Steuerungs Listen anzuzeigen, die auf Subnetze des virtuellen Netzwerks angewendet werden

![Verwalten virtueller Netzwerke](../media/manage-hyper-converged/manage-virtual-networks.png)

### <a name="connect-a-virtual-machine-to-a-virtual-network-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>Verbinden eines virtuellen Computers mit einem virtuellen Netzwerk (SDN-aktivierte HCI-Cluster mithilfe der Windows Admin Center-Vorschau)

1. Wählen Sie **Virtual Machines** aus der Navigationsleiste auf der linken Seite aus.
2. Wählen Sie einen vorhandenen virtuellen Computer aus, > klicken Sie auf **Einstellungen** > die Registerkarte **Netzwerke** in den **Einstellungen**öffnen.
3. Konfigurieren Sie die Felder **Virtual Network** und **Virtuelles Subnetz** , um den virtuellen Computer mit einem virtuellen Netzwerk zu verbinden.

Sie können das virtuelle Netzwerk auch konfigurieren, wenn Sie einen virtuellen Computer erstellen.

![Verbinden einer virtuellen Maschine mit einem virtuellen Netzwerk](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### <a name="monitor-software-defined-networking-infrastructure-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>Überwachen der Software-Defined Networking-Infrastruktur (SDN-aktivierte HCI-Cluster mithilfe der Windows Admin Center-Vorschau)

1. Wählen Sie im Navigationsbereich auf der linken Seite die Option **Sdn-Überwachung** aus.
2. Zeigen Sie ausführliche Informationen zur Integrität von Netzwerk Controller, Software Load Balancer, Virtual Gateway und Überwachung Ihres virtuellen gatewaypools, der öffentlichen und privaten IP-Pool-Verwendung und des SDN-Host Status an.

![Überwachen der Sdn-Infrastruktur](../media/manage-hyper-converged/sdn-monitoring.png)

## <a name="give-us-feedback"></a>Geben Sie uns Feedback

Ihr Feedback ist alles! Der wichtigste Vorteil von häufigen Updates besteht darin, zu erfahren, was funktioniert und was verbessert werden muss. Im folgenden finden Sie einige Möglichkeiten, uns zu informieren, was Sie denken:

- [Übermitteln und abstimmen von featureanfragen auf UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Besuchen Sie das Forum zum Windows Admin Center in der Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- Tweet zu `@servermgmt`

### <a name="additional-references"></a>Weitere Verweise

- [Windows Admin Center](../overview.md)
- [Direkte Speicherplätze](../../../storage/storage-spaces/storage-spaces-direct-overview.md)
- [Hyper-V](../../../virtualization/hyper-v/hyper-v-on-windows-server.md)
- [Softwaredefiniertes Netzwerk](../../../networking/sdn/software-defined-networking.md)