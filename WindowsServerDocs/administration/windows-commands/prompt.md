---
title: prompt
description: Erfahren Sie, wie Sie die Eingabeaufforderung anpassen.
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
ms.openlocfilehash: 8371a67ba1b8dc7d5f02272c809f916aae3df584
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544559"
---
# <a name="prompt"></a>prompt



Ändert die Eingabeaufforderung "cmd. exe". Bei Verwendung ohne Parameter setzt **prompt die Eingabe** Aufforderung auf die Standardeinstellung zurück. Hierbei handelt es sich um den aktuellen Laufwerk Buchstaben und das Verzeichnis, gefolgt vom größer **>** -als-Symbol ().

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
prompt [<Text>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Text >|Gibt den Text und die Informationen an, die Sie in die Eingabeaufforderung einschließen möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Sie können die Eingabeaufforderung anpassen, um den gewünschten Text anzuzeigen, einschließlich Informationen wie den Namen des aktuellen Verzeichnisses, das Datum und die Uhrzeit und die Microsoft Windows-Versionsnummer.

In der folgenden Tabelle sind die Zeichenkombinationen aufgelistet, die anstelle von oder zusätzlich zu einer oder mehreren Zeichen folgen im *Text* -Parameter enthalten sein können. Die Liste enthält eine kurze Beschreibung des Texts oder der Informationen, die von jeder Zeichenkombination der Eingabeaufforderung hinzugefügt werden.  

| Zeichen |                                 Beschreibung                                 |
|-----------|-----------------------------------------------------------------------------|
|    $q     |                               = (Gleichheitszeichen)                                |
|    $$     |                               $ (Dollarzeichen)                               |
|    $t     |                                Aktuelle Uhrzeit                                 |
|    $d     |                                Aktuelles Datum                                 |
|    $p     |                           Aktuelles Laufwerk und Pfad                            |
|    $v     |                           Windows-Versionsnummer                            |
|    $n     |                                Aktuelles Laufwerk                                |
|    $g     |                            > (größer als-Zeichen)                            |
|    $l     |                             < (kleiner als Vorzeichen)                              |
|    $b     |                              \|(Pipe-Symbol)                               |
|    $_     |                               EINGABE-ZEILENVORSCHUB                                |
|    $e     |                         ANSI-Escapecode (Code 27)                          |
|    $h     | Rücktaste (zum Löschen eines Zeichens, das in die Befehlszeile geschrieben wurde) |
|    $a     |                                & (kaufmännisches und-Paar)                                |
|    $c     |                            ((linke Klammer)                             |
|    $f     |                            ) (schließende Klammer)                            |
|    $s     |                                    BRaum                                    |

Wenn Befehls Erweiterungen aktiviert sind (d. h. der Standardwert), unterstützt der **prompt** -Befehl die folgenden Formatierungszeichen:  

|Zeichen|Beschreibung|
|---------|-----------|
|$+|0 (null) oder mehr **+** Pluszeichen (), abhängig von der Tiefe des **pushd-** Verzeichnis Stapels (ein Zeichen für jede Ebene wird per Push abgelegt).|
|$m|Der Remote Name, der dem aktuellen Laufwerk Buchstaben oder der leeren Zeichenfolge zugeordnet ist, wenn das aktuelle Laufwerk kein Netzwerklaufwerk ist.|

Wenn Sie das **$p** Zeichen in den Text Parameter einschließen, wird der Datenträger gelesen, nachdem Sie jeden Befehl eingegeben haben (um das aktuelle Laufwerk und den Pfad zu bestimmen). Dies kann zusätzliche Zeit in Anspruch nehmen, insbesondere bei Diskettenlaufwerken.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um eine zweizeilige Eingabeaufforderung mit der aktuellen Uhrzeit und dem aktuellen Datum in der ersten Zeile und dem größer-als-Zeichen in der nächsten Zeile festzulegen:
```
prompt $d$s$s$t$_$g 
```
Die Eingabeaufforderung wird wie folgt geändert, wobei Datum und Uhrzeit aktuell sind:
```
Fri 06/01/2007  13:53:28.91
>
```
Geben Sie Folgendes ein, um die Eingabeaufforderung als Pfeil`-->`() anzuzeigen:
```
prompt --$g
```
Geben Sie Folgendes ein, um die Eingabeaufforderung manuell in die Standardeinstellung (das aktuelle Laufwerk und den Pfad gefolgt von dem größer-als-Zeichen) zu ändern:
```
prompt $p$g
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
