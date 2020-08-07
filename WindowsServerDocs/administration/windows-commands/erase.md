---
title: erase
description: Referenz Artikel für den Löschbefehl, mit dem eine oder mehrere Dateien gelöscht werden.
ms.topic: article
ms.assetid: 024a4d0f-8679-4e06-b46f-61fdaf5464bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 144575c1886206ada0cbfd8edbe8571337b37ed9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890597"
---
# <a name="erase"></a>erase

Löscht eine oder mehrere Dateien. Wenn Sie **Erase** zum Löschen einer Datei auf dem Datenträger verwenden, können Sie Sie nicht abrufen.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl " [del](del.md)" identisch.


## <a name="syntax"></a>Syntax

```
erase [/p] [/f] [/s] [/q] [/a[:]<attributes>] <names>
del [/p] [/f] [/s] [/q] [/a[:]<attributes>] <names>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<names>` | Gibt eine Liste von mindestens einer Datei oder einem Verzeichnis an. Platzhalter können verwendet werden, um mehrere Dateien zu löschen. Wenn ein Verzeichnis angegeben wird, werden alle Dateien im Verzeichnis gelöscht. |
| /p | Fordert vor dem Löschen der angegebenen Datei eine Bestätigung an. |
| /f | Erzwingt das Löschen Schreib geschützter Dateien. |
| /s | Löscht die angegebenen Dateien aus dem aktuellen Verzeichnis und allen Unterverzeichnissen. Zeigt die Namen der Dateien an, während Sie gelöscht werden. |
| /q | Gibt den stillen Modus an. Sie werden nicht zur Bestätigung des Löschvorgangs aufgefordert. |
| /a [:]`<attributes>` | Löscht Dateien basierend auf den folgenden Dateiattributen:<ul><li>schreibgeschützte **r** -Dateien</li><li>**h** ausgeblendete Dateien</li><li>indizierte Dateien **sind nicht Inhalts**</li><li>**s** -System Dateien</li><li>**Dateien,** die für die Archivierung bereit sind</li><li>**l** -Analyse Punkte</li><li>**-** Wird als Präfix mit der Bedeutung "Not" verwendet.</li></ul>. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn Sie den `erase /p` Befehl verwenden, wird die folgende Meldung angezeigt:

    `FileName, Delete (Y/N)?`

    Drücken Sie **Y**, um den Löschvorgang zu bestätigen. Um den Löschvorgang abzubrechen und den nächsten Dateinamen anzuzeigen (wenn Sie eine Gruppe von Dateien angegeben haben), drücken Sie **N**. Drücken Sie zum Abbrechen des **Lösch** Befehls STRG + C.

- Wenn Sie die Befehls Erweiterung deaktivieren, zeigt der **/s** -Parameter die Namen aller Dateien an, die nicht gefunden wurden, anstatt die Namen der Dateien anzuzeigen, die gelöscht werden.

- Wenn Sie bestimmte Ordner im- `<names>` Parameter angeben, werden auch alle enthaltenen Dateien gelöscht. Wenn Sie z. b. alle Dateien im Ordner " *\Work* " löschen möchten, geben Sie Folgendes ein:

  ```
  erase \work
  ```

- Sie können Platzhalter (**&#42;** und **?**) verwenden, um mehrere Dateien gleichzeitig zu löschen. Um zu vermeiden, dass Dateien unbeabsichtigt gelöscht werden, sollten Sie Platzhalter jedoch vorsichtig verwenden. Wenn Sie z. b. den folgenden Befehl eingeben:

  ```
  erase *.*
  ```

  Der Befehl " **Erase** " zeigt die folgende Eingabeaufforderung an:

  `Are you sure (Y/N)?`

  Wenn Sie alle Dateien im aktuellen Verzeichnis löschen möchten, drücken Sie **Y** , und drücken Sie dann die EINGABETASTE. Drücken Sie zum Abbrechen des Löschvorgangs **N** , und drücken Sie dann die EINGABETASTE.

  > [!NOTE]
  > Bevor Sie mit dem Befehl " **Erase** " Platzhalter Zeichen verwenden, verwenden Sie die gleichen Platzhalter Zeichen mit dem Befehl " **dir** ", um alle Dateien aufzulisten, die gelöscht werden.

### <a name="examples"></a>Beispiele

Wenn Sie alle Dateien in einem Ordner mit dem Namen Test auf Laufwerk C löschen möchten, geben Sie eine der folgenden Optionen ein:

```
erase c:\test
erase c:\test\*.*
```

Wenn Sie alle Dateien mit der Dateinamenerweiterung ". bat" aus dem aktuellen Verzeichnis löschen möchten, geben Sie Folgendes ein:

```
erase *.bat
```

Wenn Sie alle schreibgeschützten Dateien im aktuellen Verzeichnis löschen möchten, geben Sie Folgendes ein:

```
erase /a:r *.*
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "del"](del.md)