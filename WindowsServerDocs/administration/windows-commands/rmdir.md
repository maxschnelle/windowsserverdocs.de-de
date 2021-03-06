---
title: rmdir
description: Referenz Artikel zum rmdir-Befehl, mit dem ein Verzeichnis gelöscht wird.
ms.topic: reference
ms.assetid: e4d7162b-7132-413c-a416-6eb3dc032a26
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 524ca632c11c7d861ed431c4bc86dbdb2b35abc8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640284"
---
# <a name="rmdir"></a>rmdir

Löscht ein Verzeichnis.

Der **rmdir** -Befehl kann auch in der Windows-Wiederherstellungskonsole mithilfe verschiedener Parameter ausgeführt werden. Weitere Informationen finden Sie in der [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

> [!NOTE]
> Dieser Befehl ist mit dem RD- [Befehl](rd.md)identisch.

## <a name="syntax"></a>Syntax

```
rmdir [<drive>:]<path> [/s [/q]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `[<drive>:]<path>` | Gibt den Speicherort und den Namen des Verzeichnisses an, das Sie löschen möchten. Der *Pfad* ist erforderlich. Wenn Sie einen umgekehrten Schrägstrich ( \) am Anfang des angegebenen *Pfads*) einschließen, wird der *Pfad* im Stammverzeichnis (unabhängig vom aktuellen Verzeichnis) gestartet. |
| /s | Löscht eine Verzeichnisstruktur (das angegebene Verzeichnis und alle Unterverzeichnisse einschließlich aller Dateien). |
| /q | Gibt den stillen Modus an. Beim Löschen einer Verzeichnisstruktur wird nicht zur Bestätigung aufgefordert. Der **/q** -Parameter funktioniert nur, wenn **/s** ebenfalls angegeben wird.<p>**Vorsicht:** Wenn Sie im stillen Modus ausführen, wird die gesamte Verzeichnisstruktur ohne Bestätigung gelöscht. Stellen Sie sicher, dass wichtige Dateien verschoben oder gesichert werden, bevor Sie die Befehlszeilenoption **/q** verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Sie können kein Verzeichnis löschen, das Dateien enthält, einschließlich ausgeblendeter Dateien oder Systemdateien. Wenn Sie versuchen, dies zu tun, wird die folgende Meldung angezeigt:

    `The directory is not empty`

    Verwenden Sie den Befehl **dir/a** , um alle Dateien (einschließlich ausgeblendeter Dateien und Systemdateien) aufzulisten. Verwenden Sie dann den **atphb** -Befehl mit **-h** , um ausgeblendete Dateiattribute zu entfernen, **-s** , um Systemdatei Attribute zu entfernen, oder **-h-s** , um ausgeblendete Attribute und Dateiattribute zu entfernen Nachdem die ausgeblendeten Attribute und Dateien entfernt wurden, können Sie die Dateien löschen.

- Sie können den **rmdir** -Befehl nicht verwenden, um das aktuelle Verzeichnis zu löschen. Wenn Sie versuchen, das aktuelle Verzeichnis zu löschen, wird die folgende Fehlermeldung angezeigt:

    `The process can't access the file because it is being used by another process.`

    Wenn Sie diese Fehlermeldung erhalten, müssen Sie in ein anderes Verzeichnis wechseln (kein Unterverzeichnis des aktuellen Verzeichnisses), und wiederholen Sie dann den Vorgang.

## <a name="examples"></a>Beispiele

Um zum übergeordneten Verzeichnis zu wechseln, damit Sie das gewünschte Verzeichnis sicher entfernen können, geben Sie Folgendes ein:

```
cd ..
```

Geben Sie Folgendes ein, um ein Verzeichnis mit dem Namen " *Test* " (und alle zugehörigen Unterverzeichnisse und Dateien) aus dem aktuellen Verzeichnis zu entfernen:

```
rmdir /s test
```

Um das vorherige Beispiel im stillen Modus auszuführen, geben Sie Folgendes ein:

```
rmdir /s /q test
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
