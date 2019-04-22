---
title: secedit
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58ed57ed-08e3-403d-a363-0620b358637a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8aaa40f21c6f14dc7d686261e9980594c14a8032
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818461"
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

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Secedit: Analysieren](secedit-analyze.md)|Können Sie die aktuellen Systemeinstellungen für die grundlegenden Einstellungen zu analysieren, die in einer Datenbank gespeichert sind.  Die Analyseergebnisse werden in einem separaten Bereich der Datenbank gespeichert und können in der Sicherheitskonfiguration und des Analysis-Snap-in angezeigt werden.|
|[Secedit:configure](secedit-configure.md)|Können Sie so konfigurieren Sie ein System mit Sicherheitseinstellungen, die in einer Datenbank gespeichert.|
|[Secedit:export](secedit-export.md)|Ermöglicht Ihnen so exportieren Sie die Sicherheitseinstellungen, die in einer Datenbank gespeichert.|
|[Secedit:generaterollback](secedit-generaterollback.md)|Können Sie eine Rollbackvorlage in Bezug auf eine Vorlage generieren.|
|[Secedit:import](secedit-import.md)|Ermöglicht es Ihnen, eine Sicherheitsvorlage in eine Datenbank importieren, sodass in der Vorlage angegebenen Einstellungen für ein System analysiert oder auf einem System angewendet werden können.|
|[Secedit:validate](secedit-validate.md)|Überprüfen Sie die Syntax einer Vorlage für Sicherheit ermöglicht.|

## <a name="remarks"></a>Hinweise

Bei allen Dateinamen wird das aktuelle Verzeichnis verwendet, wenn kein Pfad angegeben wird.

Wenn eine Sicherheitsvorlage erstellt mithilfe des MMC-Snap-ins Sicherheitsvorlage und die Sicherheitskonfiguration und Analyse-Snap-in ausgeführt wird, werden die folgenden Dateien erstellt:

|Datei|Beschreibung|
|----|-----------|
|Scesrv.log|**Speicherort**: %windir%\security\logs</br>**Erstellt von**: Betriebssystem</br>**Dateityp**: Text</br>**Aktualisierungsrate**: Überschrieben, wenn Secedit / zu analysieren, / Konfigurieren von/export oder/Import ausgeführt werden.</br>**Inhalt**: Enthält die Ergebnisse der Analyse gruppiert nach Richtlinientyp.|
|*Vom Benutzer ausgewählte Name*sdb|**Speicherort**: %Windir%\*Benutzerkonto * \Documents\Security\Database</br>**Erstellt von**: die Sicherheitskonfiguration und-Analyse-Snap-in ausgeführt</br>**Dateityp**: proprietäre</br>**Aktualisierungsrate**: Aktualisiert, wenn eine neue Sicherheitsvorlage erstellt wird.</br>**Inhalt**: Lokale Sicherheitsrichtlinien und benutzererstellte Sicherheitsvorlagen.|
|*Vom Benutzer ausgewählte Name*.log|**Speicherort**: Benutzerdefinierte, aber der Standardwert ist % windir%\*Benutzerkonto * \Documents\Security\Logs</br>**Erstellt von**: Mit dem / analyze und / Unterbefehle konfigurieren (oder mithilfe der Sicherheitskonfiguration und-Analyse-Snap-Ins)</br>**Dateityp**: Text</br>**Aktualisierungsrate**: Mit der / analyze und / Unterbefehle konfigurieren (oder mithilfe der Sicherheitskonfiguration und-Analyse-Snap-Ins) überschrieben.</br>**Inhalt**:</br>1.  Protokolldateiname</br>2.  Datum und Uhrzeit</br>3.  Ergebnisse der Analyse oder Untersuchung.|
|*Vom Benutzer ausgewählte Name*INF|**Speicherort**: %Windir%\*Benutzerkonto * \Documents\Security\Templates</br>**Erstellt von**: das Sicherheitsvorlage-Snap-in ausgeführt wird</br>**Dateityp**: Text</br>**Aktualisierungsrate**: jedes Mal, die Vorlage für die Sicherheit aktualisiert wird.</br>**Inhalt**: Enthält den Satz von Informationen für die Vorlage für jede Richtlinie, die mithilfe des Snap-Ins ausgewählt.|

> [!NOTE]
> Die Microsoft Management Console (MMC) und der Sicherheitskonfiguration und Analyse-Snap-Ins sind nicht auf Server Core verfügbar.

#### <a name="additional-references"></a>Weitere Verweise

Beispiele wie dieser Befehl verwendet werden kann finden Sie unter dem Abschnitt "Beispiele" in einem der Unterbefehl Dateien.
-   [Befehlszeilensyntax](command-line-syntax-key.md)