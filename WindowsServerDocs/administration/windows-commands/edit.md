---
title: Bearbeiten
description: Referenz Artikel für den Edit-Befehl, der den MS-DOS-Editor startet, damit Sie ASCII-Textdateien erstellen und ändern können.
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 58d2819e9a96d30e1c4fc286679fbd807ad0caa1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890713"
---
# <a name="edit"></a>Bearbeiten

Startet den MS-DOS-Editor, mit dem ASCII-Textdateien erstellt und geändert werden.

## <a name="syntax"></a>Syntax

```
edit [/b] [/h] [/r] [/s] [/<nnn>] [[<drive>:][<path>]<filename> [<filename2> [...]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `[<drive>:][<path>]<filename> [<filename2> [...]]` | Gibt den Speicherort und den Namen einer oder mehrerer ASCII-Textdateien an. Wenn die Datei nicht vorhanden ist, wird Sie vom MS-DOS-Editor erstellt. Wenn die Datei vorhanden ist, wird Sie vom MS-DOS-Editor geöffnet, und der Inhalt wird auf dem Bildschirm angezeigt. Die *filename* -Option kann Platzhalter Zeichen (**&#42;** und **?**) enthalten. Trennen Sie mehrere Dateinamen mit Leerzeichen. |
| /b | Erzwingt den Monochrom-Modus, sodass der MS-DOS-Editor in schwarz und weiß angezeigt wird. |
| /h | Zeigt die maximale Anzahl von Zeilen an, die für den aktuellen Monitor möglich sind. |
| /r | Lädt Dateien im schreibgeschützten Modus. |
| /s | Erzwingt die Verwendung von kurzen Dateinamen. |
| `<nnn>` | Lädt Binärdateien und umwickelt Zeilen in *nnn* -Zeichen breit. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn Sie weitere Hilfe benötigen, öffnen Sie den MS-DOS-Editor, und drücken Sie dann die F1-Taste.

- Einige Monitore unterstützen standardmäßig nicht die Anzeige von Tastenkombinationen. Wenn der Monitor keine Tastenkombinationen anzeigt, verwenden Sie **/b**.

### <a name="examples"></a>Beispiele

Geben Sie zum Öffnen des MS-DOS-Editors Folgendes ein:

```
edit
```

Geben Sie Folgendes ein, um eine Datei mit dem Namen *newtextfile.txt* im aktuellen Verzeichnis zu erstellen und zu bearbeiten:

```
edit newtextfile.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
