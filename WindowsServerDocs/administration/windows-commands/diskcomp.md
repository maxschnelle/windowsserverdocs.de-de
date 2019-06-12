---
title: diskcomp
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f56f534-a356-4daa-8b4f-38e089341e42
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ccd1a347f9ac51fc98c963dedb1c0ab3fcd27d41
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439590"
---
# <a name="diskcomp"></a>diskcomp



Vergleicht den Inhalt von zwei Disketten. Wenn Sie ohne Angabe von Parametern **Diskcomp** verwendet das aktuelle Laufwerk, beide Festplatten verglichen werden soll. Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
diskcomp [<Drive1>: [<Drive2>:]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk1 >|Gibt das Laufwerk eines der Disketten enthalten.|
|\<Laufwerk2 >|Gibt an, dem Laufwerk, auf die anderen Diskette.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Mithilfe von Datenträgern

  Die **Diskcomp** Befehl funktioniert nur bei Disketten. Sie können keine **Diskcomp** mit einer Festplatte. Wenn Sie angeben, dass ein Festplattenlaufwerk für *Laufwerk1* oder *Laufwerk2*, **Diskcomp** wird die folgende Fehlermeldung angezeigt:  
  ```
  Invalid drive specification
  Specified drive does not exist
  or is nonremovable
  ```  
- Vergleichen von Datenträgern

  Wenn alle Spuren auf dem zwei Datenträger, die mit dem verglichen wird gleich sind, **Diskcomp** wird die folgende Meldung angezeigt:  
  ```
  Compare OK
  ```  
  Wenn die Spuren nicht gleich sind, **Diskcomp** wird eine Meldung ähnlich der folgenden angezeigt:  
  ```
  Compare error on
  side 1, track 2
  ```  
  Wenn **Diskcomp** abgeschlossen ist den Vergleich wird die folgende Meldung angezeigt:  
  ```
  Compare another diskette (Y/N)?
  ```  
  Wenn Sie "Y" drücken **Diskcomp** fordert Sie auf den Datenträger für den nächsten Vergleich einfügen. Drücken Sie N, **Diskcomp** beendet den Vergleich.

  Wenn **Diskcomp** führt der Vergleich ignoriert eine Seriennummer des Datenträgers.
- Das Auslassen der Laufwerk-Parameter

  Wenn Sie weglassen der *Laufwerk2* Parameter **Diskcomp** verwendet das aktuelle Laufwerk für *Laufwerk2*. Wenn Sie beide Laufwerkparameter weglassen **Diskcomp** verwendet das aktuelle Laufwerk für beide. Wenn das aktuelle Laufwerk entspricht *Laufwerk1*, **Diskcomp** fordert Sie auf den Datenträger nach Bedarf austauschen.
- Verwenden ein Laufwerk

  Wenn Sie angeben, dass das gleiche Laufwerk für *Laufwerk1* und *Laufwerk2*, **Diskcomp** vergleicht diese mit einem Laufwerk, und fordert Sie auf die Datenträger nach Bedarf einfügen. Möglicherweise müssen Sie die Datenträger mehr als einmal je nach Kapazität der Datenträger und die Menge des verfügbaren Arbeitsspeichers zu wechseln.
- Vergleich von verschiedenen Typen von Datenträgern

  **Diskcomp** einen einseitiger Datenträger mit einem Datenträger beidseitiges noch einen HD-Datenträger mit einem Double-Wert-Dichte-Datenträger können nicht verglichen werden. Wenn der Datenträger im *Laufwerk1* ist nicht vom gleichen Typ wie der Datenträger im *Laufwerk2*, **Diskcomp** wird die folgende Meldung angezeigt:  
  ```
  Drive types or diskette types not compatible
  ```  
- Mithilfe von **Diskcomp** mit Netzwerken und umgeleiteten Laufwerken

  **Diskcomp** funktioniert nicht auf einem Netzlaufwerk oder auf einem Laufwerk erstellt, indem die **Subst** Befehl. Wenn Sie versuchen, **Diskcomp** ein Laufwerk eines dieser Typen **Diskcomp** wird die folgende Fehlermeldung angezeigt:  
  ```
  Invalid drive specification
  ```  
- Vergleichen von einer ursprünglichen Datenträger mit einer Kopie

  Bei Verwendung von **Diskcomp** mit einem Datenträger, die Sie mithilfe von vorgenommen **Kopie**, **Diskcomp** möglicherweise eine Meldung ähnlich der folgenden angezeigt:  
  ```
  Compare error on 
  side 0, track 0
  ```  
  Diese Art von Fehler kann auftreten, auch wenn die Dateien auf den Datenträgern identisch sind. Obwohl **Kopie** dupliziert Informationen, es ist nicht unbedingt platzieren Sie es in den gleichen Speicherort auf dem Zieldatenträger.
- Grundlegendes zu **Diskcomp** Exitcodes

  In der folgende Tabelle wird erläutert, jede Exitcode.  

  |Exitcode|Beschreibung|
  |---------|-----------|
  |0|Datenträger sind identisch|
  |1|Es wurden Unterschiede gefunden.|
  |3|Schwerwiegender Fehler aufgetreten ist.|
  |4|Fehler bei der Initialisierung aufgetreten ist.|

  Zum Prozess Exitcodes, die von zurückgegeben werden **Diskcomp**, können Sie auf der Umgebungsvariablen ERRORLEVEL den **Wenn** Befehlszeile in einem Batchprogramm.

## <a name="BKMK_examples"></a>Beispiele für

Wenn Ihr Computer nur ein Diskettenlaufwerk (z. B. Laufwerk A verfügt) und zwei Datenträger verglichen werden soll, geben Sie ein:
```
diskcomp a: a:
```
**Diskcomp** aufgefordert, jeden Datenträger und fügen Sie nach Bedarf.

Im folgende Beispiel wird veranschaulicht, wie zum Verarbeiten einer **Diskcomp** Exitcode in einem Batchprogramm, das der Umgebungsvariablen ERRORLEVEL auf verwendet die **Wenn** über die Befehlszeile:
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
echo "You just pressed CTRL+C" to stop the comparison 
goto exit 
:no_compare 
echo Disks are not the same 
goto exit 
:compare_ok 
echo The comparison was successful; the disks are the same 
goto exit 
:exit
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
