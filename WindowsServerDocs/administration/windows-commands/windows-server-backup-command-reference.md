---
title: Befehlsreferenz zur Windows Server-Sicherung
description: Referenz Artikel zur Referenz für den Sicherungs Befehl.
ms.topic: article
ms.assetid: 03de0a65-21f0-4dd7-a3ae-251c98bbf6eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2042c55774aefbb603c8592d48be12d22c0f545e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896854"
---
# <a name="windows-server-backup-command-reference"></a>Befehlsreferenz zur Windows Server-Sicherung



Die folgenden Unterbefehle für **Wbadmin** stellen die Sicherungs-und Wiederherstellungs Funktionalität von einer Eingabeaufforderung aus bereit.

Sie müssen ein Mitglied der Gruppe " **Administratoren** " sein, um einen Sicherungs Zeitplan zu konfigurieren. Wenn Sie mit diesem Befehl alle anderen Aufgaben ausführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein.

Sie müssen **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten auf **Start**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

|Unterbefehl|Beschreibung|
|----------|-----------|
|[Wbadmin enable backup](wbadmin-enable-backup.md)|Konfiguriert und aktiviert einen täglichen Sicherungs Zeitplan.|
|[Wbadmin disable backup](wbadmin-disable-backup.md)|Deaktiviert tägliche Sicherungen.|
|[Wbadmin start backup](wbadmin-start-backup.md)|Führt eine einmalige Sicherung aus. Bei Verwendung ohne Parameter verwendet die Einstellungen aus dem täglichen Sicherungs Zeitplan.|
|[Wbadmin stop job](wbadmin-stop-job.md)|Beendet den zurzeit laufenden Sicherungs-oder Wiederherstellungs Vorgang.|
|[Wbadmin get versions](wbadmin-get-versions.md)|Listet Details zu Sicherungen, die auf dem lokalen Computer wieder hergestellt werden können, oder, wenn ein anderer Speicherort angegeben ist, von einem anderen Computer.|
|[Wbadmin get items](wbadmin-get-items.md)|Listet die Elemente auf, die in einer bestimmten Sicherung enthalten sind.|
|[Wbadmin start recovery](wbadmin-start-recovery.md)|Führt eine Wiederherstellung der angegebenen Volumes, Anwendungen, Dateien oder Ordner aus.|
|[Wbadmin get status](wbadmin-get-status.md)|Zeigt den Status des zurzeit laufenden Sicherungs-oder Wiederherstellungs Vorgangs an.|
|[Wbadmin get disks](wbadmin-get-disks.md)|Listet Datenträger auf, die zurzeit online sind.|
|[Wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|Führt eine Wiederherstellung des Systemstatus aus.|
|[Wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)|Führt eine Sicherung des Systemstatus aus.|
|[Wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|Löscht mindestens eine Systemstatus Sicherung.|
|[Wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)|Führt eine Wiederherstellung des vollständigen Systems aus (mindestens alle Volumes, die den Zustand des Betriebssystems enthalten). Dieser Unterbefehl ist nur verfügbar, wenn Sie die Windows-Wiederherstellungs Umgebung verwenden.|
|[Wbadmin restore catalog](wbadmin-restore-catalog.md)|Stellt einen Sicherungs Katalog von einem angegebenen Speicherort wieder her, wenn der Sicherungs Katalog auf dem lokalen Computer beschädigt ist.|
|[Wbadmin delete catalog](wbadmin-delete-catalog.md)|Löscht den Sicherungs Katalog auf dem lokalen Computer. Verwenden Sie diesen Befehl nur, wenn der Sicherungs Katalog auf diesem Computer beschädigt ist und Sie keine Sicherungen an einem anderen Speicherort gespeichert haben, der zum Wiederherstellen des Katalogs verwendet werden kann.|