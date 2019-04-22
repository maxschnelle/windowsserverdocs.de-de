---
title: wscript
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fbaf193-cdbd-414c-84c9-bb5720f84c29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: 771c1231ee5379ec797f535505839de8671e32a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821301"
---
# <a name="wscript"></a>wscript



Windows Script Host bietet es sich um eine Umgebung, in der Benutzer Skripts in einer Vielzahl von Sprachen werden, die eine Vielzahl von Object-Modelle verwenden ausgeführt kann, um Aufgaben auszuführen.

## <a name="syntax"></a>Syntax

```
wscript [<scriptname>] [/b] [/d] [/e:<engine>] [{/h:cscript|/h:wscript}] [/i] [/job:<identifier>] [{/logo|/nologo}] [/s] [/t:<number>] [/x] [/?] [<ScriptArguments>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Skriptname|Gibt den Pfad und Namen der Skriptdatei an.|
|/b|Gibt die Batchmodus verwendet wird, der Warnungen, Skriptfehlern oder eingabeaufforderungen der Eingabe nicht angezeigt werden. Dies ist das Gegenteil von **/i**.|
|/d|Startet den Debugger.|
|/ e|Gibt die Engine, die verwendet wird, um das Skript auszuführen. Dadurch können Sie die Skripts ausgeführt werden, die eine benutzerdefinierte Erweiterung verwenden. Ohne den/e-Parameter können Sie nur Skripts ausführen, die registrierten Dateinamenerweiterungen Weitere Erweiterungen zu verwenden. Angenommen, wenn Sie versuchen, diesen Befehl ausführen:<br>```cscript test.admin```<br>Sie erhalten diese Fehlermeldung angezeigt: Eingabefehler: Es gibt keine Skript-Engine für die Dateierweiterung ". Admin."<br>Ein Vorteil der Verwendung nicht dem Standard entsprechende Erweiterung ist, dass es schützt vor versehentlichen Doppelklicken auf ein Skript ausgeführt wird, etwas wirklich nicht ausgeführt werden soll. <br>Dadurch wird eine permanente Zuordnung zwischen dem .admin Dateinamenerweiterung und VBScript nicht erstellt. Jedes Mal, wenn Sie ein Skript ausführen, die eine Dateinamenerweiterung .admin verwendet müssen Sie den/e-Parameter verwenden.|
|/h:cscript|Registriert **cscript.exe** als den Standardskripthost zum Ausführen von Skripts.|
|/h:wscript|Registriert **wscript.exe** als den Standardskripthost zum Ausführen von Skripts. Dies ist die Standardeinstellung bei der **/h** Option ausgelassen wird.|
|/i|Gibt an, interaktiven Modus, der Warnungen, Skriptfehlern und Eingabe eingabeaufforderungen angezeigt.</br>Dies ist die Standardeinstellung und das Gegenteil von **/b**.|
|/job:\<identifier>|Führt den Auftrag identifizierte *Bezeichner* in einem **.wsf** Skriptdatei.|
|/logo|Gibt an, dass die Windows Script Host-Banner in der Konsole angezeigt wird, bevor das Skript ausgeführt wird.</br>Dies ist die Standardeinstellung und das Gegenteil von **/nologo**.|
|/nologo|Gibt an, dass die Windows Script Host-Banner nicht angezeigt wird, bevor das Skript ausgeführt wird. Dies ist das Gegenteil von **/logo**.|
|/s|Speichert die aktuellen Befehlszeilenoptionen für den aktuellen Benutzer.|
|/ t:\<Anzahl >|Gibt die maximale Zeit, die das Skript (in Sekunden) ausgeführt werden kann. Sie können bis zu 32.767 Sekunden angeben.</br>Der Standardwert ist keine zeitliche Begrenzung.|
|/x|Das Skript im Debugger gestartet.|
|ScriptArguments|Gibt an, die Argumente an das Skript übergeben. Jedes Skriptargument muss ein Schrägstrich (/) vorangestellt sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Zum Ausführen dieser Aufgabe müssen Sie keine administrativen Anmeldeinformationen besitzen. Führen Sie diese Aufgabe daher aus Sicherheitsgründen als Benutzer ohne administrative Anmeldeinformationen aus.
-   Geben Sie zum Öffnen einer Eingabeaufforderung auf dem **Startbildschirm****cmd** ein, und klicken Sie auf **Eingabeaufforderung**.
-   Jeder Parameter ist optional. Sie können keine jedoch Skriptargumente angeben, ohne Angabe eines Skripts. Wenn Sie ein Skript oder Skriptargumente, nicht angeben **wscript.exe** zeigt die **Windows Script Host-Einstellungsdatei** (Dialogfeld), die Sie verwenden können, die globale Skripteigenschaften für alle Skripts, festlegen**wscript.exe** auf dem lokalen Computer ausgeführt wird.
-   Die **/t /** Parameter verhindert die übermäßige Ausführung von Skripts durch Festlegen eines Zeitgebers. Wenn die Zeit auf den angegebenen Wert überschreitet **Wscript** unterbricht die Skript-Engine und beendet den Prozess.
-   Windows Script-Dateien müssen in der Regel eines der folgenden Dateinamenerweiterungen: **.wsf**, **vbs**, **js**.
-   Wenn Sie eine Skriptdatei mit der Erweiterung doppelklicken, die keine Zuordnung verfügt über die **Öffnen mit** Dialogfeld wird angezeigt. Wählen Sie **Wscript** oder **Cscript**, und wählen Sie dann **verwenden Sie dieses Programm immer zum Öffnen dieses Dateityps**. Auf diese Weise registriert **wscript.exe** oder **cscript.exe** als den Standardskripthost für Dateien, die von diesen Dateityp.
-   Sie können Eigenschaften für einzelne Skripts festlegen. Finden Sie unter [Übersicht über Windows Script Host](https://technet.microsoft.com/library/cc738350(v=ws.10).aspx) für Weitere Informationen.
-   Windows Script Host können **.wsf** Skriptdateien. Jede **.wsf** Datei mehrere Skriptmodule verwenden kann, und führen Sie mehrere Aufträge.

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
