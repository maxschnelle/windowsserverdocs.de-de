---
title: Sicherung von "auditpol"
description: Windows-Befehle Thema **"auditpol" Backup** -sichert System Richtlinieneinstellungen, die pro Benutzer sicherheitsüberwachungs-Richtlinieneinstellungen für alle Benutzer und alle Überwachungsoptionen in eine durch Trennzeichen getrennten Werten (CSV)-Textdatei zu überwachen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc84e581-aa0f-4c91-b13b-1d970bad5517
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78594c0445ae482e49d47b3b67bb867e53866017
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867951"
---
# <a name="auditpol-backup"></a>Sicherung von "auditpol"

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sichert System überwachen Richtlinieneinstellungen, die pro Benutzer sicherheitsüberwachungs-Richtlinieneinstellungen für alle Benutzer und alle Überwachungsoptionen in eine durch Trennzeichen getrennten Werten (CSV)-Textdatei.

## <a name="syntax"></a>Syntax
```
auditpol /backup /file:<filename>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/file|Gibt den Namen der Datei, die Überwachungsrichtlinie gesichert werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
für die Sicherungsvorgänge für die pro-Benutzer und Systemrichtlinien müssen Sie schreiben müssen, oder Full Control-Berechtigung für dieses Objekt festgelegt werden, in der Sicherheitsbeschreibung. Sie können Sicherungsvorgänge auch ausführen, indem besitzt die **Verwalten von überwachungs- und Sicherheitsprotokollen** Benutzerrecht (SeSecurityPrivilege). Allerdings ermöglicht dieses Recht zusätzliche Zugriffsrechte, die nicht zum Ausführen des List-Vorgangs erforderlich ist.
## <a name="BKMK_examples"></a>Beispiele für
Um benutzerspezifische Überwachung sichern sicherheitsüberwachungs-Richtlinieneinstellungen für alle Benutzer und System-Richtlinieneinstellungen, und alle Überwachungsoptionen in eine CSV-formatierte Textdatei mit dem Namen auditpolicy.csv, Typ:
```
auditpol /backup /file:C:\auditpolicy.csv 
```
> [!NOTE]
> Wenn kein Laufwerk angegeben wird, wird das aktuelle Verzeichnis verwendet.
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Wiederherstellung mit "auditpol"](auditpol-restore.md)
