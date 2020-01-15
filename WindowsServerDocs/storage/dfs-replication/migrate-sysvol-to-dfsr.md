---
title: Migrieren der SYSVOL-Replikation zur DFS-Replikation
ms.date: 07/02/2012
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: d8d9d47ff8f14ce316d2352729247ab2dcf4acbc
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949702"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>Migrieren der SYSVOL-Replikation zur DFS-Replikation


Aktualisiert: 25. August 2010

Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008

Domänen Controller verwenden einen speziellen freigegebenen Ordner mit dem Namen SYSVOL, um Anmelde Skripts zu replizieren und Objektdateien an andere Domänen Controller Gruppenrichtlinie. Windows 2000 Server und Windows Server 2003 verwenden den Datei Replikations Dienst (File Replication Service, FRS) zum Replizieren von SYSVOL, während Windows Server 2008 den neueren DFS-Replikation-Dienst verwendet, wenn in Domänen mit der Domänen Funktionsebene Windows Server 2008 und FRS für Domänen, die Führen Sie ältere Domänen Funktionsebenen aus.

Wenn Sie DFS-Replikation verwenden möchten, um den SYSVOL-Ordner zu replizieren, können Sie entweder eine neue Domäne erstellen, die die Domänen Funktionsebene von Windows Server 2008 verwendet, oder Sie können das in diesem Dokument beschriebene Verfahren zum Aktualisieren einer vorhandenen Domäne und zum Migrieren der Replikation zu verwenden. DFS-Replikation.

In diesem Dokument wird davon ausgegangen, dass Sie über grundlegende Kenntnisse der Active Directory Domain Services (AD DS), FRS und verteiltes Dateisystem Replikation (DFS-Replikation) verfügen. Weitere Informationen finden Sie unter [Active Directory Domain Services Overview](https://go.microsoft.com/fwlink/?linkid=147787), [FRS Overview](https://go.microsoft.com/fwlink/?linkid=121763)oder [Overview of DFS-Replikation](https://go.microsoft.com/fwlink/?linkid=121762)


> [!NOTE]
> Informationen zum Herunterladen einer druckbaren Version dieses Handbuchs finden Sie unter <a href="https://go.microsoft.com/fwlink/?linkid=150375">SYSVOL Replication Migration Guide: FRS to DFS-Replikation</a> (https://go.microsoft.com/fwlink/?LinkId=150375)
<br>


## <a name="in-this-guide"></a>Inhalt dieser Anleitung

[Konzeptionelle Informationen zur SYSVOL-Migration](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640170(v=ws.10))

  - [SYSVOL-Migrations Zustände](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641052(v=ws.10))  
      
  - [Übersicht über das SYSVOL-Migrationsverfahren](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639809(v=ws.10))  
      

[SYSVOL-Migrationsverfahren](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639860(v=ws.10))

  - [Migrieren zum vorbereiteten Zustand](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641193(v=ws.10))  
      
  - [Migrieren zum umgeleiteten Zustand](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641340(v=ws.10))  
      
  - [Migrieren in den Zustand "entfernt"](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640254(v=ws.10))  
      

[Problembehandlung der SYSVOL-Migration](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640395(v=ws.10))

  - [Problembehandlung bei SYSVOL-Migrationsproblemen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639976(v=ws.10))  
      
  - [Rollback der SYSVOL-Migration zu einem vorherigen stabilen Zustand](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640509(v=ws.10))  
      

[Referenzinformationen zur SYSVOL-Migration](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640293(v=ws.10))

  - [Unterstützte SYSVOL-Migrations Szenarios](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639854(v=ws.10))  
      
  - [Überprüfen des Status der SYSVOL-Migration](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639789(v=ws.10))  
      
  - [DFSRMIG](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641227(v=ws.10))  
      
  - [Aktionen für das SYSVOL-Migrations Tool](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639712(v=ws.10))  
      

## <a name="additional-references"></a>Weitere Verweise

[SYSVOL-Migrations Reihe: Teil 1 – Einführung in den SYSVOL-Migrationsprozess](https://go.microsoft.com/fwlink/?linkid=121756)

[SYSVOL-Migrations Reihe: Teil 2 – DFSRMIG. exe: das SYSVOL-Migrationstool](https://go.microsoft.com/fwlink/?linkid=121757)

[SYSVOL-Migrations Reihe: Teil 3 – Migrieren zum Zustand "vorbereitet"](https://go.microsoft.com/fwlink/?linkid=121758)

[SYSVOL-Migrations Reihe: Teil 4 – Migrieren zum Status "umgeleitet"](https://go.microsoft.com/fwlink/?linkid=121759)

[SYSVOL-Migrations Reihe: Teil 5 – Migrieren zum Zustand "gelöscht"](https://go.microsoft.com/fwlink/?linkid=121760)

[Schritt-für-Schritt-Anleitung für verteilte Dateisysteme in Windows Server 2008](https://go.microsoft.com/fwlink/?linkid=85231)

[Technische Referenz zu FRS](https://go.microsoft.com/fwlink/?linkid=121764)

