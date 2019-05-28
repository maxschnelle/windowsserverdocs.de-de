---
title: Cmd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ec588db-31a9-4a73-a970-65a2c6f4abbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d9b99dbe7e26190e87c5dfc9de29980b9cb2f43
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192586"
---
# <a name="cmd"></a>Cmd

Startet eine neue Instanz der den Befehlsinterpreter, Cmd.exe. Wenn Sie ohne Angabe von Parametern **Cmd** zeigt die Version und urheberrechtliche Informationen des Betriebssystems.

## <a name="syntax"></a>Syntax

```
cmd [/c|/k] [/s] [/q] [/d] [/a|/u] [/t:{<B><F>|<F>}] [/e:{on|off}] [/f:{on|off}] [/v:{on|off}] [<String>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/c|Führt den Befehl anhand des *Zeichenfolge* und dann beendet wird.|
|/k|Führt den Befehl anhand des *Zeichenfolge* und wird fortgesetzt.|
|/s|Ändert die Behandlung von *Zeichenfolge* nach **/c** oder **/k**.|
|/q|Deaktiviert das Echo.|
|/d|Deaktiviert die Ausführung des AutoRun-Befehle.|
|/a|Formatiert die Ausgabe einer Pipe oder einer Datei interner Befehl als American National Standards Institute (ANSI).|
|/u|Formatiert die Ausgabe der internen Befehle in einer Pipe oder eine Datei im Unicode-Format.|
|/ t: {\<B\>\<F\>\|\<F\>}|Wird für den Hintergrund (*B*) und die Vordergrundfarbe (*F*) Farben.|
|/e:on|Befehlserweiterungen wird aktiviert.|
|/e:off|Deaktiviert Befehle Erweiterungen.|
|/f:on|Ermöglicht Datei- und Vervollständigung von Objektnamen an.|
|/f:off|Deaktiviert die Vervollständigung von Dateien und Verzeichnisse.|
|/v:on|Ermöglicht das verzögerte Erweiterung von Umgebungsvariablen.|
|/v:off|Deaktiviert die verzögerte Erweiterung von Umgebungsvariablen.|
|\<String>|Gibt den Befehl aus, die, den Sie ausführen möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

Die folgende Tabelle enthält gültige hexadezimale Ziffern, mit denen Sie als Werte für \<B\> und \<F\>

|Wert|Farbe|
|-----|-----|
|0|Schwarz|
|1|Blau|
|2|Grün|
|3|Aqua|
|4|Rot|
|5|Lila|
|6|Gelb|
|7|Weiß|
|8|Grau|
|9|Hellblau|
|a|Hellgrün|
|b)|Hell aqua|
|c|Hellrot|
|d|Helles Lila|
|e|Hosttags in Gelb|
|f|Helle weiß|

## <a name="remarks"></a>Hinweise

-   Verwenden mehrerer Befehle

    Verwenden Sie für mehrere Befehle \<Zeichenfolge >, trennen sie die durch das Befehlstrennzeichen **&&** und schließen Sie diese in Anführungszeichen ein. Zum Beispiel:  
    ```
    "<Command>&&<Command>&&<Command>"
    ```  
-   Verarbeiten von Anführungszeichen

    Bei Angabe von **/c** oder **/k**, **Cmd** verarbeitet die restliche *Zeichenfolge* und Anführungszeichen werden nur beibehalten, wenn alle der folgenden Bedingungen erfüllt sind:  
    -   Verwenden Sie nicht **/s**.
    -   Sie verwenden, exakt eine Gruppe von Anführungszeichen.
    -   Sie verwenden keine Sonderzeichen innerhalb der Anführungszeichen (z. B.: & < > (), @ ^ |).
    -   Sie verwenden eine oder mehrere Leerzeichen innerhalb der Anführungszeichen.
    -   Die *Zeichenfolge* in Anführungszeichen ist der Name einer ausführbaren Datei.

    Wenn die vorherige Bedingung nicht erfüllt sind, *Zeichenfolge* durch Untersuchen der zum Überprüfen, ob ein öffnendes Anführungszeichen ist das erste Zeichen verarbeitet wird. Wenn das erste Zeichen ein öffnendes Anführungszeichen ist, wird er zusammen mit dem schließenden Anführungszeichen entfernt. Befolgen die schließenden Anführungszeichen Text wird beibehalten.
-   Ausführen von Registrierungsunterschlüsseln

    Wenn Sie keinen angeben **/d** in *Zeichenfolge*, Cmd.exe, sucht die folgenden Registrierungsunterschlüssel:

    **HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\AutoRun\REG_SZ**

    **HKEY_CURRENT_USER\Software\Microsoft\Command Processor\AutoRun\REG_EXPAND_SZ**

    Wenn eine oder beide Registrierungsunterschlüssel vorhanden sind, werden sie vor allen anderen Variablen ausgeführt.

> [!CAUTION]
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

-   Aktivieren und Deaktivieren von befehlserweiterungen

    Befehlserweiterungen sind in Windows XP standardmäßig aktiviert. Sie können diese für einen bestimmten Prozess deaktivieren, indem Sie mithilfe von **/e: off**. Sie können aktivieren oder Deaktivieren von Erweiterungen für alle **Cmd** Befehlszeilenoptionen, indem Sie folgende Einstellungen auf einem Computer oder Benutzer **REG_DWORD** Werte:

    **HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\EnableExtensions\REG_DWORD**

    **HKEY_CURRENT_USER\Software\Microsoft\Command Processor\EnableExtensions\REG_DWORD**

    Legen Sie die **REG_DWORD** Wert entweder **0 x 1** (aktiviert) oder **0 x 0** (deaktiviert) in der Registrierung mithilfe von Regedit.exe. Benutzerdefinierte Einstellungen haben Vorrang vor Einstellungen des Computers, und Befehlszeilenoptionen haben Vorrang vor registrierungseinstellungen.

> [!CAUTION]
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

    When you enable command extensions, the following commands are affected:  
    -  **assoc**
    -  **call**
    -  **chdir (cd)**
    -  **color**
    -  **del (erase)**
    -  **endlocal**
    -  **for**
    -  **ftype**
    -  **goto**
    -  **if**
    -  **mkdir (md)**
    -  **popd**
    -  **prompt**
    -  **pushd**
    -  **set**
    -  **setlocal**
    -  **shift**
    -  **start** (also includes changes to external command processes)

-   Aktivieren des verzögerten Erweiterung von Umgebungsvariablen

    Wenn Sie verzögerte umgebungsvariablenerweiterung zu aktivieren, können Sie Ausrufezeichens, ersetzen Sie den Wert einer Umgebungsvariablen zur Laufzeit.
-   Aktivieren der Datei- und Vervollständigung von Objektnamen

    Vervollständigung von Datei- und Verzeichnis ist nicht standardmäßig aktiviert. Sie können aktivieren oder deaktivieren Sie die Datei Vervollständigung von Objektnamen für einen bestimmten Prozess die **Cmd** Befehl **/f:** {**auf**|**aus**}. Sie können aktivieren oder deaktivieren Sie die Vervollständigung von Datei- und Verzeichnis für alle Prozesse, die von der **Cmd** Befehl auf einem Computer oder für eine benutzersitzung Anmeldung, indem Sie folgende Einstellungen **REG_DWORD** Werte:

    **HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\CompletionChar\REG_DWORD**

    **HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\PathCompletionChar\REG_DWORD**

    **HKEY_CURRENT_USER\Software\Microsoft\Command Processor\CompletionChar\REG_DWORD**

    **HKEY_CURRENT_USER\Software\Microsoft\Command Processor\PathCompletionChar\REG_DWORD**

    Festlegen der **REG_DWORD** Wert und Ausführen von Regedit.exe den hexadezimalen Wert eines Steuerzeichens für eine bestimmte Funktion verwenden (z. B. **0 x 9** Registerkarte und **0 x 08** ist RÜCKTASTE). Benutzerdefinierte Einstellungen haben Vorrang vor Einstellungen des Computers, und Befehlszeilenoptionen haben Vorrang vor registrierungseinstellungen.

> [!CAUTION]
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

Wenn Sie Dateien und Verzeichnisse Vervollständigung von Objektnamen mit aktivieren **/f: auf**, verwenden Sie STRG + D, für die Vervollständigung von Objektnamen und STRG + F Dateinamen. Um ein bestimmtes Vervollständigungszeichen in der Registrierung zu deaktivieren, verwenden Sie den Wert für Leerzeichen [**0 x 20**] da es sich nicht um ein gültiges Steuerelement Zeichen ist.

Wenn Sie STRG + D oder STRG + F drücken **Cmd** Vervollständigung von Datei- und Verzeichnis verarbeitet. Diese Kombination aus Funktionen fügen Sie einem Platzhalterzeichen *Zeichenfolge* (falls nicht vorhanden ist), erstellen Sie eine Liste der Pfade, die übereinstimmen, und zeigen Sie den ersten übereinstimmenden Pfad. Wenn keiner der Pfade übereinstimmen, wird die Datei- und Verzeichnisspeicher Name-Abschluss-Funktion gibt ein akustisches Signal und ändert sich nicht auf die Anzeige. Um durch die Liste der übereinstimmenden Pfaden zu verschieben, drücken Sie STRG + D oder STRG + F wiederholt. Um rückwärts durch die Liste zu verschieben, drücken Sie gleichzeitig die UMSCHALTTASTE und STRG + D oder STRG + F. Bearbeiten Sie zum verwerfen die Liste der übereinstimmenden Pfaden, und generieren eine neue Liste, *Zeichenfolge* , und drücken Sie STRG + D oder STRG + F. Wenn Sie STRG + D bis STRG + F wechseln, wird die Liste der übereinstimmenden Pfaden verworfen, und eine neue Liste generiert. Der einzige Unterschied zwischen den Tastenkombinationen von STRG + D und STRG + F ist, dass STRG + D nur Verzeichnisnamen und STRG + F sowohl Datei- und Verzeichnisnamen entspricht. Bei Verwendung von Dateien und Verzeichnisse Vervollständigung von Objektnamen auf einen der integrierten verzeichnisrolle Befehle (d. h. **CD**, **MD**, oder **RD**), Directory Abschluss wird davon ausgegangen.

Vervollständigung von Datei- und Verzeichnis verarbeitet ordnungsgemäß Dateinamen, die Leerzeichen oder Sonderzeichen enthalten, wenn Sie den entsprechenden Pfad in Anführungszeichen setzen.

Die folgenden Sonderzeichen sind Anführungszeichen erforderlich: & < > [] {} ^ =;! "+" ~ [Leerzeichen].

Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie Anführungszeichen um den Text (z. B. "Computername").

Wenn Sie Dateien und Verzeichnisse Vervollständigung von Objektnamen aus verarbeiten *Zeichenfolge*, Teil der *Pfad* rechts neben der Cursor wird verworfen (an der Stelle im *Zeichenfolge* , in dem die Vervollständigung verarbeitet wurde).

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
