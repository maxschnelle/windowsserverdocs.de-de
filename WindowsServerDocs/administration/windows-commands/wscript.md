---
title: wscript
description: Referenz Thema für WScript, das eine Umgebung bereitstellt, in der Benutzer Skripts in einer Vielzahl von Sprachen ausführen können, die eine Vielzahl von Objekt Modellen zum Ausführen von Aufgaben verwenden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2fbaf193-cdbd-414c-84c9-bb5720f84c29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: cf2d23c7d5773662f679a9a20b0aaba118f35548
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720627"
---
# <a name="wscript"></a>wscript



Windows Script Host bietet eine Umgebung, in der Benutzer Skripts in einer Vielzahl von Sprachen ausführen können, die eine Vielzahl von Objekt Modellen zum Ausführen von Aufgaben verwenden.

## <a name="syntax"></a>Syntax

```
wscript [<scriptname>] [/b] [/d] [/e:<engine>] [{/h:cscript|/h:wscript}] [/i] [/job:<identifier>] [{/logo|/nologo}] [/s] [/t:<number>] [/x] [/?] [<ScriptArguments>]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|ScriptName|Gibt den Pfad und den Dateinamen der Skriptdatei an.|
|/b|Gibt den Batch Modus an, in dem keine Warnungen, Skript Fehler oder Eingabe Aufforderungen angezeigt werden. Dies ist das Gegenteil von **/i**.|
|/d|Startet den Debugger.|
|/e|Gibt die Engine an, die zum Ausführen des Skripts verwendet wird. Auf diese Weise können Sie Skripts ausführen, die eine benutzerdefinierte Dateinamenerweiterung verwenden. Ohne den/e-Parameter können Sie nur Skripts ausführen, die registrierte Dateinamen Erweiterungen verwenden. Wenn Sie z. b. versuchen, den folgenden Befehl auszuführen:<br>```cscript test.admin```<br>Diese Fehlermeldung wird angezeigt: Eingabefehler: Es ist keine Skript-Engine für Dateierweiterung. admin vorhanden.<br>Ein Vorteil der Verwendung von nicht standardmäßigen Dateinamen Erweiterungen besteht darin, dass Sie vor dem versehentlichen Doppelklicken auf ein Skript und dem Ausführen eines Elements, das Sie wirklich nicht ausführen wollten, schützt. <br>Dadurch wird keine permanente Zuordnung zwischen der Dateinamenerweiterung ". admin" und "VBScript" erstellt. Jedes Mal, wenn Sie ein Skript ausführen, das die Dateinamenerweiterung ". admin" verwendet, müssen Sie den/e-Parameter verwenden.|
|/h: cscript|Registriert " **cscript. exe** " als Standardskript Host für das Ausführen von Skripts.|
|/h: WScript|Registriert " **WScript. exe** " als Standardskript Host für das Ausführen von Skripts. Dies ist die Standardeinstellung, wenn die Option **/h** ausgelassen wird.|
|/i|Gibt den interaktiven Modus an, in dem Warnungen, Skript Fehler und Eingabe Aufforderungen angezeigt werden.</br>Dies ist die Standardeinstellung und das Gegenteil von **/b**.|
|/Auftrag:\<Bezeichner>|Führt den durch den *Bezeichner* identifizierten Auftrag in einer **WSF** -Skriptdatei aus.|
|/logo|Gibt an, dass das Windows Script Host-Banner in der-Konsole angezeigt wird, bevor das Skript ausgeführt wird.</br>Dies ist die Standardeinstellung und das Gegenteil von **/nologo**.|
|/nologo|Gibt an, dass das Windows Script Host-Banner vor dem Ausführen des Skripts nicht angezeigt wird. Dies ist das Gegenteil von **/Logo**.|
|/s|Speichert die aktuellen Eingabe Aufforderungs Optionen für den aktuellen Benutzer.|
|/t:\<Anzahl>|Gibt die maximale Zeit an, die das Skript ausgeführt werden kann (in Sekunden). Sie können bis zu 32.767 Sekunden angeben.</br>Der Standardwert ist kein Zeit Limit.|
|/x|Startet das Skript im Debugger.|
|Scriptarguments|Gibt die Argumente an, die an das Skript geleitet werden. Jedem Skript Argument muss ein Schrägstrich (/) vorangestellt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Zum Ausführen dieser Aufgabe benötigen Sie keine Administratorrechte. Daher sollten Sie als Best Practice für die Sicherheit diese Aufgabe als Benutzer ohne Administratorrechte ausführen.
-   Geben Sie zum Öffnen einer Eingabeaufforderung auf dem **Startbildschirm****cmd** ein, und klicken Sie auf **Eingabeaufforderung**.
-   Jeder Parameter ist optional. Sie können jedoch keine Skript Argumente angeben, ohne ein Skript anzugeben. Wenn Sie kein Skript oder Skript Argumente angeben, wird in " **WScript. exe** " das Dialogfeld " **Windows Script Host-Einstellungen** " angezeigt, das Sie verwenden können, um globale Skript Eigenschaften für alle Skripts festzulegen, die " **WScript. exe** " auf dem lokalen Computer ausführt.
-   Der **/t** -Parameter verhindert eine übermäßige Ausführung von Skripts durch Festlegen eines Timers. Wenn die Zeit den angegebenen Wert überschreitet, unterbricht **WScript** die Skript-Engine und beendet den Prozess.
-   Windows-Skriptdateien haben in der Regel eine der folgenden Dateinamen Erweiterungen: **. wsf**, **. VSB**, **. js**.
-   Wenn Sie auf eine Skriptdatei mit einer Erweiterung ohne Zuordnung doppelklicken, wird das Dialogfeld **Öffnen mit** angezeigt. Wählen Sie **WScript** oder **cscript**aus, und wählen Sie dann **dieses Programm immer verwenden aus, um diesen Dateityp zu öffnen**. Dadurch wird " **WScript. exe** " oder " **cscript. exe** " als Standardskript Host für Dateien dieses Dateityps registriert.
-   Sie können Eigenschaften für einzelne Skripts festlegen. Weitere Informationen finden Sie unter [Übersicht über Windows Script Host](https://technet.microsoft.com/library/cc738350(v=ws.10).aspx) .
-   Die **WSF** -Skriptdateien können von Windows Script Host verwendet werden. Jede **WSF** -Datei kann mehrere Skript-Engines verwenden und mehrere Aufträge ausführen.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
