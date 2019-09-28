---
title: defrag
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf1d1ac-996a-4282-9b4d-1e8245ff162c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d930e224ac1610b5e49cbf5701778bfb6f14b2e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378708"
---
# <a name="defrag"></a>defrag

>Gilt für: Windows 10, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In werden fragmentierte Dateien auf lokalen Volumes lokalisiert und konsolidiert, um die Systemleistung zu verbessern.
Sie müssen mindestens Mitglied der lokalen Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diesen Befehl ausführen zu können.

## <a name="syntax"></a>Syntax
```
defrag <volumes> | /C | /E <volumes>    [/H] [/M [n]| [/U] [/V]]
defrag <volumes> | /C | /E <volumes> /A [/H] [/M [n]| [/U] [/V]]
defrag <volumes> | /C | /E <volumes> /X [/H] [/M [n]| [/U] [/V]]
defrag <volume> [/<Parameter>]*
```
## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|`<volume>`|Gibt den Laufwerk Buchstaben oder den Bereitstellungspunktpfad des Volumes an, das zerlegt oder analysiert werden soll.|
|A|Führt eine Analyse der angegebenen Volumes aus.|
|c|Führen Sie den Vorgang auf allen Volumes aus.|
|D|Führen Sie herkömmliche Debug-Vorgänge aus (Dies ist die Standardeinstellung). Bei einem mehrstufigen Volume wird die herkömmliche decofragmentierung jedoch nur auf der Kapazitäts Ebene ausgeführt.|
|E|Führen Sie den Vorgang auf allen Volumes außer den angegebenen Volumes aus.|
|G|Optimieren Sie die Speicherebenen auf den angegebenen Volumes.|
|H|Der Vorgang wird mit normaler Priorität ausgeführt (standardmäßig niedrig).|
|I n|Die ebenenoptimierung wird für jedes Volume höchstens n Sekunden ausgeführt.|
|K|Führt eine Zusammenfassung der Laufwerke auf den angegebenen Volumes aus.|
|L|Führt den Abruf auf den angegebenen Volumes aus.|
|M [n]|Führen Sie den Vorgang auf jedem Volume parallel im Hintergrund aus. Höchstens n Threads optimieren die Speicherebenen parallel.|
|O|Führen Sie die richtige Optimierung für jeden Medientyp aus.|
|T|Verfolgt einen bereits in Bearbeitung befindlichen Vorgang auf dem angegebenen Volume.|
|U|Gibt den Fortschritt des Vorgangs auf dem Bildschirm aus.|
|B|ausführliche Ausgabe Drucken, die die Fragmentierung-Statistik enthält.|
|X|Führen Sie die Konsolidierung des freien Speicherplatzes auf den angegebenen Volumes aus.|
|?|Zeigt diese Hilfe Informationen an.|

