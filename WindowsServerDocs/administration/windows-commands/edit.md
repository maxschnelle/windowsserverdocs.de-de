---
title: bearbeiten
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 096632005b3e42dd941ccc7c72c08ead1d291b53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873151"
---
# <a name="edit"></a>bearbeiten



Startet MS-DOS-Editor, der erstellt, und Ändern von ASCII-Textdateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
edit [/b] [/h] [/r] [/s] [/<NNN>] [[<Drive>:][<Path>]<FileName> [<FileName2> [...]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk >:] [<Path>]<FileName> [<FileName2> [...]]|Gibt den Speicherort und Namen von mindestens eine ASCII-Textdateien. Wenn die Datei nicht vorhanden ist, MS-DOS-Editor wird erstellt. Wenn die Datei vorhanden ist, MS-DOS-Editor wird geöffnet, und sein Inhalt auf dem Bildschirm angezeigt. *FileName* können keine Platzhalterzeichen enthalten (**&#42;** und **?**). Trennen Sie mehrere Dateinamen mit Leerzeichen ein.|
|/b|Erzwingt, dass monochrome-Modus, sodass MS-DOS-Editor in Schwarz und Weiß angezeigt.|
|/h|Zeigt die maximale Anzahl von Zeilen möglich für den aktuellen Bildschirm an.|
|/r|Lädt die Dateien in den schreibgeschützten Modus.|
|/s|Erzwingt die Verwendung von kurzen Dateinamen.|
|\<NNN>|Lädt die Binärdateien und umbricht Zeilen *NNN* Zeichen breit.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Klicken Sie für weitere Hilfe benötigen MS-DOS-Editor öffnen, und klicken Sie dann die Taste F1 drücken.
-   Einige Monitore unterstützen nicht die Anzeige von Tastenkombinationen in der Standardeinstellung. Wenn Sie der Bildschirm die Tastenkombination nicht angezeigt wird, verwenden Sie **/b**.

## <a name="BKMK_examples"></a>Beispiele für

Um die MS-DOS-Editor zu öffnen, geben Sie Folgendes ein:
```
edit
```
Zum Erstellen und bearbeiten eine Datei namens newtextfile.txt im aktuellen Verzeichnis, geben Sie Folgendes ein:
```
edit newtextfile.txt
```