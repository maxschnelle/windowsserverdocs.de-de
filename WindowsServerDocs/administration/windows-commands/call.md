---
title: Anruf
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d34a41dc-e6c7-4467-bf6a-15cec704833e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/05/2018
ms.openlocfilehash: 1f5253700f2932b2afa725163121e64ea4c1748d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434582"
---
# <a name="call"></a>Anruf



Ruft eine Batchdatei aus einem anderen ohne das übergeordnete Batchprogramm beenden zu müssen. Die **Aufrufen** Befehl akzeptiert Bezeichnungen als Ziel des Aufrufs.

> [!NOTE]
> **Rufen Sie** hat keine Auswirkung an der Eingabeaufforderung ein, wenn sie außerhalb einer Skript- oder Batchausführung-Datei verwendet wird.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
call [Drive:][Path]<FileName> [<BatchParameters>] [:<Label> [<Arguments>]]
```

## <a name="parameters"></a>Parameter

|           Parameter           |                                                                         Beschreibung                                                                          |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [\<Drive>:][<Path>]<FileName> | Gibt den Speicherort und Namen, der die Batch-Anwendung, die Sie aufrufen möchten. Die *FileName* -Parameter ist erforderlich, und sie muss eine BAT- oder cmd-Erweiterung. |
|      \<BatchParameters>       |                                            Gibt alle Angaben in der Befehlszeile, die von der Batch-Anwendung erforderlich sind.                                             |
|           :\<Label>           |                                            Gibt die Bezeichnung, die ein Batch-Programmsteuerung zu springen soll.                                             |
|         \<Arguments>          |                     Gibt die Befehlszeile Informationen an die neue Instanz des aufzurufenden Programms, beginnend bei zu übergebenden *: Bezeichnung.*                     |
|              /?               |                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                             |

## <a name="batch-parameters"></a>Batchparameter

Die Batch-Skriptverweise Argument ( **%0**, **%1**,...) werden in den folgenden Tabellen aufgeführt.

**%** * in einem Batch von Skripts, bezieht sich auf alle Argumente (z. B. **%1**, **%2**, **%3**...)

Können Sie die folgenden optionalen Syntaxen als Ersatz für Batchparameter ( **%n**):

|Batchparameter|Beschreibung|
|---------------|-----------|
|%~1|Wird erweitert, **%1** und entfernt, die umgebenden Anführungszeichen ("").|
|%~f1|Wird erweitert, **%1** in einen vollständig qualifizierten Pfad.|
|%~d1|Wird erweitert, **%1** nur einen Laufwerkbuchstaben.|
|%~p1|Wird erweitert, **%1** nur zu einem Pfad.|
|%~n1|Wird erweitert, **%1** nur zu einer Datei.|
|%~x1|Wird erweitert, **%1** mit nur einer Dateierweiterung.|
|%~s1|Wird erweitert, **%1** in einen vollqualifizierten Pfad, der nur einen kurze Namen enthält.|
|%~a1|Wird erweitert, **%1** an den Dateiattributen.|
|%~t1|Wird erweitert, **%1** auf das Datum und Uhrzeit der Datei.|
|%~z1|Wird erweitert, **%1** auf die Größe der Datei.|
|%~$PATH:1|Durchsucht die Verzeichnisse, die in der PATH-Umgebungsvariablen aufgelistet, und erweitert **%1** auf den vollqualifizierten Namen der das erste Verzeichnis gefunden. Wenn der Name der Umgebungsvariablen nicht definiert ist oder die Datei wird von der Suche nicht gefunden, wird dieser Modifizierer auf eine leere Zeichenfolge erweitert.|

Die folgende Tabelle zeigt, wie Sie die Modifizierer mit den Batchparametern für zusammengesetzte Ergebnisse kombinieren können:

|Batchparameter mit dem Modifizierer|Beschreibung|
|-----------------------------|-----------|
|%~dp1|Wird erweitert, **%1** auf einem Laufwerkbuchstaben und Pfad nur.|
|%~nx1|Wird erweitert, **%1** , einen Dateinamen und die Erweiterung nur.|
|%~dp$PATH:1|Durchsucht den in der PATH-Umgebungsvariable für die aufgeführten Verzeichnisse **%1**, und klicken Sie dann erweitert, um den Laufwerkbuchstaben und Pfad, der das erste Verzeichnis gefunden.|
|%~ftza1|Wird erweitert, **%1** zur Anzeige der Ausgabe ähnelt der **Dir** Befehl.|

In den obigen Beispielen **%1** und der Pfad kann durch andere Werte gültige Werte ersetzt werden. Die <strong>%~</strong> Syntax wird durch ein gültiges Argument Anzahl beendet. Die <strong>%~</strong> Modifizierer können nicht verwendet werden, mit ** %\\***.

## <a name="remarks"></a>Hinweise

-   Verwenden von Batchparametern

    Batchparameter darf keine Informationen, die Sie in einem Batchprogramm, z. B. Befehlszeilenoptionen, Dateinamen, die Batchparameter übergeben können **%0** über **%9**, und Variablen (z. B. **Baud %** ).
-   Mithilfe der *Bezeichnung* Parameter

    Mithilfe von **Aufrufen** mit der *Bezeichnung* Parameter, Sie erstellen einen neuen Kontext von Batch-Datei und übergibt die Steuerung an die Anweisung nach der angegebenen Bezeichnung. Beim ersten Ende der Batchdatei auftritt (d. h. nachdem Springen zur Bezeichnung), Steuerelement zurückgegeben wird, an die Anweisung nach der **Aufrufen** Anweisung. Das Ende der Batchdatei gefunden wird, das zum zweiten Mal wird der Batchskript wurde beendet.
-   Pipes und Umleitungssymbole

    Verwenden Sie keine Pipes ( **|** ) und Umleitungssymbole ( **<** oder **>** ) mit **Aufrufen**.
-   Rekursive Aufrufe

    Sie können eine Batchdatei erstellen, die sich selbst aufruft. Allerdings müssen Sie eine beenden-Bedingung angeben. Andernfalls können die Batch-Programme von übergeordneten und untergeordneten endlos durchlaufen wird.
-   Arbeiten mit befehlserweiterungen

    Wenn der befehlserweiterungen aktiviert sind, **Aufrufen** akzeptiert *Bezeichnung* als Ziel des Aufrufs. Die richtige Syntax lautet wie folgt:

    `call :\<Label> <Arguments>`

## <a name="BKMK_examples"></a>Beispiele für

Um das Programm Checknew.bat aus einem anderen Batchprogramm auszuführen, geben Sie den folgenden Befehl in der übergeordneten Batch-Anwendung:
```
call checknew
```
Wenn das übergeordnete Batchprogramm zwei Batchparameter akzeptiert, und Sie diesen Parameter an Checknew.bat übergeben soll, geben Sie den folgenden Befehl in der übergeordneten Batch-Anwendung:
```
call checknew %1 %2
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)