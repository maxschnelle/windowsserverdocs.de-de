---
title: Auditpol-Sicherung
description: Referenz Thema für den Befehl Auditpol Backup, mit dem die Richtlinien Einstellungen für die Systemüberwachung, Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer und alle Überprüfungs Optionen für eine CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte) gesichert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc84e581-aa0f-4c91-b13b-1d970bad5517
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ddc6bbbc379453c86df27674b57f29f7c0960772
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719168"
---
# <a name="auditpol-backup"></a>Auditpol-Sicherung

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

Geben Sie Folgendes ein, um die Überwachungs Richtlinien Einstellungen pro Benutzer für alle Benutzer, System Überwachungs Richtlinien Einstellungen und alle Überwachungs Optionen in eine CSV-formatierte Textdatei mit dem Namen "Auditpolicy. csv" zu sichern:

```
auditpol /backup /file:C:\auditpolicy.csv
```

> [!NOTE]
> Wenn kein Laufwerk angegeben wird, wird das aktuelle Verzeichnis verwendet.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Auditpol-Wiederherstellung](auditpol-restore.md)

- [Auditpol-Befehle](auditpol.md)
