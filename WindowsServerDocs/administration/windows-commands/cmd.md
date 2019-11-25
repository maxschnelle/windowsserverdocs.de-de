---
title: Cmd
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 032fbea2039faa09753ac0c2b51e4b62004d36ac
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379333"
---
# <a name="cmd"></a>Cmd

Startet eine neue Instanz des Befehls interpreterers, cmd. exe. Bei Verwendung ohne Parameter zeigt **cmd** die Version und die Copyright Informationen des Betriebssystems an.

## <a name="syntax"></a>Syntax

```
cmd [/c|/k] [/s] [/q] [/d] [/a|/u] [/t:{<B><F>|<F>}] [/e:{on|off}] [/f:{on|off}] [/v:{on|off}] [<String>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/c|Führt den durch die *Zeichenfolge* angegebenen Befehl aus und wird dann beendet.|
|/k|Führt den durch die *Zeichenfolge* angegebenen Befehl aus und wird fortgesetzt.|
|/s|Ändert die Behandlung der *Zeichenfolge* nach **/c** oder **/k**.|
|/q|Schaltet das Echo ein.|
|/d|Deaktiviert die Ausführung von Autorun-Befehlen.|
|/a|Formatiert die Ausgabe eines internen Befehls in eine Pipe oder eine Datei als American National Standards Institute (ANSI).|
|/u|Formatiert die interne Befehlsausgabe in eine Pipe oder eine Datei als Unicode.|
|/t: {\<B\>\<f\>\|\<f\>}|Legt die Hintergrundfarben (*B*) und Vordergrund Farben (*F*) fest.|
|/e: ein|Aktiviert Befehls Erweiterungen.|
|/e: Off|Deaktiviert Befehls Erweiterungen.|
|/f: ein|Ermöglicht das Abschließen von Datei-und Verzeichnisnamen.|
|/f: Off|Deaktiviert den Abschluss von Datei-und Verzeichnisnamen.|
|/v: ein|Ermöglicht die verzögerte Erweiterung der Umgebungsvariablen.|
|/v: Off|Deaktiviert die Erweiterung der verzögerten Umgebungsvariablen.|
|\<Zeichenfolge >|Gibt den Befehl an, den Sie ausführen möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

In der folgenden Tabelle werden gültige hexadezimale Ziffern aufgelistet, die Sie als Werte für \<B\> und \<F verwenden können\>

|Wert|Farbe|
|-----|-----|
|0|Black|
|1|Blau|
|2|Grün|
|3|CE|
|4|Rot|
|5|Viol|
|6|Gelb|
|7|White|
|8|Grau|
|9|Hellblau|
|a|Hellgrün|
|b)|Hell Aqua|
|c|Hellrot|
|d|Hell lila|
|Fresser|Hellgelb|
|f|Helles Weiß|

## <a name="remarks"></a>Hinweise

-   Verwenden mehrerer Befehle

    Wenn Sie mehrere Befehle für \<Zeichenfolge > verwenden möchten, trennen Sie diese durch das Befehls Trennzeichen **&&** und schließen Sie Sie in Anführungszeichen ein. Zum Beispiel:

    ```
    "<Command>&&<Command>&&<Command>"
    ``` 
 
-   Verarbeiten von Anführungszeichen

    Wenn Sie **/c** oder **/k**angeben, verarbeitet **cmd** den Rest der *Zeichenfolge,* und Anführungszeichen werden nur beibehalten, wenn alle der folgenden Bedingungen erfüllt sind:  
    -   **/S**wird nicht verwendet.
    -   Sie verwenden genau einen Satz von Anführungszeichen.
    -   Sie verwenden keine Sonderzeichen innerhalb der Anführungszeichen (z. b. & < > () @ ^ |).
    -   Sie verwenden ein oder mehrere Leerzeichen innerhalb der Anführungszeichen.
    -   Die *Zeichenfolge* in Anführungszeichen ist der Name einer ausführbaren Datei.

    Wenn die vorherigen Bedingungen nicht erfüllt sind, wird die *Zeichenfolge* verarbeitet, indem das erste Zeichen überprüft wird, um zu prüfen, ob es sich um ein öffnendes Anführungszeichen handelt Wenn das erste Zeichen ein öffnendes Anführungszeichen ist, wird es zusammen mit dem schließenden Anführungszeichen entfernt. Jeder Text, der auf die schließenden Anführungszeichen folgt, wird beibehalten.
-   Ausführen von Registrierungs unter Schlüsseln

    Wenn Sie **/d** nicht in der *Zeichenfolge*angeben, sucht cmd. exe nach den folgenden Registrierungs unter Schlüsseln:

    **HKEY_LOCAL_MACHINE \software\microsoft\command processor\autorun\ REG_SZ**

    **HKEY_CURRENT_USER \software\microsoft\command processor\autorun\ REG_EXPAND_SZ**

    Wenn ein oder beide Registrierungs Unterschlüssel vorhanden sind, werden diese vor allen anderen Variablen ausgeführt.

> [!CAUTION]
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

-   Aktivieren und Deaktivieren von Befehls Erweiterungen

    Befehls Erweiterungen sind in Windows XP standardmäßig aktiviert. Sie können Sie für einen bestimmten Prozess mithilfe von **/e: Off**deaktivieren. Sie können Erweiterungen für alle **cmd** -Befehlszeilenoptionen auf einem Computer oder in einer Benutzersitzung aktivieren oder deaktivieren, indem Sie die folgenden **REG_DWORD** Werte festlegen:

    **HKEY_LOCAL_MACHINE \software\microsoft\command processor\enableextensions\ REG_DWORD**

    **HKEY_CURRENT_USER \software\microsoft\command processor\enableextensions\ REG_DWORD**

    Legen Sie den **REG_DWORD** -Wert in der Registrierung mithilfe von regedit. exe entweder auf **0 × 1** (aktiviert) oder auf **0 × 0** (deaktiviert) fest. Benutzerdefinierte Einstellungen haben Vorrang vor Computereinstellungen, und Befehlszeilenoptionen haben Vorrang vor den Registrierungs Einstellungen.

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

-   Aktivieren der Erweiterung für verzögerte Umgebungsvariablen

    Wenn Sie die verzögerte Erweiterung der Umgebungsvariablen aktivieren, können Sie das Ausrufezeichen verwenden, um den Wert einer Umgebungsvariablen zur Laufzeit zu ersetzen.
-   Aktivieren der Datei-und Verzeichnisnamen Vervollständigung

    Die Vervollständigung von Datei-und Verzeichnisnamen ist standardmäßig nicht aktiviert. Sie können den Abschluss des Datei namens für einen bestimmten Prozess des Befehls **cmd** mit **/f:** {**on**|**Off**} aktivieren oder deaktivieren. Sie können den Abschluss von Datei-und Verzeichnisnamen für alle Prozesse des Befehls " **cmd** " auf einem Computer oder für eine Benutzer Anmelde Sitzung aktivieren bzw. deaktivieren, indem Sie die folgenden **REG_DWORD** Werte festlegen:

    **HKEY_LOCAL_MACHINE \software\microsoft\command processor\completionchar\ REG_DWORD**

    **HKEY_LOCAL_MACHINE \software\microsoft\command processor\pathcompletionchar\ REG_DWORD**

    **HKEY_CURRENT_USER \software\microsoft\command processor\completionchar\ REG_DWORD**

    **HKEY_CURRENT_USER \software\microsoft\command processor\pathcompletionchar\ REG_DWORD**

    Wenn Sie den **REG_DWORD** Wert festlegen möchten, führen Sie regedit. exe aus, und verwenden Sie den Hexadezimalwert eines Steuer Zeichens für eine bestimmte Funktion (z. b. **0 × 9** ist Tab, und **0 × 08** ist RÜCKTASTE). Benutzerdefinierte Einstellungen haben Vorrang vor Computereinstellungen, und Befehlszeilenoptionen haben Vorrang vor den Registrierungs Einstellungen.

> [!CAUTION]
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

Wenn Sie die Vervollständigung von Datei-und Verzeichnisnamen mithilfe von **/f: on**aktivieren, verwenden Sie STRG + D für den Abschluss des Verzeichnis namens und Strg + f für den Abschluss des Datei namens. Um ein bestimmtes Abschluss Zeichen in der Registrierung zu deaktivieren, verwenden Sie den Wert für Leerraum [**0 × 20**], da es sich nicht um ein gültiges Steuerzeichen handelt.

Wenn Sie STRG + D oder STRG + F drücken, verarbeitet **cmd** den Datei-und Verzeichnisnamen. Diese Tastenkombination fügen ein Platzhalter Zeichen an eine *Zeichenfolge* an (sofern nicht vorhanden), erstellen eine Liste von Pfaden, die mit übereinstimmen, und zeigen dann den ersten übereinstimmenden Pfad an. Wenn keiner der Pfade entspricht, wird die Datei-und Verzeichnisnamen Vervollständigungsfunktion nicht geändert, und die Anzeige wird nicht geändert. Drücken Sie zum Durchlaufen der Liste der übereinstimmenden Pfade wiederholt STRG + D oder STRG + F. Drücken Sie die UMSCHALTTASTE, und drücken Sie STRG + D oder STRG + F gleichzeitig, um durch die Liste rückwärts zu navigieren. Wenn Sie die gespeicherte Liste der übereinstimmenden Pfade verwerfen und eine neue Liste generieren möchten, bearbeiten Sie die *Zeichenfolge* , und drücken Sie STRG + D oder STRG + F. Wenn Sie zwischen STRG + D und STRG + F wechseln, wird die gespeicherte Liste der übereinstimmenden Pfade verworfen und eine neue Liste generiert. Der einzige Unterschied zwischen den Tastenkombinationen STRG + D und Strg + f besteht darin, dass Strg + d nur mit Verzeichnisnamen übereinstimmt und Strg + f sowohl Datei-als auch Verzeichnisnamen entspricht. Wenn Sie die Vervollständigung von Datei-und Verzeichnisnamen in einem der integrierten Verzeichnis Befehle (d. h. **CD**, **MD**oder **RD**) verwenden, wird die Verzeichnis Vervollständigung angenommen.

Datei-und Verzeichnisnamen Vervollständigung verarbeitet ordnungsgemäß Dateinamen, die Leerzeichen oder Sonderzeichen enthalten, wenn Sie den übereinstimmenden Pfad in Anführungszeichen setzen.

Die folgenden Sonderzeichen erfordern Anführungszeichen: & < > [] {} ^ =;! ' +, ' ~ [Leerraum].

Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Computer Name").

Wenn Sie die Vervollständigung von Datei-und Verzeichnisnamen innerhalb der *Zeichenfolge*verarbeiten, wird jeder Teil des *Pfads* rechts vom Cursor verworfen (an der Stelle in der *Zeichenfolge* , an der der Abschluss verarbeitet wurde).

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
