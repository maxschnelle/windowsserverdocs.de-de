---
title: del
description: Referenz Artikel für den Befehl "del", mit dem eine oder mehrere Dateien gelöscht werden.
ms.topic: reference
ms.assetid: 346eede2-2085-44f5-9936-6877b5d5a833
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bb7c060dbcfe4d08018b5616e5227b64a0434e28
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628896"
---
# <a name="del"></a>del

Löscht eine oder mehrere Dateien. Dieser Befehl führt dieselben Aktionen aus wie der **Lösch** Befehl.

Der Befehl " **del** " kann auch in der Windows-Wiederherstellungskonsole mit unterschiedlichen Parametern ausgeführt werden. Weitere Informationen finden Sie in der [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

> [!WARNING]
> Wenn Sie die **Datei zum Löschen** einer Datei auf dem Datenträger verwenden, können Sie Sie nicht abrufen.

## <a name="syntax"></a>Syntax

```
del [/p] [/f] [/s] [/q] [/a[:]<attributes>] <names>
erase [/p] [/f] [/s] [/q] [/a[:]<attributes>] <names>
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

#### <a name="remarks"></a>Hinweise

- Wenn Sie den `del /p` Befehl verwenden, wird die folgende Meldung angezeigt:

    `FileName, Delete (Y/N)?`

    Drücken Sie **Y**, um den Löschvorgang zu bestätigen. Um den Löschvorgang abzubrechen und den nächsten Dateinamen anzuzeigen (wenn Sie eine Gruppe von Dateien angegeben haben), drücken Sie **N**. Drücken Sie STRG + C, um den Befehl " **del** " anzuhalten.

- Wenn Sie die Befehls Erweiterung deaktivieren, zeigt der **/s** -Parameter die Namen aller Dateien an, die nicht gefunden wurden, anstatt die Namen der Dateien anzuzeigen, die gelöscht werden.

- Wenn Sie bestimmte Ordner im- `<names>` Parameter angeben, werden auch alle enthaltenen Dateien gelöscht. Wenn Sie z. b. alle Dateien im Ordner " *\Work* " löschen möchten, geben Sie Folgendes ein:

  ```
  del \work
  ```

- Sie können Platzhalter (**&#42;** und **?**) verwenden, um mehrere Dateien gleichzeitig zu löschen. Um zu vermeiden, dass Dateien unbeabsichtigt gelöscht werden, sollten Sie Platzhalter jedoch vorsichtig verwenden. Wenn Sie z. b. den folgenden Befehl eingeben:

  ```
  del *.*
  ```

  Der Befehl " **del** " zeigt die folgende Eingabeaufforderung an:

  `Are you sure (Y/N)?`

  Wenn Sie alle Dateien im aktuellen Verzeichnis löschen möchten, drücken Sie **Y** , und drücken Sie dann die EINGABETASTE. Drücken Sie zum Abbrechen des Löschvorgangs **N** , und drücken Sie dann die EINGABETASTE.

  > [!NOTE]
  > Bevor Sie mit dem Befehl " **del** " Platzhalter Zeichen verwenden, verwenden Sie die gleichen Platzhalter Zeichen mit dem Befehl " **dir** ", um alle Dateien aufzulisten, die gelöscht werden.

## <a name="examples"></a>Beispiele

Wenn Sie alle Dateien in einem Ordner mit dem Namen Test auf Laufwerk C löschen möchten, geben Sie eine der folgenden Optionen ein:

```
del c:\test
del c:\test\*.*
```

Wenn Sie alle Dateien mit der Dateinamenerweiterung ". bat" aus dem aktuellen Verzeichnis löschen möchten, geben Sie Folgendes ein:

```
del *.bat
```

Wenn Sie alle schreibgeschützten Dateien im aktuellen Verzeichnis löschen möchten, geben Sie Folgendes ein:

```
del /a:r *.*
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)
