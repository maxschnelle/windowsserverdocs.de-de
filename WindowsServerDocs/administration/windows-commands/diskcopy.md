---
title: diskcopy
description: Referenz Thema für diskcopy, das den Inhalt der Diskette im Quelllaufwerk in eine formatierte oder unformatierte Diskette auf dem Ziellaufwerk kopiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fd21efa-52cc-4e70-a7fe-35125a435106
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/07/2018
ms.openlocfilehash: b5c9186a539a58ed0d3362ba83d7a3bcedcaabad
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719470"
---
# <a name="diskcopy"></a>diskcopy

Kopiert den Inhalt des Disketten Datenträgers im Quelllaufwerk in eine formatierte oder unformatierte Diskette auf dem Ziellaufwerk. Bei Verwendung ohne Parameter verwendet **diskcopy** das aktuelle Laufwerk für den Quell Datenträger und den Ziel Datenträger.



> [!NOTE]
> Dieser Befehl ist nicht in Windows 10 enthalten.

## <a name="syntax"></a>Syntax

```
diskcopy [<Drive1>: [<Drive2>:]] [/v]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive1>|Gibt das Laufwerk an, das den Quell Datenträger enthält.|
|\<Drive2>|Gibt das Laufwerk an, das den Ziel Datenträger enthält.|
|/v|Überprüft, ob die Informationen ordnungsgemäß kopiert werden. Diese Option verlangsamt den Kopiervorgang.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Verwenden von Datenträgern

    **Diskcopy** funktioniert nur mit Wechsel Datenträgern, z. b. Disketten Datenträgern, die denselben Typ aufweisen müssen. **Diskcopy** kann nicht mit einer Festplatte verwendet werden. Wenn Sie ein Festplattenlaufwerk für *Drive1* oder *drive2*angeben, wird von **diskcopy** die folgende Fehlermeldung angezeigt:  
    ```
    Invalid drive specification
    Specified drive does not exist or is nonremovable
    ```  
    Der **diskcopy** -Befehl fordert Sie auf, die Quell-und Ziel Datenträger einzufügen, und wartet, bis Sie eine beliebige Taste drücken, bevor Sie fortfahren.

    Nachdem der Datenträger kopiert wurde, zeigt **diskcopy** die folgende Meldung an:  
    ```
    Copy another diskette (Y/N)?
    ```  
    Wenn Sie Y drücken, werden Sie von **diskcopy** aufgefordert, Quell-und Ziel Datenträger für den nächsten Kopiervorgang einzufügen. Um den **diskcopy** -Prozess anzuhalten, drücken Sie **N**.

    Wenn Sie auf eine unformatierte Diskette in *drive2*kopieren, formatiert **diskcopy** den Datenträger mit der gleichen Anzahl von Seiten und Sektoren pro Spur, die sich auf dem Datenträger in *Drive1*befinden. **Diskcopy** zeigt die folgende Meldung an, während die Festplatte formatiert und die Dateien kopiert werden:  
    ```
    Formatting while copying
    ```  
-   Seriennummern von Datenträgern

    Wenn der Quell Datenträger eine Volumeseriennummer aufweist, erstellt **diskcopy** eine neue Volumeseriennummer für den Ziel Datenträger und zeigt die Nummer an, wenn der Kopiervorgang beendet ist
-   Weglassen von Laufwerk Parametern

    Wenn Sie den *drive2* -Parameter weglassen, verwendet **diskcopy** das aktuelle Laufwerk als Ziellaufwerk. Wenn Sie beide Laufwerk Parameter weglassen, verwendet **diskcopy** das aktuelle Laufwerk für beide. Wenn das aktuelle Laufwerk mit *Drive1*identisch ist, werden Sie von **diskcopy** aufgefordert, Datenträger nach Bedarf auszutauschen.
-   Verwenden eines Laufwerks zum Kopieren

    Führen Sie **diskcopy** von einem anderen Laufwerk als dem Diskettenlaufwerk aus, z. b. von Laufwerk C. Wenn Disketten *Drive1* und Diskette *drive2* identisch sind, werden Sie von **diskcopy** aufgefordert, Datenträger zu wechseln. Wenn die Datenträger mehr Informationen enthalten, als der verfügbare Arbeitsspeicher aufnehmen kann, kann **diskcopy** nicht alle Informationen gleichzeitig lesen. **Diskcopy** liest vom Quell Datenträger, schreibt auf den Ziel Datenträger und fordert Sie auf, den Quell Datenträger erneut einzufügen. Dieser Prozess wird fortgesetzt, bis Sie den gesamten Datenträger kopiert haben.
-   Vermeiden von Datenträger Fragmentierung

    Fragmentierung ist das vorhanden sein kleiner Bereiche von nicht verwendetem Speicherplatz zwischen vorhandenen Dateien auf einem Datenträger. Ein fragmentierter Quell Datenträger kann das Auffinden, lesen oder Schreiben von Dateien verlangsamen.

    Da **diskcopy** eine exakte Kopie des Quell Datenträgers auf dem Ziel Datenträger erstellt, wird jede Fragmentierung auf dem Quell Datenträger auf den Ziel Datenträger über Um zu vermeiden, dass die Fragmentierung von einem Datenträger auf einen anderen übertragen wird, kopieren Sie den Datenträger mit **Kopieren** oder **xcopy** Da **Kopier** -und **xcopy** -Dateien nacheinander kopiert werden, wird der neue Datenträger nicht fragmentiert.

> [!NOTE]
> Sie können mit **xcopy** keinen Start Datenträger kopieren.

### <a name="understanding-diskcopy-exit-codes"></a>Grundlegendes zu den **Beendigungs Codes**

    The following table explains each exit code.
    
    |Exitcode|BESCHREIBUNG|
    |---------|-----------|
    |0|Der Kopiervorgang war erfolgreich.|
    |1|Nicht schwerwiegender Lese-/Schreibfehler|
    |3|Schwerwiegender schwerwiegender Fehler|
    |4|Initialisierungsfehler|

    To process the exit codes that are returned by **diskcomp**, you can use the *ERRORLEVEL* environment variable on the **if** command line in a batch program.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Datenträger in Laufwerk B auf den Datenträger in Laufwerk a zu kopieren:
```
diskcopy b: a:
```
Wenn Sie Diskettenlaufwerk A verwenden möchten, um eine Diskette in eine andere zu kopieren, wechseln Sie zunächst zum Laufwerk C, und geben Sie dann Folgendes ein:

DISKCOPY a: a:

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)