---
title: Migrieren der SYSVOL-Replikation zur DFS-Replikation
ms.date: 07/02/2012
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: d4c34484f7eb12b9876dcca7809a31c0c291bcce
ms.sourcegitcommit: 3da6fcf4d853f6ff24b785b87787d0677b878253
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/12/2020
ms.locfileid: "90044827"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>Migrieren der SYSVOL-Replikation zur DFS-Replikation


Aktualisiert: 25. August 2010

Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008

Domänencontroller verwenden einen speziellen freigegebenen Ordner mit dem Namen SYSVOL, um Anmeldeskripts und Gruppenrichtlinien-Objektdateien auf andere Domänencontroller zu replizieren. Windows 2000 Server und Windows Server 2003 nutzen den Dateireplikationsdienst (File Replication Service, FRS) zum Replizieren von SYSVOL. Windows Server 2008 nutzt hingegen in Domänen mit der Domänenfunktionsebene Windows Server 2008 den neueren DFS-Replikationsdienst und in Domänen mit älteren Domänenfunktionsebenen FRS.

Um den SYSVOL-Ordner mithilfe der DFS-Replikation zu replizieren, kannst du entweder eine neue Domäne erstellen, die die Domänenfunktionsebene Windows Server 2008 verwendet, oder das in diesem Dokument beschriebene Verfahren nutzen, um eine vorhandene Domäne zu aktualisieren und die Replikation zur DFS-Replikation zu migrieren.

In diesem Dokument wird davon ausgegangen, dass du über grundlegende Kenntnisse von Active Directory Domain Services (AD DS), FRS und der DFS-Replikation (Distributed File System, verteiltes Dateisystem) verfügst. Weitere Informationen findest du in der [Übersicht über Active Directory Domain Services](https://go.microsoft.com/fwlink/?linkid=147787), [Übersicht über FRS](https://go.microsoft.com/fwlink/?linkid=121763) oder [Übersicht über die DFS-Replikation](https://go.microsoft.com/fwlink/?linkid=121762).


> [!NOTE]
> Um eine Druckversion dieser Anleitung herunterzuladen, navigierst du zur <a href="https://go.microsoft.com/fwlink/?linkid=150375">Anleitung für die Migration der SYSVOL-Replikation: FRS-zu-DFS-Replikation</a> (https://go.microsoft.com/fwlink/?LinkId=150375)
<br>


## <a name="in-this-guide"></a>Inhalt dieser Anleitung

[Grundlegende Informationen zur SYSVOL-Migration](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640170(v=ws.10))

  - [SYSVOL-Migrationsstatus](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641052(v=ws.10))

  - [Übersicht über den SYSVOL-Migrationsvorgang](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639809(v=ws.10))


[SYSVOL-Migrationsvorgang](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639860(v=ws.10))

  - [Migration zum Status „Vorbereitet“](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641193(v=ws.10))

  - [Migration zum Status „Umgeleitet“](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641340(v=ws.10))

  - [Migration zum Status „Entfernt“](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640254(v=ws.10))


[Problembehandlung bei der SYSVOL-Migration](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640395(v=ws.10))

  - [Beheben von SYSVOL-Migrationsproblemen](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639976(v=ws.10))

  - [Rollback der SYSVOL-Migration zu einem früheren stabilen Status](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640509(v=ws.10))


[Referenzinformationen zur SYSVOL-Migration](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640293(v=ws.10))

  - [Unterstützte SYSVOL-Migrationsszenarien](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639854(v=ws.10))

  - [Überprüfen des Status der SYSVOL-Migration](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639789(v=ws.10))

  - [Dfsrmig](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641227(v=ws.10))

  - [Aktionen des SYSVOL-Migrationstools](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639712(v=ws.10))


## <a name="additional-references"></a>Weitere Verweise

[SYSVOL-Migrationsreihe: Teil 1 – Einführung in den SYSVOL-Migrationsprozess](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-1-8211-introduction-to-the-sysvol/ba-p/423456)

[SYSVOL-Migrationsreihe: Teil 2 – Dfsrmig.exe: Das SYSVOL-Migrationstool](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-2-8211-dfsrmig-exe-the-sysvol/ba-p/423470)

[SYSVOL-Migrationsreihe: Teil 3 – Migration zum Status „VORBEREITET“](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-3-migrating-to-the-prepared-state/ba-p/423503)

[SYSVOL-Migrationsreihe: Teil 4 – Migration zum Status „UMGELEITET“](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-4-8211-migrating-to-the-8216/ba-p/423514)

[SYSVOL-Migrationsreihe: Teil 5 – Migration zum Status „ENTFERNT“](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-5-8211-migrating-to-the-8216/ba-p/423516)

[Schritt-für-Schritt-Anleitung zu verteilten Dateisystemen für Windows Server 2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732863(v=ws.10))

[Technische Referenz zu FRS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759297(v=ws.10))
