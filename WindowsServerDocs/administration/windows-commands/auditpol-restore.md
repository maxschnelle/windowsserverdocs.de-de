---
title: Auditpol-Wiederherstellung
description: Referenz Thema für den Befehl Auditpol Restore, bei dem Systemüberwachungs-Richtlinien Einstellungen, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen aus einer Datei, die syntaktisch konsistent mit dem von der Option/Backup verwendeten CSV-Dateiformat (Comma-Separated Value) ist, wieder hergestellt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ad73e520-484f-4cf1-a7f9-ae7488e9edf6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 64605a985c1cff13b842a99ae4ea52485bfc8220
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719061"
---
# <a name="auditpol-restore"></a>Auditpol-Wiederherstellung

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

Geben Sie Folgendes ein, um die Richtlinien Einstellungen für die Systemüberwachung, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überwachungs Optionen aus einer Datei mit dem Namen "Auditpolicy. csv", die mit dem/Backup-Befehl erstellt wurde, wiederherzustellen:

```
auditpol /restore /file:c:\auditpolicy.csv
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Auditpol-Sicherung](auditpol-backup.md)

- [Auditpol-Befehle](auditpol.md)
