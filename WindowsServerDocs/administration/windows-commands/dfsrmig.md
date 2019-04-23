---
title: dfsrmig
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da05aec5ca5a5634585c5f5406181c5c90ee3a30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856941"
---
# <a name="dfsrmig"></a>dfsrmig

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Die `dfsrmig` Befehl migriert SYSvol-Replikation aus der Windows-Verwaltungsinstrumentation (File Replication Service, FRS) zur Replikation des verteilten Dateisystems (Distributed File System, DFS), enthält Informationen über den Fortschritt der Migration und ändert die active Directory-Domänendienste (AD DS)-Objekte zu die Migration unterstützt.
Beispiele zur Verwendung mit diesem Befehl finden Sie in der [Beispiele](#BKMK_examples) weiter unten in diesem Dokument.
## <a name="syntax"></a>Syntax
```
dfsrmig [/SetGlobalState <state> | /GetGlobalState | /GetMigrationState | /createGlobalObjects | 
/deleteRoNtfrsMember [<read_only_domain_controller_name>] | /deleteRoDfsrMember [<read_only_domain_controller_name>] | /?]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/SetGlobalState <state>|Legt den gewünschten globale Migrationsstatus für die Domäne in den Zustand, der dem angegebenen Wert entspricht *Zustand*.<br /><br />Verwenden Sie diesen Befehl zum Fortsetzen des Vorgangs durch die Migration oder die Rollback-Prozesse, die gültigen Zustände zu durchlaufen. Diese Option können Sie zum Initialisieren und steuern den Migrationsprozess durch Festlegen der globalen Migrationsstatus in AD DS auf dem PDC-Emulator. Wenn der PDC-Emulator nicht verfügbar ist, schlägt dieser Befehl fehl.<br /><br /> Sie können den Migrationsstatus für die globale nur festlegen, um einen stabilen Zustand. Die gültigen Werte für *Zustand*, daher sind **0** für den Startstatus **1** für den Zustand "vorbereitet" **2** für den Zustand "Redirected" und **3** für den Status der eliminiert.<br /><br />Migration zu den eliminiert-Status ist nicht umkehrbar und Rollback in diesem Status ist nicht möglich, daher verwenden Sie den Wert **3** für *Zustand* nur wenn Sie vollständig Committd für die Verwendung von DFS-Replikation für SYSvol sind die Replikation.|
|/GetGlobalState|Ruft den aktuellen globalen Migrationsstatus für die Domäne aus der lokalen Kopie des AD DS-Datenbank, die bei Ausführung auf dem PDC-Emulator ab.<br /><br />Verwenden Sie diese Option, um sicherzustellen, dass Sie den richtigen globalen Migrationsstatus festlegen. Nur stabile Migrationsstatus globale Migrationsstatus, daher werden die Ergebnisse, die die **Dfsrmig** Berichten mithilfe des Befehls die **/GetGlobalState** Option entsprechen den Zuständen, Sie können festlegen, mit der **/SetGlobalState** Option.<br /><br />Führen Sie die **Dfsrmig** -Befehl mit der **/GetGlobalState** Option nur für den PDC-Emulator. Active Directory-Replikation repliziert den globalen Zustand auf die anderen Domänencontroller in der Domäne, aber die Replikationswartezeiten zu Inkonsistenzen führen können, wenn das Ausführen der **Dfsrmig** -Befehl mit der **/GetGlobalState**  Option auf einem Domänencontroller als PDC-Emulator. Verwenden Sie zum Überprüfen des von lokalen Migrationsstatus eines Domänencontrollers als PDC-Emulator die **/GetMigrationState** option.|
|/GetMigrationState|Ruft den aktuellen Zustand der lokalen Migration für alle Domänencontroller in der Domäne, und bestimmt, ob diese lokalen Status dem aktuellen globalen Migration entsprechen.<br /><br />Verwenden Sie diese Option, um festzustellen, ob alle anderen Domänencontroller den globalen Migrationsstatus erreicht haben. Die Ausgabe der **Dsfrmig** Befehl bei der Verwendung der **/GetMigrationState** Option gibt an, ob Migration mit dem aktuellen globalen Status abgeschlossen ist, und den Migrationsstatus für die lokale für alle Listet Domänencontroller, die nicht den aktuellen Zustand des globalen Migration erreicht haben. Lokale Migrationsstatus für Domänencontroller kann es sich um Übergänge zwischen Zuständen für Domänencontroller enthalten, die nicht den aktuellen Zustand des globalen Migration erreicht haben.|
|/createGlobalObjects|erstellt von der globalen Objekte und Einstellungen in AD DS, das DFS-Replikation verwendet.<br /><br />Sie sollten nicht benötigen, verwenden Sie diese Option während einer normalen Migration, weil der DFS-Replikationsdienst automatisch diese AD DS-Objekte und Einstellungen während der Migration vom Startstatus in den Zustand "vorbereitet" erstellt. Verwenden Sie diese Option, um diese Objekte und Einstellungen manuell in den folgenden Situationen zu erstellen:<br /><br />-   **Ein neue schreibgeschützte Domänencontroller heraufgestuft wird, während der Migration**. Der DFS-Replikationsdienst erstellt automatisch die AD DS-Objekte und Einstellungen für die DFS-Replikation während der Migration vom Startstatus in den Status ' vorbereitet '. Wenn ein neue schreibgeschützte Domänencontroller in der Domäne, nach diesem Übergang heraufgestuft wird, aber vor der Migration in den Zustand eliminiert, klicken Sie dann die Objekte, die der neu aktivierten nur-Lese Domänencontroller entsprechen, sind nicht in AD DS erstellt Replikation und die Migration fehlschlägt.<br />– In diesem Fall können Sie führen die **Dfsrmig** Befehl mit der **/createGlobalObjects** Option aus, um auf schreibgeschützte Domänencontroller manuell die Objekte zu erstellen, die sie nicht noch. Das Ausführen dieses Befehls hat keine Auswirkungen auf den Domänencontrollern, die bereits die Objekte und Einstellungen für die DFS-Replikationsdienst.<br />-   **Die globalen Einstellungen für die DFS-Replikationsdienst fehlen oder gelöscht wurden**. Wenn diese Einstellungen für einen bestimmten Domänencontroller fehlen, stoppt Migration vom Zustand "Start" zum Zustand "vorbereitet", bei dem Vorbereiten der Übergangsstatus für den Domänencontroller. In diesem Fall können Sie die **Dfsrmig** -Befehl mit der **/createGlobalObjects** Option aus, um die Einstellungen manuell zu erstellen. **Hinweis**: Da der globalen AD DS-Einstellungen für die DFS-Replikationsdienst für einen schreibgeschützten Domänencontroller, auf dem PDC-Emulator erstellt werden, müssen diese Einstellungen auf den schreibgeschützten Domänencontroller vom PDC-Emulator vor der DFS-Replikationsdienst replizieren, auf die Read-only-Domänencontroller kann diese Einstellungen verwenden. Aufgrund von aktiven bei Replikationswartezeiten dauert diese Replikation einige Zeit ausgeführt.|
|/deleteRoNtfrsMember [< Read_only_domain_controller_name >]|Löschen der globale AD DS-Einstellungen für FRS-Replikation, die die angegebenen schreibgeschützten Domänencontroller entsprechen, oder der globalen AD DS-Einstellungen für FRS-Replikation für alle schreibgeschützten Domänencontroller löscht, wenn kein Wert angegeben wird, für die *Read_only_ Domänencontrollername*.<br /><br />Sie sollten nicht müssen verwenden Sie diese Option während einer normalen Migration, da der DFS-Replikationsdienst automatisch diese Einstellungen für die AD DS während der Migration vom Zustand "Redirected" in den Zustand eliminiert gelöscht. Da diese Einstellungen aus AD DS Read-only-Domänencontroller gelöscht werden können, der PDC-Emulator führt diesen Vorgang und die Änderungen, die letztlich auf die schreibgeschützte Domänencontroller nach der entsprechenden Latenzzeiten für active Directory-Replikation repliziert werden.<br /><br />Sie können diese Option verwenden, die AD DS-Einstellungen manuell zu löschen, nur, wenn das automatische Löschen ein Fehler, auf einem schreibgeschützten Domänencontroller auftritt und den schreibgeschützten Domänencontroller für einen langen Ime während der Migration vom Zustand "Redirected" in den Zustand eliminiert stoppt.|
|/deleteRoDfsrMember [< Read_only_domain_controller_name >]|Löschen der globale AD DS-Einstellungen für die DFS-Replikation, die die angegebenen schreibgeschützten Domänencontroller entsprechen, oder der globale AD DS-Einstellungen für die DFS-Replikation für alle schreibgeschützten Domänencontroller löscht, wenn kein Wert angegeben wird, für die *Read_only_ Domänencontrollername*.<br /><br />Mit dieser Option können Sie um die AD DS-Einstellungen manuell zu löschen, nur, wenn das automatische Löschen ein Fehler, auf einem schreibgeschützten Domänencontroller auftritt und die Read-only-Domänencontroller für eine lange stoppt Zeit bei die Migration vom Zustand "vorbereitet" auf den Anfangszustand zurückgesetzt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an. Wie ein ausführen **Dfsrmig** ohne Optionen.|
## <a name="remarks"></a>Hinweise
-   DFSRMIG.exe, das Migrationstool für den DFS-Replikationsdienst wird mit der DFS-Replikationsdienst installiert.
    Dcpromo.exe installiert und den DFS-Replikationsdienst wird gestartet, wenn Sie den Computer zu einem Domänencontroller heraufstufen, einen neuen Windows Server 2008-Server. Beim Aktualisieren eines Servers von Windows Server 2003 auf Windows Server 2008, den Upgradevorgang installiert und startet den Dienst für die DFS-Replikation. Sie müssen nicht den DFS-Replikationsdienst installiert und gestartet, dass der DFS-Replikation-Rollendienst installiert.
-   Die **Dfsrmig** Tool wird nur auf Domänencontrollern, die auf dem Windows Server 2008-Domänenfunktionsebene ausgeführt unterstützt, da der SYSvol-Migration von der FRS-zur DFS-Replikation nur auf einem Domänencontroller möglich ist, die auf der  Windows Server 2008-Domänenfunktionsebene.
-   Können Sie ausführen, die **Dfsrmig** Befehl auf allen Domänencontrollern, aber das Erstellen bzw. bearbeiten die AD DS Objekte sind nur für Lese-/ Schreibzugriff kann Domänencontroller (nicht auf Read-only-Domänencontroller) zulässig.
-   Ausführung **Dfsrmig** ohne Optionen zeigt die Hilfe an der Eingabeaufforderung.
## <a name="BKMK_examples"></a>Beispiele für
Auf den globalen Migrationsstatus vorbereiteten festgelegt werden soll (**1**), und Starten der Migration zu oder Rollback aus dem Zustand "vorbereitet", Typ:
```
dfsrmig /SetGlobalState 1
```
Zum Festlegen des Migrationsstatus der globalen zu starten (**0**), und initiieren Sie Rollback auf den Startzustand, Typ:
```
dfsrmig /SetGlobalState 0
```
Um den globalen Migrationsstatus anzuzeigen, geben Sie Folgendes ein:
```
dfsrmig /GetGlobalState
```
Dieses Beispiel zeigt die normale Ausgabe aus dem **Dfsrmig /GetGlobalState** Befehl.
```
Current DFSR global state:  Prepared 
Succeeded.
```
Zum Anzeigen von Informationen, ob die von lokalen Migrationsstatus auf allen Domänencontrollern entsprechen, den globalen Migrationsstatus und die von lokalen Migrationsstatus für alle Domänencontroller, in denen des lokale Status nicht mit den globalen Zustand übereinstimmt, geben Sie Folgendes ein:
```
dfsrmig /GetMigrationState
```
Dieses Beispiel zeigt die normale Ausgabe aus dem **Dfsrmig /GetMigrationState** Befehl, wenn die von lokalen Migrationsstatus für alle Domänencontroller den globalen Migrationsstatus übereinstimmen.
```
All Domain Controllers have migrated successfully to Global state ( Prepared ).
Migration has reached a consistent state on all Domain Controllers.
Succeeded.
```
Dieses Beispiel zeigt die normale Ausgabe aus dem **Dfsrmig /GetMigrationState** Befehl, wenn die von lokalen Migrationsstatus auf einige Domänencontroller nicht über den Migrationsstatus für die globale übereinstimmen.
```
The following Domain Controllers are not in sync with Global state ( Prepared ):
Domain Controller (Local Migration State)   DC type
=========
CONTOSO-DC2 ( start )   ReadOnly DC
CONTOSO-DC3 ( Preparing )   Writable DC
Migration has not yet reached a consistent state on all domain controllers
State information might be stale due to AD latency.
```
So erstellen globalen Objekte und Einstellungen, die DFS-Replikation verwendet, in AD DS auf Domänencontroller, in denen diese Einstellungen nicht automatisch während der Migration erstellt wurden, oder, bei dem diese Einstellungen fehlen:
```
dfsrmig /createGlobalObjects
```
Um die globalen AD DS-Einstellungen für FRS-Replikation für einen schreibgeschützten Domänencontroller, der mit dem Namen "Contoso-dc2", wenn diese Einstellungen nicht gelöscht werden konnten, automatisch gelöscht wird während der Migration zu löschen, geben Sie Folgendes ein:
```
dfsrmig /deleteRoNtfrsMember contoso-dc2
```
Um die globalen AD DS-Einstellungen für FRS-Replikation für alle schreibgeschützten Domänencontroller zu löschen, wenn diese Einstellungen nicht automatisch vom Migrationsprozess gelöscht wurden, geben Sie Folgendes ein:
```
dfsrmig /deleteRoNtfrsMember
```
Zum Löschen der globale AD DS-Einstellungen für die DFS-Replikation für einen schreibgeschützten Domänencontroller, der mit dem Namen "Contoso-dc2", wenn diese Einstellungen nicht automatisch vom Migrationsprozess gelöscht wurden, geben Sie Folgendes ein:
```
dfsrmig /deleteRoDfsrMember contoso-dc2
```
Um die globalen AD DS-Einstellungen für die DFS-Replikation für alle schreibgeschützten Domänencontroller zu löschen, wenn diese Einstellungen nicht automatisch vom Migrationsprozess gelöscht wurden, geben Sie Folgendes ein:
```
dfsrmig /deleteRoDfsrMember
```
## <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](https://go.microsoft.com/fwlink/?LinkId=122056)

[Reihe für SYSvol-Migration: Part 2 dfsrmig.exe: Das SYSvol-Migrationstool](https://go.microsoft.com/fwlink/?LinkID=121757)
