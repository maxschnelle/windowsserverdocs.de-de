---
title: cscript
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 32cfd70266abdcdc247bf79b34ae220a73729837
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378801"
---
# <a name="cscript"></a>cscript

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

startet ein Skript, sodass es in einer Befehlszeilen Umgebung ausgeführt wird.
## <a name="syntax"></a>Syntax
```
cscript <Scriptname.extension> [/B] [/D] [/E:<Engine>] [{/H:cscript|/H:wscript}] [/I] [/Job:<Identifier>] [{/Logo|/NoLogo}] [/S] [/T:<Seconds>] [/X] [/U] [/?] [<ScriptArguments>]
```
### <a name="parameters"></a>Parameter

|      Parameter       |                                                                      Beschreibung                                                                       |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| ScriptName. Extension |                                 Gibt den Pfad und den Dateinamen der Skriptdatei mit der optionalen Dateinamenerweiterung an.                                 |
|          /B          |                                Gibt den Batch Modus an, in dem keine Warnungen, Skript Fehler oder Eingabe Aufforderungen angezeigt werden.                                |
|          /D          |                                                                  Startet den Debugger.                                                                  |
|     /E: <Engine>      |                                                  Gibt die Engine an, die zum Ausführen des Skripts verwendet wird.                                                  |
|      /H: cscript      |                                         Registriert "Cscript. exe" als Standardskript Host für das Ausführen von Skripts.                                          |
|      /H: WScript      |                               Registriert "Wscript. exe" als Standardskript Host für das Ausführen von Skripts. Dies ist die Standardeinstellung.                               |
|          /I          |        Gibt den interaktiven Modus an, in dem Warnungen, Skript Fehler und Eingabe Aufforderungen angezeigt werden. Dies ist die Standardeinstellung und das Gegenteil von **/B**.         |
|  /Auftrag: <Identifier>   |                                             Führt den durch den *Bezeichner* identifizierten Auftrag in einer WSF-Skriptdatei aus.                                             |
|        /Logo         | Gibt an, dass das Windows Script Host-Banner in der-Konsole angezeigt wird, bevor das Skript ausgeführt wird. Dies ist die Standardeinstellung und das Gegenteil von **/nologo**. |
|       /Nologo        |                                 Gibt an, dass das Windows Script Host-Banner vor dem Ausführen des Skripts nicht angezeigt wird.                                 |
|          /S          |                                             Speichert die aktuellen Eingabe Aufforderungs Optionen für den aktuellen Benutzer.                                             |
|     /T: <Seconds>     |            Gibt die maximale Zeit an, die das Skript ausgeführt werden kann (in Sekunden). Sie können bis zu 32.767 Sekunden angeben. Der Standardwert ist kein Zeit Limit.             |
|          /U          |                                      Gibt Unicode für die Eingabe und die Ausgabe an, die von der Konsole umgeleitet werden.                                       |
|          /X          |                                                           Startet das Skript im Debugger.                                                           |
|          /?          |  Zeigt verfügbare Befehlsparameter an und bietet Hilfe zur Verwendung. Dies ist identisch mit der Eingabe von " **cscript. exe** " ohne Parameter und ohne Skript.  |
|   Scriptarguments    |                        Gibt die Argumente an, die an das Skript geleitet werden. Jedem Skript Argument muss ein Schrägstrich ( **/** ) vorangestellt werden.                         |

### <a name="remarks"></a>Hinweise
-   Zum Ausführen dieser Aufgabe müssen Sie keine administrativen Anmeldeinformationen besitzen. Führen Sie diese Aufgabe daher aus Sicherheitsgründen als Benutzer ohne administrative Anmeldeinformationen aus.
-   Geben Sie zum Öffnen einer Eingabeaufforderung auf dem **Start** Bildschirm **cmd**ein, und klicken Sie dann auf **Eingabeaufforderung**.
-   Jeder Parameter ist optional. Sie können jedoch keine Skript Argumente angeben, ohne ein Skript anzugeben. Wenn Sie kein Skript oder Skript Argumente angeben, zeigt Cscript. exe die Syntax cscript. exe und die gültigen Host Optionen an.
-   Der **/T** -Parameter verhindert eine übermäßige Ausführung von Skripts durch Festlegen eines Timers. Wenn die Laufzeit den angegebenen Wert überschreitet, unterbricht cscript die Skript-Engine und beendet den Prozess.
-   Windows-Skriptdateien haben in der Regel eine der folgenden Dateinamen Erweiterungen:. wsf,. VSB,. js.
-   Sie können Eigenschaften für einzelne Skripts festlegen. Weitere Informationen finden Sie in den verwandten Themen.
-   Die WSF-Skriptdateien können von Windows Script Host verwendet werden. Jede WSF-Datei kann mehrere Skript-Engines verwenden und mehrere Aufträge ausführen.
-   Wenn Sie auf eine Skriptdatei mit einer Erweiterung ohne Zuordnung doppelklicken, wird das Dialogfeld **Öffnen mit** angezeigt. Wählen Sie Wscript oder cscript aus, und wählen Sie dann **dieses Programm immer verwenden aus, um diesen Dateityp zu öffnen**. Dadurch wird "Wscript. exe" oder "Cscript" als Standardskript Host für Dateien dieses Dateityps registriert.
-   Sie können Eigenschaften für einzelne Skripts festlegen. Weitere Informationen finden Sie unter [Zusätzliche Verweise](#BKMK_references) .
-   Die WSF-Skriptdateien können von Windows Script Host verwendet werden. Jede WSF-Datei kann mehrere Skript-Engines verwenden und mehrere Aufträge ausführen.

#### <a name="BKMK_references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
