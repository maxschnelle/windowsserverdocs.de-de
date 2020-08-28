---
title: replace
description: Referenz Artikel für den Replace-Befehl, der vorhandene Dateien ersetzen oder neue Dateien zu einem Verzeichnis hinzufügen kann.
ms.topic: reference
ms.assetid: 6143661e-d90f-4812-b265-6669b567dd1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 5dfab76427a8f91339c29ac37607ce422d4f7e39
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037018"
---
# <a name="replace"></a>replace

Ersetzen vorhandener Dateien in einem Verzeichnis. Bei Verwendung mit der **/a** -Option werden durch diesen Befehl neue Dateien zu einem Verzeichnis hinzugefügt, anstatt vorhandene Dateien zu ersetzen.

## <a name="syntax"></a>Syntax

```
replace [<drive1>:][<path1>]<filename> [<drive2>:][<path2>] [/a] [/p] [/r] [/w]
replace [<drive1>:][<path1>]<filename> [<drive2>:][<path2>] [/p] [/r] [/s] [/w] [/u]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| `[<drive1>:][<path1>]<filename>` | Gibt den Speicherort und den Namen der Quelldatei oder des Satzes von Dateien an. Die *filename* -Option ist erforderlich und kann Platzhalter Zeichen (**&#42;** und **?**) enthalten. |
| `[<drive2>:][<path2>]` | Gibt den Speicherort der Zieldatei an. Sie können keinen Dateinamen für die Dateien angeben, die Sie ersetzen. Wenn Sie kein Laufwerk oder einen Pfad angeben, verwendet dieser Befehl das aktuelle Laufwerk und Verzeichnis als Ziel. |
| /a | Fügt dem Zielverzeichnis neue Dateien hinzu, anstatt vorhandene Dateien zu ersetzen. Sie können diese Befehlszeilenoption nicht mit der Befehlszeilenoption **/s** oder **/u** verwenden. |
| /p | Sie werden zur Bestätigung aufgefordert, bevor Sie eine Zieldatei ersetzen oder eine Quelldatei hinzufügen. |
| /r | Ersetzt schreibgeschützte und ungeschützte Dateien. Wenn Sie versuchen, eine schreibgeschützte Datei zu ersetzen, aber **/r**nicht angeben, wird ein Fehler ausgegeben, und der Ersetzungs Vorgang wird beendet. |
| /w | Wartet darauf, dass Sie vor Beginn der Suche nach Quelldateien einen Datenträger einfügen. Wenn Sie **/w**nicht angeben, beginnt dieser Befehl mit dem ersetzen oder Hinzufügen von Dateien, sobald Sie die EINGABETASTE gedrückt haben. |
| /s | Durchsucht alle Unterverzeichnisse im Zielverzeichnis und ersetzt übereinstimmende Dateien. **/S** kann nicht mit der Befehlszeilenoption **/a** verwendet werden. Der Befehl durchsucht keine Unterverzeichnisse, die in *Path1*angegeben sind. |
| /U | Ersetzt nur die Dateien im Zielverzeichnis, die älter sind als die im Quellverzeichnis. **/U** kann nicht mit der Befehlszeilenoption **/a** verwendet werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Da mit diesem Befehl Dateien hinzugefügt oder ersetzt werden, werden die Dateinamen auf dem Bildschirm angezeigt. Nachdem dieser Befehl ausgeführt wurde, wird eine Zusammenfassungs Zeile in einem der folgenden Formate angezeigt:

  ```
  nnn files added
  nnn files replaced
  no file added
  no file replaced
  ```

- Wenn Sie Disketten verwenden und beim Ausführen dieses Befehlsdaten Träger wechseln müssen, können Sie die Befehlszeilenoption **/w** angeben, damit dieser Befehl darauf wartet, dass Sie die Datenträger wechseln.

- Mit diesem Befehl können Sie ausgeblendete Dateien oder Systemdateien nicht aktualisieren.

- Die folgende Tabelle zeigt jeden Exitcode und eine kurze Beschreibung seiner Bedeutung:

  | Exitcode | BESCHREIBUNG |
  |--|--|
  | 0 | Mit diesem Befehl wurden die Dateien erfolgreich ersetzt oder hinzugefügt. |
  | 1 | Bei diesem Befehl ist eine falsche Version von MS-DOS aufgetreten. |
  | 2 | Mit diesem Befehl konnten die Quelldateien nicht gefunden werden. |
  | 3 | Dieser Befehl konnte den Quell-oder Zielpfad nicht finden. |
  | 5 | Der Benutzer hat keinen Zugriff auf die Dateien, die Sie ersetzen möchten. |
  | 8 | Es ist nicht genügend System Arbeitsspeicher vorhanden, um den Befehl auszuführen. |
  | 11 | Der Benutzer hat die falsche Syntax in der Befehlszeile verwendet. |

> [!NOTE]
> Sie können den ERRORLEVEL-Parameter in der **if** -Befehlszeile in einem Batch Programm verwenden, um Exitcodes zu verarbeiten, die von diesem Befehl zurückgegeben werden.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Versionen einer Datei mit dem Namen " *Phones. CLI* " (die in mehreren Verzeichnissen auf Laufwerk C:) angezeigt wird, mit der neuesten Version der Datei " *Phones. CLI* " von einer Diskette in Laufwerk a: zu aktualisieren:

```
replace a:\phones.cli c:\ /s
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
