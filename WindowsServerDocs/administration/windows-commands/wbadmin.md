---
title: wbadmin
description: Referenz Thema für Wbadmin, mit dem Sie das Betriebssystem, die Volumes, Dateien, Ordner und Anwendungen über eine Eingabeaufforderung sichern und wiederherstellen können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b0b3f32-d21f-4861-84bb-b2eadbf1e7b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94f07d17d46dad4e5301ba3ea6be94b10f26a3af
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725836"
---
# <a name="wbadmin"></a>wbadmin



Ermöglicht das Sichern und Wiederherstellen von Betriebssystem, Volumes, Dateien, Ordnern und Anwendungen über eine Eingabeaufforderung.

Sie müssen ein Mitglied der Gruppe " **Administratoren** " sein, um eine regelmäßig geplante Sicherung zu konfigurieren. Wenn Sie mit diesem Befehl alle anderen Aufgaben ausführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein.

Sie müssen **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="subcommands"></a>Unterbefehle

|Unterbefehl|BESCHREIBUNG|
|----------|-----------|
|[Wbadmin enable backup](wbadmin-enable-backup.md)|Konfiguriert und aktiviert eine regelmäßig geplante Sicherung.|
|[Wbadmin disable backup](wbadmin-disable-backup.md)|Deaktiviert tägliche Sicherungen.|
|[Wbadmin start backup](wbadmin-start-backup.md)|Führt eine einmalige Sicherung aus. Bei Verwendung ohne Parameter verwendet die Einstellungen aus dem täglichen Sicherungs Zeitplan.|
|[Wbadmin stop job](wbadmin-stop-job.md)|Beendet den zurzeit laufenden Sicherungs-oder Wiederherstellungs Vorgang.|
|[Wbadmin get versions](wbadmin-get-versions.md)|Listet Details zu Sicherungen, die auf dem lokalen Computer wieder hergestellt werden können, oder, wenn ein anderer Speicherort angegeben ist, von einem anderen Computer.|
|[Wbadmin get items](wbadmin-get-items.md)|Listet die Elemente auf, die in einer Sicherung enthalten sind.|
|[Wbadmin start recovery](wbadmin-start-recovery.md)|Führt eine Wiederherstellung der angegebenen Volumes, Anwendungen, Dateien oder Ordner aus.|
|[Wbadmin get status](wbadmin-get-status.md)|Zeigt den Status des zurzeit laufenden Sicherungs-oder Wiederherstellungs Vorgangs an.|
|[Wbadmin get disks](wbadmin-get-disks.md)|Listet Datenträger auf, die zurzeit online sind.|
|[Wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|Führt eine Wiederherstellung des Systemstatus aus.|
|[Wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)|Führt eine Sicherung des Systemstatus aus.|
|[Wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|Löscht mindestens eine Systemstatus Sicherung.|
|[Wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)|Führt eine Wiederherstellung des vollständigen Systems aus (mindestens alle Volumes, die den Zustand des Betriebssystems enthalten). Dieser Unterbefehl ist nur verfügbar, wenn Sie die Windows-Wiederherstellungs Umgebung verwenden.|
|[Wbadmin restore catalog](wbadmin-restore-catalog.md)|Stellt einen Sicherungs Katalog von einem angegebenen Speicherort wieder her, wenn der Sicherungs Katalog auf dem lokalen Computer beschädigt ist.|
|[Wbadmin delete catalog](wbadmin-delete-catalog.md)|Löscht den Sicherungs Katalog auf dem lokalen Computer. Verwenden Sie diesen Unterbefehl nur, wenn der Sicherungs Katalog auf diesem Computer beschädigt ist und Sie keine Sicherungen an einem anderen Speicherort gespeichert haben, der zum Wiederherstellen des Katalogs verwendet werden kann.|

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Sicherung und Wiederherstellung](https://go.microsoft.com/fwlink/?LinkID=195054)
-   [Windows Server-Sicherung-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj902428.aspx)