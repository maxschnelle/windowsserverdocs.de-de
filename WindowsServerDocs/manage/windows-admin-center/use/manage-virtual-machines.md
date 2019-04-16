---
title: Verwalten von virtuellen Computern mit Windows Admin Center
description: Verwalten von Hyper-V-Hosts und virtuelle Computer mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 374ee30dcbaf9af3caa60ee85ec59fd3c158206b
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296752"
---
# Verwalten von virtuellen Computern mit Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Das Tool virtuelle Computer ist in [Server](manage-servers.md), [Failovercluster](manage-failover-clusters.md) oder [Hyper-converged Cluster](manage-hyper-converged.md) -Verbindungen verfügbar, wenn die Hyper-V-Rolle auf dem Server oder Cluster aktiviert ist. Können die virtuellen Computer-Tool zum Verwalten von Hyper-V-Hosts mit Windows Server 2012 oder höher, können entweder mit Desktop Experience oder als Server Core installiert. Hyper-V Server 2012, 2016 und 2019 werden ebenfalls unterstützt.

## Wichtige Funktionen

Der virtuelle Computer-Tool im Windows Admin Center bietet folgende Vorteile:

- **Allgemeine Hyper-V-Host Überwachung von Ressourcen.** Allgemeine CPU-und speicherauslastung, e/a-Leistungsmetriken, VM Health Warnungen und Ereignisse für die Hyper-V-Hostserver oder den gesamten Cluster in einem einzelnen Dashboard anzeigen.
- **Einheitliche Erfahrung Portieren von Hyper-V-Manager und Failovercluster-Manager-Funktionen zusammen.** Anzeigen aller virtuellen Computer auf einem Cluster und Drilldown in einen einzelnen virtuellen Computer für die erweiterte Verwaltung und Problembehandlung.
- **Vereinfachte noch einmal, aber leistungsstarke Workflows für die Verwaltung der virtuellen Computer.** Neue UI-Erlebnisse speziell für IT-Verwaltungsszenarien erstellen, verwalten und virtuelle Computer replizieren.

Hier sind einige der Hyper-V-Aufgaben, die Sie im Windows Admin Center ausführen können:

