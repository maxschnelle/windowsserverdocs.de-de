---
title: diskcomp
description: Referenz Artikel für den diskcomp-Befehl, der den Inhalt von zwei Disketten vergleicht.
ms.topic: reference
ms.assetid: 4f56f534-a356-4daa-8b4f-38e089341e42
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 058092595e106fdc60663ec81e68523c609d34c7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028318"
---
# <a name="diskcomp"></a>diskcomp

Vergleicht den Inhalt von zwei Disketten. Bei Verwendung ohne Parameter verwendet **diskcomp** das aktuelle Laufwerk, um beide Datenträger zu vergleichen.

## <a name="syntax"></a>Syntax

```
diskcomp [<drive1>: [<drive2>:]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive1>` | Gibt das Laufwerk an, das eine der Disketten enthält. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Der **diskcomp** -Befehl kann nur mit Disketten verwendet werden. **Diskcomp** kann nicht mit einer Festplatte verwendet werden. Wenn Sie ein Festplattenlaufwerk für *drive1* oder *drive2*angeben, zeigt **diskcomp** die folgende Fehlermeldung an:

  ```
  Invalid drive specification
  Specified drive does not exist
  or is nonremovable
  ```

- Wenn alle Spuren auf den zwei verglichenen Datenträgern identisch sind (es wird die Volumenummer eines Datenträgers ignoriert), zeigt **diskcomp** die folgende Meldung an:

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

  Wenn Sie **Y**drücken, werden Sie von **diskcomp** aufgefordert, den Datenträger für den nächsten Vergleich einzufügen. Wenn Sie " **N**" drücken, hält **diskcomp** den Vergleich an.

- Wenn Sie den *drive2* -Parameter weglassen, verwendet **diskcomp** das aktuelle Laufwerk für *drive2*. Wenn Sie beide Laufwerk Parameter weglassen, verwendet **diskcomp** das aktuelle Laufwerk für beide. Wenn das aktuelle Laufwerk mit *drive1*identisch ist, werden Sie von **diskcomp** aufgefordert, Datenträger nach Bedarf auszutauschen.

- Wenn Sie für *drive1* und *drive2*dasselbe Diskettenlaufwerk angeben, vergleicht **diskcomp** diese mithilfe eines Laufwerks und fordert Sie auf, die Datenträger bei Bedarf einzufügen. Abhängig von der Kapazität der Datenträger und der Menge an verfügbarem Arbeitsspeicher müssen Sie die Datenträger möglicherweise mehrmals austauschen.

- **Diskcomp** kann einen einseitigen Datenträger nicht mit einem doppelten Datenträger oder mit einem Datenträger mit hoher Dichte mit einem Datenträger mit doppelter Dichte vergleichen. Wenn der Datenträger in *drive1* nicht denselben Typ aufweist wie der Datenträger in *drive2*, zeigt **diskcomp** die folgende Meldung an:

  ```
  Drive types or diskette types not compatible
  ```

- **Diskcomp** funktioniert nicht auf einem Netzlaufwerk oder auf einem Laufwerk, das mit dem Befehl **subst** erstellt wurde. Wenn Sie versuchen, **diskcomp** mit einem Laufwerk eines dieser Typen zu verwenden, zeigt **diskcomp** die folgende Fehlermeldung an:

  ```
  Invalid drive specification
  ```

- Wenn Sie **diskcomp** mit einem Datenträger verwenden, den Sie mithilfe von **Copy**erstellt haben, zeigt **diskcomp** möglicherweise eine Meldung ähnlich der folgenden an:

  ```
  Compare error on
  side 0, track 0
  ```

  Diese Art von Fehler kann auch auftreten, wenn die Dateien auf den Datenträgern identisch sind. Obwohl die **Kopie** Informationen dupliziert, wird Sie nicht notwendigerweise am gleichen Speicherort auf dem Ziel Datenträger platziert.

- **diskcomp** -Exitcodes:

  | Exitcode | BESCHREIBUNG |
  | --------- | ----------- |
  | 0 | Datenträger sind identisch. |
  | 1 | Unterschiede wurden gefunden. |
  | 3 | Schwer fehlerhaft |
  | 4 | Initialisierungsfehler |

  Zum Verarbeiten von Exitcodes, die von **diskcomp**zurückgegeben werden, können Sie die *ERRORLEVEL* -Umgebungsvariable in der **if** -Befehlszeile in einem Batch-Programm verwenden.

## <a name="examples"></a>Beispiele

Wenn Ihr Computer nur über ein Diskettenlaufwerk (z. b. Laufwerk A) verfügt und Sie zwei Datenträger vergleichen möchten, geben Sie Folgendes ein:

```
diskcomp a: a:
```

Bei Bedarf werden Sie von **diskcomp** aufgefordert, jeden Datenträger einzufügen.

Veranschaulicht, wie ein **diskcomp** -Exitcode in einem Batch-Programm verarbeitet wird, das die *ERRORLEVEL* -Umgebungsvariable in der **if** -Befehlszeile verwendet:

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
