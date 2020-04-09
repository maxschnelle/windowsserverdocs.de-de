---
title: auditpol
description: Windows-Befehls Thema für **Auditpol**, das Informationen zu und Funktionen zum Bearbeiten von Überwachungs Richtlinien anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a02cfb9d-732f-4e77-aeba-f18265daa3af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 00365b0e46b8bff761cf991dbdbd09d8f5e9c687
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851133"
---
# <a name="auditpol"></a>auditpol

Zeigt Informationen zu und führt Funktionen zum Bearbeiten von Überwachungs Richtlinien aus.

Beispiele für die Verwendung dieses Befehls finden Sie im Abschnitt "Beispiele" in den einzelnen Themen.

## <a name="syntax"></a>Syntax

```
auditpol command [<sub-command><options>]
```

#### <a name="parameters"></a>Parameter

| Unterbefehl | Beschreibung |
| ----------- | ----------- |
| /Get | Zeigt die aktuelle Überwachungsrichtlinie an. Weitere Informationen finden Sie unter [Auditpol Get](auditpol-get.md) für Syntax und Optionen. |
| /set | Legt die Überwachungsrichtlinie fest. Weitere Informationen finden Sie unter [Auditpol Set](auditpol-set.md) für Syntax und Optionen. |
| /list | Zeigt auswählbare Richtlinien Elemente an. Weitere Informationen finden Sie unter [auditpol list](auditpol-list.md) (Syntax und Optionen). |
| /backup | Speichert die Überwachungsrichtlinie in einer Datei. Weitere Informationen finden Sie unter [Auditpol-Sicherung](auditpol-backup.md) für Syntax und Optionen. |
| /Restore | Stellt die Überwachungsrichtlinie aus einer Datei wieder her, die zuvor mit Auditpol/Backup. erstellt wurde. Weitere Informationen finden Sie unter [Auditpol Restore](auditpol-restore.md) für Syntax und Optionen. |
| /Clear | Löscht die Überwachungsrichtlinie. Weitere Informationen finden Sie unter [Auditpol Clear](auditpol-clear.md) für Syntax und Optionen. |
| /remove | Entfernt alle Überwachungs Richtlinien Einstellungen pro Benutzer und deaktiviert alle Systemüberwachungs-Richtlinien Einstellungen. Weitere Informationen finden Sie unter [Auditpol Remove](auditpol-remove.md) (Syntax und Optionen). |
| /resourceSACL | Konfiguriert globale Ressourcensystem-Zugriffs Steuerungs Listen (SACLs). **Hinweis:** Gilt nur für Windows 7 und Windows Server 2008 R2. Weitere Informationen finden Sie unter [Auditpol resourcesacl](auditpol-resourcesacl.md). |
| /?| Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

Mit dem Befehlszeilenprogramm der Überwachungsrichtlinie können folgende Aktionen verwendet werden:

- Festlegen und Abfragen einer System Überwachungsrichtlinie

- Festlegen und Abfragen einer Überwachungsrichtlinie pro Benutzer

- Festlegen und Abfragen von Überwachungs Optionen.

- Festlegen und Abfragen der Sicherheits Beschreibung, die zum Delegieren des Zugriffs auf eine Überwachungsrichtlinie verwendet wird.

- Dient zum melden oder Sichern einer Überwachungsrichtlinie in einer CSV-Textdatei (Comma-Separated Value, Komma getrennte Werte).

- Laden einer Überwachungsrichtlinie aus einer CSV-Textdatei.

- Konfigurieren Sie globale Ressourcen-SACLs.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)