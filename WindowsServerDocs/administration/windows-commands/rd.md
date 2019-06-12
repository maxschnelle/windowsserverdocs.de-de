---
title: rd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42e672f6-5bc2-4c16-af25-18e7ed2dd555
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94231e3ec032280beb91a14db7949a1296c2d811
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442028"
---
# <a name="rd"></a>rd



Löscht ein Verzeichnis. Dieser Befehl ist identisch mit der **Rmdir** Befehl.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
rd [<Drive>:]<Path> [/s [/q]]
rmdir [<Drive>:]<Path> [/s [/q]]
```

## <a name="parameters"></a>Parameter

|     Parameter     |                                                                 Beschreibung                                                                  |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [\<Drive>:]<Path> |                      Gibt den Speicherort und den Namen des Verzeichnisses, das Sie löschen möchten. *Pfad* ist erforderlich.                       |
|        /s         |                     Löscht eine Verzeichnisstruktur (das angegebene Verzeichnis und allen seinen Unterverzeichnisse, einschließlich aller Dateien).                      |
|        /q         | Gibt den stillen Modus. Wird nicht zur Bestätigung aufgefordert werden, wenn Sie eine Verzeichnisstruktur zu löschen. (Beachten Sie, dass **/q /** funktioniert nur, wenn **/s** angegeben ist.) |
|        /?         |                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                     |

## <a name="remarks"></a>Hinweise

-   Sie können nicht gelöscht, ein Verzeichnis mit Dateien, einschließlich der ausgeblendeten oder Systemdateien. Wenn Sie versuchen möchten, wird die folgende Meldung angezeigt:

    `The directory is not empty`

    Verwenden der **Dir/a** Befehl zum Auflisten aller Dateien (einschließlich der ausgeblendete Dateien und Systemdateien). Verwenden Sie dann die **Attrib** Befehl **-h** versteckte Dateiattribute zu entfernen **-s** System Dateiattribute, entfernen oder **-h -s** entfernen Beide ausgeblendet und Dateiattributen System. Nach dem Ausblend- und Attribute der Datei entfernt wurden, können Sie die Dateien löschen.
-   Wenn Sie einen umgekehrten Schrägstrich (\) am Anfang des *Pfad*, *Pfad* beginnt im Stammverzeichnis (unabhängig vom aktuellen Verzeichnis).
-   Sie können keine **rd** im aktuelle Verzeichnis zu löschen. Wenn Sie versuchen, die das aktuelle Verzeichnis zu löschen, wird die folgende Fehlermeldung angezeigt:

    `The process cannot access the file because it is being used by another process.`

    Wenn Sie diese Fehlermeldung erhalten, müssen Sie in ein anderes Verzeichnis (kein Unterverzeichnis des aktuellen Verzeichnisses) ändern und dann **rd** (Geben Sie *Pfad* bei Bedarf).
-   Die **rd** -Befehl, mit verschiedenen Parametern finden Sie in der Wiederherstellungskonsole.

## <a name="BKMK_examples"></a>Beispiele für

Das Verzeichnis, das Sie gerade arbeiten, kann nicht gelöscht werden. Sie müssen in einem Verzeichnis ändern, die nicht im aktuellen Verzeichnis vorhanden ist. Geben Sie beispielsweise, um in das übergeordnete Verzeichnis zu ändern:
```
cd ..
```
Sie können jetzt problemlos auf das gewünschte Verzeichnis entfernen.

Verwenden der **/s** Option zum Entfernen einer Verzeichnisstruktur. Z. B. So entfernen Sie ein Verzeichnis namens Test (und alle seine Unterverzeichnisse und Dateien) aus dem aktuellen Verzeichnis, Typ:
```
rd /s test
```
Um das vorherige Beispiel im stillen Modus auszuführen, geben Sie Folgendes ein:
```
rd /s /q test
```

> [!CAUTION]
> Beim Ausführen von **rd/s** im stillen Modus, wird die gesamte Verzeichnisstruktur ohne Bestätigung gelöscht. Stellen Sie sicher, dass wichtige Dateien verschoben oder gesichert, bevor Sie mit der **/q /** Befehlszeilenoption.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)