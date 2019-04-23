---
title: clip
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b10876e115c1f0dcac3448948003852449012087
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862391"
---
# <a name="clip"></a>clip



Leitet die Ausgabe des Befehls über die Befehlszeile in die Windows-Zwischenablage. Sie können dann diese Ausgabe von Text in andere Programme einfügen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
<Command> | clip
clip < <FileName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Befehl >|Gibt einen Befehl aus, deren Ausgabe Sie in die Windows-Zwischenablage senden möchten.|
|\<FileName>|Gibt eine Datei, deren Inhalt in die Windows-Zwischenablage senden möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Sie können die **Clip** -Befehl zum Kopieren von Daten direkt in eine Anwendung, die Text aus der Zwischenablage empfangen kann.

## <a name="BKMK_examples"></a>Beispiele für

Um das aktuelle Verzeichnis auflisten, die in die Windows-Zwischenablage zu kopieren, geben Sie Folgendes ein:
```
dir | clip
```
Um die Ausgabe der ein Programm namens Generic.awk in die Windows-Zwischenablage zu kopieren, geben Sie Folgendes ein:
```
awk -f generic.awk input.txt | clip
```
Um den Inhalt einer Datei namens "Readme.txt" in die Windows-Zwischenablage zu kopieren, geben Sie Folgendes ein:
```
clip < readme.txt
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)