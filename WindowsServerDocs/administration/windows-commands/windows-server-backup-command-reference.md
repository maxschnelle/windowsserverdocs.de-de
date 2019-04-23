---
title: Befehlsreferenz zur Windows Server-Sicherung
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03de0a65-21f0-4dd7-a3ae-251c98bbf6eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ded5039e122832c95eda864bcdcc76f580ca7108
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839811"
---
# <a name="windows-server-backup-command-reference"></a>Befehlsreferenz zur Windows Server-Sicherung



Die folgenden Unterbefehle für **Wbadmin** sicherungs- und Wiederherstellungsfunktionalität an einer Eingabeaufforderung angeben.

Um einen Sicherungszeitplan konfigurieren zu können, müssen Sie Mitglied werden die **Administratoren** Gruppe. Um alle anderen Vorgänge mit dem folgenden Befehl ausführen zu können, müssen Sie Mitglied werden die **Sicherungs-Operatoren** oder **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert.

Sie müssen ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie auf **starten**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

|Unterbefehl|Beschreibung|
|----------|-----------|
|[Sicherung des Wbadmin-aktivieren](wbadmin-enable-backup.md)|Konfiguriert und aktiviert einen täglichen Sicherungszeitplan aus.|
|[Wbadmin deaktiviert die Sicherung](wbadmin-disable-backup.md)|Deaktiviert Ihre täglichen Sicherungen.|
|[Sicherung des Wbadmin-starten](wbadmin-start-backup.md)|Führt eine einmalige Sicherung aus. Wenn ohne Parameter verwendet wird, verwendet die Einstellungen aus den täglichen Sicherungszeitplan aus.|
|[Auftrag zum Beenden des Wbadmin](wbadmin-stop-job.md)|Beendet die derzeit ausgeführten sicherungs- oder Wiederherstellungsvorgang.|
|[Wbadmin Get-Versionen](wbadmin-get-versions.md)|Listet die Details von Sicherungen, die vom lokalen Computer oder, wenn Sie einen anderen Speicherort angegeben wird, von einem anderen Computer.|
|[Wbadmin Get-Elemente](wbadmin-get-items.md)|Listet die Elemente in einer bestimmten Sicherung enthalten.|
|[Wbadmin Start-Wiederherstellung](wbadmin-start-recovery.md)|Führt eine Wiederherstellung von Volumes, Anwendungen, Dateien oder Ordner angegeben.|
|[Wbadmin Get status](wbadmin-get-status.md)|Zeigt den Status der aktuell ausgeführten sicherungs- oder Wiederherstellungsvorgang.|
|[Wbadmin Get-Datenträger](wbadmin-get-disks.md)|Werden Datenträger aufgeführt, die zurzeit online sind.|
|[Wbadmin Start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|Wird eine systemstatuswiederherstellung ausgeführt.|
|[Wbadmin Start systemstatebackup](wbadmin-start-systemstatebackup.md)|Führt eine Sicherung des Systemstatus an.|
|[Wbadmin Delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|Löscht eine oder mehrere systemstatussicherungen.|
|[Wbadmin Start sysrecovery](wbadmin-start-sysrecovery.md)|Führt eine Wiederherstellung des vollständigen Systems (mindestens alle Volumes, die das Betriebssystem Status enthalten). Dieses Unterbefehl ist nur verfügbar, wenn Sie die Windows-Wiederherstellungsumgebung verwenden.|
|[Wbadmin-Restore-Katalog](wbadmin-restore-catalog.md)|Wiederherstellung ein Sicherungskatalogs einen angegebenen Speicherort in dem Fall, in dem der Sicherungskatalog auf dem lokalen Computer beschädigt wurde.|
|[Befehl Wbadmin Delete catalog](wbadmin-delete-catalog.md)|Löscht den Sicherungskatalog auf dem lokalen Computer. Verwenden Sie diesen Befehl nur, wenn der Sicherungskatalog auf diesem Computer ist beschädigt, und Sie haben keine Sicherungen an einem anderen Standort, mit denen Sie zum Wiederherstellen des Katalogs.|