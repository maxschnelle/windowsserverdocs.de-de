---
title: rd
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 42e672f6-5bc2-4c16-af25-18e7ed2dd555
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb169a44f9613b237af71321f9619d9ea93a6912
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722645"
---
# <a name="rd"></a>rd



Löscht ein Verzeichnis. Dieser Befehl ist mit dem Befehl **rmdir** identisch.



## <a name="syntax"></a>Syntax

```
rd [<Drive>:]<Path> [/s [/q]]
rmdir [<Drive>:]<Path> [/s [/q]]
```

### <a name="parameters"></a>Parameter

|     Parameter     |                                                                 BESCHREIBUNG                                                                  |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [\<Laufwerk>:]<Path> |                      Gibt den Speicherort und den Namen des Verzeichnisses an, das Sie löschen möchten. Der *Pfad* ist erforderlich.                       |
|        /s         |                     Löscht eine Verzeichnisstruktur (das angegebene Verzeichnis und alle Unterverzeichnisse einschließlich aller Dateien).                      |
|        /q         | Gibt den stillen Modus an. Beim Löschen einer Verzeichnisstruktur wird nicht zur Bestätigung aufgefordert. (Beachten Sie, dass **/q** nur funktioniert, wenn **/s** angegeben wird.) |
|        /?         |                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                     |

## <a name="remarks"></a>Bemerkungen

-   Sie können kein Verzeichnis löschen, das Dateien enthält, einschließlich ausgeblendeter Dateien oder Systemdateien. Wenn Sie versuchen, dies zu tun, wird die folgende Meldung angezeigt:

    `The directory is not empty`

    Verwenden Sie den Befehl **dir/a** , um alle Dateien (einschließlich ausgeblendeter Dateien und Systemdateien) aufzulisten. Verwenden Sie dann den **atphb** -Befehl mit **-h** , um ausgeblendete Dateiattribute zu entfernen, **-s** , um Systemdatei Attribute zu entfernen, oder **-h-s** , um ausgeblendete Attribute und Dateiattribute zu entfernen Nachdem die ausgeblendeten Attribute und Dateien entfernt wurden, können Sie die Dateien löschen.
-   Wenn Sie einen umgekehrten Schrägstrich (\) am Anfang des *Pfads*) einfügen, wird der *Pfad* im Stammverzeichnis (unabhängig vom aktuellen Verzeichnis) gestartet.
-   Sie können **RD** nicht zum Löschen des aktuellen Verzeichnisses verwenden. Wenn Sie versuchen, das aktuelle Verzeichnis zu löschen, wird die folgende Fehlermeldung angezeigt:

    `The process cannot access the file because it is being used by another process.`

    Wenn Sie diese Fehlermeldung erhalten, müssen Sie in ein anderes Verzeichnis wechseln (kein Unterverzeichnis des aktuellen Verzeichnisses) und anschließend **RD** verwenden ( *Pfad* angeben, falls erforderlich).
-   Der **RD** -Befehl mit unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar.

## <a name="examples"></a>Beispiele

Das Verzeichnis, in dem Sie gerade arbeiten, kann nicht gelöscht werden. Sie müssen zu einem Verzeichnis wechseln, das sich nicht im aktuellen Verzeichnis befindet. Um z. b. in das übergeordnete Verzeichnis zu wechseln, geben Sie Folgendes ein:
```
cd ..
```
Sie können das gewünschte Verzeichnis nun sicher entfernen.

Verwenden Sie die **/s** -Option, um eine Verzeichnisstruktur zu entfernen. Wenn Sie z. b. ein Verzeichnis mit dem Namen Test (und alle zugehörigen Unterverzeichnisse und Dateien) aus dem aktuellen Verzeichnis entfernen möchten, geben Sie Folgendes ein:
```
rd /s test
```
Um das vorherige Beispiel im stillen Modus auszuführen, geben Sie Folgendes ein:
```
rd /s /q test
```

> [!CAUTION]
> Wenn Sie **RD/s** im stillen Modus ausführen, wird die gesamte Verzeichnisstruktur ohne Bestätigung gelöscht. Stellen Sie sicher, dass wichtige Dateien verschoben oder gesichert werden, bevor Sie die Befehlszeilenoption **/q** verwenden.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)