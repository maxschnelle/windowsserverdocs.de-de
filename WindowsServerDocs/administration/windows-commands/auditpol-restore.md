---
title: Auditpol-Wiederherstellung
description: 'Windows-Befehle Topic für **Auditpol Restore** : stellt Systemüberwachungs-Richtlinien Einstellungen, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen aus einer Datei wieder her, die syntaktisch konsistent mit dem von der/Backup-Option verwendeten CSV-Dateiformat (Comma-Separated Value) ist.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b91f3745354c695c4ab0c71b429718bff05d8098
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382408"
---
# <a name="auditpol-restore"></a>Auditpol-Wiederherstellung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt System Überwachungs Richtlinien Einstellungen, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen aus einer Datei wieder her, die syntaktisch konsistent mit dem von der/Backup-Option verwendeten CSV-Dateiformat (Comma-Separated Value) ist.

## <a name="syntax"></a>Syntax
```
auditpol /restore /file:<filename>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/file|Gibt die Datei an, aus der die Überwachungsrichtlinie wieder hergestellt werden soll. Die Datei muss mithilfe der/Backup-Option erstellt worden sein oder muss syntaktisch konsistent mit dem CSV-Dateiformat sein, das von der/Backup-Option verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
bei Wiederherstellungs Vorgängen für die Richtlinie und die System Richtlinie pro Benutzer müssen Sie über die Berechtigung Schreiben oder Vollzugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können den Wiederherstellungs Vorgang auch durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. SeSecurityPrivilege ist nützlich, wenn die Sicherheits Beschreibung im Falle eines unbeabsichtigten Fehlers oder böswilligen Angriffs wieder hergestellt wird.
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um die Richtlinien Einstellungen für die Systemüberwachung, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen aus einer Datei mit dem Namen "Auditpolicy. csv", die mit dem/Backup-Befehl erstellt wurde, wiederherzustellen:
```
auditpol /restore /file:c:\auditpolicy.csv
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Auditpol-Sicherung](auditpol-backup.md)
