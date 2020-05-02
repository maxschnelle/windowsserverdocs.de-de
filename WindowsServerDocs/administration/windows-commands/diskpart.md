---
title: DiskPart
description: Referenz Thema für **DiskPart**, das Sie bei der Verwaltung der Laufwerke Ihres Computers unterstützt.
ms.prod: windows-server
ms.technology: storage
author: jasongerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: f127ff4ef1c2d143c956069d1ab3788382e70cc3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719460"
---
# <a name="diskpart"></a>DiskPart

> Gilt für: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2, Windows Server 2008

DiskPart-Befehle helfen Ihnen beim Verwalten der Laufwerke Ihres Computers (Datenträger, Partitionen, Volumes oder virtuelle Festplatten).

Bevor Sie Diskpart-Befehle verwenden können, müssen Sie zuerst auflisten und dann ein Objekt auswählen, um den Fokus zu erhalten. Wenn ein Objekt den Fokus besitzt, werden alle DiskPart-Befehle, die Sie eingeben, für dieses Objekt ausgeführt.

## <a name="list-available-objects"></a>Auflisten der verfügbaren Objekte

Mithilfe der folgenden Schritte können Sie die verfügbaren Objekte auflisten und die Nummer oder den Laufwerk Buchstaben eines Objekts ermitteln:

- `list disk`-Zeigt alle Datenträger auf dem Computer an.

- `list volume`-Zeigt alle Volumes auf dem Computer an.

- `list partition`-Zeigt die Partitionen auf dem Datenträger an, die den Fokus auf dem Computer haben.

- `list vdisk`-Zeigt alle virtuellen Datenträger auf dem Computer an.

Wenn Sie die **List** -Befehle verwenden, wird neben dem Objekt mit dem Fokus ein Sternchen (*) angezeigt.

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

Sie können die folgenden Befehle über den DiskPart-Befehls Interpreter ausführen:

