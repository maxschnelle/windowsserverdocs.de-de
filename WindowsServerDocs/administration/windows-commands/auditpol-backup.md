---
title: auditpol backup
description: Referenz Artikel für den Befehl Auditpol Backup, mit dem die Richtlinien Einstellungen für die Systemüberwachung, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen für eine CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte) gesichert werden.
ms.topic: reference
ms.assetid: dc84e581-aa0f-4c91-b13b-1d970bad5517
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1bee18b3bbad093364301543dda1199598e8ad00
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633247"
---
# <a name="auditpol-backup"></a>auditpol backup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert die Richtlinien Einstellungen für die Systemüberwachung, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen für eine CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte).

Zum Ausführen von *Sicherungs* Vorgängen für die *Benutzer-* und *System* Richtlinien müssen Sie über die Berechtigung **Schreiben** oder **voll** Zugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch *Sicherungs* Vorgänge durchführen, wenn Sie über das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) verfügen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der für die Ausführung der gesamten *Sicherungs* Vorgänge nicht erforderlich ist.

## <a name="syntax"></a>Syntax

```
auditpol /backup /file:<filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|-----------|------------- |
| /file | Gibt den Namen der Datei an, in der die Überwachungsrichtlinie gesichert wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer, System Überwachungs Richtlinien Einstellungen und alle Überwachungs Optionen in eine CSV-formatierte Textdatei mit dem Namen auditpolicy.csv zu sichern:

```
auditpol /backup /file:C:\auditpolicy.csv
```

> [!NOTE]
> Wenn kein Laufwerk angegeben wird, wird das aktuelle Verzeichnis verwendet.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [auditpol restore](auditpol-restore.md)

- [Auditpol-Befehle](auditpol.md)
