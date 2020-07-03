---
title: defrag
description: Referenz Artikel für den Defragmentierung-Befehl, der fragmentierte Dateien auf lokalen Volumes sucht und konsolidiert, um die Systemleistung zu verbessern.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aaf1d1ac-996a-4282-9b4d-1e8245ff162c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c952ff78147d3b4c6097aaf9dd87e55ecc7911ad
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928794"
---
# <a name="defrag"></a>defrag

> Gilt für: Windows 10, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In werden fragmentierte Dateien auf lokalen Volumes lokalisiert und konsolidiert, um die Systemleistung zu verbessern.

Sie müssen mindestens Mitglied der lokalen Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diesen Befehl ausführen zu können.

## <a name="syntax"></a>Syntax

```
defrag <volumes> | /c | /e <volumes>    [/h] [/m [n]| [/u] [v]]
defrag <volumes> | /c | /e <volumes> /a [/h] [/m [n]| [/u] [v]]
defrag <volumes> | /c | /e <volumes> /x [/h] [/m [n]| [/u] [v]]
defrag <volume> [<parameters>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<volume>` | Gibt den Laufwerk Buchstaben oder den Bereitstellungspunktpfad des Volumes an, das zerlegt oder analysiert werden soll. |
| /a | Führt eine Analyse der angegebenen Volumes aus. |
| /C | Führen Sie den Vorgang auf allen Volumes aus. |
| /d | Führen Sie herkömmliche Debug-Vorgänge aus (Dies ist die Standardeinstellung). Bei einem mehrstufigen Volume wird die herkömmliche decofragmentierung jedoch nur auf der Kapazitäts Ebene ausgeführt. |
| /e | Führen Sie den Vorgang auf allen Volumes außer den angegebenen Volumes aus. |
| /g | Optimieren Sie die Speicherebenen auf den angegebenen Volumes. |
| /h | Der Vorgang wird mit normaler Priorität ausgeführt (standardmäßig niedrig). |
| /i [n] | Die ebenenoptimierung wird für jedes Volume höchstens n Sekunden ausgeführt. |
| /k | Führt eine Zusammenfassung der Laufwerke auf den angegebenen Volumes aus. |
| /l | Führt den Abruf auf den angegebenen Volumes aus. |
| /m [n] | Führen Sie den Vorgang auf jedem Volume parallel im Hintergrund aus. Höchstens n Threads optimieren die Speicherebenen parallel. |
| /o | Führen Sie die richtige Optimierung für jeden Medientyp aus. |
| /t | Verfolgt einen bereits in Bearbeitung befindlichen Vorgang auf dem angegebenen Volume. |
| /U | Gibt den Fortschritt des Vorgangs auf dem Bildschirm aus. |
| /v | Ausführliche Ausgabe Drucken, die die Fragmentierung-Statistik enthält. |
| /x | Führen Sie die Konsolidierung des freien Speicherplatzes auf den angegebenen Volumes aus. |
| /? | Zeigt diese Hilfe Informationen an. |

#### <a name="remarks"></a>Hinweise

- Sie können keine bestimmten Dateisystemvolumes oder-Laufwerke defragmentieren, einschließlich:

  - Volumes, die vom Dateisystem gesperrt sind.

  - Volumes das Dateisystem, das als geändert gekennzeichnet ist, und deutet auf mögliche Beschädigungen hin.<br>Sie müssen ausführen, `chkdsk` bevor Sie dieses Volume oder Laufwerk zerlegen können. Mithilfe des-Befehls können Sie feststellen, ob ein Volume geändert wurde `fsutil dirty` .

  - Netzwerklaufwerke.

  - CD-ROMs.

  - Datei Systemvolumes, bei denen es sich nicht um **NTFS**, **Refs**, **FAT** oder **FAT32**handelt.

- Sie können das Defragmentieren eines Solid-State-Laufwerks (SSD) oder eines Volumes auf einer virtuellen Festplatte (VHD), die sich auf einem SSD befindet, nicht planen.

- Um diese Schritte auszuführen, müssen Sie Mitglied der Gruppe "Administratoren" auf dem lokalen Computer sein, oder die entsprechende Berechtigung muss an Sie delegiert worden sein. Wenn der Computer zu einer Domäne gehört, können möglicherweise Mitglieder der Gruppe "Domänen-Admins" dieses Verfahren ausführen. Als bewährte Sicherheitsmaßnahme sollten Sie die Verwendung von " **Ausführen als** " verwenden, um dieses Verfahren auszuführen.

- Ein Volume muss über mindestens 15% freien Speicherplatz verfügen, damit es von der **decofragmentierung** vollständig und ordnungsgemäß zerlegt werden kann. **Defragmentierung** verwendet dieses Leerzeichen als Sortierbereich für Dateifragmente. Wenn ein Volume über weniger als 15% freien Speicherplatz verfügt, wird es von der **decofragmentierung** nur teilweise zerlegt. Um den freien Speicherplatz auf einem Volume zu erhöhen, löschen Sie nicht benötigte Dateien, oder verschieben Sie Sie auf einen anderen Datenträger.

