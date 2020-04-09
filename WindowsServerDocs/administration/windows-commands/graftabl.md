---
title: graftabl
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d55df814cb962e82775a86e154a024c579987cf2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842413"
---
# <a name="graftabl"></a>graftabl



Ermöglicht Windows-Betriebssystemen das Anzeigen eines erweiterten Zeichensatzes im Grafikmodus. Bei Verwendung ohne Parameter zeigt **graftabl** die vorherige und die aktuelle Codepage an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
graftabl <CodePage>
graftabl /status
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Codepage->|Gibt eine Codepage an, um die Darstellung erweiterter Zeichen im Grafikmodus zu definieren.</br>Gültige Codepage-Identifikationsnummern sind:</br>437: USA</br>850: mehrsprachig (lateinisch I)</br>852: slawisch (Lateinisch II)</br>855: Kyrillisch (Russisch)</br>857: Türkisch</br>860: Portugiesisch</br>861: Isländisch</br>863: Französisch (Kanada)</br>865: Nordisch</br>866: Russisch</br>869: modernes Griechisch|
|/status|Zeigt die aktuelle Codepage an, die von **graftabl** verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   **Graftabl** wirkt sich nur auf die Monitor Anzeige erweiterter Zeichen der von Ihnen angegebenen Codepage aus. Die tatsächliche Konsolen Eingabe Codepage wird nicht geändert. Zum Ändern der Konsolen Eingabe Codepage verwenden Sie den Befehl **Mode** oder **chcp** .
-   In der folgenden Tabelle sind die einzelnen Exitcodes und eine kurze Beschreibung aufgeführt.  
    |Exitcode|Beschreibung|
    |---------|-----------|
    |0|Der Zeichensatz wurde erfolgreich geladen. Es wurde keine vorherige Codepage geladen.|
    |1|Es wurde ein falscher Parameter angegeben. Es wurde keine Aktion ausgeführt.|
    |2|Ein Datei Fehler ist aufgetreten.|
-   Mit der ERRORLEVEL-Umgebungsvariablen in einem Batch-Programm können Sie Exitcodes verarbeiten, die von **graftabl**zurückgegeben werden.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die von **graftabl**verwendete aktuelle Codepage anzuzeigen:
```
graftabl /status
```
Geben Sie Folgendes ein, um den Grafikzeichen Satz für die Codepage 437 (USA) in den Arbeitsspeicher zu laden:
```
graftabl 437
```
Geben Sie Folgendes ein, um den Grafikzeichen Satz für Codepage 850 (mehrsprachig) in den Arbeitsspeicher zu laden:
```
graftabl 850
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Freiplatte](freedisk.md)

[CHCP](chcp.md)