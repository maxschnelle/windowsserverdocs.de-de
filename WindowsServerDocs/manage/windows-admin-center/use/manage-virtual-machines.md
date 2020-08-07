---
title: Verwalten von Virtual Machines mit dem Windows Admin Center
description: Verwalten von Hyper-V-Hosts und virtuellen Maschinen mit dem Windows Admin Center (Project Honolulu)
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1f3696cc4bd88e401cbbe3a6db83ba5a90cb7049
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962424"
---
# <a name="managing-virtual-machines-with-windows-admin-center"></a>Verwalten von Virtual Machines mit dem Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Das Virtual Machines Tool ist in [Server](manage-servers.md)-, [Failovercluster](manage-failover-clusters.md) -oder [hyperkonvergierten Cluster](manage-hyper-converged.md) Verbindungen verfügbar, wenn die Hyper-V-Rolle auf dem Server oder Cluster aktiviert ist. Mit dem Virtual Machines Tool können Sie Hyper-V-Hosts verwalten, auf denen Windows Server 2012 oder höher ausgeführt wird, die entweder mit Desktop Darstellung oder als Server Core installiert werden. Hyper-V Server 2012, 2016 und 2019 werden ebenfalls unterstützt.

## <a name="key-features"></a>Wichtige Features

Zu den Highlights des Virtual Machines Tools im Windows Admin Center gehören:

- **Übergeordnete Hyper-V-Host Ressourcenüberwachung.** Anzeigen der CPU-und Speicherauslastung insgesamt, e/a-Leistungsmetriken, VM-Integritäts Warnungen und-Ereignisse für den Hyper-V-Host Server oder den gesamten Cluster in einem einzelnen Dashboard
- **Einheitliche Funktionen für die gemeinsame Nutzung von Hyper-V-Manager und Failovercluster-Manager Funktionen.** Zeigen Sie alle virtuellen Computer in einem Cluster an, und führen Sie einen Drilldown zu einem einzelnen virtuellen Computer für die Erweiterte Verwaltung und Problembehandlung durch
- **Vereinfachte, aber leistungsstarke Workflows für die Verwaltung virtueller Computer.** Neue Benutzeroberflächen Umgebungen, die auf IT-Verwaltungs Szenarien zum Erstellen, verwalten und replizieren virtueller Computer zugeschnitten sind.

Im folgenden sind einige der Hyper-V-Aufgaben aufgeführt, die Sie im Windows Admin Center ausführen können:

