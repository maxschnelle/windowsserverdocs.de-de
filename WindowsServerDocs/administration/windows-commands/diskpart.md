---
title: diskpart
description: Referenz Artikel für den DiskPart-Befehls Interpreter, der Sie bei der Verwaltung der Laufwerke Ihres Computers unterstützt.
ms.topic: reference
author: jasongerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 1d2f4cc814dad4313e7eb0925b60f44ec0348a30
ms.sourcegitcommit: de207e887575757f3389ccf940c2e0ad2dc70bd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2020
ms.locfileid: "94617200"
---
# <a name="diskpart"></a>diskpart

> Gilt für: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2, Windows Server 2008

Der DiskPart-Befehls Interpreter unterstützt Sie bei der Verwaltung der Laufwerke Ihres Computers (Datenträger, Partitionen, Volumes oder virtuelle Festplatten).

Bevor Sie **DiskPart** -Befehle verwenden können, müssen Sie zuerst auflisten und dann ein Objekt auswählen, um den Fokus zu erhalten. Nachdem ein Objekt den Fokus besitzt, werden alle DiskPart-Befehle, die Sie eingeben, für dieses Objekt ausgeführt.

## <a name="list-available-objects"></a>Auflisten der verfügbaren Objekte

Mithilfe der folgenden Schritte können Sie die verfügbaren Objekte auflisten und die Nummer oder den Laufwerk Buchstaben eines Objekts ermitteln:

- `list disk` -Zeigt alle Datenträger auf dem Computer an.

- `list volume` -Zeigt alle Volumes auf dem Computer an.

- `list partition` -Zeigt die Partitionen auf dem Datenträger an, die den Fokus auf dem Computer haben.

- `list vdisk` -Zeigt alle virtuellen Datenträger auf dem Computer an.

Nachdem Sie die **Listen** Befehle ausgeführt haben, wird neben dem Objekt mit dem Fokus ein Sternchen (*) angezeigt.

## <a name="determine-focus"></a>Fokus bestimmen

Wenn Sie ein Objekt auswählen, bleibt der Fokus auf diesem Objekt, bis Sie ein anderes Objekt auswählen. Wenn beispielsweise der Fokus auf Datenträger 0 festgelegt ist und Sie Volume 8 auf Datenträger 2 auswählen, wechselt der Fokus von Datenträger 0 zu Datenträger 2, Volume 8.

Einige Befehle ändern automatisch den Fokus. Wenn Sie z. b. eine neue Partition erstellen, wechselt der Fokus automatisch zur neuen Partition.

Sie können den Fokus nur auf eine Partition auf dem ausgewählten Datenträger legen. Nachdem eine Partition den Fokus besitzt, hat das zugehörige Volume (sofern vorhanden) ebenfalls den Fokus. Nachdem ein Volume den Fokus besitzt, haben der zugehörige Datenträger und die Partition ebenfalls den Fokus, wenn das Volume einer einzelnen bestimmten Partition zugeordnet wird. Wenn dies nicht der Fall ist, geht der Fokus auf den Datenträger und die Partition verloren.

## <a name="syntax"></a>Syntax

Geben Sie Folgendes an der Eingabeaufforderung ein, um den DiskPart-Befehls Interpreter zu starten:

```
diskpart <parameter>
```

> [!IMPORTANT]
> Sie müssen sich in der lokalen Gruppe " **Administratoren** " oder einer Gruppe mit ähnlichen Berechtigungen befinden, um DiskPart auszuführen.

### <a name="parameters"></a>Parameter

Sie können die folgenden Befehle über den DiskPart-Befehls Interpreter ausführen:

