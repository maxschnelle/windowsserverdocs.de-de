---
title: wbadmin
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b0b3f32-d21f-4861-84bb-b2eadbf1e7b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ce8109ef6a0885abd02ef1dee9f11d21b7d7e9b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858881"
---
# <a name="wbadmin"></a>wbadmin



Können Sie sichern und Wiederherstellen von Ihrem Betriebssystem, Volumes, Dateien, Ordner und Anwendungen über eine Eingabeaufforderung.

Um einer regelmäßig geplanten Sicherung zu konfigurieren, Sie müssen Mitglied der **Administratoren** Gruppe. Um alle anderen Vorgänge mit dem folgenden Befehl ausführen zu können, müssen Sie Mitglied werden die **Sicherungs-Operatoren** oder **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert.

Sie müssen ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, mit der Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="subcommands"></a>Unterbefehle

|Unterbefehl|Beschreibung|
|----------|-----------|
|[Sicherung des Wbadmin-aktivieren](wbadmin-enable-backup.md)|Konfiguriert, und ermöglicht es eine regelmäßig geplante Sicherung.|
|[Wbadmin deaktiviert die Sicherung](wbadmin-disable-backup.md)|Deaktiviert Ihre täglichen Sicherungen.|
|[Sicherung des Wbadmin-starten](wbadmin-start-backup.md)|Führt eine einmalige Sicherung aus. Wenn ohne Parameter verwendet wird, verwendet die Einstellungen aus den täglichen Sicherungszeitplan aus.|
|[Auftrag zum Beenden des Wbadmin](wbadmin-stop-job.md)|Beendet die derzeit ausgeführten sicherungs- oder Wiederherstellungsvorgang.|
|[Wbadmin Get-Versionen](wbadmin-get-versions.md)|Listet die Details von Sicherungen, die vom lokalen Computer oder, wenn Sie einen anderen Speicherort angegeben wird, von einem anderen Computer.|
|[Wbadmin Get-Elemente](wbadmin-get-items.md)|Listet die Elemente in einer Sicherung enthalten.|
|[Wbadmin Start-Wiederherstellung](wbadmin-start-recovery.md)|Führt eine Wiederherstellung von Volumes, Anwendungen, Dateien oder Ordner angegeben.|
|[Wbadmin Get status](wbadmin-get-status.md)|Zeigt den Status der aktuell ausgeführten sicherungs- oder Wiederherstellungsvorgang.|
|[Wbadmin Get-Datenträger](wbadmin-get-disks.md)|Werden Datenträger aufgeführt, die zurzeit online sind.|
|[Wbadmin Start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|Wird eine systemstatuswiederherstellung ausgeführt.|
|[Wbadmin Start systemstatebackup](wbadmin-start-systemstatebackup.md)|Führt eine Sicherung des Systemstatus an.|
|[Wbadmin Delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|Löscht eine oder mehrere systemstatussicherungen.|
|[Wbadmin Start sysrecovery](wbadmin-start-sysrecovery.md)|Führt eine Wiederherstellung des vollständigen Systems (mindestens alle Volumes, die das Betriebssystem Status enthalten). Dieses Unterbefehl ist nur verfügbar, wenn Sie die Windows-Wiederherstellungsumgebung verwenden.|
|[Wbadmin-Restore-Katalog](wbadmin-restore-catalog.md)|Wiederherstellung ein Sicherungskatalogs einen angegebenen Speicherort in dem Fall, in dem der Sicherungskatalog auf dem lokalen Computer beschädigt wurde.|
|[Befehl Wbadmin Delete catalog](wbadmin-delete-catalog.md)|Löscht den Sicherungskatalog auf dem lokalen Computer. Verwenden Sie diese Unterbefehl, nur, wenn der Sicherungskatalog auf diesem Computer ist beschädigt, und Sie haben keine Sicherungen an einem anderen Standort, mit denen Sie zum Wiederherstellen des Katalogs.|

#### <a name="additional-references"></a>Weitere Verweise

-   [Sicherung und Wiederherstellung](https://go.microsoft.com/fwlink/?LinkID=195054)
-   [Windows Server Backup Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj902428.aspx)