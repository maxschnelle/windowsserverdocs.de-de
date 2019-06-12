---
title: defrag
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6b5f6231273fb9fe9a99a1cd1bf72dbd0bad71af
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433913"
---
# <a name="defrag"></a>defrag

>Gilt für: Windows 10, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Sucht und konsolidiert fragmentierte Dateien auf lokalen Volumes die Systemleistung zu verbessern.
Mitgliedschaft in der lokalen **Administratoren** oder einer gleichwertigen Gruppe, ist die mindestvoraussetzung, um diesen Befehl auszuführen.

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
|`<volume>`|Gibt an, der Laufwerkbuchstabe oder Bereitstellungspunkt Punkt Laufwerkpfad des Volumes, defragmentiert oder analysiert werden soll.|
|A|Führen Sie auf die angegebenen Volumes Analyse.|
|c|Führen Sie den Vorgang für alle Volumes.|
|D|Führen Sie die herkömmlichen Defrag (Dies ist die Standardeinstellung). Herkömmliche Defragmentierung ist jedoch auf einem mehrstufigen Volume nur auf der Kapazität-Ebene ausgeführt.|
|E|Führen Sie den Vorgang für alle Volumes mit Ausnahme derjenigen angegeben.|
|G|Optimieren Sie die Speicherebenen für die angegebenen Volumes.|
|H|Führen Sie den Vorgang mit normaler Priorität (Standard ist niedrig).|
|Ich n|Ebenenoptimierung würde für maximal n Sekunden auf jedem Volume ausgeführt.|
|K|Durchführen der bereichskonsolidierung auf den angegebenen Volumes.|
|L|Führen Sie auf die angegebenen Volumes erneut optimieren.|
|M [n]|Den Vorgang auf jedem Volume werden parallel im Hintergrund ausgeführt. Höchstens n Threads die Speicherebenen parallel zu optimieren.|
|O|Führen Sie die richtige Optimierung für jeden Medientyp.|
|T|Verfolgen eines Vorgangs bereits auf dem angegebenen Volume.|
|U|Drucken Sie den Fortschritt des Vorgangs auf dem Bildschirm.|
|B|Drucken Sie die ausführlichen Ausgabe, die mit der Fragmentierungsstatistik.|
|X|Führen Sie auf die angegebenen Volumes Speicherplatz Konsolidierung.|
|?|Zeigt diese Hilfeinformationen an.|

