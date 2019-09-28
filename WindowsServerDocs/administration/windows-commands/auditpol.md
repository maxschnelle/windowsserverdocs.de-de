---
title: auditpol
description: Thema Windows-Befehle für **Auditpol** -zeigt Informationen zu und führt Funktionen zum Bearbeiten von Überwachungs Richtlinien aus.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a02cfb9d-732f-4e77-aeba-f18265daa3af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e249a9e2a07505f052b774208c514b4d16879b8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382381"
---
# <a name="auditpol"></a>auditpol



Zeigt Informationen zu und führt Funktionen zum Bearbeiten von Überwachungs Richtlinien aus.

Beispiele für die Verwendung dieses Befehls finden Sie im Abschnitt "Beispiele" in den einzelnen Themen.

## <a name="syntax"></a>Syntax

```
Auditpol command [<sub-command><options>]
```

## <a name="parameters"></a>Parameter

|Unterbefehl|Beschreibung|
|-----------|-----------|
|/Get|Zeigt die aktuelle Überwachungsrichtlinie an.</br>Syntax und Optionen finden [Sie unter Auditpol Get](auditpol-get.md) .|
|/Set|Legt die Überwachungsrichtlinie fest.</br>Informationen zur Syntax und zu Optionen finden Sie unter [Auditpol-Satz](auditpol-set.md) .|
|/List|Zeigt auswählbare Richtlinien Elemente an.</br>Syntax und Optionen finden Sie unter [auditpol list](auditpol-list.md) .|
|/backup|Speichert die Überwachungsrichtlinie in einer Datei.</br>Syntax und Optionen finden Sie unter [Auditpol-Sicherung](auditpol-backup.md) .|
|/Restore|Stellt die Überwachungsrichtlinie aus einer Datei wieder her, die zuvor mit Auditpol/Backup. erstellt wurde.</br>Syntax und Optionen finden Sie unter [Auditpol Restore](auditpol-restore.md) .|
|/Clear|Löscht die Überwachungsrichtlinie.</br>Syntax und Optionen finden Sie unter [Auditpol Clear](auditpol-clear.md) .|
|/remove|Entfernt alle Überwachungs Richtlinien Einstellungen pro Benutzer und deaktiviert alle Systemüberwachungs-Richtlinien Einstellungen.</br>Syntax und Optionen finden Sie unter [Auditpol Remove](auditpol-remove.md) .|
|/resourceSACL|Konfiguriert globale Ressourcensystem-Zugriffs Steuerungs Listen (SACLs).</br>Hinweis: Gilt nur für Windows 7 und Windows Server 2008 R2.</br>Weitere Informationen finden Sie unter [Auditpol resourcesacl](auditpol-resourcesacl.md).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Mit dem Befehlszeilenprogramm der Überwachungsrichtlinie können folgende Aktionen verwendet werden:
-   Festlegen und Abfragen einer System Überwachungsrichtlinie
-   Festlegen und Abfragen einer Überwachungsrichtlinie pro Benutzer
-   Festlegen und Abfragen von Überwachungs Optionen.
-   Festlegen und Abfragen der Sicherheits Beschreibung, die zum Delegieren des Zugriffs auf eine Überwachungsrichtlinie verwendet wird.
-   Dient zum melden oder Sichern einer Überwachungsrichtlinie in einer CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte).
-   Laden einer Überwachungsrichtlinie aus einer CSV-Textdatei.
-   Konfigurieren Sie globale Ressourcen-SACLs.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)