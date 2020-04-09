---
title: Auditpol-Sicherung
description: Windows-Befehle für die **Auditpol-Sicherung**, mit der die Richtlinien Einstellungen für die Systemüberwachung, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen für eine CSV-Textdatei (Comma-Separated Value) gesichert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc84e581-aa0f-4c91-b13b-1d970bad5517
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8895f312606a6a6c45a77c659a1cd98d115babe3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851213"
---
# <a name="auditpol-backup"></a>Auditpol-Sicherung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert die Richtlinien Einstellungen für die Systemüberwachung, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen für eine CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte).

## <a name="syntax"></a>Syntax

```
auditpol /backup /file:<filename>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|-----------|------------- |
| /file | Gibt den Namen der Datei an, in der die Überwachungsrichtlinie gesichert wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

Bei Sicherungs Vorgängen für die Richtlinie und die System Richtlinie pro Benutzer müssen Sie über die Berechtigung Schreiben oder Vollzugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können Sicherungs Vorgänge auch durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der nicht erforderlich ist, um den Auflistungs Vorgang auszuführen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer, System Überwachungs Richtlinien Einstellungen und alle Überwachungs Optionen in eine CSV-formatierte Textdatei mit dem Namen "Auditpolicy. csv" zu sichern:

```
auditpol /backup /file:C:\auditpolicy.csv
```

> [!NOTE]
> Wenn kein Laufwerk angegeben wird, wird das aktuelle Verzeichnis verwendet.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Auditpol-Wiederherstellung](auditpol-restore.md)
