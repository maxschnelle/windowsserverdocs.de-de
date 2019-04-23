---
title: diskcopy
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fd21efa-52cc-4e70-a7fe-35125a435106
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/07/2018
ms.openlocfilehash: 5b9343dc2f6b4c74da5a9d89a2ea804b702248cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841171"
---
# <a name="diskcopy"></a>diskcopy



Kopiert den Inhalt der Diskette im Source-Laufwerk auf einer Diskette formatiert oder unformatiert in das Ziellaufwerk. Wenn Sie ohne Angabe von Parametern **Diskcopy** verwendet das aktuelle Laufwerk für die Quelldatenträger und dem Zieldatenträger.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> Mit diesem Befehl wird nicht in Windows 10 enthalten.

## <a name="syntax"></a>Syntax

```
diskcopy [<Drive1>: [<Drive2>:]] [/v]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk1 >|Gibt an, das Laufwerk, das die Quell-Datenträger enthält.|
|\<Laufwerk2 >|Gibt an, das Laufwerk, das die Ziel-Datenträger enthält.|
|/v|Stellt sicher, dass die Informationen richtig kopiert wird. Diese Option ist der Kopiervorgang verlangsamt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Mithilfe von Datenträgern

    **Diskcopy** funktioniert nur mit Wechselmedien wie z. B. Disketten, die den gleichen Typ sein muss. Sie können keine **Diskcopy** mit einer Festplatte. Wenn Sie angeben, dass ein Festplattenlaufwerk für *Laufwerk1* oder *Laufwerk2*, **Diskcopy** wird die folgende Fehlermeldung angezeigt:  
    ```
    Invalid drive specification
    Specified drive does not exist or is nonremovable
    ```  
    Die **Diskcopy** Befehl fordert Sie zum Einfügen von der Quelle und Ziel-Datenträger und darauf wartet, bis Sie eine beliebige Taste, auf der Tastatur drücken, bevor Sie fortfahren.

    Nach Abschluss des Kopiervorgangs des Datenträgers **Diskcopy** wird die folgende Meldung angezeigt:  
    ```
    Copy another diskette (Y/N)?
    ```  
    Wenn Sie "Y" drücken **Diskcopy** fordert Sie auf die Quell- und Ziel für den nächsten Kopiervorgang einzulegen. Zum Beenden der **Diskcopy** verarbeiten, drücken Sie die **N**.

    Wenn Sie auf einen unformatierten Datenträger in kopieren *Laufwerk2*, **Diskcopy** formatiert die Datenträger mit der gleichen Anzahl von Seiten und Sektoren pro Spur, auf dem Datenträger im *Laufwerk1*. **Diskcopy** wird die folgende Meldung angezeigt, während die Dateien kopiert und die Datenträger formatiert:  
    ```
    Formatting while copying
    ```  
-   Datenträger-Seriennummern

    Wenn der Quelldatenträger eine Seriennummer des Datenträgers, verfügt **Diskcopy** erstellt eine neue Volumeseriennummer für den Zieldatenträger und zeigt die Anzahl an, wenn der Kopiervorgang abgeschlossen ist.
-   Das Auslassen der Laufwerk-Parameter

    Wenn Sie weglassen der *Laufwerk2* Parameter **Diskcopy** verwendet das aktuelle Laufwerk als das Ziellaufwerk. Wenn Sie beide Laufwerkparameter weglassen **Diskcopy** verwendet das aktuelle Laufwerk für beide. Wenn das aktuelle Laufwerk entspricht *Laufwerk1*, **Diskcopy** fordert Sie auf den Datenträger nach Bedarf austauschen.
-   Mit nur einem Laufwerk kopieren

    Führen Sie **Diskcopy** Laufwerk von einem anderen Laufwerk als das Diskettenlaufwerk ein, z. B. C. Wenn Diskette *Laufwerk1* und Diskette *Laufwerk2* sind identisch, **Diskcopy** fordert Sie auf den Datenträger zu wechseln. Wenn der Datenträger mehr Informationen enthält als der verfügbare Arbeitsspeicher enthalten kann, **Diskcopy** kann nicht gelesen werden alle Informationen auf einmal. **Diskcopy** vom Quelldatenträger liest, schreibt in die Ziel-Datenträger und fordert Sie auf den Quelldatenträger erneut einfügen. Dieser Prozess wird fortgesetzt, bis Sie das gesamte Laufwerk kopiert haben.
-   Vermeiden der Fragmentierungsgrad eines Datenträgers

    Fragmentierung ist das Vorhandensein von kleine Bereiche des nicht verwendeten Speicherplatzes zwischen vorhandenen Dateien auf einem Datenträger. Der Prozess suchen, lesen oder Schreiben von Dateien kann fragmentierte Quelldatenträgers verlangsamen.

    Da **Diskcopy** macht eine genaue Kopie der Quelldatenträger auf dem Zieldatenträger, jegliche Fragmentierung auf dem Datenträger für die Datenquelle auf dem Zieldatenträger übertragen wird. Verwenden Sie zum Übertragen der Fragmentierung von einem Datenträger zu einem anderen vermeiden **Kopie** oder **Xcopy** um Ihre Datenträger zu kopieren. Da **Kopie** und **Xcopy** kopieren Dateien sequenziell, den neuen Datenträger wird nicht fragmentiert.

> [!NOTE]
> Sie können keine **Xcopy** ein Startdatenträger zu kopieren.
-   Grundlegendes zu **Diskcopy** Exitcodes

    In der folgende Tabelle wird erläutert, jede Exitcode.  
    |Exitcode|Beschreibung|
    |---------|-----------|
    |0|Copy-Vorgang war erfolgreich.|
    |1|Lese-/Schreibzugriff-Fehler|
    |3|Schwerwiegender Fehler aufgetreten ist.|
    |4|Fehler bei der Initialisierung aufgetreten ist.|

    Die Exitcodes zu verarbeiten, die von zurückgegeben werden **Diskcomp**, können Sie die *ERRORLEVEL* Umgebungsvariable auf den **Wenn** Befehlszeile in einem Batchprogramm.

## <a name="BKMK_examples"></a>Beispiele für

Um den Datenträger im Laufwerk B auf die Diskette in Laufwerk A zu kopieren, geben Sie Folgendes ein:
```
diskcopy b: a:
```
Um das Diskettenlaufwerk ein verwenden, um eine Diskette in einen anderen zu kopieren, wechseln Sie dazu zunächst auf das Laufwerk C, und geben Sie dann:

Diskcopy a: a:

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)