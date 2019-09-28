---
title: Auditpol-Sicherung
description: 'Thema zu Windows-Befehlen für die **Auditpol-Sicherung** : sichert Systemüberwachungs-Richtlinien Einstellungen, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen für eine CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte).'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 96b98a05740d3ce1bfe14eda4c5d97ba6c09ff32
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382452"
---
# <a name="auditpol-backup"></a>Auditpol-Sicherung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert die Richtlinien Einstellungen für die Systemüberwachung, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen für eine CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte).

## <a name="syntax"></a>Syntax
```
auditpol /backup /file:<filename>
```
## <a name="parameters"></a>Parameter

| Parameter |                                 Beschreibung                                 |
|-----------|-----------------------------------------------------------------------------|
|   /file   | Gibt den Namen der Datei an, in der die Überwachungsrichtlinie gesichert wird. |
|    /?     |                    Zeigt die Hilfe an der Eingabeaufforderung an.                     |

## <a name="remarks"></a>Hinweise
bei Sicherungs Vorgängen für die Richtlinie und die System Richtlinie pro Benutzer müssen Sie über die Berechtigung Schreiben oder Vollzugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können Sicherungs Vorgänge auch durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der nicht erforderlich ist, um den Auflistungs Vorgang auszuführen.
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um die Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer, System Überwachungs Richtlinien Einstellungen und alle Überwachungs Optionen in eine CSV-formatierte Textdatei mit dem Namen "Auditpolicy. csv" zu sichern:
```
auditpol /backup /file:C:\auditpolicy.csv 
```
> [!NOTE]
> Wenn kein Laufwerk angegeben wird, wird das aktuelle Verzeichnis verwendet.
> #### <a name="additional-references"></a>Weitere Verweise
> [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
> [Auditpol Restore](auditpol-restore.md)