## <a name="remarks"></a>Hinweise
- Sie können keine bestimmten Typen von Datei Systemvolumes oder-Laufwerken defragmentieren:
  -   Sie können keine Volumes defragmentieren, die das Dateisystem gesperrt hat.
  -   Sie können keine Volumes defragmentieren, die das Dateisystem als geändert markiert hat. Dies deutet auf eine mögliche Beschädigung hin. Sie müssen **chkdsk** auf einem Dirty Volume ausführen, bevor Sie es zerlegen können. Sie können ermitteln, ob ein Volume geändert wird, indem Sie den Befehl "bereinigen" **mit der Befehls** Zeilen Änderung verwenden. Weitere Informationen zu CHKDSK **und zum** fehlerhaften **Befehl "Chkdsk** " finden Sie unter [Zusätzliche Verweise](defrag.md#BKMK_additionalRef).
  -   Netzwerklaufwerke können nicht zerlegt werden.
  -   CDROMs können nicht defragmentieren.
  -   Sie können keine Datei Systemvolumes defragmentieren, bei denen es sich nicht um **NTFS**, **Refs**, **FAT** oder **FAT32**handelt.
- Mit Windows Server 2008 R2, Windows Server 2008 und Windows Vista können Sie das Defragmentieren eines Volumes planen. Es ist jedoch nicht möglich, ein Festplattenlaufwerk (Solid State Drive, SSD) oder ein Volume auf einer virtuellen Festplatte (VHD), die sich auf einem SSD befindet, zu defragmentieren.
- Um diese Schritte ausführen zu können, müssen Sie auf dem lokalen Computer ein Mitglied der Gruppe %%amp;quot;Administratoren%%amp;quot; sein oder Ihnen muss die entsprechende Berechtigung übertragen worden sein. Wenn der Computer zu einer Domäne gehört, können möglicherweise Mitglieder der Gruppe "Domänen-Admins" dieses Verfahren ausführen. Als bewährte Sicherheitsmaßnahme sollten Sie die Verwendung von " **Ausführen als** " verwenden, um dieses Verfahren auszuführen.
- Ein Volume muss über mindestens 15% freien Speicherplatz verfügen, damit es von der **decofragmentierung** vollständig und ordnungsgemäß zerlegt werden kann. **Defragmentierung** verwendet dieses Leerzeichen als Sortierbereich für Dateifragmente. Wenn ein Volume über weniger als 15% freien Speicherplatz verfügt, wird es von der **decofragmentierung** nur teilweise zerlegt. Um den freien Speicherplatz auf einem Volume zu erhöhen, löschen Sie nicht benötigte Dateien, oder verschieben Sie Sie auf einen anderen Datenträger.
- Beim **analysieren und decomieren** eines Volumes durch die Debug-Funktionen wird ein blinkender Cursor angezeigt. Wenn die **Defragmentierung** das analysieren und Defragmentieren des Volumes abgeschlossen hat, werden der Analysebericht, der Defragmentierungs Bericht oder beide Berichte angezeigt und dann an der Eingabeaufforderung beendet.
- Standardmäßig zeigt **Defragmentierung** eine Zusammenfassung der Analyse-und Defragmentierungsberichte an, wenn Sie die Parameter **/a** und **/v** nicht angeben.
- Sie können die Berichte an eine Textdatei senden, indem Sie **>** <em>filename. txt</em>eingeben, wobei *filename. txt* für einen von Ihnen angegebenen Dateinamen steht. Beispiel: `defrag volume /v > FileName.txt`
- Um den Defragmentierungs Prozess zu unterbrechen, drücken Sie in der Befehlszeile **STRG + C**.
- **Das Ausführen** des Befehls "Debug" und "Disk Debug" schließen sich gegenseitig aus. Wenn Sie die Datenträger Defragmentierung zum Defragmentieren eines Volumes verwenden und den **Defragmentierung** -Befehl in einer Befehlszeile ausführen, schlägt der **Defragmentierung** -Befehl fehl. Wenn Sie hingegen den Defragmentierungsbefehl ausführen und die Datenträger Defragmentierung öffnen, sind die Defragmentierungsoptionen in der Datenträger Defragmentierung nicht verfügbar.

## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um das Volume auf Laufwerk C beim Bereitstellen von Fortschritt und ausführlicher Ausgabe zu defragmentieren:
```
defrag C: /U /V
```
Wenn Sie die Volumes auf den Laufwerken C und D parallel im Hintergrund defragmentieren möchten, geben Sie Folgendes ein:
```
defrag C: D: /M
```
Geben Sie Folgendes ein, um eine Fragmentierungs Analyse eines Volumes auszuführen, das auf Laufwerk C eingebunden ist, und den Fortschritt
```
defrag C: mountpoint /A /U
```
Wenn Sie alle Volumes mit normaler Priorität defragmentieren und eine ausführliche Ausgabe bereitstellen möchten, geben Sie Folgendes ein:
```
defrag /C /H /V
```

## <a name="BKMK_scheduledTask"></a>Geplanter Task
Die geplante Aufgabe Defrag wird als Wartungs Task ausgeführt und ist in der Regel wöchentlich geplant. Der Administrator kann die Häufigkeit mit der App "App **optimieren** " ändern.
- Bei der Ausführung aus dem geplanten Task weist **Defragmentierung** die Richtlinie für SSDs auf:
   - **Herkömmliche** defragmentierungsdateien (d. h. das Verschieben von Dateien, um Sie in angemessener zusammenhängend zu gestalten) und das **Abrufen** werden nur einmal monatlich ausgeführt.
   - Wenn sowohl **herkömmliche** als auch **Abruf** Vorgang übersprungen werden, wird die **Analyse** nicht ausgeführt.
      - Wenn der Benutzer **herkömmliche Defragmentierung** manuell auf einem SSD ausgeführt hat, beispielsweise 3 Wochen nach der letzten geplanten Aufgabe, führt die nächste geplante Task Ausführung eine **Analyse** durch und **Ruft** Sie ab, überspringt aber die **herkömmliche Defragmentierung** auf diesem SSD.
   - Wenn die **Analyse** übersprungen wird, wird die **Letzte Laufzeit** in **Optimierungs Laufwerken** nicht aktualisiert.  Daher kann für SSDs die **Letzte Laufzeit** in **Optimierungs Laufwerken** ein monatlicher Zeitraum sein.
- Mit diesem Wartungs Task werden möglicherweise nicht alle Volumes defragmentiert, es sei denn, diese Aufgabe führt folgende Schritte aus:
   - Der Computer wird nicht zum Ausführen von "Debug" aktiviert.
   - Startet nur, wenn sich der Computer in der Stromversorgung befindet, und wird beendet, wenn der Computer in den Akku Betrieb wechselt.
   - Wird beendet, wenn der Computer nicht mehr im Leerlauf ist.

## <a name="BKMK_additionalRef"></a>Weitere Verweise
-   [chkdsk](chkdsk.md)
-   [fsutil](fsutil.md)
-   [nicht geändert](fsutil-dirty.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
