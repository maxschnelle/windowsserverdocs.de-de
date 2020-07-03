---
title: CD
description: Referenz Artikel für den CD-Befehl, der den Namen des aktuellen Verzeichnisses anzeigt oder ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 932d9cc1-3dff-40da-835c-1cb0894874f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37ce63cd4fce871c615ac64756f8fc17f1d28460
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922910"
---
# <a name="cd"></a>CD

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt den Namen des aktuellen Verzeichnisses an oder ändert das aktuelle Verzeichnis. Bei Verwendung mit nur einem Laufwerk Buchstaben (z. b. `cd C:` ) zeigt **CD** die Namen des aktuellen Verzeichnisses auf dem angegebenen Laufwerk an. Bei Verwendung ohne Parameter zeigt **CD** das aktuelle Laufwerk und Verzeichnis an.

> [!NOTE]
> Dieser Befehl ist mit dem ["chdir"-Befehl](chdir.md)identisch.

## <a name="syntax"></a>Syntax

```
cd [/d] [<drive>:][<path>]
cd [..]
chdir [/d] [<drive>:][<path>]
chdir [..]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /d | Ändert das aktuelle Laufwerk und das aktuelle Verzeichnis für ein Laufwerk. |
| `<drive>:` | Gibt das anzuzeigende oder zu ändernde Laufwerk an (wenn sich das aktuelle Laufwerk unterscheidet). |
| `<path>` | Gibt den Pfad zu dem Verzeichnis an, das Sie anzeigen oder ändern möchten. |
| [..] | Gibt an, dass Sie in den übergeordneten Ordner wechseln möchten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

Wenn Befehls Erweiterungen aktiviert sind, gelten die folgenden Bedingungen für den Befehl **CD** :

- Die aktuelle Verzeichnis Zeichenfolge wird so konvertiert, dass Sie dieselbe Groß-/Kleinschreibung wie die Namen auf dem Datenträger Beispielsweise `cd c:\temp` würde das aktuelle Verzeichnis auf "c:\temp" festlegen, wenn dies auf dem Datenträger der Fall ist.

- Leerzeichen werden nicht als Trennzeichen behandelt und `<path>` können daher Leerzeichen ohne schließende Anführungszeichen enthalten. Beispiel:

  ```
  cd username\programs\start menu
  ```

  der gleiche wie:

  ```
  cd "username\programs\start menu"
  ```

  Wenn Erweiterungen deaktiviert sind, sind die Anführungszeichen erforderlich.

- Um Befehls Erweiterungen zu deaktivieren, geben Sie Folgendes ein:

  ```
  cmd /e:off
  ```

## <a name="examples"></a>Beispiele

Um zum Stammverzeichnis zurückzukehren, der oberste Teil der Verzeichnishierarchie für ein Laufwerk:

```
cd\
```

So ändern Sie das Standardverzeichnis auf einem anderen Laufwerk als das, auf dem Sie sich befinden:

```
cd [<drive>:[<directory>]]
```

Um die Änderung am Verzeichnis zu überprüfen, geben Sie Folgendes ein:

```
cd [<drive>:]
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- ["chdir"-Befehl](chdir.md)
