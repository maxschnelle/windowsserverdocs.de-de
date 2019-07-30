---
title: more
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ded14f6a-d82f-4aeb-a2d8-7ec1c94dfb8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/26/2019
ms.openlocfilehash: 291d98492f3f2b200ff0567c28a97927ca8c75be
ms.sourcegitcommit: e55e27143dad1d3fb956cfdac4c23ef4186af321
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2019
ms.locfileid: "68603231"
---
# <a name="more"></a>more



Zeigt jeweils einen Bildschirm der Ausgabe an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
<Command> | more [/c] [/p] [/s] [/t<N>] [+<N>]
more [[/c] [/p] [/s] [/t<N>] [+<N>]] < [<Drive>:][<Path>]<FileName>
more [/c] [/p] [/s] [/t<N>] [+<N>] [<Files>]
```

## <a name="parameters"></a>Parameter

|           Parameter            |                               Beschreibung                               |
|--------------------------------|-------------------------------------------------------------------------|
|           \<Befehls >           |      Gibt einen Befehl an, für den die Ausgabe angezeigt werden soll.      |
|               /c               |               Löscht den Bildschirm, bevor eine Seite angezeigt wird.               |
|               /p               |                      Erweitert Formular-Feed-Zeichen.                      |
|               /s               |          Zeigt mehrere leere Zeilen als einzelne Leerzeile an.          |
|             /t\<N >             |         Zeigt Registerkarten als Anzahl von Leerzeichen an, die durch *N*angegeben werden.         |
|             +\<N >              |     Zeigt die erste Datei an, die in der durch *N*angegebenen Zeile beginnt.     |
| [\<Laufwerk >:] [\<Pfad >]\<Dateiname > |          Gibt den Speicherort und den Namen einer Datei an, die angezeigt werden soll.          |
|            \<Dateien >            | Gibt eine Liste der anzuzeigenden Dateien an. Trennen Sie die Dateinamen durch ein Leerzeichen. |
|               /?               |                  Zeigt die Hilfe an der Eingabeaufforderung an.                   |

## <a name="remarks"></a>Hinweise

-   Die folgenden Unterbefehle werden an der **ausführlicheren** Eingabeaufforderung`-- More --`() akzeptiert. 

    | Key | Aktion |
    | --- | ------ |
    | LEERTASTE | Zeigt die nächste Seite an. |
    | EINGABETASTE | Zeigt die nächste Zeile an. |
    | f | Zeigt die nächste Datei an. |
    | q | Beendet den **weiteren** Befehl. |
    | = | Zeigt die Zeilennummer an. |
    | p \<N > | Zeigt die nächsten *N* Zeilen an. |
    | s \<N > |S kippt die nächsten *N* Zeilen. |
    | ? | Zeigt die Befehle an, die an der **ausführlicheren** Eingabeaufforderung verfügbar sind.| 
    
-   Wenn Sie das-Umleitungs **<** Zeichen () verwenden, müssen Sie einen Dateinamen als Quelle angeben. Wenn Sie die Pipe ( **\|** ) verwenden, können Sie diese Befehle wie **dir**, **Sort**und **Type**verwenden.
-   Der **Weitere** Befehl mit unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie einen der folgenden Befehle ein, um den ersten Bildschirm der Informationen einer Datei mit dem Namen Clients. New anzuzeigen:
```
more < clients.new
type clients.new | more
```
Der Befehl **Weitere** zeigt den ersten Bildschirm der Informationen von Clients. neu an und zeigt dann die folgende Eingabeaufforderung an:
```
-- More --
```
Sie können dann die Leertaste drücken, um den nächsten Bildschirm anzuzeigen.

Geben Sie einen der folgenden Befehle ein, um den Bildschirm zu löschen und alle zusätzlichen leeren Zeilen vor dem Anzeigen der Datei Clients. New zu entfernen:
```
more /c /s < clients.new
type clients.new | more /c /s
```
Der Befehl **Weitere** zeigt den ersten Bildschirm der Informationen von Clients. neu an und zeigt dann die folgende Eingabeaufforderung an:
```
-- More --
```

### <a name="using-more-subcommands"></a>Verwenden von weiteren unter Befehlen

Die folgenden Beispiele können an der **ausführlicheren** Eingabeaufforderung (`-- More --`) verwendet werden.
- Drücken **Sie die Eingabe** Taste, um die Datei nacheinander anzuzeigen.
- Um den nächsten Bildschirm anzuzeigen, drücken Sie die Leertaste an **der Eingabeaufforderung** .
- Wenn Sie die nächste Datei anzeigen möchten, die in der Befehlszeile aufgelistet ist, geben Sie **f** **an der Eingabe** Aufforderung ein.
- **Geben Sie** ein, um die verfügbaren Befehle anzuzeigen. an der **ausführlicheren** Aufforderung.
- Um **Weitere Informationen**zu erhalten, geben Sie **q** **an der Eingabe** Aufforderung ein.
- Wenn Sie die aktuelle Zeilennummer anzeigen möchten **=** , geben Sie **an der Eingabe** Aufforderung ein. Die aktuelle Zeilennummer wird wie folgt der **weiteren** Eingabeaufforderung hinzugefügt:  
  ```
  -- More [Line: 24] --
  ```  
- Wenn Sie eine bestimmte Anzahl von Zeilen anzeigen möchten, geben Sie **p** **an der Eingabe** Aufforderung ein. **Weitere** werden Sie aufgefordert, die Anzahl der anzuzeigenden Zeilen wie folgt anzuzeigen:  
  ```
  -- More -- Lines:
  ```  
  Geben Sie die Anzahl der anzuzeigenden Zeilen ein, und drücken Sie dann die EINGABETASTE. **Weitere** zeigt die angegebene Anzahl von Zeilen an.
- Um eine bestimmte Anzahl von Zeilen zu überspringen, geben Sie **s** **an der Eingabe** Aufforderung ein. **Weitere** werden Sie aufgefordert, die Anzahl der zu über springenden Zeilen wie folgt zu überspringen:  
  ```
  -- More -- Lines:
  ```  
  Geben Sie die Anzahl der zu über springenden Zeilen ein, und drücken Sie die EINGABETASTE. **Mehr** überspringt die angegebene Anzahl von Zeilen und zeigt den nächsten Bildschirm der Informationen an.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
