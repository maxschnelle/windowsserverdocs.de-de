---
title: compact
description: Referenz Artikel für den Compact-Befehl, der die Komprimierung von Dateien oder Verzeichnissen auf NTFS-Partitionen anzeigt oder ändert.
ms.topic: reference
ms.assetid: 429b3752-df0a-43a4-a210-df2f3ad03c3b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 210aaf8c20741659bb29d4855ae39099c964a400
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025944"
---
# <a name="compact"></a>compact

Zeigt die Komprimierung von Dateien oder Verzeichnissen auf NTFS-Partitionen an oder ändert diese. Bei Verwendung ohne Parameter zeigt **Compact** den Komprimierungs Status des aktuellen Verzeichnisses und der darin enthaltenen Dateien an.

## <a name="syntax"></a>Syntax

```
compact [/c | /u] [/s[:<dir>]] [/a] [/i] [/f] [/q] [<filename>[...]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /C | Komprimiert das angegebene Verzeichnis oder die angegebene Datei. |
| /U | Deinstalkomprimiert das angegebene Verzeichnis oder die angegebene Datei. |
| /s [: `<dir>` ] | Wendet den **Compact** -Befehl auf alle Unterverzeichnisse des angegebenen Verzeichnisses an (bzw. auf das aktuelle Verzeichnis, wenn kein Wert angegeben ist). |
| /a | Zeigt ausgeblendete oder Systemdateien an. |
| /i | Ignoriert Fehler. |
| /f | Erzwingt die Komprimierung oder Dekomprimierung des angegebenen Verzeichnisses oder der Datei. **/f** wird im Fall einer Datei verwendet, die teilweise komprimiert wurde, als der Vorgang durch einen Systemabsturz unterbrochen wurde. Um zu erzwingen, dass die Datei vollständig komprimiert wird, verwenden Sie die Parameter **/c** und **/f** , und geben Sie die teilweise komprimierte Datei an. |
| /q | Meldet nur die wichtigsten Informationen. |
| `<filename>` | Gibt die Datei oder das Verzeichnis an. Sie können mehrere Dateinamen verwenden, und die **&#42;** und **?** Platzhalter Zeichen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Dieser Befehl ist die Befehlszeilenversion des NTFS-Dateisystem Komprimierungs Features. Der Komprimierungs Status eines Verzeichnisses gibt an, ob Dateien automatisch komprimiert werden, wenn Sie dem Verzeichnis hinzugefügt werden. Wenn Sie den Komprimierungs Status eines Verzeichnisses festlegen, wird der Komprimierungs Status von Dateien, die sich bereits im Verzeichnis befinden, nicht notwendigerweise geändert.

- Mit diesem Befehl können Sie mithilfe von DriveSpace oder DoubleSpace komprimierte Volumes nicht lesen, schreiben oder einbinden. Sie können diesen Befehl auch nicht verwenden, um FAT-oder FAT32-Partitionen zu komprimieren.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Komprimierungs Status des aktuellen Verzeichnisses, seiner Unterverzeichnisse und vorhandener Dateien festzulegen:

```
compact /c /s
```

Um den Komprimierungs Status von Dateien und Unterverzeichnissen innerhalb des aktuellen Verzeichnisses festzulegen, ohne den Komprimierungs Status des aktuellen Verzeichnisses zu ändern, geben Sie Folgendes ein:

```
compact /c /s *.*
```

Zum Komprimieren eines Volumes geben Sie aus dem Stammverzeichnis des Volumes Folgendes ein:

```
compact /c /i /s:\
```

> [!NOTE]
> In diesem Beispiel wird der Komprimierungs Status aller Verzeichnisse (einschließlich des Stamm Verzeichnisses auf dem Volume) festgelegt und jede Datei auf dem Volume komprimiert. Der **/i** -Parameter verhindert, dass Fehlermeldungen den Komprimierungs Prozess unterbrechen.

Wenn Sie alle Dateien mit der Dateinamenerweiterung ". bmp" im Verzeichnis "" \tmp "und alle Unterverzeichnisse von" \tmp komprimieren möchten, ohne das komprimierte Attribut der Verzeichnisse zu ändern, geben Sie Folgendes ein:

```
compact /c /s:\tmp *.bmp
```

Um das vollständige Komprimieren der Datei *zebra.bmp*zu erzwingen, die während eines Systemabsturzes teilweise komprimiert wurde, geben Sie Folgendes ein:

```
compact /c /f zebra.bmp
```

Um das komprimierte Attribut aus dem Verzeichnis "c:\tmp" zu entfernen, ohne den Komprimierungs Status von Dateien in diesem Verzeichnis zu ändern, geben Sie Folgendes ein:

```
compact /u c:\tmp
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)