---
title: Verwalten von virtuellen Computern mit Windows Admin Center
description: Verwalten von Hyper-V-Hosts und virtuellen Computern mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 41767b9e53c0106931e78f86f8675e413cca0d0a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816881"
---
# <a name="managing-virtual-machines-with-windows-admin-center"></a>Verwalten von virtuellen Computern mit Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Das Tool für die virtuellen Computer steht in [Server](manage-servers.md), [Failovercluster](manage-failover-clusters.md) oder [Hyper-Converged Cluster](manage-hyper-converged.md) Verbindungen, wenn die Hyper-V-Rolle auf dem Server oder Cluster aktiviert ist. Sie können das Tool für die virtuellen Computer verwenden, zum Verwalten von Hyper-V-Hosts unter Windows Server 2012 oder höher, entweder mit Desktopdarstellung oder als Server Core installiert. Hyper-V Server 2012 und 2016 werden ebenfalls unterstützt.

## <a name="key-features"></a>Hauptmerkmale

Der virtuelle Computer-Tool in Windows Admin Center bietet folgende Vorteile:

- **Allgemeine Hyper-V-Host Ressourcen überwachen.** Anzeigen von allgemeinen CPU-und speicherauslastung, e/a-Leistungsmetriken, VM-Health-Warnungen und Ereignisse für die Hyper-V-Hostserver oder im gesamten Cluster in einem einzelnen Dashboard.
- **Einheitliche Funktionen für Hyper-V-Manager und Failovercluster-Manager-Funktionen vereinen.** Zeigen Sie alle virtuellen Computer in einem Cluster und einen Drilldown in einem einzelnen virtuellen Computer für die erweiterte Verwaltung und Problembehandlung.
- **Vereinfachte, aber leistungsfähiges-Workflows für die Verwaltung virtueller Computer.** Neue Benutzeroberflächen, die auf IT-Verwaltung-Szenarios zu erstellen, verwalten und Replizieren von virtuellen Computern zugeschnitten sind.

Hier sind einige der Hyper-V-Aufgaben, die Sie in Windows Admin Center ausführen können:

