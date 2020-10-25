---
title: wbadmin
description: Referenz Artikel für die Wbadmin-Befehle, mit denen Sie das Betriebssystem, die Volumes, Dateien, Ordner und Anwendungen über eine Eingabeaufforderung sichern und wiederherstellen können.
ms.topic: reference
ms.assetid: 4b0b3f32-d21f-4861-84bb-b2eadbf1e7b8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: df96e85d7cb4999088efe9bd6ede70087cd24cb7
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524665"
---
# <a name="wbadmin"></a>wbadmin

Ermöglicht das Sichern und Wiederherstellen von Betriebssystem, Volumes, Dateien, Ordnern und Anwendungen über eine Eingabeaufforderung.

Zum Konfigurieren einer regelmäßig geplanten Sicherung mithilfe dieses Befehls müssen Sie Mitglied der Gruppe " **Administratoren** " sein. Wenn Sie mit diesem Befehl alle anderen Aufgaben ausführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein.

Sie müssen **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [wbadmin delete catalog](wbadmin-delete-catalog.md) | Löscht den Sicherungs Katalog auf dem lokalen Computer. Verwenden Sie diesen Befehl nur, wenn der Sicherungs Katalog auf diesem Computer beschädigt ist und Sie keine Sicherungen an einem anderen Speicherort gespeichert haben, der zum Wiederherstellen des Katalogs verwendet werden kann. |
| [wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md) | Löscht mindestens eine Systemstatus Sicherung. |
| [wbadmin disable backup](wbadmin-disable-backup.md) | Deaktiviert tägliche Sicherungen. |
| [wbadmin enable backup](wbadmin-enable-backup.md) | Konfiguriert und aktiviert eine regelmäßig geplante Sicherung. |
| [wbadmin get disks](wbadmin-get-disks.md) | Listet Datenträger auf, die zurzeit online sind. |
| [wbadmin get items](wbadmin-get-items.md) | Listet die Elemente auf, die in einer Sicherung enthalten sind. |
| [wbadmin get status](wbadmin-get-status.md) | Zeigt den Status des zurzeit laufenden Sicherungs-oder Wiederherstellungs Vorgangs an. |
| [wbadmin get versions](wbadmin-get-versions.md) | Listet Details zu Sicherungen, die auf dem lokalen Computer wieder hergestellt werden können, oder, wenn ein anderer Speicherort angegeben ist, von einem anderen Computer. |
| [wbadmin restore catalog](wbadmin-restore-catalog.md) | Stellt einen Sicherungs Katalog von einem angegebenen Speicherort wieder her, wenn der Sicherungs Katalog auf dem lokalen Computer beschädigt ist. |
| [wbadmin start backup](wbadmin-start-backup.md) | Führt eine einmalige Sicherung aus. Bei Verwendung ohne Parameter verwendet die Einstellungen aus dem täglichen Sicherungs Zeitplan. |
| [wbadmin start recovery](wbadmin-start-recovery.md) | Führt eine Wiederherstellung der angegebenen Volumes, Anwendungen, Dateien oder Ordner aus. |
| [wbadmin start sysrecovery](wbadmin-start-sysrecovery.md) | Führt eine Wiederherstellung des vollständigen Systems aus (mindestens alle Volumes, die den Zustand des Betriebssystems enthalten). Dieser Befehl ist nur verfügbar, wenn Sie die Windows-Wiederherstellungs Umgebung verwenden. |
| [wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md) | Führt eine Sicherung des Systemstatus aus. |
| [wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md) | Führt eine Wiederherstellung des Systemstatus aus. |
| [wbadmin stop job](wbadmin-stop-job.md) | Beendet den zurzeit laufenden Sicherungs-oder Wiederherstellungs Vorgang. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Windows Server-Sicherung-Cmdlets in Windows PowerShell](/powershell/module/windowsserverbackup)

- [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)
