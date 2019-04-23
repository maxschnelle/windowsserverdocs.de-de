---
title: auditpol
description: Windows-Befehle Thema **"auditpol"** – zeigt Informationen zu und führt die Funktionen zum Bearbeiten von Überwachungsrichtlinien.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d7e8364be977e868ac161704e67c37ec5c400e49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849221"
---
# <a name="auditpol"></a>auditpol



Zeigt Informationen zu und führt die Funktionen zum Bearbeiten von Überwachungsrichtlinien.

Beispiele wie dieser Befehl verwendet werden kann finden Sie im Abschnitt "Beispiele" in jedem Thema.

## <a name="syntax"></a>Syntax

```
Auditpol command [<sub-command><options>]
```

## <a name="parameters"></a>Parameter

|Unterbefehl|Beschreibung|
|-----------|-----------|
|/get|Zeigt den aktuellen Überwachungsrichtlinie.</br>Finden Sie unter ["auditpol" Get](auditpol-get.md) für die Syntax und Optionen.|
|/set|Legt die Überwachungsrichtlinie fest.</br>Finden Sie unter [Auditpol set](auditpol-set.md) für die Syntax und Optionen.|
|/list|Zeigt auswählbare Richtlinienelementen.</br>Finden Sie unter [Auditpol List](auditpol-list.md) für die Syntax und Optionen.|
|/backup|Speichert die Überwachungsrichtlinie in einer Datei an.</br>Finden Sie unter ["auditpol" Backup](auditpol-backup.md) für die Syntax und Optionen.|
|/ Restore|Stellt die Überwachungsrichtlinie aus einer Datei, die zuvor mithilfe von Auditpol/Backup erstellt wurde.</br>Finden Sie unter ["auditpol" Wiederherstellung](auditpol-restore.md) für die Syntax und Optionen.|
|/clear|Löscht die Überwachungsrichtlinie.</br>Finden Sie unter ["auditpol" clear](auditpol-clear.md) für die Syntax und Optionen.|
|/remove|Entfernt alle pro-Benutzer sicherheitsüberwachungs-Richtlinieneinstellungen, und alle System-sicherheitsüberwachungs-Richtlinieneinstellungen deaktiviert.</br>Finden Sie unter ["auditpol"-Remove](auditpol-remove.md) für die Syntax und Optionen.|
|/resourceSACL|Konfiguriert die globale Ressource Systemzugriff-Steuerungslisten (SACLs).</br>Hinweis: Gilt nur für Windows 7 und Windows Server 2008 R2.</br>Finden Sie unter ["auditpol" ResourceSACL](auditpol-resourcesacl.md).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Das Befehlszeilentool Tool für Überwachungsrichtlinien kann, verwendet werden:
-   Festlegen und Abfragen von einem Dateisystem-Überwachungsrichtlinie.
-   Festlegen und Abfragen von einer Überwachungsrichtlinie pro Benutzer.
-   Gruppe und die Abfrage, die Optionen für die Überwachung.
-   Festlegen und die Sicherheitsbeschreibung, die zum Delegieren des Zugriffs auf eine Überwachungsrichtlinie Abfragen.
-   Melden oder eine Überwachungsrichtlinie auf eine Text-Datei mit kommagetrennten Werten (CSV) sichern.
-   Laden Sie eine Überwachungsrichtlinie aus einer CSV-Textdatei.
-   Konfigurieren Sie globale Ressource SACLs.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)