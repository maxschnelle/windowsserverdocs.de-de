---
Title: Migrieren der SYSVOL-Replikation zur DFS-Replikation
ms.date: 07/02/2012
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 7ea883730fcab83d064fa41f610bde4837510276
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836641"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>Migrieren der SYSVOL-Replikation zur DFS-Replikation


Aktualisiert: 25 August 2010

Gilt für: WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2 und WindowsServer 2008

Domänencontroller verwenden speziellen freigegebenen Ordner SYSVOL Anmeldeskripts und Gruppenrichtlinien-Objektdateien mit anderen Domänencontrollern zu replizieren. Verwenden Sie Windows 2000 Server und Windows Server 2003 (File Replication Service, FRS) zum Replizieren von SYSVOL, während Windows Server 2008 mit den neueren DFS-Replikationsdienst in Domänen verwendet, die die Windows Server 2008-Domänenfunktionsebene verwenden und FRS für Domänen, Führen Sie die ältere Domänenfunktionsebenen dar.

Um DFS-Replikation zum Replizieren von SYSVOL-Ordners zu verwenden, können Sie eine neue Domäne, die die Windows Server 2008-Domänenfunktionsebene verwendet entweder erstellen oder können Sie die Prozedur, die in diesem Dokument zum Aktualisieren einer vorhandenen Domäne und Migrieren von Replikation beschrieben wird DFS-Replikation.

In diesem Dokument wird davon ausgegangen, dass Sie über grundlegende Kenntnisse von Active Directory Domain Services (AD DS), FRS- und Distributed File System Replication (DFS-Replikation) verfügen. Weitere Informationen finden Sie unter [Active Directory Domain Services Overview](http://go.microsoft.com/fwlink/?linkid=147787), [Dateireplikationsdienst (FRS) Übersicht über](http://go.microsoft.com/fwlink/?linkid=121763), oder [Übersicht über die der DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=121762)


> [!NOTE]
> Um eine druckbare Version dieses Handbuchs herunterzuladen, wechseln Sie zu <a href="http://go.microsoft.com/fwlink/?linkid=150375">Anleitung zur SYSVOL-Replikationsmigration: FRS-zu DFS-Replikation</a> ()http://go.microsoft.com/fwlink/?LinkId=150375)
<br>


## <a name="in-this-guide"></a>Inhalt dieser Anleitung

[Konzeptionelle Informationen für die SYSVOL-Migration](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640170(v=ws.10))

  - [SYSVOL-Migrationsstatus](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641052(v=ws.10))  
      
  - [Übersicht über die SYSVOL-Migrationsvorgang](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639809(v=ws.10))  
      

[SYSVOL-Migrationsvorgang](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639860(v=ws.10))

  - [Migrieren zu Zustand "vorbereitet"](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641193(v=ws.10))  
      
  - [Migration zu den Status "umgeleitet"](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641340(v=ws.10))  
      
  - [Migration zu den Status "entfernt"](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640254(v=ws.10))  
      

[Problembehandlung bei der SYSVOL-Migration](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640395(v=ws.10))

  - [Beheben von SYSVOL-Migrationsproblemen](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639976(v=ws.10))  
      
  - [Rollback der SYSVOL-Migration zu einem früheren stabilen Status](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640509(v=ws.10))  
      

[Referenzinformationen für SYSVOL-Migration](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640293(v=ws.10))

  - [Unterstützte SYSVOL-Migrationsszenarien](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639854(v=ws.10))  
      
  - [Überprüfen des Status der SYSVOL-Migration](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639789(v=ws.10))  
      
  - [Dfsrmig](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641227(v=ws.10))  
      
  - [Aktionen des SYSVOL-Migration](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639712(v=ws.10))  
      

## <a name="additional-references"></a>Weitere Verweise

[Reihe für SYSVOL-Migration: Teil 1 – Einführung in die SYSVOL-Migrationsvorgang](http://go.microsoft.com/fwlink/?linkid=121756)

[Reihe für SYSVOL-Migration: Teil 2—Dfsrmig.exe: Das SYSVOL-Migrationstool](http://go.microsoft.com/fwlink/?linkid=121757)

[Reihe für SYSVOL-Migration: Teil 3 – Migrieren zu den Status 'Vorbereitet'](http://go.microsoft.com/fwlink/?linkid=121758)

[Reihe für SYSVOL-Migration: Teil 4 – in den Zustand "REDIRECTED" Migrieren](http://go.microsoft.com/fwlink/?linkid=121759)

[Reihe für SYSVOL-Migration: Teil 5 – migrieren zu den Status "Gelöscht"](http://go.microsoft.com/fwlink/?linkid=121760)

[Schrittweise Anleitung für DFS-Systeme in WindowsServer 2008](http://go.microsoft.com/fwlink/?linkid=85231)

[Dateireplikationsdienst (FRS) – technische Referenz](http://go.microsoft.com/fwlink/?linkid=121764)

