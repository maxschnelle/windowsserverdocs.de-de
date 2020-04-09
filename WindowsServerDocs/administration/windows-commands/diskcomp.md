---
title: diskcomp
description: Windows-Befehls Thema für diskcomp, das den Inhalt von zwei Disketten vergleicht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4f56f534-a356-4daa-8b4f-38e089341e42
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e36e644616e25659c1a2a5ca684e975fd06fc19f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845553"
---
# <a name="diskcomp"></a>diskcomp

Vergleicht den Inhalt von zwei Disketten. Bei Verwendung ohne Parameter verwendet **diskcomp** das aktuelle Laufwerk, um beide Datenträger zu vergleichen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
diskcomp [<Drive1>: [<Drive2>:]]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive1 >|Gibt das Laufwerk an, das eine der Disketten enthält.|
|\<drive2 >|Gibt das Laufwerk an, das die andere Diskette enthält.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Verwenden von Datenträgern

  Der **diskcomp** -Befehl kann nur mit Disketten verwendet werden. **Diskcomp** kann nicht mit einer Festplatte verwendet werden. Wenn Sie ein Festplattenlaufwerk für *Drive1* oder *drive2*angeben, zeigt **diskcomp** die folgende Fehlermeldung an:  
  ```
  Invalid drive specification
  Specified drive does not exist
  or is nonremovable
  ```  
- Vergleichen von Datenträgern

  Wenn alle Spuren auf den zwei verglichenen Datenträgern identisch sind, zeigt **diskcomp** die folgende Meldung an:  
  ```
  Compare OK
  ```  
  Wenn die Spuren nicht identisch sind, zeigt **diskcomp** eine Meldung ähnlich der folgenden an:  
  ```
  Compare error on
  side 1, track 2
  ```  
  Wenn **diskcomp** den Vergleich abschließt, wird die folgende Meldung angezeigt:  
  ```
  Compare another diskette (Y/N)?
  ```  
  Wenn Sie Y drücken, werden Sie von **diskcomp** aufgefordert, den Datenträger für den nächsten Vergleich einzufügen. Wenn Sie "N" drücken, hält **diskcomp** den Vergleich an.

  Wenn **diskcomp** den Vergleich durchführt, wird die Volumenummer eines Datenträgers ignoriert.
- Weglassen von Laufwerk Parametern

  Wenn Sie den *drive2* -Parameter weglassen, verwendet **diskcomp** das aktuelle Laufwerk für *drive2*. Wenn Sie beide Laufwerk Parameter weglassen, verwendet **diskcomp** das aktuelle Laufwerk für beide. Wenn das aktuelle Laufwerk mit *Drive1*identisch ist, werden Sie von **diskcomp** aufgefordert, Datenträger nach Bedarf auszutauschen.
- Verwenden eines Laufwerks

  Wenn Sie für *Drive1* und *drive2*dasselbe Diskettenlaufwerk angeben, vergleicht **diskcomp** diese mithilfe eines Laufwerks und fordert Sie auf, die Datenträger bei Bedarf einzufügen. Abhängig von der Kapazität der Datenträger und der Menge an verfügbarem Arbeitsspeicher müssen Sie die Datenträger möglicherweise mehrmals austauschen.
- Vergleichen verschiedener Typen von Datenträgern

  **Diskcomp** kann keinen einseitigen Datenträger mit einem Datenträger mit doppelter Dichte und einem Datenträger mit hoher Dichte mit einem Datenträger mit doppelter Dichte vergleichen. Wenn der Datenträger in *Drive1* nicht denselben Typ aufweist wie der Datenträger in *drive2*, zeigt **diskcomp** die folgende Meldung an:  
  ```
  Drive types or diskette types not compatible
  ```  
- Verwenden von **diskcomp** mit Netzwerken und umgeleiteten Laufwerken

  **Diskcomp** funktioniert nicht auf einem Netzlaufwerk oder auf einem Laufwerk, das mit dem Befehl **subst** erstellt wurde. Wenn Sie versuchen, **diskcomp** mit einem Laufwerk eines dieser Typen zu verwenden, zeigt **diskcomp** die folgende Fehlermeldung an:  
  ```
  Invalid drive specification
  ```  
- Vergleichen eines Original Datenträgers mit einer Kopie

  Wenn Sie **diskcomp** mit einem Datenträger verwenden, den Sie mithilfe von **Copy**erstellt haben, zeigt **diskcomp** möglicherweise eine Meldung ähnlich der folgenden an:  
  ```
  Compare error on 
  side 0, track 0
  ```  
  Diese Art von Fehler kann auch auftreten, wenn die Dateien auf den Datenträgern identisch sind. Obwohl die **Kopie** Informationen dupliziert, wird Sie nicht notwendigerweise am gleichen Speicherort auf dem Ziel Datenträger gespeichert.
- Informationen zu **diskcomp** -Exitcodes

  In der folgenden Tabelle werden die einzelnen Exitcodes erläutert.  

  |Exitcode|Beschreibung|
  |---------|-----------|
  |0|Datenträger sind identisch.|
  |1|Unterschiede wurden gefunden.|
  |3|Schwer fehlerhaft|
  |4|Initialisierungsfehler|

  Zum Verarbeiten von Exitcodes, die von **diskcomp**zurückgegeben werden, können Sie die ERRORLEVEL-Umgebungsvariable in der **if** -Befehlszeile in einem Batch-Programm verwenden.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn Ihr Computer nur über ein Diskettenlaufwerk (z. b. Laufwerk A) verfügt und Sie zwei Datenträger vergleichen möchten, geben Sie Folgendes ein:
```
diskcomp a: a:
```
Bei Bedarf werden Sie von **diskcomp** aufgefordert, jeden Datenträger einzufügen.

Im folgenden Beispiel wird veranschaulicht, wie ein **diskcomp** -Exitcode in einem Batch-Programm verarbeitet wird, das die ERRORLEVEL-Umgebungsvariable in der **if** -Befehlszeile verwendet:
```
rem Checkout.bat compares the disks in drive A and B 
echo off 
diskcomp a: b: 
if errorlevel 4 goto ini_error 
if errorlevel 3 goto hard_error 
if errorlevel 1 goto no_compare
if errorlevel 0 goto compare_ok 
:ini_error 
echo ERROR: Insufficient memory or command invalid 
goto exit 
:hard_error 
echo ERROR: An irrecoverable error occurred 
goto exit 
:break 
echo You just pressed CTRL+C to stop the comparison 
goto exit 
:no_compare 
echo Disks are not the same 
goto exit 
:compare_ok 
echo The comparison was successful; the disks are the same 
goto exit 
:exit
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