- [Überwachen von Hyper-V-Host-Ressourcen und Leistung](#monitor-hyper-v-host-resources-and-performance)
- [Ansicht Virtual Machine Inventar](#view-virtual-machine-inventory)
- [Erstellen eines neuen virtuellen Computers](#create-a-new-virtual-machine)
- [Ändern der Einstellungen des virtuellen Computers](#change-virtual-machine-settings)
- [Livemigration eines virtuellen Computers auf einen anderen Clusterknoten](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [Erweiterte Verwaltung und Problembehandlung für einen einzelnen virtuellen Computer](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [Verwalten von einem virtuellen Computer über den Hyper-V-Host (VMConnect)](#manage-a-virtual-machine-through-the-hyper-v-host-vmconnect)
- [Hyper-V-Host-Einstellungen ändern](#change-hyper-v-host-settings)
- [Hyper-V-Ereignisprotokolle anzeigen](#view-hyper-v-event-logs)
- [Virtuelle Maschinen mit Azure Site Recovery schützen](#protect-virtual-machines-with-azure-site-recovery)

## Überwachen von Hyper-V-Host-Ressourcen und Leistung

![Virtuelle Computer Zusammenfassung Bildschirm](../media/manage-virtual-machines/virtual-machines-summary.png)

1. Klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Es gibt zwei Registerkarten am oberen Rand den **virtuellen Computern** , die Registerkarte " **Zusammenfassung** " und das **Inventar** -Register. Die Registerkarte " **Zusammenfassung** " bietet eine umfassende Ansicht der Hyper-V-Host-Ressourcen und Leistung für den aktuellen Server oder den gesamten Cluster, einschließlich der folgenden:
    - Die Anzahl von VMs gruppiert nach dem Zustand - ausgeführt, deaktiviert, angehalten und gespeichert
    - Aktuelle integritätswarnungen oder Hyper-V-Ereignisprotokoll-Ereignisse (Warnungen sind nur verfügbar für zusammengeführte Cluster mit Windows Server 2016 oder höher)
    - Nutzung von CPU und Arbeitsspeicher mit Aufschlüsselung der Host und Gast
    - Nutzung der CPU- und Ressourcen mit den meisten Top-VMs
    - Live und Protokolldaten Zeile Diagramme für IOPS und e/a-Durchsatz (Speicher Leistungsdiagramme Zeile sind nur verfügbar für zusammengeführte Cluster mit Windows Server 2016 oder höher. Verlaufsdaten ist nur verfügbar für zusammengeführte Cluster, die unter Windows Server 2019)

## Ansicht Virtual Machine Inventar

![Virtuelle Computer Bestandsliste](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. Klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Es gibt zwei Registerkarten am oberen Rand den **virtuellen Computern** , die Registerkarte " **Zusammenfassung** " und das **Inventar** -Register. Das **Inventar** -Register enthält die virtuellen Computer auf den aktuellen Server oder die gesamten Cluster verfügbar und enthält Befehle zum Verwalten der einzelnen virtuellen Computern. Sie haben folgende Möglichkeiten:
    - Anzeigen einer Liste der virtuellen Computer auf den aktuellen Server oder Cluster ausführen.
    - Anzeigen des virtuellen Computers Zustand und die Host-Server, wenn Sie virtuelle Computer für einen Cluster anzeigen. Auch die zeigen Sie Nutzung von CPU und Arbeitsspeicher aus der Perspektive des Servers, einschließlich genügend Arbeitsspeicher zur Verfügung, Speicherbedarf und zugewiesenen Arbeitsspeichers und des virtuellen Computers Betriebszeit, Heartbeat-Status und mithilfe von Azure Site Recovery Schutzstatus an.
    - [Erstellen eines neuen virtuellen Computers](#create-a-new-virtual-machine).
    - Löschen, starten, deaktivieren, Herunterfahren, anhalten, fortsetzen, zurücksetzen oder Umbenennen eines virtuellen Computers. Auch speichern Sie der virtuelle Computer zu, löschen Sie einen gespeicherten Zustand oder erstellen Sie einen Prüfpunkt.
    - [Änderung der Einstellungen für einen virtuellen Computer](#change-virtual-machine-settings).
    - Verbinden Sie mit einem virtuellen Computer-Konsole, die mit VMConnect über Hyper-V-Host.
    - [Replizieren von einem virtuellen Computer mithilfe von Azure Site Recovery](#protect-virtual-machines-with-azure-site-recovery).
    - Für Vorgänge, die auf mehrere virtuelle Computer, z. B. Start, Herunterfahren, speichern, Pause, ausgeführt werden können können löschen, zurücksetzen, Sie wählen Sie mehrere virtuelle Computer und führen Sie den Vorgang auf einmal.

Hinweis: Wenn Sie zu einem Cluster verbunden sind, virtuelle Computer zeigt das Tool nur gruppierte virtuelle Computer. Wir planen, auch nicht gruppierte virtuelle Computer in der Zukunft angezeigt.

## Erstellen eines neuen virtuellen Computers

![Erstellen von neuen virtuellen Computer-Bildschirm](../media/manage-virtual-machines/new-vm.png)

1. Klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Am oberen Rand der virtuelle Computer-Tool wählen Sie die Registerkarte " **Inventar** ", und klicken Sie dann **neu** , um einen neuen virtuellen Computer zu erstellen.
3. Geben Sie den virtuellen Computer ein, und wählen Sie zwischen virtuelle Computer der Generation 1 und 2.
4. Wenn Sie einen virtuellen Computer auf einem Cluster erstellen, können Sie welche Host des virtuellen Computers anfänglich auf zu erstellen. Wenn Sie WindowsServer 2016 oder höher ausführen, wird das Tool eine Host-Empfehlung für Sie bereitstellen.
5. Wählen Sie einen Pfad für die Dateien des virtuellen Computers. Wählen Sie ein Volume aus der Dropdown-Liste, oder klicken Sie auf **Durchsuchen** , um einen Ordner mit der Ordnerauswahl auszuwählen. Die VM-Konfigurationsdateien und die virtuelle Festplatte in einen einzelnen Ordner unter gespeichert werden die `\Hyper-V\\[virtual machine name]` Pfad des ausgewählten Datenträgers oder Pfad.

>[!Tip]
> In der Ordnerauswahl können Sie suchen alle verfügbaren SMB-Freigabe auf das Netzwerk durch den Pfad im Feld **Ordnername** als Eingabe ```\\server\share```. Verwendung von einer Netzwerkfreigabe für VM-Speicher erfordern [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp).

6. Wählen Sie die Anzahl der virtuellen Prozessoren, ob Sie die geschachtelte Virtualisierung aktiviert werden soll, Arbeitsspeicher-Einstellungen, Netzwerkadapter, virtuelle Festplatten konfigurieren und auswählen, ob Sie ein Betriebssystem aus einer Bilddatei ISO- oder über das Netzwerk installieren möchten.
7. Klicken Sie auf **Erstellen** , um den virtuellen Computer zu erstellen.
8. Sobald der virtuelle Computer erstellt wird und in der Liste der virtuellen Computer angezeigt, können Sie den virtuellen Computer starten.
9. Sobald der virtuelle Computer gestartet wird, können Sie mit des virtuellen Computers Konsole über VMConnect auf die Installation des Betriebssystems verbinden. Wählen Sie den virtuellen Computer aus der Liste aus, klicken Sie auf **Weitere** > **Verbinden** , um die RDP-Datei herunterzuladen. Öffnen Sie die RDP-Datei, in der Remotedesktopverbindung-app. Da dies mit des virtuellen Computers-Konsole verbunden ist, müssen Sie den Hyper-V-Host-Administrator-Anmeldeinformationen eingeben.

## Ändern der Einstellungen des virtuellen Computers

![Die Einstellungen des virtuellen Computers](../media/manage-virtual-machines/vm-settings.png)

1. Klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Wählen Sie am oberen Rand der virtuelle Computer-Tool, das **Inventar** Registerkarte wählen einen virtuellen Computer aus der Liste, und klicken Sie auf **Weitere** > **Einstellungen**.
3. Wechseln Sie zwischen der Registerkarte " **Allgemein**, **Sicherheit**, **Speicher**, **Prozessoren**, **Datenträger**, **Netzwerke**, **Startreihenfolge** und **Prüfpunkte** ", konfigurieren Sie die erforderlichen Einstellungen, und klicken Sie dann zum Speichern **Speichern** Einstellungen für die aktuelle Registerkarte. Die verfügbaren Einstellungen variiert je nach der Generation des virtuellen Computers. Außerdem einige Einstellungen können nicht geändert werden, für die Ausführung von virtuellen Computern und müssen Sie zuerst den virtuellen Computer zu beenden.

## Livemigration eines virtuellen Computers auf einen anderen Clusterknoten

Wenn Sie mit einem Cluster verbunden sind, können Sie einen virtuellen Computer auf einen anderen Clusterknoten live migrieren.

1. Ein Failovercluster oder zusammengeführte Cluster-Verbindung klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Wählen Sie am oberen Rand der virtuelle Computer-Tool, das **Inventar** Registerkarte wählen einen virtuellen Computer aus der Liste, und klicken Sie auf **Weitere** > **Verschieben**.
3. Wählen Sie einen Server aus der Liste der verfügbaren Clusterknoten, und klicken Sie auf **Verschieben**.
4. Benachrichtigungen für den Wechsel Fortschritt werden in der oberen rechten Ecke von Windows Admin Center angezeigt. Wenn der Vorgang erfolgreich ausgeführt wurde, sehen Sie den Server-Hostnamen, die in der Liste der virtuellen Computer nicht geändert.

## Erweiterte Verwaltung und Problembehandlung für einen einzelnen virtuellen Computer

![Einzelner virtueller Computer Detailbildschirm](../media/manage-virtual-machines/vm-details.png)

Sie können ausführliche Informationen und Leistungsdiagramme für einen einzelnen virtuellen Computer aus der einzelnen virtuellen Computer-Seite anzeigen.

1. Klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Wählen Sie am oberen Rand der virtuelle Computer-Tool das **Inventar** Registerkarte auf den Namen eines virtuellen Computers aus der Liste der virtuellen Computer.
3. Von der Seite der einzelnen virtuellen Computer können Sie folgende Aktionen ausführen:
    - Zeigen Sie detaillierte Informationen für den virtuellen Computer.
    - Anzeigen von Live- und Verlaufsdaten Zeile Diagramme für CPU, Arbeitsspeicher, Netzwerk, IOPS und e/a-Durchsatz (Verlaufsdaten ist nur verfügbar für zusammengeführte Cluster, die unter Windows Server 2019)
    - Anzeigen, erstellen, anwenden, umbenennen und Löschen von Prüfpunkten.
    - Hier werden Details des virtuellen Computers virtuelle Festplatte (VHD)-Dateien, Netzwerkadapter und Host-Server.
    - Löschen Sie, starten Sie, deaktivieren Sie, Herunterfahren Sie, halten Sie an, fortsetzen Sie, Zurücksetzen Sie oder benennen Sie den virtuellen Computer. Auch speichern Sie der virtuelle Computer zu, löschen Sie einen gespeicherten Zustand oder erstellen Sie einen Prüfpunkt.
    - [Änderung der Einstellungen für den virtuellen Computer](#change-virtual-machine-settings).
    - Verbinden Sie mit der VM-Konsole mithilfe von VMConnect über Hyper-V-Host.
    - [Replizieren Sie den virtuellen Computer mithilfe von Azure Site Recovery](#protect-virtual-machines-with-azure-site-recovery).

## Verwalten von einem virtuellen Computer über den Hyper-V-Host (VMConnect)

![Virtuellen Computer eine Verbindung herstellen über Ihren Webbrowser](../media/manage-virtual-machines/vm-connect.png)

1. Klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Wählen Sie am oberen Rand der virtuelle Computer-Tool, das **Inventar** Registerkarte wählen einen virtuellen Computer aus der Liste, und klicken Sie auf **Weitere** > **Connect** oder **herunterladen RDP-Datei**. **Connect** ermöglichen die Interaktion mit dem Gast-VM über der Remotedesktop-Web-Konsole Windows Admin Center integriert. **Herunterladen von RDP-Datei** wird eine RDP-Datei herunterladen, die Sie mit der Remotedesktopverbindung-Anwendung (mstsc.exe) öffnen können. Beide Optionen für die Verbindung an den Gast-VM über den Hyper-V-Host VMConnect verwenden und erfordert, dass Sie Administratoranmeldeinformationen für den Hyper-V-Host-Server eingeben.

## Hyper-V-Host-Einstellungen ändern

![Bildschirm "Einstellungen" Hyper-V-host](../media/manage-virtual-machines/host-settings.png)

1. Klicken Sie auf eine Verbindung zum Server, zusammengeführte Cluster oder Failovercluster **Einstellungsmenü am unteren Rand des Navigationsbereichs der linken Seite** aus.
2. Auf einem Hyper-V-Hostserver oder Cluster sehen Sie eine Gruppe **Hyper-V-Host-Einstellungsdatei** mit den folgenden Abschnitten:
    - Allgemeine: Änderung virtuelle Festplatten und virtuelle Computer Dateipfad und Hypervisor planen Typ (falls unterstützt)
    - Erweiterte Sitzungsmodus
    - NUMA Speicherbus
    - Live-Migration
    - Speichermigration
3. Wenn Sie alle einstellungsänderungen in einer Verbindung zusammengeführte Cluster oder Failovercluster Hyper-V-Host vornehmen, wird die Änderung auf alle Clusterknoten angewendet werden.

## Hyper-V-Ereignisprotokolle anzeigen

Sie können Hyper-V-Ereignisprotokolle direkt über das Tool virtuelle Computer anzeigen.

1. Klicken Sie auf das Tool **virtuelle Computer** im Navigationsbereich mit der linken Seite.
2. Am oberen Rand der virtuelle Computer-Tool wählen Sie die Registerkarte " **Zusammenfassung** ". Klicken Sie im oberen rechten Abschnitt Ereignisse auf **Alle Ereignisse anzeigen**.
3. Das Tool Ereignisanzeige wird die Hyper-V-Ereignis Kanäle im linken Bereich angezeigt. Wählen Sie einen Kanal für die Ereignisse im rechten Bereich anzuzeigen. Wenn Sie einen Failovercluster oder zusammengeführte Cluster verwalten, wird die Ereignisprotokolle Ereignisse für alle Clusterknoten, Anzeigen von des Hostservers in der Spalte "Computer" angezeigt.

## Virtuelle Maschinen mit Azure Site Recovery schützen

Sie können Windows Admin Center verwenden, Konfigurieren von Azure Site Recovery und Ihre lokale virtuellen Computer in Azure replizieren. [Weitere Informationen](../azure/azure-site-recovery.md)

## Weitere kommen

Verwaltung virtueller Computer in Windows Admin Center ist aktiv in der Entwicklung, und neue Features in naher Zukunft hinzugefügt werden. Sie können den Status und die Zustimmung zum Features in UserVoice anzeigen:

|Feature-Anforderung|
|-------|
|[Virtuelle Computer importieren/exportieren](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)|
|[Sortieren von virtuellen Computern in Ordnern](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)|
|[Unterstützung für zusätzliche virtuelle Computer Einstellungen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)|
|[Unterstützung für Hyper-V-Replikat](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)|
|[Delegieren des virtuellen Computers den Besitz](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)|
|[Klonen des virtuellen Computers](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)|
|[Erstellen Sie eine Vorlage aus einem vorhandenen virtuellen Computer](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)|
|[Anzeigen von virtuellen Computern auf Hyper-V-hosts](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)|
|[Konfigurieren von VLAN im Bereich des neuen virtuellen Computer](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)|
|[**Alle oder neues Feature vorschlagen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D)|