| Get-Help | BESCHREIBUNG |
| ------- | ----------- |
| [Aktiv](active.md) | Markiert die Partition des Datenträgers mit dem Fokus als aktiv. |
| [Add (Hinzufügen)](add.md) | Spiegelt das einfache Volume mit dem Fokus auf den angegebenen Datenträger. |
| [Zuweisen](assign.md) | Weist dem Volume mit dem Fokus einen Laufwerk Buchstaben oder einen Einfügepunkt zu. |
| [Vdisk anfügen](attach-vdisk.md) | Wird eine virtuelle Festplatte (auch als Bereitstellung oder Oberfläche bezeichnet) an eine virtuelle Festplatte (VHD) angefügt, sodass Sie auf dem Host Computer als lokales Festplattenlaufwerk angezeigt wird. |
| [Attribute](attributes.md) | Hiermit werden die Attribute eines Datenträgers oder Volumes angezeigt, festgelegt oder gelöscht. |
| [Automatische Bereitstellung](automount.md) | Aktiviert oder deaktiviert das Feature "automatischen Bereitstellung". | 
| [Umbruch](break.md) | Unterbricht das gespiegelte Volume mit dem Fokus auf zwei einfache Volumes. |
| [Räumen](clean.md) | Entfernt alle Partitionen oder volumeformatierung aus dem Datenträger mit dem Fokus. |
| [Compact Vdisk](compact-vdisk.md) | Verringert die physische Größe einer dynamisch erweiterbaren virtuellen Festplatten Datei (VHD). |
| [Umgebaut](convert.md) | Konvertiert Dateizuordnungs-und FAT32-Volumes in das NTFS-Dateisystem, sodass vorhandene Dateien und Verzeichnisse intakt bleiben. |
| [Erstellen](create.md) | Erstellt eine Partition auf einem Datenträger, einem Volume auf einem oder mehreren Datenträgern oder einer virtuellen Festplatte (VHD). |
| [Löschen](delete.md) | Löscht eine Partition oder ein Volume. |
| [Vdisk trennen](detach-vdisk.md) | Verhindert, dass die ausgewählte virtuelle Festplatte (VHD) als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird. |
| [Detail](detail.md) | Zeigt Informationen zum ausgewählten Datenträger, der Partition, dem Volume oder der virtuellen Festplatte (VHD) an. |
| [Exit](exit.md) | Beendet den DiskPart-Befehls Interpreter. |
| [Erweitern von Vdisk](expand-vdisk.md) | Erweitert eine virtuelle Festplatte (VHD) auf die Größe, die Sie angeben. |
| [Gewähren](extend.md) | Erweitert das Volume oder die Partition mit dem Fokus zusammen mit dem Dateisystem in den freien (nicht zugeordneten) Speicherplatz auf einem Datenträger. |
| [Dateisysteme](filesystems.md) | Zeigt Informationen zum aktuellen Dateisystem des Volumes mit dem Fokus an und listet die Dateisysteme auf, die zum Formatieren des Volumes unterstützt werden. |
| [Ges](format.md) | Formatiert einen Datenträger zum Akzeptieren von Windows-Dateien. |
| [GPT](gpt.md) | Weist die GPT-Attribute der Partition zu, wobei der Fokus auf Basis Datenträgern für die GUID-Partitionstabelle (GPT) liegt. |
| [Hilfe](help.md) | Zeigt eine Liste der verfügbaren Befehle oder ausführliche Hilfe Informationen zu einem angegebenen Befehl an. |
| [Importieren](import.md) | Importiert eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers. |
| [Inaktiv](inactive.md) | Markiert die Systempartition oder Start Partition, deren Fokus auf grundlegenden Master Boot Record-Datenträgern (MBR) liegt. |
| [Liste](list.md) | Zeigt eine Liste von Datenträgern, von Partitionen auf einem Datenträger, von Volumes auf einem Datenträger oder von virtuellen Festplatten (VHDs) an. |
| [Vdisk zusammenführen](merge-vdisk.md) | Führt eine differenzierende virtuelle Festplatte (VHD) mit der entsprechenden übergeordneten VHD zusammen. |
| [Offline](offline.md) | Nimmt einen Online Datenträger oder ein Online Volume in den Offline Zustand. |
| [Online](online.md) | Nimmt einen Offline Datenträger oder ein Offline Volume in den Online Zustand. |
| [Wiederherstellen](recover.md) | Aktualisiert den Status aller Datenträger in einer Datenträger Gruppe, versucht, Datenträger in einer ungültigen Datenträger Gruppe wiederherzustellen, und synchronisiert die gespiegelten Volumes und RAID-5-Volumes mit veralteten Daten erneut. |
| [REM](rem.md) | Bietet eine Möglichkeit zum Hinzufügen von Kommentaren zu einem Skript. |
| [Remove](remove.md) | Entfernt einen Laufwerk Buchstaben oder einen Einfügepunkt von einem Volume. |
| [Reparatur](repair.md) | Repariert das RAID-5-Volume mit dem Fokus, indem der fehlerhafte Datenträger Bereich durch die angegebene dynamische Festplatte ersetzt wird. |
| [Neu einlesen](rescan.md) | Es werden neue Datenträger gesucht, die möglicherweise dem Computer hinzugefügt wurden. |
| [Beibehalten](retain.md) | Bereitet ein vorhandenes dynamisches einfaches Volume vor, das als Start-oder System Volume verwendet werden soll. |
| [Chen](san.md) | Zeigt die Storage Area Network-Richtlinie (San) für das Betriebssystem an oder legt diese fest. |
| [Auswählen](select.md) | Verschiebt den Fokus auf einen Datenträger, eine Partition, ein Volume oder eine virtuelle Festplatte (VHD). |
| [ID festlegen](set-id.md) | Ändert das Feld Partitionstyp für die Partition mit dem Fokus. |
| [Verkleinern](shrink.md) | Verringert die Größe des ausgewählten Volumes um den angegebenen Betrag. |
| [UniqueId](uniqueid.md) | Zeigt den GPT-Bezeichner (GUID-Partitionstabelle) oder die Master Boot Record (MBR)-Signatur für den Datenträger mit Fokus an oder legt ihn fest. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Datenträgerverwaltung: Übersicht](https://docs.microsoft.com/windows-server/storage/disk-management/overview-of-disk-management)

- [Speicher-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/storage/)
