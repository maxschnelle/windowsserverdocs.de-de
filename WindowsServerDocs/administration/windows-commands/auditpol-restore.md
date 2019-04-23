---
title: Wiederherstellen von "auditpol"
description: Windows-Befehle Thema **"auditpol" Wiederherstellung** -System sicherheitsüberwachungs-Richtlinieneinstellungen, die pro Benutzer sicherheitsüberwachungs-Richtlinieneinstellungen für alle Benutzer und alle Überwachungsoptionen aus einer Datei, die syntaktisch konsistent mit der durch Trennzeichen getrennte ist wiederhergestellt Werten (CSV)-Dateiformat, die von der/Backup Option.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad73e520-484f-4cf1-a7f9-ae7488e9edf6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1961387083a8a61b27f3e44a2380a6060a02f98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868981"
---
# <a name="auditpol-restore"></a>Wiederherstellen von "auditpol"

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Stellt System sicherheitsüberwachungs-Richtlinieneinstellungen, die pro Benutzer sicherheitsüberwachungs-Richtlinieneinstellungen für alle Benutzer und alle Überwachungsoptionen aus einer Datei, die syntaktisch konsistent mit dem die/Backup ein, die durch Trennzeichen getrennten Werten (CSV)-Dateiformat ist Option.

## <a name="syntax"></a>Syntax
```
auditpol /restore /file:<filename>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/file|Gibt die Datei, die von der die Überwachungsrichtlinie wiederhergestellt werden soll. Die Datei muss mit der/Backup erstellt wurden option muss syntaktisch mit dem CSV-Dateiformat, die von der/Backup verwendet konsistent sein, oder wählen Sie Option.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
für die Wiederherstellungsvorgänge für die pro-Benutzer und Systemrichtlinien müssen Sie schreiben müssen, oder Full Control-Berechtigung für dieses Objekt festgelegt werden, in der Sicherheitsbeschreibung. Sie können auch die Restore-Vorgang ausführen, indem besitzt die **Verwalten von überwachungs- und Sicherheitsprotokollen** Benutzerrecht (SeSecurityPrivilege). Berechtigung "SeSecurityPrivilege" ist nützlich, beim Wiederherstellen der Sicherheitsbeschreibung im Falle einer unbeabsichtigter Fehler oder böswilligen Angriffen.
## <a name="BKMK_examples"></a>Beispiele für
Zum Wiederherstellen von System sicherheitsüberwachungs-Richtlinieneinstellungen, die pro Benutzer sicherheitsüberwachungs-Richtlinieneinstellungen für alle Benutzer und alle Überwachungsoptionen aus einer Datei namens auditpolicy.csv, die erstellt wurde, mithilfe der/Backup-Befehl müssen:
```
auditpol /restore /file:c:\auditpolicy.csv
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Sicherung mit "auditpol"](auditpol-backup.md)