- [Hyper-V-Host-Ressourcen und Leistung überwachen](#monitor-hyper-v-host-resources-and-performance)
- [Die virtuellen Computer Bestand anzeigen](#view-virtual-machine-inventory)
- [Erstellen eines neuen virtuellen Computers](#create-a-new-virtual-machine)
- [Ändern der Einstellungen des virtuellen Computers](#change-virtual-machine-settings)
- [Die Livemigration eines virtuellen Computers auf einen anderen Clusterknoten](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [Erweiterte Verwaltung und Problembehandlung für ein einzelner virtueller Computer](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [Hyper-V-Ereignisprotokolle anzeigen](#view-hyper-v-event-logs)
- [Schützen Sie virtueller Computer mit Azure Site Recovery](#protect-virtual-machines-with-azure-site-recovery)

## <a name="monitor-hyper-v-host-resources-and-performance"></a>Hyper-V-Host-Ressourcen und Leistung überwachen

![Übersichtsbildschirm für den virtuellen Computer](../media/manage-virtual-machines/virtual-machines-summary.png)

1. Klicken Sie auf die **VMs** Tool im Navigationsbereich mit der linken Seite.
2. Befinden sich zwei Registerkarten am oberen Rand der **virtuelle Computer** -Tool die **Zusammenfassung** Registerkarte und der **Inventur** Registerkarte. Die **Zusammenfassung** Registerkarte bietet eine Übersicht über Hyper-V-Host-Ressourcen und Leistung für den aktuellen Server oder den gesamten Cluster, einschließlich der folgenden:
    - Die Anzahl von VMs, gruppiert nach Zustand - ausgeführt wird, deaktiviert, angehalten und gespeichert
    - Aktuelle Health-Warnungen oder Hyper-V-Ereignisprotokoll-Ereignisse (Warnungen sind nur für den hyperkonvergenten Cluster unter Windows Server 2016 oder höher verfügbar)
    - Auslastung von CPU und Arbeitsspeicher mit Host und Gast Aufschlüsselung
    - Nutzen die CPU- und Speicherressourcen Top-VMs
    - Live- und historische Daten Liniendiagramme für den IOPS- und e/a-Durchsatz (Storage Performance Liniendiagramme sind nur für den hyperkonvergenten Cluster unter Windows Server 2016 oder höher verfügbar. Historische Daten ist nur für hyper-konvergiert für Cluster unter Windows Server-2019 verfügbar)

## <a name="view-virtual-machine-inventory"></a>Die virtuellen Computer Bestand anzeigen

![Bildschirm der Inventur von virtuellen Computern](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. Klicken Sie auf die **VMs** Tool im Navigationsbereich mit der linken Seite.
2. Befinden sich zwei Registerkarten am oberen Rand der **virtuelle Computer** -Tool die **Zusammenfassung** Registerkarte und der **Inventur** Registerkarte. Die **Inventur** Registerkarte enthält Befehle zum Verwalten einzelnen virtueller Computer und führt die virtuellen Maschinen auf dem aktuellen Server oder den gesamten Cluster zur Verfügung. Sie haben folgende Möglichkeiten:
    - Anzeigen einer Liste der virtuellen Computer auf dem aktuellen Server oder Cluster ausgeführt wird.
    - Anzeigen der VM Status und die Host-Server an, wenn Sie virtuelle Computer für einen Cluster anzeigen. Auch zeigen Sie an, Auslastung von CPU und Arbeitsspeicher aus der Perspektive des Servers, einschließlich arbeitsspeicherauslastung, Speicherbedarf und zugewiesenen Speichers und des virtuellen Computers Betriebszeit, Heartbeat-Status und Schutzstatus mit Azure Site Recovery.
    - [Erstellen eines neues virtuellen Computers](#create-a-new-virtual-machine).
    - Löschen, starten, deaktivieren, Herunterfahren, anhalten, fortsetzen, zurückgesetzt oder Umbenennen eines virtuellen Computers. Auch speichern Sie der virtuelle Computer zu, löschen Sie einen gespeicherten Zustand oder erstellen Sie einen Prüfpunkt.
    - [Ändern der Einstellungen für eine virtuelle Maschine](#change-virtual-machine-settings).
    - Verbinden Sie mit einer Konsole für virtuelle Computer unter Verwendung von VMConnect über Hyper-V-Hosts.
    - [Replikation eines virtuellen Computers mit Azure Site Recovery](#protect-virtual-machines-with-azure-site-recovery).

HINWEIS: Wenn Sie in einem Cluster verbunden sind, zeigt das Tool für die virtuellen Computer nur virtuelle Clustercomputer. Wir planen, auch nicht gruppierte virtuelle Computer in der Zukunft angezeigt.

## <a name="create-a-new-virtual-machine"></a>Erstellen eines neuen virtuellen Computers

![Bildschirm für neue virtuelle Maschine erstellen](../media/manage-virtual-machines/new-vm.png)

1. Klicken Sie auf die **VMs** Tool im Navigationsbereich mit der linken Seite.
2. Wählen Sie am Anfang des VM-Tools, die **Inventur** Registerkarte, und klicken Sie dann **neu** um einen neuen virtuellen Computer zu erstellen.
3. Geben Sie den virtuellen Computer ein, und wählen Sie zwischen virtuellen Computern der Generation 1 und 2.
4. Wenn Sie einen virtuellen Computer in einem Cluster erstellen, können Sie die Hostgruppen, auf dem virtuellen Computer auf die erste Erstellung auswählen. Wenn Sie WindowsServer 2016 oder höher ausführen, wird das Tool eine Host-Empfehlung für Sie bereit.
5. Wählen Sie einen Pfad für die Dateien der virtuellen Maschine. Wählen Sie ein Volume aus der Dropdownliste aus, oder klicken Sie auf **Durchsuchen** um einen Ordner, die über die Ordnerauswahl auszuwählen. Die Konfigurationsdateien der virtuellen Computer und die VHD-Datei werden gespeichert in einem einzigen Ordner unter dem `\Hyper-V\\[virtual machine name]` Pfad des ausgewählten Volumes oder der Pfad.
6. Wählen Sie die Anzahl virtueller Prozessoren, ob Sie die geschachtelte Virtualisierung aktiviert werden soll, konfigurieren Einstellungen für den Arbeitsspeicher, Netzwerkadapter, virtuelle Festplatten und auswählen, ob ein Betriebssystem von einer ISO-Abbilddatei oder vom Netzwerk installiert werden soll.
7. Klicken Sie auf **Erstellen**, um die virtuelle Maschine zu erstellen.
8. Nachdem Sie den virtuellen Computer erstellt und wird in der Liste der virtuellen Computer angezeigt, können Sie den virtuellen Computer starten.
9. Nachdem der virtuelle Computer gestartet wurde, können Sie mit der VM Konsole über das VMConnect zum Installieren des Betriebssystems verbinden. Wählen Sie den virtuellen Computer aus der Liste aus, klicken Sie auf **weitere** > **Connect** zum Herunterladen der RDP-Datei. Öffnen Sie die RDP-Datei, in der app für die Remotedesktopverbindung. Da dies in der VM Konsole verbunden ist, müssen Sie den Hyper-V-Host-Administratoranmeldeinformationen einzugeben.

## <a name="change-virtual-machine-settings"></a>Ändern der Einstellungen des virtuellen Computers

![Virtuellen Computer für den Bildschirm "Einstellungen"](../media/manage-virtual-machines/vm-settings.png)

1. Klicken Sie auf die **VMs** Tool im Navigationsbereich mit der linken Seite.
2. Wählen Sie am Anfang des VM-Tools, die **Inventur** Registerkarte. Wählen Sie einen virtuellen Computer aus der Liste aus, und klicken Sie auf **weitere** > **Einstellungen**.
3. Wechseln Sie zwischen den **allgemeine**, **Arbeitsspeicher**, **Prozessoren**, **Datenträger**, **Netzwerke**, **Startreihenfolge** und **Prüfpunkte** Registerkarte, konfigurieren Sie die erforderlichen Einstellungen, und klicken Sie dann **speichern** beim Speichern der Einstellungen für die aktuelle Registerkarte. Die verfügbaren Einstellungen variieren abhängig von der VM Generation. Darüber hinaus einige Einstellungen können nicht geändert werden, für die Ausführung von virtuellen Computern aus, und Sie müssen zuerst den virtuellen Computer zu beenden.

## <a name="live-migrate-a-virtual-machine-to-another-cluster-node"></a>Die Livemigration eines virtuellen Computers auf einen anderen Clusterknoten

Wenn Sie in einem Cluster verbunden sind, können Sie einen virtuellen Computer live auf einen anderen Clusterknoten migrieren.

1. Ein Failovercluster oder eine zusammengeführte Verbindung, klicken Sie auf die **VMs** Tool im Navigationsbereich mit der linken Seite.
2. Wählen Sie am Anfang des VM-Tools, die **Inventur** Registerkarte. Wählen Sie einen virtuellen Computer aus der Liste aus, und klicken Sie auf **weitere** > **verschieben**.
3. Wählen Sie einen Server aus der Liste der verfügbaren Clusterknoten, und klicken Sie auf **verschieben**.
4. Benachrichtigungen für die Move-Status werden in der oberen rechten Ecke von Windows Admin Center angezeigt. Wenn die Verschiebung erfolgreich war, sehen Sie den Namen des Hostservers in der Liste der virtuellen Computer geändert.

## <a name="advanced-management-and-troubleshooting-for-a-single-virtual-machine"></a>Erweiterte Verwaltung und Problembehandlung für ein einzelner virtueller Computer

![Detailbildschirm für die einzelnen virtuellen Computer](../media/manage-virtual-machines/vm-details.png)

Sie können ausführliche Informationen und Leistungsdiagramme für einen einzelnen virtuellen Computer auf der Seite für die einzelnen virtuellen Computer anzeigen.

1. Klicken Sie auf die **VMs** Tool im Navigationsbereich mit der linken Seite.
2. Wählen Sie am Anfang des VM-Tools, die **Inventur** Registerkarte. Klicken Sie auf den Namen eines virtuellen Computers aus der Liste der virtuellen Computer.
3. Klicken Sie auf der einzelnen virtuellen Computer können Sie folgende Aktionen ausführen:
    - Detaillierte Informationen für den virtuellen Computer anzeigen.
    - Anzeigen von Live und Liniendiagramme für historische Daten für CPU, Arbeitsspeicher, Netzwerk, IOPS und e/a-Durchsatz (Historische Daten ist nur für hyperkonvergenten Cluster unter Windows Server-2019 verfügbar.)
    - Anzeigen, erstellen, anzuwenden, umbenennen und Löschen von Prüfpunkten.
    - Zeigen Sie Details für den VM Dateien der virtuellen Festplatte (VHD), Netzwerkadapter und Hostserver.
    - Löschen, starten, deaktivieren, Herunterfahren, anhalten, fortsetzen, zurückgesetzt oder benennen Sie den virtuellen Computer. Auch speichern Sie der virtuelle Computer zu, löschen Sie einen gespeicherten Zustand oder erstellen Sie einen Prüfpunkt.
    - [Ändern der Einstellungen für den virtuellen Computer](#change-virtual-machine-settings).
    - Verbinden Sie mit der Konsole des virtuellen Computers über Hyper-V-Host unter Verwendung von VMConnect.
    - [Replizieren Sie den virtuellen Computer mit Azure Site Recovery](#protect-virtual-machines-with-azure-site-recovery).

## <a name="view-hyper-v-event-logs"></a>Hyper-V-Ereignisprotokolle anzeigen

Sie können Hyper-V-Ereignisprotokolle direkt aus dem Tool für die virtuellen Computer anzeigen.

1. Klicken Sie auf die **VMs** Tool im Navigationsbereich mit der linken Seite.
2. Wählen Sie am Anfang des VM-Tools, die **Zusammenfassung** Registerkarte. Klicken Sie in der oberen rechten Abschnitt Events auf **Ansicht aller Ereignisse**.
3. Das Ereignis-Viewer-Tool wird die Hyper-V-ereigniskanäle im linken Bereich angezeigt. Wählen Sie einen Kanal aus, um die Ereignisse im rechten Bereich anzuzeigen. Wenn Sie einen Failovercluster oder einen hyperkonvergenten Cluster verwalten, zeigt die Ereignisprotokolle Ereignisse für alle Clusterknoten, die das Host-Server in der Spalte für die Computer anzeigen.

## <a name="protect-virtual-machines-with-azure-site-recovery"></a>Schützen Sie virtueller Computer mit Azure Site Recovery

Sie können Windows Admin Center verwenden, konfigurieren Sie Azure Site Recovery und replizieren Ihre lokalen virtuellen Computer in Azure. [Weitere Informationen](azure-services.md)

## <a name="more-coming"></a>Weitere folgen

Verwaltungsdienst für virtuelle Computer in Windows Admin Center wird aktiv weiterentwickelt, und werden in naher Zukunft neue Funktionen hinzugefügt werden. Sie können den Status und stimmen Sie für Funktionen in UserVoice anzeigen:

|Die Anforderung zur|
|-------|
|[Import/Export-VM](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)|
|[Sortieren von VMs in Ordnern](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)|
|[Zusätzliche VM-Einstellungen werden unterstützt](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)|
|[Unterstützung für Hyper-V-Replikate](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)|
|[VM-Eigentümerschaft delegieren](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)|
|[Klonen virtueller Maschinen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)|
|[Erstellen einer Vorlage aus einer vorhandenen virtuellen Maschine](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)|
|[Anzeigen von virtuellen Computern auf Hyper-V-hosts](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)|
|[VLAN im Bereich der neuen virtuellen Computer konfigurieren](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)|
|[**Alle anzeigen oder neues Feature vorschlagen**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D)|