| Get-Help | BESCHREIBUNG |
| ------- | ----------- |
| [active](active.md) | Markiert die Partition des Datenträgers mit dem Fokus als aktiv. |
| [add](add.md) | Spiegelt das einfache Volume mit dem Fokus auf den angegebenen Datenträger. |
| [assign](assign.md) | Weist dem Volume mit dem Fokus einen Laufwerk Buchstaben oder einen Einfügepunkt zu. |
| [attach vdisk](attach-vdisk.md) | Wird eine virtuelle Festplatte (auch als Bereitstellung oder Oberfläche bezeichnet) an eine virtuelle Festplatte (VHD) angefügt, sodass Sie auf dem Host Computer als lokales Festplattenlaufwerk angezeigt wird. |
| [attributes](attributes.md) | Hiermit werden die Attribute eines Datenträgers oder Volumes angezeigt, festgelegt oder gelöscht. |
| [automount](automount.md) | Aktiviert oder deaktiviert das Feature "automatischen Bereitstellung". |
| [break](break.md) | Unterbricht das gespiegelte Volume mit dem Fokus auf zwei einfache Volumes. |
| [clean](clean.md) | Entfernt alle Partitionen oder volumeformatierung aus dem Datenträger mit dem Fokus. |
| [compact vdisk](compact-vdisk.md) | Verringert die physische Größe einer dynamisch erweiterbaren virtuellen Festplatten Datei (VHD). |
| [convert](convert.md) | Konvertiert Dateizuordnungs-und FAT32-Volumes in das NTFS-Dateisystem, sodass vorhandene Dateien und Verzeichnisse intakt bleiben. |
| [erstellen](create.md) | Erstellt eine Partition auf einem Datenträger, einem Volume auf einem oder mehreren Datenträgern oder einer virtuellen Festplatte (VHD). |
| [delete](delete.md) | Löscht eine Partition oder ein Volume. |
| [detach vdisk](detach-vdisk.md) | Verhindert, dass die ausgewählte virtuelle Festplatte (VHD) als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird. |
| [detail](detail.md) | Zeigt Informationen zum ausgewählten Datenträger, der Partition, dem Volume oder der virtuellen Festplatte (VHD) an. |
| [exit](exit.md) | Beendet den DiskPart-Befehls Interpreter. |
| [expand vdisk](expand-vdisk.md) | Erweitert eine virtuelle Festplatte (VHD) auf die Größe, die Sie angeben. |
| [extend](extend.md) | Erweitert das Volume oder die Partition mit dem Fokus zusammen mit dem Dateisystem in den freien (nicht zugeordneten) Speicherplatz auf einem Datenträger. |
| [filesystems](filesystems.md) | Zeigt Informationen zum aktuellen Dateisystem des Volumes mit dem Fokus an und listet die Dateisysteme auf, die zum Formatieren des Volumes unterstützt werden. |
| [format](format.md) | Formatiert einen Datenträger zum Akzeptieren von Windows-Dateien. |
| [gpt](gpt.md) | Weist die GPT-Attribute der Partition zu, wobei der Fokus auf Basis Datenträgern für die GUID-Partitionstabelle (GPT) liegt. |
| [help](help.md) | Zeigt eine Liste der verfügbaren Befehle oder ausführliche Hilfe Informationen zu einem angegebenen Befehl an. |
| [import](import.md) | Importiert eine fremde Datenträger Gruppe in die Datenträger Gruppe des lokalen Computers. |
| [inactive](inactive.md) | Markiert die Systempartition oder Start Partition, deren Fokus auf grundlegenden Master Boot Record-Datenträgern (MBR) liegt. |
| [list](list.md) | Zeigt eine Liste von Datenträgern, von Partitionen auf einem Datenträger, von Volumes auf einem Datenträger oder von virtuellen Festplatten (VHDs) an. |
| [merge vdisk](merge-vdisk.md) | Führt eine differenzierende virtuelle Festplatte (VHD) mit der entsprechenden übergeordneten VHD zusammen. |
| [offline](offline.md) | Nimmt einen Online Datenträger oder ein Online Volume in den Offline Zustand. |
| [online](online.md) | Nimmt einen Offline Datenträger oder ein Offline Volume in den Online Zustand. |
| [recover](recover.md) | Aktualisiert den Status aller Datenträger in einer Datenträger Gruppe, versucht, Datenträger in einer ungültigen Datenträger Gruppe wiederherzustellen, und synchronisiert die gespiegelten Volumes und RAID-5-Volumes mit veralteten Daten erneut. |
| [rem](rem.md) | Bietet eine Möglichkeit zum Hinzufügen von Kommentaren zu einem Skript. |
| [remove](remove.md) | Entfernt einen Laufwerk Buchstaben oder einen Einfügepunkt von einem Volume. |
| [repair](repair.md) | Repariert das RAID-5-Volume mit dem Fokus, indem der fehlerhafte Datenträger Bereich durch die angegebene dynamische Festplatte ersetzt wird. |
| [rescan](rescan.md) | Es werden neue Datenträger gesucht, die möglicherweise dem Computer hinzugefügt wurden. |
| [retain](retain.md) | Bereitet ein vorhandenes dynamisches einfaches Volume vor, das als Start-oder System Volume verwendet werden soll. |
| [san](san.md) | Zeigt die Storage Area Network-Richtlinie (San) für das Betriebssystem an oder legt diese fest. |
| [select](select.md) | Verschiebt den Fokus auf einen Datenträger, eine Partition, ein Volume oder eine virtuelle Festplatte (VHD). |
| [set id](set-id.md) | Ändert das Feld Partitionstyp für die Partition mit dem Fokus. |
| [shrink](shrink.md) | Verringert die Größe des ausgewählten Volumes um den angegebenen Betrag. |
| [uniqueid](uniqueid.md) | Zeigt den GPT-Bezeichner (GUID-Partitionstabelle) oder die Master Boot Record (MBR)-Signatur für den Datenträger mit Fokus an oder legt ihn fest. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Datenträgerverwaltung: Übersicht](../../storage/disk-management/overview-of-disk-management.md)

- [Speicher-Cmdlets in Windows PowerShell](/powershell/module/storage/)