- Beim **analysieren und decomieren** eines Volumes durch die Debug-Funktionen wird ein blinkender Cursor angezeigt. Wenn die **Defragmentierung** das analysieren und Defragmentieren des Volumes abgeschlossen hat, werden der Analysebericht, der Defragmentierungs Bericht oder beide Berichte angezeigt und dann an der Eingabeaufforderung beendet.

- Standardmäßig zeigt **Defragmentierung** eine Zusammenfassung der Analyse-und Defragmentierungsberichte an, wenn Sie die Parameter **/a** und **/v** nicht angeben.

- Sie können die Berichte an eine Textdatei senden, indem Sie **>** <em>FileName.txt</em>eingeben, wobei *FileName.txt* für einen von Ihnen angegebenen Dateinamen steht. Beispiel: `defrag volume /v > FileName.txt`

- Um den Defragmentierungs Prozess zu unterbrechen, drücken Sie in der Befehlszeile **STRG + C**.

- **Das Ausführen** des Befehls "Debug" und "Disk Debug" schließen sich gegenseitig aus. Wenn Sie die Datenträger Defragmentierung zum Defragmentieren eines Volumes verwenden und den **Defragmentierung** -Befehl in einer Befehlszeile ausführen, schlägt der **Defragmentierung** -Befehl fehl. Wenn Sie hingegen den Defragmentierungsbefehl ausführen und die Datenträger Defragmentierung öffnen, sind die Defragmentierungsoptionen in der Datenträger Defragmentierung nicht verfügbar. **defrag**

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Volume auf Laufwerk C beim Bereitstellen von Fortschritt und ausführlicher Ausgabe zu defragmentieren:

```
defrag c: /u /v
```

Wenn Sie die Volumes auf den Laufwerken C und D parallel im Hintergrund defragmentieren möchten, geben Sie Folgendes ein:

```
defrag c: d: /m
```

Geben Sie Folgendes ein, um eine Fragmentierungs Analyse eines Volumes auszuführen, das auf Laufwerk C eingebunden ist, und den Fortschritt

```
defrag c: mountpoint /a /u
```

Wenn Sie alle Volumes mit normaler Priorität defragmentieren und eine ausführliche Ausgabe bereitstellen möchten, geben Sie Folgendes ein:

```
defrag /c /h /v
```

## <a name="scheduled-task"></a>Geplanter Task

Der Defragmentierungsprozess führt die geplante Aufgabe als Wartungs Task aus, der normalerweise jede Woche ausgeführt wird. Als Administrator können Sie die Häufigkeit ändern, mit der der Task ausgeführt wird, indem Sie die APP APP **optimieren** verwenden.

- Bei der Ausführung aus dem geplanten Task verwendet **Defragmentierung** die unten aufgeführten Richtlinien für SSDs:

  - **Herkömmliche Optimierungsprozesse**. Schließt die **herkömmliche Defragmentierung**ein, **z. b**. das Verschieben von Dateien, um Sie in angemessener zusammenhängend zu machen. Dies erfolgt einmal pro Monat. Wenn jedoch sowohl die **herkömmliche Defragmentierung** als auch der **Abruf** Vorgang übersprungen werden, wird die **Analyse** nicht ausgeführt.

  - Wenn Sie die **herkömmliche Defragmentierung** auf einem SSD manuell ausführen, werden bei der nächsten geplanten Ausführung von der nächsten geplanten Aufgaben **Analyse** und **Abruf**Vorgänge ausgeführt, die **herkömmliche Defragmentierung** auf diesem SSD wird jedoch überladen.

  - Wenn Sie die **Analyse**überspringen, wird in der App " **Optimieren von Laufwerken** " keine aktualisierte **Letzte Laufzeit** angezeigt. Aus diesem Grund kann die **Letzte Laufzeit** bis zu einem Monat alt sein.

  - Möglicherweise stellen Sie fest, dass die geplante Aufgabe nicht alle Volumes defragmentiert hat. Dies liegt in der Regel daran:

    - Der Prozess wird nicht zum Ausführen des Computers reaktiviert.

    - Der Computer ist nicht angeschlossen. Der Prozess wird nicht ausgeführt, wenn der Computer im Akku Betrieb ausgeführt wird.

    - Der Computer wurde erneut gestartet (im Leerlauf wieder aufgenommen).

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [chkdsk](chkdsk.md)

- [fsutil](fsutil.md)

- [fsutil dirty](fsutil-dirty.md)

- [PowerShell-Volumen Optimierung](https://docs.microsoft.com/powershell/module/storage/optimize-volume?view=win10-ps)
