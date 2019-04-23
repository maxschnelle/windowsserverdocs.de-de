---
title: WinSAT mfmedia
description: Windows-Befehle
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09a3b3dd-f746-4e6e-b684-76a9bde0c78d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 69ce4fac127a6af8a94f3800d62c45989cf7020b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845431"
---
# <a name="winsat-mfmedia"></a>WinSAT mfmedia



Misst die Leistung der video Decodierung (Wiedergabe) mit dem Media Foundation-Framework.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
winsat mfmedia <parameters>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|----------|-----------|
|-Eingabe \<Dateiname >|Erforderlich: Geben Sie die Datei mit den Videoclip wiedergegeben oder codiert werden soll. Die Datei kann in einem beliebigen Format sein, die von Media Foundation gerendert werden können.|
|-dumpgraph|Geben Sie an, dass im Filterdiagramm in eine GraphEdit-kompatible Datei gespeichert werden soll, bevor die Bewertung beginnt.|
|-ns|Geben Sie an, dass im Filterdiagramm in der Eingabedatei der normale wiedergabegeschwindigkeit ausgeführt werden soll. Standardmäßig wird so schnell wie möglich ausgeführt werden, wird ignoriert, wie oft die Präsentation im Filterdiagramm ausgeführt.|
|-Spielen|Führen Sie die Bewertung in decodieren, Modus und Wiedergabe, die alle Audioinhalte in der Datei im angegebenen bereitgestellten **-Eingabe** DirectSound Standardgerät verwenden. Standardmäßig ist die Audiowiedergabe deaktiviert.|
|-nopmp|Machen Sie verwenden, der die Media Foundation Protected Media Pipeline (MFPMP) nicht verarbeiten, während der Bewertung.|
|-pmp|Stellen Sie immer die MFPMP verwenden bei der Bewertung verarbeiten.</br>Hinweis: Wenn **- Pmp** oder **- Nopmp** nicht angegeben ist, MFPMP wird nur bei Bedarf verwendet werden.|
|-v|Senden Sie ausführlichen Ausgabe an STDOUT, einschließlich Status und Fortschritt Informationen. Fehler werden auch das Befehlsfenster geschrieben werden.|
|-XML- \<Dateiname >|Speichern Sie die Ausgabe der Bewertung der angegebenen XML-Datei ein. Wenn die angegebene Datei vorhanden ist, wird sie überschrieben.|
|-idiskinfo|Speichern von Informationen zu physischen Datenträgern und logische Datenträger als Teil der  **\<SystemConfig >** Abschnitt in der XML-Ausgabe.|
|-iguid|Erstellen Sie einen global eindeutigen Bezeichner (GUID), in die XML-Ausgabedatei.|
|– Beachten Sie "Text" Hinweis "|Fügen Sie den Text der Anmerkung, die  **\<Hinweis >** Abschnitt in der XML-Ausgabedatei.|
|-icn|Schließen Sie Namen des lokalen Computers in die XML-Ausgabedatei an.|
|-eef|Auflisten von zusätzlichen Systeminformationen in die XML-Ausgabedatei.|

## <a name="BKMK_examples"></a>Beispiele für

-   Im folgenden Beispiel wird die Bewertung mit der Eingabedatei, die während der verwendet wird eine **Winsat formale** ohne Verwendung der Media Foundation Protected Media Pipeline (MFPMP), auf einem Computer, in denen c:\windows der Speicherort der ist-Bewertung der Windows-Ordner.  
    ```
    winsat mfmedia -input c:\windows\performance\winsat\winsat.wmv -nopmp
    ```

## <a name="remarks"></a>Hinweise

-   Ist erforderlich, um verwenden mindestens die Mitgliedschaft in der lokalen Gruppe "Administratoren" oder entsprechende **Winsat**. Der Befehl muss von einer Eingabeaufforderung mit erhöhten Rechten ausgeführt werden.
-   Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie auf **starten**, klicken Sie auf **Zubehör**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie auf **als AdministratorAusführen**.

#### <a name="additional-references"></a>Weitere Verweise

