---
title: cscript
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fba3cbca-594e-4663-bb22-4ee0f63a1ac6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef98a98088e345f267aa852318cee6e237604aa4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433992"
---
# <a name="cscript"></a>cscript

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

startet Sie ein Skript, damit es in einer Befehlszeilen-Umgebung ausgeführt wird.
## <a name="syntax"></a>Syntax
```
cscript <Scriptname.extension> [/B] [/D] [/E:<Engine>] [{/H:cscript|/H:wscript}] [/I] [/Job:<Identifier>] [{/Logo|/NoLogo}] [/S] [/T:<Seconds>] [/X] [/U] [/?] [<ScriptArguments>]
```
### <a name="parameters"></a>Parameter

|      Parameter       |                                                                      Beschreibung                                                                       |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Scriptname.extension |                                 Gibt den Pfad und Namen der Skriptdatei mit der Dateinamenerweiterung "optional" an.                                 |
|          /B          |                                Gibt die Batchmodus verwendet wird, der Warnungen, Skriptfehlern oder eingabeaufforderungen der Eingabe nicht angezeigt werden.                                |
|          /D          |                                                                  Startet den Debugger.                                                                  |
|     /E:<Engine>      |                                                  Gibt die Engine, die verwendet wird, um das Skript auszuführen.                                                  |
|      /H:cscript      |                                         Registriert von cscript.exe als den Standardskripthost zum Ausführen von Skripts.                                          |
|      /H:wscript      |                               Register wscript.exe als den Standardskripthost zum Ausführen von Skripts. Dies ist die Standardeinstellung.                               |
|          /I          |        Gibt an, interaktiven Modus, der Warnungen, Skriptfehlern und Eingabe eingabeaufforderungen angezeigt. Dies ist die Standardeinstellung und das Gegenteil von **/b**.         |
|  /Job:<Identifier>   |                                             Führt den Auftrag identifizierte *Bezeichner* in einer WSF-Skriptdatei.                                             |
|        /Logo         | Gibt an, dass die Windows Script Host-Banner in der Konsole angezeigt wird, bevor das Skript ausgeführt wird. Dies ist die Standardeinstellung und das Gegenteil von **/nologo**. |
|       /Nologo        |                                 Gibt an, dass die Windows Script Host-Banner nicht angezeigt wird, bevor das Skript ausgeführt wird.                                 |
|          /S          |                                             Speichert die aktuelle Befehlszeilen-Optionen für den aktuellen Benutzer.                                             |
|     /T:<Seconds>     |            Gibt die maximale Zeit, die das Skript (in Sekunden) ausgeführt werden kann. Sie können bis zu 32.767 Sekunden angeben. Der Standardwert ist keine zeitliche Begrenzung.             |
|          /U          |                                      Gibt die Unicode für ein- und Ausgabe, die in der Konsole umgeleitet wird.                                       |
|          /X          |                                                           Das Skript im Debugger gestartet.                                                           |
|          /?          |  Zeigt verfügbare Befehlsparameter an und enthält die Hilfe zu ihrer Verwendung. Dies ist identisch mit der Eingabe **cscript.exe** ohne Parameter und kein Skript.  |
|   ScriptArguments    |                        Gibt an, die Argumente an das Skript übergeben. Jedes Skriptargument muss ein Schrägstrich vorangestellt werden ( **/** ).                         |

### <a name="remarks"></a>Hinweise
-   Zum Ausführen dieser Aufgabe müssen Sie keine administrativen Anmeldeinformationen besitzen. Führen Sie diese Aufgabe daher aus Sicherheitsgründen als Benutzer ohne administrative Anmeldeinformationen aus.
-   So öffnen Sie eine Eingabeaufforderung auf die **starten** geben **Cmd**, und klicken Sie dann auf **Eingabeaufforderung**.
-   Jeder Parameter ist optional. Sie können keine jedoch Skriptargumente angeben, ohne Angabe eines Skripts. Wenn Sie ein Skript oder Skriptargumente nicht angeben, zeigt cscript.exe die cscript.exe-Syntax und die gültigen Host-Optionen.
-   Die **/t /** Parameter verhindert die übermäßige Ausführung von Skripts durch Festlegen eines Zeitgebers. Wenn die Laufzeit über den angegebenen Wert überschreitet, wird "cscript" unterbricht die Skript-Engine und beendet den Prozess.
-   Windows Script-Dateien müssen in der Regel eines der folgenden Dateinamenerweiterungen: .wsf, .vbs,. js.
-   Sie können Eigenschaften für einzelne Skripts festlegen. Weitere Informationen finden Sie in der verwandten Themen.
-   Windows Script Host können wsf-Skriptdateien verwenden. Jede WSF-Datei mithilfe von mehreren Skript-Engines und führen Sie mehrere Aufträge.
-   Wenn Sie eine Skriptdatei mit der Erweiterung doppelklicken, die keine Zuordnung verfügt über die **Öffnen mit** Dialogfeld wird angezeigt. Wählen Sie Wscript oder "cscript", und wählen Sie dann **verwenden Sie dieses Programm immer zum Öffnen dieses Dateityps**. Dadurch wird wscript.exe oder "cscript" als den Standardskripthost für Dateien dieses Dateityps registriert.
-   Sie können Eigenschaften für einzelne Skripts festlegen. Finden Sie unter [zusätzliche Verweise](#BKMK_references) für Weitere Informationen.
-   Windows Script Host können wsf-Skriptdateien verwenden. Jede WSF-Datei mithilfe von mehreren Skript-Engines und führen Sie mehrere Aufträge.

#### <a name="BKMK_references"></a>Zusätzliche Referenzen

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
