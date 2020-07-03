---
title: secedit
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 58ed57ed-08e3-403d-a363-0620b358637a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e5918265feb7dc72759ea22d2f582e4754df96c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936494"
---
# <a name="secedit"></a>secedit



Konfiguriert und Analysiert die Systemsicherheit, indem es Ihre aktuelle Konfiguration mit festgelegten Sicherheitsvorlagen vergleicht.

## <a name="syntax"></a>Syntax

```
secedit
[/analyze /db <database file name> /cfg <configuration file name> [/overwrite] /log <log file name> [/quiet]]
[/configure /db <database file name> [/cfg <configuration filename>] [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]]
[/export /db <database file name> [/mergedpolicy] /cfg <configuration file name> [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>]]
[/generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback file name> [/log <log file name>] [/quiet]]
[/import /db <database file name> /cfg <configuration file name> [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]]
[/validate <configuration file name>]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[Secedit:analyze](secedit-analyze.md)|Ermöglicht es Ihnen, die aktuellen Systemeinstellungen anhand von baselineeinstellungen zu analysieren, die in einer Datenbank gespeichert sind.  Die Analyseergebnisse werden in einem separaten Bereich der Datenbank gespeichert und können im Snap-in "Sicherheitskonfiguration und-Analyse" angezeigt werden.|
|[Secedit:configure](secedit-configure.md)|Ermöglicht das Konfigurieren eines Systems mit Sicherheitseinstellungen, die in einer-Datenbank gespeichert sind.|
|[Secedit:export](secedit-export.md)|Ermöglicht das Exportieren von Sicherheitseinstellungen, die in einer-Datenbank gespeichert sind.|
|[Secedit:generaterollback](secedit-generaterollback.md)|Ermöglicht das Generieren einer Rollback-Vorlage in Bezug auf eine Konfigurations Vorlage.|
|[Secedit:import](secedit-import.md)|Ermöglicht es Ihnen, eine Sicherheits Vorlage in eine-Datenbank zu importieren, damit die in der Vorlage angegebenen Einstellungen auf ein System angewendet oder anhand eines Systems analysiert werden können.|
|[Secedit:validate](secedit-validate.md)|Ermöglicht es Ihnen, die Syntax einer Sicherheits Vorlage zu validieren.|

## <a name="remarks"></a>Hinweise

Für alle Dateinamen wird das aktuelle Verzeichnis verwendet, wenn kein Pfad angegeben wird.

Wenn eine Sicherheits Vorlage mithilfe des Sicherheits Vorlagen-Snap-Ins erstellt wird und das Sicherheitskonfigurations-und Analyse-Snap-in ausgeführt wird, werden die folgenden Dateien erstellt:


|           Datei           |                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        Scesrv. log        |                                                                                                                             **Speicherort**:%windir%\security\logs</br>**Erstellt von**: Betriebssystem</br>**Dateityp**: Text</br>**Aktualisierungsrate**: wird überschrieben, wenn secedit/analyze,/configure,/Export oder/Import ausgeführt wird.</br>**Content**: enthält die Ergebnisse der Analyse nach Richtlinientyp gruppiert.                                                                                                                             |
| Vom *Benutzer ausgewählter Name*. SDB |                                                                                    **Speicherort**:% windir% \* Benutzerkonto <em> \documents\security\database</br></em>*Erstellt von* <em> : Ausführen des Snap-Ins "Sicherheitskonfiguration und-Analyse"</br></em>*Dateityp* <em> : proprietäre</br></em>*Refresh rate* <em> Aktualisierungsrate: wird immer dann aktualisiert, wenn eine neue Sicherheits Vorlage erstellt wird.</br></em>*Inhalt* \* : lokale Sicherheitsrichtlinien und vom Benutzer erstellte Sicherheits Vorlagen.                                                                                    |
| Vom *Benutzer ausgewählter Name*. log | **Speicherort**: Benutzer definiert, aber standardmäßig% windir% \* Benutzerkonto <em> \documents\security\logs</br></em>*Erstellt von* <em> : Ausführen der Unterbefehle/analyze und/configure (oder mithilfe des Sicherheitskonfigurations-und Analyse-Snap-Ins)</br></em>*Dateityp* <em> : Text</br></em>*Aktualisierungsrate* <em> : Ausführen der Unterbefehle/analyze und/configure (oder mithilfe des Sicherheitskonfigurations-und Analyse-Snap-Ins); überschrieben.</br></em>*Inhalt* \* :</br>1. Protokoll Dateiname</br>2. Datum und Uhrzeit</br>3. Ergebnisse der Analyse oder Untersuchung. |
| Vom *Benutzer ausgewählter Name*. inf |                                                                                     **Speicherort**:% windir% \* Benutzerkonto <em> \documents\security\templates</br></em>*Erstellt von* <em> : Ausführen des Snap-Ins "Sicherheits Vorlage"</br></em>*Dateityp* <em> : Text</br></em>Aktualisierungs *Rate* <em> : jedes Mal, wenn die Sicherheits Vorlage aktualisiert wird</br></em>*Inhalt* \* : enthält die Informationen zum Einrichten der Vorlage für jede Richtlinie, die mithilfe des-Snap-Ins ausgewählt wird.                                                                                     |

> [!NOTE]
> Die Microsoft Management Console (MMC) und das Snap-in "Sicherheitskonfiguration und-Analyse" sind auf Server Core nicht verfügbar.

## <a name="additional-references"></a>Weitere Verweise

Beispiele für die Verwendung dieses Befehls finden Sie im Abschnitt "Beispiele" in einer der untergeordneten Befehls Dateien.
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)