- [Überwachen von Hyper-V-Host Ressourcen und-Leistung](#monitor-hyper-v-host-resources-and-performance)
- [Inventur der virtuellen Maschine anzeigen](#view-virtual-machine-inventory)
- [Erstellen einer neuen VM](#create-a-new-virtual-machine)
- [Einstellungen für virtuelle Maschinen ändern](#change-virtual-machine-settings)
- [Live Migration einer virtuellen Maschine zu einem anderen Cluster Knoten](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [Erweiterte Verwaltung und Problembehandlung für einen einzelnen virtuellen Computer](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [Verwalten einer virtuellen Maschine über den Hyper-V-Host (VMConnect)](#manage-a-virtual-machine-through-the-hyper-v-host-vmconnect)
- [Ändern der Hyper-V-Host Einstellungen](#change-hyper-v-host-settings)
- [Anzeigen von Hyper-V-Ereignisprotokollen](#view-hyper-v-event-logs)
- [Schützen virtueller Computer mit Azure Site Recovery](#protect-virtual-machines-with-azure-site-recovery)

## <a name="monitor-hyper-v-host-resources-and-performance"></a>Überwachen von Hyper-V-Host Ressourcen und-Leistung

![Virtual Machines Zusammenfassungs Bildschirm](../media/manage-virtual-machines/virtual-machines-summary.png)

1. Klicken Sie im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Es gibt zwei Registerkarten am oberen Rand des **Virtual Machines** Tools, die Registerkarte **Zusammenfassung** und die Registerkarte **Inventur** . Die Registerkarte **Zusammenfassung** bietet eine ganzheitliche Ansicht der Hyper-V-Host Ressourcen und-Leistung für den aktuellen Server oder gesamten Cluster, einschließlich der folgenden:
    - Die Anzahl der VMS, gruppiert nach Status: wird ausgeführt, aus, angehalten und gespeichert
    - Aktuelle Integritäts Warnungen oder Hyper-V-Ereignisprotokoll Ereignisse (Warnungen sind nur für hyperkonvergierte Cluster mit Windows Server 2016 oder höher verfügbar)
    - CPU- und Speicherauslastung mit Aufschlüsselung nach Host und Gast
    - Die größten VMS, die die meisten CPU-und Arbeitsspeicher Ressourcen beanspruchen
    - Live-und Verlaufs Daten Liniendiagramme für IOPS-und e/a-Durchsatz (Speicher Leistungs Liniendiagramme sind nur für hyperkonvergierte Cluster mit Windows Server 2016 oder höher verfügbar. Verlaufs Daten sind nur für hyperkonvergierte Cluster mit Windows Server 2019 verfügbar.)

## <a name="view-virtual-machine-inventory"></a>Inventur der virtuellen Maschine anzeigen

![Virtual Machines Inventur Bildschirm](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. Klicken Sie im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Es gibt zwei Registerkarten am oberen Rand des **Virtual Machines** Tools, die Registerkarte **Zusammenfassung** und die Registerkarte **Inventur** . Auf der Registerkarte **Inventur** werden die auf dem aktuellen Server oder im gesamten Cluster verfügbaren virtuellen Maschinen aufgelistet, und es werden Befehle zum Verwalten einzelner virtueller Maschinen bereitgestellt. Ihre Möglichkeiten:
    - Anzeigen einer Liste der virtuellen Computer, die auf dem aktuellen Server oder Cluster ausgeführt werden.
    - Zeigen Sie den Zustand und den Host Server des virtuellen Computers an, wenn Sie virtuelle Computer für einen Cluster anzeigen. Sehen Sie sich auch die CPU-und Speicherauslastung aus der Host Perspektive an, einschließlich Arbeitsspeicher Auslastung, Speicherbedarf und zugewiesenem Arbeitsspeicher sowie die Betriebszeit des virtuellen Computers, den Takt Status und den Schutzstatus mithilfe Azure Site Recovery.
    - [Erstellen Sie einen neuen virtuellen Computer](#create-a-new-virtual-machine).
    - Löschen, starten, ausschalten, Herunterfahren, anhalten, fortsetzen, zurücksetzen oder Umbenennen eines virtuellen Computers. Speichern Sie auch den virtuellen Computer, löschen Sie einen gespeicherten Zustand, oder erstellen Sie einen Prüfpunkt.
    - [Ändern Sie die Einstellungen für einen virtuellen Computer](#change-virtual-machine-settings).
    - Stellen Sie mithilfe von VMConnect über den Hyper-V-Host eine Verbindung mit einer Konsole für virtuelle Maschinen her.
    - [Replizieren Sie einen virtuellen Computer mit Azure Site Recovery](#protect-virtual-machines-with-azure-site-recovery).
    - Für Vorgänge, die auf mehreren VMS ausgeführt werden können, z. b. starten, Herunterfahren, speichern, anhalten, löschen, zurücksetzen, können Sie mehrere VMS auswählen und den Vorgang gleichzeitig ausführen.

Hinweis: Wenn Sie mit einem Cluster verbunden sind, zeigt das Tool für virtuelle Maschinen nur gruppierte virtuelle Maschinen an. Wir planen auch, nicht gruppierte virtuelle Computer in Zukunft anzuzeigen.

## <a name="create-a-new-virtual-machine"></a>Erstellen einer neuen VM

![Bildschirm zum Erstellen eines neuen virtuellen Computers](../media/manage-virtual-machines/new-vm.png)

1. Klicken Sie im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Wählen Sie am oberen Rand des Virtual Machines Tools die Registerkarte **Inventur** aus, und klicken Sie dann auf **neu** , um einen neuen virtuellen Computer zu erstellen.
3. Geben Sie den Namen des virtuellen Computers ein, und wählen Sie zwischen virtuellen Computern der Generation 1 und 2.
4. Wenn Sie einen virtuellen Computer in einem Cluster erstellen, können Sie den Host auswählen, auf dem die virtuelle Maschine zunächst erstellt werden soll. Wenn Sie Windows Server 2016 oder höher ausführen, stellt das Tool eine Host Empfehlung für Sie bereit.
5. Wählen Sie einen Pfad für die Dateien der virtuellen Maschine aus. Wählen Sie ein Volume aus der Dropdown Liste aus, oder klicken Sie auf **Durchsuchen** , um einen Ordner mithilfe der Ordner Auswahl auszuwählen. Die Konfigurationsdateien und virtuellen Festplatten Dateien der virtuellen Maschine werden in einem einzelnen Ordner unter dem `\Hyper-V\\[virtual machine name]` Pfad des ausgewählten Volumes oder Pfads gespeichert.

   >[!Tip]
   > Sie können in der Ordner Auswahl eine beliebige verfügbare SMB-Freigabe im Netzwerk durchsuchen, indem Sie den Pfad im Feld **Ordnername** als eingeben ```\\server\share``` . Die Verwendung einer Netzwerkfreigabe für den VM-Speicher erfordert " [kredssp](../understand/faq.md#does-windows-admin-center-use-credssp)".

6. Wählen Sie die Anzahl der virtuellen Prozessoren aus, egal ob Sie die aktivierte aktivierte Virtualisierung aktivieren möchten, konfigurieren Sie Arbeitsspeicher Einstellungen, Netzwerkadapter und virtuelle Festplatten, und wählen Sie aus, ob Sie ein Betriebssystem aus einer ISO-Abbild Datei oder aus dem Netzwerk installieren möchten.
7. Klicken Sie auf **Erstellen**, um die virtuelle Maschine zu erstellen.
8. Nachdem der virtuelle Computer erstellt und in der Liste der virtuellen Computer angezeigt wird, können Sie den virtuellen Computer starten.
9. Nachdem der virtuelle Computer gestartet wurde, können Sie über VMConnect eine Verbindung mit der Konsole des virtuellen Computers herstellen, um das Betriebssystem zu installieren. Wählen Sie den virtuellen Computer aus der Liste aus, klicken Sie auf **Weitere**  >  **Verbindung** , um die RDP-Datei herunterzuladen. Öffnen Sie die RDP-Datei in der Remotedesktopverbindung-app. Da diese Verbindung mit der Konsole des virtuellen Computers hergestellt wird, müssen Sie die Administrator Anmelde Informationen für den Hyper-V-Host eingeben.

## <a name="change-virtual-machine-settings"></a>Einstellungen für virtuelle Maschinen ändern

![Bildschirm für Einstellungen der virtuellen Maschine](../media/manage-virtual-machines/vm-settings.png)

1. Klicken Sie im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Wählen Sie am oberen Rand des Virtual Machines Tools die Registerkarte **Inventur** aus. Wählen Sie einen virtuellen Computer aus der Liste aus, und klicken Sie auf **Weitere**  >  **Einstellungen**.
3. Wechseln Sie zwischen den Registerkarten **Allgemein**, **Sicherheit**, Arbeits **Speicher**, **Prozessoren** **, Daten**Träger, **Netzwerke**, **Start Auftrag** und **Prüfpunkte** , konfigurieren Sie die erforderlichen Einstellungen, und klicken Sie dann auf **Speichern** , um die Einstellungen der aktuellen Registerkarte zu speichern. Welche Einstellungen verfügbar sind, hängt von der Generation des virtuellen Computers ab. Außerdem können einige Einstellungen für die Ausführung virtueller Maschinen nicht geändert werden, und Sie müssen den virtuellen Computer zuerst abbrechen.

## <a name="live-migrate-a-virtual-machine-to-another-cluster-node"></a>Live Migration einer virtuellen Maschine zu einem anderen Cluster Knoten

Wenn Sie eine Verbindung mit einem Cluster hergestellt haben, können Sie eine virtuelle Maschine Live zu einem anderen Cluster Knoten migrieren.

1. Klicken Sie in einem Failovercluster oder einer hyperkonvergierten Cluster Verbindung im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Wählen Sie am oberen Rand des Virtual Machines Tools die Registerkarte **Inventur** aus. Wählen Sie einen virtuellen Computer aus der Liste aus, und klicken Sie auf **Weitere**  >  **verschieben**.
3. Wählen Sie einen Server aus der Liste der verfügbaren Cluster Knoten aus, und klicken Sie auf **verschieben**.
4. Benachrichtigungen für den Verschiebungs Fortschritt werden in der oberen rechten Ecke des Windows Admin Centers angezeigt. Wenn die Verschiebung erfolgreich ist, wird der Name des Host Servers in der Liste der virtuellen Computer geändert.

## <a name="advanced-management-and-troubleshooting-for-a-single-virtual-machine"></a>Erweiterte Verwaltung und Problembehandlung für einen einzelnen virtuellen Computer

![Detailbildschirm für einen einzelnen virtuellen Computer](../media/manage-virtual-machines/vm-details.png)

Auf der Seite einzelner virtueller Computer können Sie detaillierte Informationen und Leistungsdiagramme für einen einzelnen virtuellen Computer anzeigen.

1. Klicken Sie im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Wählen Sie am oberen Rand des Virtual Machines Tools die Registerkarte **Inventur** aus. Klicken Sie auf den Namen eines virtuellen Computers aus der Liste der virtuellen Computer.
3. Auf der Seite einzelner virtueller Computer können Sie folgende Aktionen ausführen:
    - Ausführliche Informationen zum virtuellen Computer anzeigen.
    - Anzeigen von Live-und Verlaufs Daten Linien Diagrammen für CPU, Arbeitsspeicher, Netzwerk, IOPS und e/a-Durchsatz (Verlaufs Daten sind nur für hyperkonvergierte Cluster unter Windows Server 2019 verfügbar)
    - Anzeigen, erstellen, anwenden, umbenennen und Löschen von Prüfpunkten.
    - Anzeigen von Details für die virtuellen Festplatten Dateien (VHD-Dateien) der virtuellen Maschine, Netzwerkadapter und Host Server.
    - Löschen, starten, ausschalten, Herunterfahren, anhalten, fortsetzen, zurücksetzen oder Umbenennen des virtuellen Computers. Speichern Sie auch den virtuellen Computer, löschen Sie einen gespeicherten Zustand, oder erstellen Sie einen Prüfpunkt.
    - [Ändern Sie die Einstellungen für die virtuelle Maschine](#change-virtual-machine-settings).
    - Stellen Sie mithilfe von VMConnect über den Hyper-V-Host eine Verbindung mit der Konsole für virtuelle Maschinen her.
    - [Replizieren Sie den virtuellen Computer mit Azure Site Recovery](#protect-virtual-machines-with-azure-site-recovery).

## <a name="manage-a-virtual-machine-through-the-hyper-v-host-vmconnect"></a>Verwalten einer virtuellen Maschine über den Hyper-V-Host (VMConnect)

![VM-Verbindung über Ihren Webbrowser](../media/manage-virtual-machines/vm-connect.png)

1. Klicken Sie im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Wählen Sie am oberen Rand des Virtual Machines Tools die Registerkarte **Inventur** aus. Wählen Sie einen virtuellen Computer aus der Liste aus, und klicken Sie auf **Weitere**  >  **Verbindung herstellen** oder **RDP-Datei herunterladen**. **Connect** ermöglicht Ihnen die Interaktion mit der Gast-VM über die Remotedesktop Webkonsole, die in Windows Admin Center integriert ist. **RDP-Datei herunterladen** lädt eine RDP-Datei herunter, die Sie mit der Remotedesktopverbindung Anwendung (mstsc.exe) öffnen können. Bei beiden Optionen wird VMConnect verwendet, um eine Verbindung mit dem virtuellen Gastcomputer über den Hyper-v-Host herzustellen, und Sie müssen die Administrator Anmelde Informationen für den Hyper-v-Host Server eingeben.

## <a name="change-hyper-v-host-settings"></a>Ändern der Hyper-V-Host Einstellungen

![Bildschirm für Hyper-V-Host Einstellungen](../media/manage-virtual-machines/host-settings.png)

1. Klicken Sie auf einem Server, einem hyperkonvergenten Cluster oder einer failoverclusterverbindung auf das **Einstellungs** Menü unten im Navigationsbereich auf der linken Seite.
2. Auf einem Hyper-v-Host Server oder-Cluster wird eine **Hyper-v-Host Einstellungs** Gruppe mit den folgenden Abschnitten angezeigt:
    - Allgemein: Ändern von virtuellen Festplatten und virtuellen Computern Dateipfad und Typ des hypervisorzeitplans (falls unterstützt)
    - Erweiterter Sitzungsmodus
    - NUMA-Aufteilung
    - Livemigration
    - Speicher Migration
3. Wenn Sie Änderungen an Hyper-V-Host Einstellungen in einem hyperkonvergierten Cluster oder einer failoverclusterverbindung vornehmen, wird die Änderung auf alle Cluster Knoten angewendet.

## <a name="view-hyper-v-event-logs"></a>Anzeigen von Hyper-V-Ereignisprotokollen

Sie können die Hyper-V-Ereignisprotokolle direkt über das Virtual Machines Tool anzeigen.

1. Klicken Sie im Navigationsbereich auf der linken Seite auf das **Virtual Machines** Tool.
2. Wählen Sie am oberen Rand des Virtual Machines Tools die Registerkarte **Zusammenfassung** aus. Klicken Sie im Abschnitt Top Right Events auf **alle Ereignisse anzeigen**.
3. Das Ereignisanzeige Tool zeigt die Hyper-V-Ereignis Kanäle im linken Bereich an. Wählen Sie einen Kanal aus, um die Ereignisse im rechten Bereich anzuzeigen. Wenn Sie einen Failovercluster oder einen hyperkonvergenten Cluster verwalten, werden in den Ereignisprotokollen Ereignisse für alle Cluster Knoten angezeigt, und der Host Server wird in der Spalte Computer angezeigt.

## <a name="protect-virtual-machines-with-azure-site-recovery"></a>Schützen virtueller Computer mit Azure Site Recovery

Sie können das Windows Admin Center verwenden, um Azure Site Recovery zu konfigurieren und ihre lokalen virtuellen Computer in Azure zu replizieren. [Weitere Informationen](../azure/azure-site-recovery.md)

## <a name="more-coming"></a>Weitere Informationen

Die Verwaltung virtueller Computer im Windows Admin Center befindet sich aktiv in der Entwicklungsphase, und in naher Zukunft werden neue Funktionen hinzugefügt. Sie können den Status anzeigen und die Features in UserVoice abstimmen:

- [Importieren/Exportieren von virtuellen Computern](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)
- [Virtuelle Maschinen in Ordnern sortieren](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)
- [Zusätzliche Einstellungen für virtuelle Computer unterstützen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)
- [Hyper-V-Replikat Unterstützung](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)
- [Delegieren des Besitzes der virtuellen Maschine](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)
- [Virtuellen Computer klonen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)
- [Erstellen einer Vorlage aus einer vorhandenen virtuellen Maschine](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)
- [Anzeigen von virtuellen Maschinen auf Hyper-V-Hosts](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)
- [VLAN im Bereich "neuer virtueller Computer" Konfigurieren](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)

[Alle anzeigen oder neue Features vorschlagen](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D).
