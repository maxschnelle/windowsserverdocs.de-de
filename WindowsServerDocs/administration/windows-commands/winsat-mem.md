---
title: WinSAT mem
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cda017bf-6193-43c1-b71f-e379c23e1152
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7cdae81694a916905f36cdd9e941015e3ce5f15c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440081"
---
# <a name="winsat-mem"></a>WinSAT mem



Tests System Speicherbandbreite in einer Weise, die von großen Arbeitsspeicher-Puffer reflektierende kopiert, da bei der multimedia-Verarbeitung verwendet werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
winsat mem <parameters>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-up|Arbeitsspeicher, die Tests mit nur einem Thread zu erzwingen. Der Standardwert ist ein Thread pro physischen CPU- oder Core ausführen.|
|-rn|Geben Sie an, dass die Bewertung des Threads mit normaler Priorität ausgeführt werden soll. Der Standardwert ist 15-Priorität ausgeführt.|
|-nc|Geben Sie an, dass die Bewertung sollte Arbeitsspeicher zuweisen und kennzeichnen es als nicht zwischengespeichert. Dies bedeutet, dass der Prozessor des Caches für Kopiervorgänge umgangen werden werden. Der Standardwert ist im Cache Speicherplatz ausgeführt.|
|-do \<n>|Geben Sie den Abstand in Byte, zwischen dem Ende der Quellpuffer und dem Beginn des Zielpuffers. Der Standardwert ist 64 Bytes. Die maximale zulässige Zieloffset beträgt 16MB. Angeben eines Offsets ungültiges Ziel führt zu einem Fehler.</br>Hinweis: 0 (null) ist ein gültiger Wert für  **\<n >** , negative Zahlen sind jedoch nicht.|
|-Mint \<n >|Geben Sie die minimale Zeit in Sekunden für die Bewertung ausgeführt. Der Standardwert ist 2.0. Der Mindestwert ist 1.0. Der maximale Wert ist 30,0.</br>Hinweis: Angeben einer **-Mint** Wert größer als die **- Maxt** Wert, wenn die beiden Parameter in Kombination verwendet werden zu einem Fehler führt.|
|-Maxt \<n >|Geben Sie die maximal zulässige Laufzeit in Sekunden für die Bewertung. Der Standardwert ist 5.0. Der Mindestwert ist 1.0. Der maximale Wert ist 30,0. Wenn Sie in Kombination mit der **-Mint** Parameter, die Bewertung beginnt die Vorgehensweise statistische periodisch ausgeführten Überprüfung über die Ergebnisse nach der im angegebenen Zeitraum **-Mint**. Wenn die statistische Prüfungen, die Bewertung wird abgeschlossen ist, bevor die im angegebenen Zeitraum **- Maxt** ist abgelaufen. Wenn die Bewertung für die im angegebenen Zeitraum erfolgt **- Maxt** ohne zu diesem Zeitpunkt abgeschlossen und die Ergebnisse zurückgeben werden erfüllen, die statistische überprüft, und klicken Sie dann auf der Bewertung wurden erfasst.|
|-Buffersize \<n >|Geben Sie die Größe des Puffers, die die Speichertest Kopie verwenden soll. Dieser Betrag wird zweimal pro CPU, zugeordnet werden, der bestimmt, die Menge der Daten aus einem Puffer in einen anderen kopiert. Der Standardwert ist 16MB. Dieser Wert wird auf die nächsten 4-KB-Grenze gerundet. Der maximale Wert beträgt 32MB. Der minimale Wert beträgt 4 KB. Gibt eine ungültige Puffergröße führt zu einem Fehler.|
|-v|Senden Sie ausführlichen Ausgabe an STDOUT, einschließlich Status und Fortschritt Informationen. Fehler werden auch das Befehlsfenster geschrieben werden.|
|-XML- \<Dateiname >|Speichern Sie die Ausgabe der Bewertung der angegebenen XML-Datei ein. Wenn die angegebene Datei vorhanden ist, wird sie überschrieben.|
|-idiskinfo|Speichern von Informationen zu physischen Datenträgern und logische Datenträger als Teil der  **\<SystemConfig >** Abschnitt in der XML-Ausgabe.|
|-iguid|Erstellen Sie einen global eindeutigen Bezeichner (GUID), in die XML-Ausgabedatei.|
|– Beachten Sie "Text" Hinweis "|Fügen Sie den Text der Anmerkung, die  **\<Hinweis >** Abschnitt in der XML-Ausgabedatei.|
|-icn|Schließen Sie Namen des lokalen Computers in die XML-Ausgabedatei an.|
|-eef|Auflisten von zusätzlichen Systeminformationen in die XML-Ausgabedatei.|

## <a name="BKMK_examples"></a>Beispiele für

- Im folgenden Beispiel wird die Bewertung für ein Minimum von vier Sekunden und nicht mehr als 12 Sekunden, die unter Verwendung einer 32MB-Puffergröße, und speichern die Ergebnisse im XML-Format in die Datei **memtest.xml**.  
  ```
  winsat mem -mint 4.0 -maxt 12.0 -buffersize 32MB -xml memtest.xml
  ```

## <a name="remarks"></a>Hinweise

-   Ist erforderlich, um verwenden mindestens die Mitgliedschaft in der lokalen Gruppe "Administratoren" oder entsprechende **Winsat**. Der Befehl muss von einer Eingabeaufforderung mit erhöhten Rechten ausgeführt werden.
-   Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie auf **starten**, klicken Sie auf **Zubehör**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie auf **als AdministratorAusführen**.

#### <a name="additional-references"></a>Weitere Verweise

