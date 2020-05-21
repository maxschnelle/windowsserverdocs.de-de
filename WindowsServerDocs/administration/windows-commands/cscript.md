---
title: cscript
description: Referenz Thema zum cscript-Befehl, mit dem ein Skript gestartet wird, sodass es in einer Befehlszeilen Umgebung ausgeführt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fba3cbca-594e-4663-bb22-4ee0f63a1ac6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 24d5d46a0a994ca44230076786fbd59c00cbdc57
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437055"
---
# <a name="cscript"></a>cscript

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet ein Skript, das in einer Befehlszeilen Umgebung ausgeführt werden soll.

>[!IMPORTANT]
> Zum Ausführen dieser Aufgabe benötigen Sie keine Administratorrechte. Daher sollten Sie als Best Practice für die Sicherheit diese Aufgabe als Benutzer ohne Administratorrechte ausführen.

## <a name="syntax"></a>Syntax

```
cscript <scriptname.extension> [/b] [/d] [/e:<engine>] [{/h:cscript | /h:wscript}] [/i] [/job:<identifier>] [{/logo | /nologo}] [/s] [/t:<seconds>] [x] [/u] [/?] [<scriptarguments>]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| ScriptName. Extension | Gibt den Pfad und den Dateinamen der Skriptdatei mit der optionalen Dateinamenerweiterung an. |
| /b | Gibt den Batch Modus an, in dem keine Warnungen, Skript Fehler oder Eingabe Aufforderungen angezeigt werden. |
| /d | Startet den Debugger. |
| /e:`<engine>` | Gibt die Engine an, die zum Ausführen des Skripts verwendet wird. |
| /h: cscript | Registriert "Cscript. exe" als Standardskript Host für das Ausführen von Skripts. |
| /h: WScript | Registriert "Wscript. exe" als Standardskript Host für das Ausführen von Skripts. Dies ist der Standardwert. |
| /i | Gibt den interaktiven Modus an, in dem Warnungen, Skript Fehler und Eingabe Aufforderungen angezeigt werden. Dies ist die Standardeinstellung und das Gegenteil von `/b` . |
| /Auftrag<identifier> | Führt den durch den *Bezeichner* identifizierten Auftrag in einer WSF-Skriptdatei aus. |
| /logo | Gibt an, dass das Windows Script Host-Banner in der-Konsole angezeigt wird, bevor das Skript ausgeführt wird. Dies ist die Standardeinstellung und das Gegenteil von `/nologo` . |
| /nologo | Gibt an, dass das Windows Script Host-Banner vor dem Ausführen des Skripts nicht angezeigt wird. |
| /s | Speichert die aktuellen Eingabe Aufforderungs Optionen für den aktuellen Benutzer. |
| /t:<seconds> | Gibt die maximale Zeit an, die das Skript ausgeführt werden kann (in Sekunden). Sie können bis zu 32.767 Sekunden angeben. Der Standardwert ist kein Zeit Limit. |
| /U | Gibt Unicode für die Eingabe und die Ausgabe an, die von der Konsole umgeleitet werden. |
| /x | Startet das Skript im Debugger. |
| /? | Zeigt verfügbare Befehlsparameter an und bietet Hilfe zur Verwendung. Dies ist identisch mit der Eingabe von " **cscript. exe** " ohne Parameter und ohne Skript. |
| scriptarguments | Gibt die Argumente an, die an das Skript geleitet werden. Jedem Skript Argument muss ein Schrägstrich () vorangestellt werden **/** . |

#### <a name="remarks"></a>Hinweise

- Jeder Parameter ist optional. Sie können jedoch keine Skript Argumente angeben, ohne ein Skript anzugeben. Wenn Sie kein Skript oder Skript Argumente angeben, zeigt Cscript. exe die Syntax cscript. exe und die gültigen Host Optionen an.

- Der **/t** -Parameter verhindert eine übermäßige Ausführung von Skripts durch Festlegen eines Timers. Wenn die Laufzeit den angegebenen Wert überschreitet, unterbricht cscript die Skript-Engine und beendet den Prozess.

- Windows-Skriptdateien haben in der Regel eine der folgenden Dateinamen Erweiterungen:. wsf,. VSB,. js. Die WSF-Skriptdateien können von Windows Script Host verwendet werden. Jede WSF-Datei kann mehrere Skript-Engines verwenden und mehrere Aufträge ausführen.

- Wenn Sie auf eine Skriptdatei mit einer Erweiterung ohne Zuordnung doppelklicken, wird das Dialogfeld **Öffnen mit** angezeigt. Wählen Sie Wscript oder cscript aus, und wählen Sie dann **dieses Programm immer verwenden aus, um diesen Dateityp zu öffnen**. Dadurch wird "Wscript. exe" oder "Cscript" als Standardskript Host für Dateien dieses Dateityps registriert.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
