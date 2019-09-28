---
title: clip
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 82186869782c47f41930d46b4c33a710e6addedf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379342"
---
# <a name="clip"></a>clip



Leitet die Befehlsausgabe von der Befehlszeile an die Windows-Zwischenablage um. Anschließend können Sie diese Textausgabe in andere Programme einfügen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
<Command> | clip
clip < <FileName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<-Befehl >|Gibt einen Befehl an, dessen Ausgabe Sie an die Windows-Zwischenablage senden möchten.|
|\<Dateiname >|Gibt eine Datei an, deren Inhalt Sie an die Windows-Zwischenablage senden möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Sie können den **Clip** -Befehl verwenden, um Daten direkt in alle Anwendungen zu kopieren, die Text aus der Zwischenablage empfangen können.

## <a name="BKMK_examples"></a>Beispiele

Um die aktuelle Verzeichnisliste in die Windows-Zwischenablage zu kopieren, geben Sie Folgendes ein:
```
dir | clip
```
Geben Sie Folgendes ein, um die Ausgabe eines Programms namens generic. awk in die Windows-Zwischenablage zu kopieren:
```
awk -f generic.awk input.txt | clip
```
Geben Sie Folgendes ein, um den Inhalt einer Datei namens "Infodatei. txt" in die Windows-Zwischenablage zu kopieren:
```
clip < readme.txt
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)