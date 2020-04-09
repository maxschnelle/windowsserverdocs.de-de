---
title: del
description: Windows-Befehls Thema für del, mit dem eine oder mehrere Dateien gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 346eede2-2085-44f5-9936-6877b5d5a833
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7069ee50a810296d31e1a034b24955299918020a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846663"
---
# <a name="del"></a>del

Löscht eine oder mehrere Dateien. Dieser Befehl ist mit dem Befehl zum **Löschen** identisch.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
del [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
erase [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Namen >|Gibt eine Liste von mindestens einer Datei oder einem Verzeichnis an. Platzhalter können verwendet werden, um mehrere Dateien zu löschen. Wenn ein Verzeichnis angegeben wird, werden alle Dateien im Verzeichnis gelöscht.|
|/p|Fordert vor dem Löschen der angegebenen Datei eine Bestätigung an.|
|/f|Erzwingt das Löschen Schreib geschützter Dateien.|
|/s|Löscht die angegebenen Dateien aus dem aktuellen Verzeichnis und allen Unterverzeichnissen. Zeigt die Namen der Dateien an, während Sie gelöscht werden.|
|/q|Gibt den stillen Modus an. Sie werden nicht zur Bestätigung des Löschvorgangs aufgefordert.|
|/a [:]\<Attribute >|Löscht Dateien basierend auf den folgenden Dateiattributen:</br>schreibgeschützte **r** -Dateien</br>**h** ausgeblendete Dateien</br>indizierte Dateien **sind nicht Inhalts**</br>**s** -System Dateien</br>**Dateien,** die für die Archivierung bereit sind</br>**l** -Analyse Punkte</br>-Prefix Bedeutung "Not"|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

> [!CAUTION]
> Wenn Sie die **Datei zum Löschen** einer Datei auf dem Datenträger verwenden, kann Sie nicht abgerufen werden.

-   Wenn Sie **/p**verwenden, zeigt **del** den Namen einer Datei an und sendet die folgende Meldung:

    `FileName, Delete (Y/N)?`

    Drücken Sie Y, um den Löschvorgang zu bestätigen. Um den Löschvorgang abzubrechen und den nächsten Dateinamen anzuzeigen (d. h., wenn Sie eine Gruppe von Dateien angegeben haben), drücken Sie N. Drücken Sie STRG + C, um den Befehl " **del** " anzuhalten.
- Wenn Sie die Befehls Erweiterungen deaktivieren, zeigt **/s** die Namen aller Dateien an, die nicht gefunden wurden, anstatt die Namen der Dateien anzuzeigen, die gelöscht werden (d. h. das Verhalten ist umgekehrt).
- Wenn Sie einen Ordner in *Namen*angeben, werden alle Dateien im Ordner gelöscht. Der folgende Befehl löscht z. b. alle Dateien im Ordner "\Work":  
  ```
  del \work
  ```  
- Sie können Platzhalter ( **&#42;** und **?** ) verwenden, um mehrere Dateien gleichzeitig zu löschen. Um zu vermeiden, dass Dateien unbeabsichtigt gelöscht werden, sollten Sie Platzhalter mit dem Befehl " **del** " vorsichtig verwenden. Wenn Sie z. b. den folgenden Befehl eingeben:  
  ```
  del *.*
  ```  
  Der Befehl " **del** " zeigt die folgende Eingabeaufforderung an:

  `Are you sure (Y/N)?`

  Wenn Sie alle Dateien im aktuellen Verzeichnis löschen möchten, drücken Sie Y, und drücken Sie dann die EINGABETASTE. Drücken Sie zum Abbrechen des Löschvorgangs N, und drücken Sie dann die EINGABETASTE.

> [!NOTE]
> Bevor Sie mit dem Befehl " **del** " Platzhalter Zeichen verwenden, verwenden Sie die gleichen Platzhalter Zeichen mit dem Befehl " **dir** ", um alle Dateien aufzulisten, die gelöscht werden.

-   Der Befehl " **del** " mit unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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
