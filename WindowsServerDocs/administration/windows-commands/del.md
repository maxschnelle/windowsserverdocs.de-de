---
title: del
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 346eede2-2085-44f5-9936-6877b5d5a833
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1c2756e53d9f047160ddd037b3868e47d6e3181
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822991"
---
# <a name="del"></a>del



Löscht eine oder mehrere Dateien. Dieser Befehl ist identisch mit der **löschen** Befehl.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
del [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
erase [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Names>|Gibt eine Liste der eine oder mehrere Dateien oder Verzeichnisse. Platzhalter können verwendet werden, um mehrere Dateien zu löschen. Wenn ein Verzeichnis angegeben ist, werden alle Dateien im Verzeichnis gelöscht.|
|/p|Eingabeaufforderungen zur Bestätigung vor dem Löschen der angegebenen Datei.|
|/f|Erzwingt das Löschen von Dateien als schreibgeschützt.|
|/s|Löscht die angegebenen Dateien aus dem aktuellen Verzeichnis und alle Unterverzeichnisse. Zeigt den Namen der Dateien an, wie sie gelöscht werden.|
|/q|Gibt den stillen Modus. Sie sind nicht für Delete-Bestätigung aufgefordert.|
|/ a [:]\<Attribute >|Löscht Dateien basierend auf die folgenden Attribute:</br>**R** schreibgeschützte Dateien</br>**h** auflisten versteckter Dateien</br>**ich** Inhalte nicht indizierte Dateien</br>**s** Systemdateien</br>**eine** Dateien archiviert</br>**l** Analysepunkte</br>-Präfix, d. h. 'nicht'|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

> [!CAUTION]
> Bei Verwendung von **del** um eine Datei vom Datenträger zu löschen, Sie können nicht abrufen.
-   Bei Verwendung von **/p**, **del** zeigt den Namen einer Datei, und sendet Sie die folgende Meldung:

    `FileName, Delete (Y/N)?`

    Drücken Sie Y, um den Löschvorgang zu bestätigen. Zum Abbrechen der Löschung und der Anzeige der nächsten Dateinamen (d.h., wenn Sie eine Gruppe von Dateien angegeben), drücken Sie N. Zum Beenden der **del** Befehl ist, drücken Sie STRG + C.
-   Wenn Sie befehlserweiterungen deaktivieren **/s** zeigt die Namen von Dateien, die nicht gefunden wurden, anstatt die Namen der Dateien, die gelöscht werden (d. h. das Verhalten wird umgekehrt).
-   Wenn Sie einen Ordner im angeben *Namen*, alle Dateien im Ordner werden gelöscht. Der folgende Befehl löscht beispielsweise alle Dateien im Ordner "\Work":  
    ```
    del \work
    ```  
-   Sie können Platzhalter verwenden (**&#42;** und **?**) auf mehrere Dateien gleichzeitig löschen. Um zu vermeiden, versehentlich Dateien gelöscht, Sie sollten jedoch verwenden Platzhalter mit Vorsicht bei der **del** Befehl. Angenommen, wenn Sie den folgenden Befehl eingeben:  
    ```
    del *.*
    ```  
    Die **del** Befehl wird die folgende Eingabeaufforderung angezeigt:

    `Are you sure (Y/N)?`

    Um alle Dateien im aktuellen Verzeichnis zu löschen, drücken Sie Y, und drücken Sie dann die EINGABETASTE. Geben Sie um den Löschvorgang abzubrechen, drücken Sie N, und drücken Sie dann aus.

> [!NOTE]
> Vor der Verwendung von Platzhalterzeichen mit dem **del** Befehl können Sie die gleichen Platzhalterzeichen mit der **Dir** Befehl, um alle Dateien aufzulisten, die gelöscht werden.
-   Die **del** -Befehl, mit verschiedenen Parametern finden Sie in der Wiederherstellungskonsole.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie eine der folgenden Schritte aus, um alle Dateien in einen Ordner namens Test auf Laufwerk C zu löschen:
```
del c:\test
del c:\test\*.*
```
Um alle Dateien mit der Erweiterung .bat aus dem aktuellen Verzeichnis zu löschen, geben Sie Folgendes ein:
```
del *.bak
```
Um alle schreibgeschützten Dateien im aktuellen Verzeichnis zu löschen, geben Sie Folgendes ein:
```
del /a:r *.*
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)