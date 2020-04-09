---
title: DiskPart
description: Windows-Befehle-Thema für Diskpart, das Sie bei der Verwaltung der Laufwerke Ihres Computers unterstützt.
ms.prod: windows-server
ms.technology: storage
author: jasongerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 45fe66e4843b96db8e4593c0e963e4a80dbd22c2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845473"
---
# <a name="diskpart"></a>DiskPart

>Gilt für: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2, Windows Server 2008

DiskPart-Befehle helfen Ihnen beim Verwalten der Laufwerke Ihres Computers (Datenträger, Partitionen, Volumes oder virtuelle Festplatten). 

Bevor Sie Diskpart-Befehle verwenden können, müssen Sie zuerst auflisten und dann ein Objekt auswählen, um den Fokus zu erhalten. Wenn ein Objekt den Fokus besitzt, werden alle DiskPart-Befehle, die Sie eingeben, für dieses Objekt ausgeführt.

## <a name="list-the-available-objects"></a>Auflisten der verfügbaren Objekte

Mithilfe der folgenden Schritte können Sie die verfügbaren Objekte auflisten und die Nummer oder den Laufwerk Buchstaben eines Objekts ermitteln:

- `list disk`: zeigt alle Datenträger auf dem Computer an.

- `list volume`: zeigt alle Volumes auf dem Computer an.

- `list partition`: zeigt die Partitionen auf dem Datenträger an, die den Fokus auf dem Computer haben.

- `list vdisk`: zeigt alle virtuellen Datenträger auf dem Computer an.

Wenn Sie die **List** -Befehle verwenden, wird ein Sternchen (\*) neben dem Objekt mit dem Fokus angezeigt.

## <a name="determine-focus"></a>Fokus bestimmen

Wenn Sie ein Objekt auswählen, bleibt der Fokus auf diesem Objekt, bis Sie ein anderes Objekt auswählen. Wenn beispielsweise der Fokus auf Datenträger 0 festgelegt ist und Sie Volume 8 auf Datenträger 2 auswählen, wechselt der Fokus von Datenträger 0 zu Datenträger 2, Volume 8.

Einige Befehle ändern automatisch den Fokus. Wenn Sie z. b. eine neue Partition erstellen, wechselt der Fokus automatisch zur neuen Partition.

Sie können den Fokus nur auf eine Partition auf dem ausgewählten Datenträger legen. Wenn eine Partition den Fokus besitzt, hat das zugehörige Volume (sofern vorhanden) ebenfalls den Fokus. Wenn ein Volume den Fokus besitzt, haben der zugehörige Datenträger und die Partition ebenfalls den Fokus, wenn das Volume einer einzelnen bestimmten Partition zugeordnet wird. Wenn dies nicht der Fall ist, geht der Fokus auf den Datenträger und die Partition verloren.

## <a name="diskpart-commands"></a>DiskPart-Befehle

Geben Sie Folgendes an der Eingabeaufforderung ein, um den DiskPart-Befehls Interpreter zu starten:

```
diskpart
```

> [!IMPORTANT]
> Sie müssen sich in der lokalen Gruppe " **Administratoren** " oder einer Gruppe mit ähnlichen Berechtigungen befinden, um DiskPart auszuführen. 

Sie können die folgenden Befehle im DiskPart-Befehls Interpreter ausführen:

| Befehl | Beschreibung |
| ------- | ----------- |
| [Active](active.md) | Markiert die Partition des Datenträgers mit dem Fokus als aktiv. |
| [Hinzufügen](add.md) | Spiegelt das einfache Volume mit dem Fokus auf den angegebenen Datenträger. |
| [Einräumen](assign.md) | Weist dem Volume mit dem Fokus einen Laufwerk Buchstaben oder einen Einfügepunkt zu. |
| [Vdisk anfügen](attach-vdisk.md) | Wird eine virtuelle Festplatte (auch als Bereitstellung oder Oberfläche bezeichnet) an eine virtuelle Festplatte (VHD) angefügt, sodass Sie auf dem Host Computer als lokales Festplattenlaufwerk angezeigt wird. |
| [Legt](attributes.md) | Hiermit werden die Attribute eines Datenträgers oder Volumes angezeigt, festgelegt oder gelöscht. |
| [Automatischen Bereitstellung](automount.md) | Aktiviert oder deaktiviert das Feature "automatischen Bereitstellung". | 
| [Umbruch](break.md) | Unterbricht das gespiegelte Volume mit dem Fokus auf zwei einfache Volumes. |
| [Räumen](clean.md) | Entfernt alle Partitionen oder volumeformatierung aus dem Datenträger mit dem Fokus. |
| [Compact Vdisk](compact-vdisk.md) | Verringert die physische Größe einer dynamisch erweiterbaren virtuellen Festplatten Datei (VHD). |
| [Umgebaut](convert.md) | Konvertiert Dateizuordnungs-und FAT32-Volumes in das NTFS-Dateisystem, sodass vorhandene Dateien und Verzeichnisse intakt bleiben. |
| [Stelle](create.md) | Erstellt eine Partition auf einem Datenträger, einem Volume auf einem oder mehreren Datenträgern oder einer virtuellen Festplatte (VHD). |
| [Löschen](delete.md) | Löscht eine Partition oder ein Volume. |
| [Vdisk trennen](detach-vdisk.md) | Verhindert, dass die ausgewählte virtuelle Festplatte (VHD) als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird. |
| [Einzelnen](detail.md) | Zeigt Informationen zum ausgewählten Datenträger, der Partition, dem Volume oder der virtuellen Festplatte (VHD) an. |
| [Exit](exit.md) | Beendet den DiskPart-Befehls Interpreter. |
| [Erweitern von Vdisk](expand-vdisk.md) | 
| [Extend](extend.md) | 
| [Dateisysteme](filesystems.md) | 
| [Format](format.md) | 
| [GPT](gpt.md) | 
| [Hilfe](help.md) | 
| [Importieren](import.md) | 
| [VSTE](inactive.md) | 
| [List](list.md) | 
| [Vdisk zusammenführen](merge-vdisk.md) | 
| [Aufzu](offline.md) | 
| [Internet](online.md) | 
| [Wiederherstellen](recover.md) | 
| [REM](rem.md) | 
| [Entfernen](remove.md) | 
| [Reparatur](repair.md) | 
| [Neu einlesen](rescan.md) | 
| [Erhalten](retain.md) | 
| [Chen](san.md) | 
| [Auswahl](select.md) | 
| [ID festlegen](set-id.md) | 
| [Verkleinern](shrink.md) | 
| [UniqueId](uniqueid.md) | 

## <a name="additional-references"></a>Weitere Verweise

- [Befehlszeilen-Syntax Schlüssel] (Command-Line-Syntax-Key.MD

- [Übersicht über Datenträgerverwaltung](https://docs.microsoft.com/windows-server/storage/disk-management/overview-of-disk-management)

- [Storage-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/storage/)