## <a name="remarks"></a>Hinweise
- Sie können keine bestimmte Typen von Dateisystem-Datenträger oder Laufwerke defragmentieren:
  -   Sie können keine Volumes zu defragmentieren, die im Dateisystem gesperrt hat.
  -   Sie können keine Defragmentieren Volumes, die im Dateisystem als fehlerhaft gekennzeichnet wurde gibt möglicherweise an. Sie müssen ausführen **Chkdsk** auf einen fehlerhaften Datenträger zu defragmentieren können. Sie können feststellen, ob ein Volume fehlerhaft ist, mit der **Fsutil** Abfragebefehl geändert. Weitere Informationen zu **Chkdsk** und **Fsutil** modifizierte, finden Sie unter [zusätzliche Verweise](defrag.md#BKMK_additionalRef).
  -   Sie können keine Netzwerklaufwerke defragmentieren.
  -   Sie können keine CD-ROMs defragmentieren.
  -   Sie können keine Dateisystemlaufwerke, die nicht defragmentieren **NTFS**, **ReFS**, **Fat** oder **Fat32**.
- Mit WindowsServer 2008 R2, Windows Server 2008 und Windows Vista können Sie planen, um ein Volume defragmentiert. Allerdings können Sie keine planen Defragmentieren ein Solid State Drive (SSD) oder ein Volume auf einer virtuellen Festplatte (VHD), die sich auf einem SSD-befindet.
- Um diese Schritte ausführen zu können, müssen Sie auf dem lokalen Computer ein Mitglied der Gruppe %%amp;quot;Administratoren%%amp;quot; sein oder Ihnen muss die entsprechende Berechtigung übertragen worden sein. Wenn der Computer zu einer Domäne gehört, können möglicherweise Mitglieder der Gruppe "Domänen-Admins" dieses Verfahren ausführen. Als Security best Practices, sollten Sie verwenden **ausführenden** zum Ausführen dieses Verfahrens.
- Das Volume muss mindestens 15 % freier Speicherplatz für gibt **Defragmentieren** vollständig und ordnungsgemäß defragmentiert werden kann. **Defragmentieren** verwendet diesen als Sortierbereich zum Dateifragmente. Wenn ein Volume mit weniger als 15 % freien Speicherplatz, verfügt **Defragmentieren** wird nur teilweise defragmentiert werden. Um den freien Speicherplatz auf einem Volume zu erhöhen, nicht benötigte Dateien löschen, oder auf einen anderen Datenträger verschieben.
- Während **Defragmentieren** ist analysieren und Defragmentieren eines Volumes, einen blinkenden Cursor angezeigt. Wenn **Defragmentieren** ist fertig analysieren und Defragmentieren das Volume, er zeigt den Bericht, Defragmentierungsberichts oder beide Berichte, beendet das Hilfsprogramm dann to the commund Prompt.
- In der Standardeinstellung **Defragmentieren** wird eine Zusammenfassung der Analyse und die Defragmentierung Berichte angezeigt, wenn Sie nicht angeben der **/a** oder **/v** Parameter.
- Sie können die Berichte in eine Textdatei senden, indem Sie eingeben **>** <em>Dateiname.txt</em>, wobei *Dateiname.txt* ist ein Dateiname, die Sie angeben. Beispiel: `defrag volume /v > FileName.txt`
- Um die Defragmentierung ab, in der Befehlszeile zu unterbrechen, drücken Sie **STRG + C**.
- Ausführen der **Defragmentieren** Befehl und Defragmentierung schließen sich gegenseitig. Wenn Sie die Defragmentierung Defragmentieren ein Volumes verwenden und Ausführen der **Defragmentieren** -Befehl an einer Befehlszeile, die **Defragmentieren** Befehl schlägt fehl. Im Gegensatz dazu, wenn das Ausführen der **Defragmentieren** Befehl, und Öffnen von Defragmentierung, für die Defragmentierungsoptionen in der Defragmentierung nicht verfügbar sind.

## <a name="BKMK_examples"></a>Beispiele für
Geben Sie Folgendes ein, um das Volume auf dem Laufwerk C: zu defragmentieren und gleichzeitig ausgeführt und die ausführliche Ausgabe:
```
defrag C: /U /V
```
Geben Sie Folgendes ein, um die Volumes auf einem Laufwerk C und D parallel im Hintergrund zu defragmentieren:
```
defrag C: D: /M
```
Zum Durchführen einer Analyse der Fragmentierung eines Volumes auf Laufwerk C bereitgestellt, und geben Sie Status, geben Sie Folgendes ein:
```
defrag C: mountpoint /A /U
```
Um alle Volumes mit normaler Priorität zu defragmentieren, und geben Sie die ausführlichen Ausgabe, geben Sie Folgendes ein:
```
defrag /C /H /V
```

## <a name="BKMK_scheduledTask"></a>Geplante Aufgabe
Defragmentieren des Task ausgeführt wird als ein Wartungstask und wird in der Regel geplant, jede Woche auszuführen. Administrator kann die Häufigkeit mit ändern **Laufwerke optimieren** Anwendung.
- Wenn von den geplanten Task ausführen **Defragmentieren** hat folgende Richtlinie für SSDs:
   - **Traditionell Defragmentieren** (d. h. Verschieben von Dateien, um sie angemessen zusammenhängend zu machen) und **retrim** nur einmal monatlich ausgeführt wird.
   - Wenn beide **herkömmliche Defragmentieren** und **retrim** werden übersprungen, **Analysis** wird nicht ausgeführt.
      - Wenn Benutzer ausgeführt haben **herkömmliche Defragmentieren** manuell auf einem SSD-Speicher, z. B., drei Wochen nach der letzten geplanten task ausführen, und klicken Sie dann der nächsten geplante Task ausführen führt **Analysis** und **retrim** jedoch Überspringen Sie **herkömmliche Defragmentieren** auf dieser SSD.
   - Wenn **Analysis** wird übersprungen; das **der letzten Ausführung** Zeit in **Laufwerke optimieren** wird nicht aktualisiert werden.  Für SSDs der **der letzten Ausführung** Zeit in **Laufwerke optimieren** kann ein Monat Alt sein.
- Dieser Wartungstask möglicherweise alle Volumes, nicht zu Zeiten defragmentieren, da diese Aufgabe Folgendes durchführt:
   - Der Computer nicht aktiviert werden, um die Defragmentierung
   - Startet nur, wenn der Computer über das Netzteil ist, und wird beendet, wenn der Computer auf Akkubetrieb umschaltet
   - Wird beendet, wenn der Computer nicht mehr im Leerlauf befinden

## <a name="BKMK_additionalRef"></a>Zusätzliche Referenzen
-   [chkdsk](chkdsk.md)
-   [fsutil](fsutil.md)
-   [fsutil dirty](fsutil-dirty.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
