---
title: Clip
description: Windows-Befehls Thema für Clip, das die Befehlszeile von der Befehlszeile an die Windows-Zwischenablage umleitet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d997154a382cf39aa2b877d7a2b84f4ff34157d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847643"
---
# <a name="clip"></a>Clip

Leitet die Befehlsausgabe von der Befehlszeile an die Windows-Zwischenablage um. Anschließend können Sie diese Textausgabe in andere Programme einfügen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
<Command> | clip
clip < <FileName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Befehl >|Gibt einen Befehl an, dessen Ausgabe Sie an die Windows-Zwischenablage senden möchten.|
|\<Dateiname >|Gibt eine Datei an, deren Inhalt Sie an die Windows-Zwischenablage senden möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Sie können den **Clip** -Befehl verwenden, um Daten direkt in alle Anwendungen zu kopieren, die Text aus der Zwischenablage empfangen können.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)