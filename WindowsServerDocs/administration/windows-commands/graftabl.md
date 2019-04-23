---
title: graftabl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 395873cf3dbeb574dd9abc69f45b410bece80c25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848441"
---
# <a name="graftabl"></a>graftabl



Ermöglicht es Windows-Betriebssystemen einen erweiterten Zeichensatz im Grafikmodus angezeigt. Wenn Sie ohne Angabe von Parametern **Graftabl** zeigt die vorherige und die aktuelle Codepage.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
graftabl <CodePage>
graftabl /status
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<CodePage>|Gibt an, eine Codepage an, um die Darstellung von Sonderzeichen im Grafikmodus definieren.</br>Gültige Identifikation Zahlen sind:</br>437: USA</br>850: Mehrsprachige (Lateinisch I)</br>852: Altslawisch (Lateinisch II)</br>855: Kyrillisch (Russisch)</br>857: Türkisch</br>860: Portugiesisch</br>861: Isländisch</br>863: Französisch (Kanada)</br>865: Nordisch</br>866: Russisch</br>869: Neugriechisch|
|/status|Zeigt den aktuellen Code, auf die **Graftabl** verwendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   **Graftabl** wirkt sich nur auf der Bildschirmanzeige von erweiterten Zeichen der Codepage, die Sie angeben. Es ändert sich nicht auf die Eingabe Codepage für die Konsole aus. Um eine Codepage, die auf der Konsole Eingabe zu ändern, verwenden die **Modus** oder **Chcp** Befehl.
-   Die folgende Tabelle enthält alle Exitcodes und eine kurze Beschreibung des Zertifikats.  
    |Exitcode|Beschreibung|
    |---------|-----------|
    |0|Zeichensatz wurde erfolgreich geladen. Keine Codepage wurde geladen.|
    |1|Es wurde ein falscher Parameter angegeben. Es wurde keine Aktion ausgeführt.|
    |2|Datei ist ein Fehler aufgetreten ist.|
-   Können Sie in einem Batchprogramm zum Verarbeiten von Exitcodes, die von zurückgegeben werden der Umgebungsvariablen ERRORLEVEL **Graftabl**.

## <a name="BKMK_examples"></a>Beispiele für

Anzeigen die aktuellen Codepage, die von verwendet **Graftabl**, Typ:
```
graftabl /status
```
Um den Grafikzeichensatz für Codepage 437 (Vereinigte Staaten) in den Arbeitsspeicher zu laden, geben Sie Folgendes ein:
```
graftabl 437
```
Um den Grafikzeichensatz für Codepage 850 (multilingual) in den Arbeitsspeicher zu laden, geben Sie Folgendes ein:
```
graftabl 850
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Freedisk](freedisk.md)

[Chcp](chcp.md)