---
title: auditpol restore
description: Referenz Artikel für den Befehl Auditpol Restore, der Systemüberwachungs-Richtlinien Einstellungen, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen aus einer Datei, die syntaktisch konsistent mit dem von der Option/Backup verwendeten CSV-Dateiformat (Comma-Separated Value) ist, wiederherstellt.
ms.topic: reference
ms.assetid: ad73e520-484f-4cf1-a7f9-ae7488e9edf6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d6dc8dde77189cbd1134779bf89f253402f181dc
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633118"
---
# <a name="auditpol-restore"></a>auditpol restore

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt System Überwachungs Richtlinien Einstellungen, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen aus einer Datei wieder her, die syntaktisch konsistent mit dem von der/Backup-Option verwendeten CSV-Dateiformat (Comma-Separated Value) ist.

Zum Ausführen von *Wiederherstellungs* Vorgängen für *Benutzer-* und *System* Richtlinien müssen Sie über die Berechtigung **Schreiben** oder **voll** Zugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können *Wiederherstellungs* Vorgänge auch ausführen, wenn Sie über das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) verfügen. Dies ist nützlich, wenn die Sicherheits Beschreibung im Falle eines Fehlers oder böswilligen Angriffs wieder hergestellt wird.

## <a name="syntax"></a>Syntax

```
auditpol /restore /file:<filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ------- | -------- |
| /file | Gibt die Datei an, aus der die Überwachungsrichtlinie wieder hergestellt werden soll. Die Datei muss mithilfe der/Backup-Option erstellt worden sein oder muss syntaktisch konsistent mit dem CSV-Dateiformat sein, das von der/Backup-Option verwendet wird. |
| /? |Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Richtlinien Einstellungen für die Systemüberwachung, die Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen aus einer Datei mit dem Namen auditpolicy.csv, die mit dem/Backup-Befehl erstellt wurde, wiederherzustellen:

```
auditpol /restore /file:c:\auditpolicy.csv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [auditpol backup](auditpol-backup.md)

- [Auditpol-Befehle](auditpol.md)
