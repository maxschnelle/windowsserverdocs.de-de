---
title: Aufruf
description: Referenz Artikel für den Aufruf Befehl, der ein Batch Programm von einem anderen aufruft, ohne das übergeordnete Batch Programm zu beenden.
ms.topic: reference
ms.assetid: d34a41dc-e6c7-4467-bf6a-15cec704833e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/05/2018
ms.openlocfilehash: 749f073fa3f96f51aec5bf47e4e09ce7263d3205
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034258"
---
# <a name="call"></a>Aufruf

Ruft ein Batch Programm von einem anderen auf, ohne das übergeordnete Batch Programm zu beenden. Der **Befehl "** Befehl" akzeptiert Bezeichnungen als Ziel des Aufrufes.

> [!NOTE]
> Der-Befehl hat an der Eingabeaufforderung keine Auswirkung, wenn er außerhalb eines Skripts oder einer Batchdatei verwendet wird.

## <a name="syntax"></a>Syntax

```
call [drive:][path]<filename> [<batchparameters>] [:<label> [<arguments>]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `[<drive>:][<path>]<filename>` | Gibt den Speicherort und den Namen des aufzurufenden Batch Programms an. Der `<filename>` -Parameter ist erforderlich und muss über die Erweiterung ". bat" oder ". cmd" verfügen. |
| `<batchparameters>` | Gibt alle Befehlszeilen Informationen an, die vom Batch Programm benötigt werden. |
| `:<label>` | Gibt die Bezeichnung an, zu der ein Batch Programm-Steuerelement springen soll. |
| `<arguments>` | Gibt die Befehlszeilen Informationen an, die an die neue Instanz des Batch-Programms, beginnend bei, geleitet werden `:<label>` .|
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="batch-parameters"></a>Batch Parameter

Die Batch Skript-Argument Verweise (**%0**, **%1**,...) sind in den folgenden Tabellen aufgeführt.

Die Verwendung des Werts " **% &#42;** " in einem Batch Skript bezieht sich auf alle Argumente (z. b. **%1**, **%2**, **%3**...).

Sie können die folgenden optionalen Syntaxen als Ersatz für Batch Parameter (**% n**) verwenden:

| Batch-Parameter | Beschreibung |
| --------------- | ----------- |
| % ~ 1 | Erweitert **%1** und entfernt umgebende Anführungszeichen. |
| % ~ F1 | " **%1** " wird in einen voll qualifizierten Pfad erweitert. |
| % ~ D1 | " **%1** " wird nur auf einen Laufwerk Buchstaben erweitert. |
| % ~ P1 | " **%1** " wird nur in einen Pfad erweitert. |
| % ~ N1 | " **%1** " wird nur in einen Dateinamen erweitert. |
| % ~ x1 | " **%1** " wird nur zu einer Dateinamenerweiterung erweitert. |
| % ~ S1 | **%1** wird auf einen voll qualifizierten Pfad erweitert, der nur Kurznamen enthält. |
| % ~ a1 | **%1** wird auf die Dateiattribute erweitert. |
| % ~ T1 | Erweitert **%1** auf das Datum und die Uhrzeit der Datei. |
| % ~ Z1 | Erweitert **%1** auf die Größe der Datei. |
| % ~ $Path: 1 | Durchsucht die Verzeichnisse, die in der PATH-Umgebungsvariablen aufgelistet sind, und erweitert **%1** auf den voll qualifizierten Namen des ersten gefundenen Verzeichnisses. Wenn der Name der Umgebungsvariablen nicht definiert ist oder die Datei von der Suche nicht gefunden wird, wird dieser Modifizierer auf die leere Zeichenfolge erweitert. |

In der folgenden Tabelle wird gezeigt, wie Modifizierern mit den Batch Parametern für Verbund Ergebnisse kombiniert werden können:

| Batch-Parameter mit Modifizierer | Beschreibung |
| ----------------------------- | ----------- |
| % ~ DP1 | " **%1** " wird nur auf einen Laufwerk Buchstaben und einen Pfad erweitert. |
| % ~ NX1 | " **%1** " wird nur in einen Dateinamen und eine Erweiterung erweitert. |
| % ~ DP $ Pfad: 1 | Durchsucht die Verzeichnisse, die in der PATH-Umgebungsvariablen für **%1**aufgelistet sind, und wird dann auf den Laufwerk Buchstaben und den Pfad des ersten gefundenen Verzeichnisses erweitert. |
| % ~ ftza1 | Erweitert **%1** , um eine Ausgabe ähnlich dem **dir** -Befehl anzuzeigen. |

In den obigen Beispielen können **%1** und path durch andere gültige Werte ersetzt werden. Die **%~** Syntax wird mit einer gültigen Argument Nummer beendet. Die **%~** modifiziererer können nicht mit **% #b0 **verwendet werden.

### <a name="remarks"></a>Bemerkungen

- Verwenden von Batch-Parametern:

    Batch Parameter können alle Informationen enthalten, die an ein Batch-Programm übergeben werden können, einschließlich Befehlszeilenoptionen, Dateinamen, Batch Parameter **%0** bis **%9**und Variablen (z. b. **% Baud%**).

- Verwenden des- `<label>` Parameters:

    Wenn Sie einen- **Befehl mit dem** - `<label>` Parameter verwenden, erstellen Sie einen neuen Batchdatei Kontext und übergeben die Steuerung an die Anweisung nach der angegebenen Bezeichnung. Wenn das Ende der Batchdatei das erste Mal erreicht wird (d. h. nach dem Springen zur Bezeichnung), wird die Steuerung an die Anweisung nach der **Aufruf** Anweisung zurückgegeben. Das zweite Mal, wenn das Ende der Batchdatei gefunden wird, wird das Batch Skript beendet.

- Verwenden von Pipes und Umleitungs Symbolen:

    Verwenden Sie keine Pipes `(|)` oder Umleitungs Symbole ( `<` oder `>` ) **call**mit dem-Befehl.

- Rekursiver Rückruf

    Sie können ein Batch-Programm erstellen, das sich selbst aufruft. Sie müssen jedoch eine Exit-Bedingung angeben. Andernfalls können das übergeordnete und das untergeordnete Batch Programm Endlosschleifen.

- Arbeiten mit Befehls Erweiterungen

    Wenn Befehls Erweiterungen aktiviert **sind, wird** `<label>` als Ziel des Aufrufes akzeptiert. Die korrekte Syntax lautet: `call :<label> <arguments>`

## <a name="examples"></a>Beispiele

Um das checknew.bat Programm von einem anderen Batch Programm auszuführen, geben Sie den folgenden Befehl in das übergeordnete Batch-Programm ein:

```
call checknew
```

Wenn das übergeordnete Batch-Programm zwei Batch Parameter annimmt und Sie diese Parameter an checknew.bat übergeben möchten, geben Sie den folgenden Befehl in das übergeordnete Batch-Programm ein:

```
call checknew %1 %2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
