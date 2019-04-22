---
title: assoc
description: Windows-Befehle Thema **Assoc** -zeigt oder ändert die Dateinamenerweiterungen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d893167081b66c81366b59613c52182a4ddba370
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816641"
---
# <a name="assoc"></a>assoc



Zeigt oder ändert die Dateinamenerweiterungen. Wenn Sie ohne Angabe von Parametern **Assoc** zeigt eine Liste aller der aktuellen Dateinamenerweiterungen.

> [!NOTE]
> Mit diesem Befehl wird nur in cmd ein. unterstützt werden. EXE-Datei und nicht über PowerShell verfügbar ist.
>

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
assoc [<.ext>[=[<FileType>]]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|<.ext>|Gibt die Dateinamenerweiterung an.|
|\<FileType>|Gibt den Dateityp, die angegebene Dateinamenerweiterung zugeordnet werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um die dateitypzuordnung für die Erweiterung zu entfernen, fügen Sie ein Leerzeichen hinter dem Gleichheitszeichen, durch Drücken der LEERTASTE.
-   Zum aktuellen Dateitypen anzeigen, die open definiert sind, verwenden die **Ftype** Befehl.
-   Die Ausgabe umgeleitet **Assoc** verwenden, um eine Textdatei, die **>** Umleitungsoperator.

## <a name="BKMK_examples"></a>Beispiele für

Um die aktuellen dateitypzuordnung für die Datei namens Erweiterung .txt anzuzeigen, geben Sie Folgendes ein:
```
assoc .txt
```
Um die dateitypzuordnung für die Datei namens Erweiterung BAK zu entfernen, geben Sie Folgendes ein:
```
assoc .bak= 
```

> [!NOTE]
> Achten Sie darauf, um ein Leerzeichen hinter dem Gleichheitszeichen hinzuzufügen.

Zum Anzeigen der Ausgabe von **Assoc** einen Bildschirm zu einem Zeitpunkt, Typ:
```
assoc | more
```
Zum Senden der Ausgabe der **Assoc** Geben Sie die assoc.txt Datei:
```
assoc>assoc.txt
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
