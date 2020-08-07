---
title: auditpol
description: Referenz Artikel zum Auditpol-Befehl, in dem Informationen zu und zum Bearbeiten von Überwachungs Richtlinien angezeigt werden.
ms.topic: article
ms.assetid: a02cfb9d-732f-4e77-aeba-f18265daa3af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 026dfb747f6013c6d2b6469eb2082819c4018504
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895296"
---
# <a name="auditpol"></a>auditpol

Zeigt Informationen zu und führt Funktionen zum Bearbeiten von Überwachungs Richtlinien aus, einschließlich:

- Festlegen und Abfragen einer System Überwachungsrichtlinie

- Festlegen und Abfragen einer Überwachungsrichtlinie pro Benutzer

- Festlegen und Abfragen von Überwachungs Optionen.

- Festlegen und Abfragen der Sicherheits Beschreibung, die zum Delegieren des Zugriffs auf eine Überwachungsrichtlinie verwendet wird.

- Berichterstellung oder Sicherung einer Überwachungsrichtlinie in eine CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte).

- Laden einer Überwachungsrichtlinie aus einer CSV-Textdatei.

- Konfigurieren globaler Ressourcen-SACLs.

## <a name="syntax"></a>Syntax

```
auditpol command [<sub-command><options>]
```

### <a name="parameters"></a>Parameter

| Unterbefehl | Beschreibung |
| ----------- | ----------- |
| /Get | Zeigt die aktuelle Überwachungsrichtlinie an. Weitere Informationen finden Sie unter [Auditpol Get](auditpol-get.md) für Syntax und Optionen. |
| /Set | Legt die Überwachungsrichtlinie fest. Weitere Informationen finden Sie unter [Auditpol Set](auditpol-set.md) für Syntax und Optionen. |
| /list | Zeigt auswählbare Richtlinien Elemente an. Weitere Informationen finden Sie unter [auditpol list](auditpol-list.md) (Syntax und Optionen). |
| /backup | Speichert die Überwachungsrichtlinie in einer Datei. Weitere Informationen finden Sie unter [Auditpol-Sicherung](auditpol-backup.md) für Syntax und Optionen. |
| /Restore | Stellt die Überwachungsrichtlinie aus einer Datei wieder her, die zuvor mit Auditpol/Backup. erstellt wurde. Weitere Informationen finden Sie unter [Auditpol Restore](auditpol-restore.md) für Syntax und Optionen. |
| /Clear | Löscht die Überwachungsrichtlinie. Weitere Informationen finden Sie unter [Auditpol Clear](auditpol-clear.md) für Syntax und Optionen. |
| /remove | Entfernt alle Überwachungs Richtlinien Einstellungen pro Benutzer und deaktiviert alle Systemüberwachungs-Richtlinien Einstellungen. Weitere Informationen finden Sie unter [Auditpol Remove](auditpol-remove.md) (Syntax und Optionen). |
| /resourceSACL | Konfiguriert globale Ressourcensystem-Zugriffs Steuerungs Listen (SACLs). **Hinweis:** Gilt nur für Windows 7 und Windows Server 2008 R2. Weitere Informationen finden Sie unter [Auditpol resourcesacl](auditpol-resourcesacl.md). |
| /?| Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
