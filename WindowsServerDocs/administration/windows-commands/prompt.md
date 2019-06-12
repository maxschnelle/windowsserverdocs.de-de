---
title: prompt
description: Informationen Sie zum Anpassen von der Eingabeaufforderung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d98e965-02eb-46ad-9d0a-5dc44830373e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 5ef487ce9799c1f09660cdfcd6fba71336fc4d9a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442146"
---
# <a name="prompt"></a>prompt



Ändert die Cmd.exe-Eingabeaufforderung. Wenn Sie ohne Angabe von Parametern **Eingabeaufforderung** setzt die Eingabeaufforderung auf die Standardeinstellung, die den aktuellen Laufwerkbuchstaben und das Verzeichnis, das größer-als-Zeichen gefolgt wird ( **>** ).

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
prompt [<Text>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Text>|Gibt den Text und die Informationen, die in der Befehlszeile enthalten sein sollen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Sie können anpassen, dass die Eingabeaufforderung Text nicht angezeigt, die Sie verwenden, einschließlich Informationen wie den Namen der im aktuellen Verzeichnis, die Uhrzeit und Datum und die Microsoft Windows-Versionsnummer möchten.

Die folgende Tabelle enthält die Zeichenkombinationen, die Sie, anstelle von oder zusätzlich einen oder mehrere Zeichenfolgen in einschließen können die *Text* Parameter. Die Liste enthält eine kurze Beschreibung des Textes oder Informationen, die jede Zeichenkombination an der Eingabeaufforderung hinzufügt.  

| Zeichen |                                 Beschreibung                                 |
|-----------|-----------------------------------------------------------------------------|
|    $q     |                               = (Gleichheitszeichen)                                |
|    $$     |                               $ (Dollarzeichen)                               |
|    $t     |                                Aktuelle Zeit                                 |
|    $d     |                                Aktuelles Datum                                 |
|    $p     |                           Aktuelle Laufwerk und Pfad                            |
|    $v     |                           Windows-Versionsnummer                            |
|    $n     |                                Aktuelles Laufwerk                                |
|    $g     |                            > (größer als-Zeichen)                            |
|    $l     |                             < (kleiner-als-Zeichen)                              |
|    $b     |                                                                             |
|    $_     |                               GEBEN SIE ZEILENVORSCHUB                                |
|    $e     |                         ANSI-Escape-Code (Code 27)                          |
|    $h     | Mit der RÜCKTASTE (löschen ein Zeichen, das in der Befehlszeile geschrieben wurden) |
|    $ein     |                                & (kaufmännisches und-Zeichen)                                |
|    $c     |                            ((Klammer)                             |
|    $f     |                            ) (Klammer)                            |
|    $s     |                                    Speicherplatz                                    |

Befehlserweiterungen sind aktiviert, wenn (d. h. Standard) die **Eingabeaufforderung** -Befehl unterstützt die folgenden Formatierungszeichen:  

|Zeichen|Beschreibung|
|---------|-----------|
|$+|NULL oder mehr Pluszeichen (+) ( **+** ) Zeichen, abhängig von die Tiefe der **Pushd** Directory Stack (ein Zeichen für jede Ebene mithilfe von Push übertragen).|
|$m|Der Remotename der aktuellen Laufwerkbuchstabe oder eine leere Zeichenfolge zugeordnet, wenn aktuelle Laufwerk nicht auf einem Netzlaufwerk ist.|

Wenn Sie enthalten die **$p** Zeichen im Textparameter wird der Datenträger nach der Eingabe jedes Befehls (um zu bestimmen, das aktuelle Laufwerk und Pfad) gelesen. Dies kann zusätzliche Zeit, insbesondere für Diskettenlaufwerke dauern.

## <a name="BKMK_examples"></a>Beispiele für

Um die erste Zeile und dem größer-als-Zeichen in der nächsten Zeile eine zweizeiligen-Eingabeaufforderung mit der aktuellen Uhrzeit und Datum festzulegen, geben Sie Folgendes ein:
```
prompt $d$s$s$t$_$g 
```
Die Eingabeaufforderung wird wie folgt geändert, in denen das Datum und Uhrzeit aktuell sind:
```
Fri 06/01/2007  13:53:28.91
>
```
Festlegen von der Eingabeaufforderung als ein Pfeil angezeigt (`-->`), Typ:
```
prompt --$g
```
Um die Eingabeaufforderung auf die Standardeinstellung (das aktuelle Laufwerk und Pfad durch das größer-als-Zeichen) manuell zu ändern, geben Sie Folgendes ein:
```
prompt $p$g
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)