---
title: dfsrmig
description: Referenz Artikel für den DFSRMIG-Befehl, der die SYSVOL-Replikation von FRS zu DFS-Replikation migriert, Informationen zum Fortschritt der Migration bereitstellt und AD DS Objekte zur Unterstützung der Migration ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87882ebe0beb687f704c5573091f56c067c278ee
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928635"
---
# <a name="dfsrmig"></a>dfsrmig

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Das Migrationstool für den DFS-Replikation-Dienst, dfsrmig.exe, wird mit dem DFS-Replikation-Dienst installiert. Dieses Tool migriert die SYSVOL-Replikation vom Datei Replikations Dienst (File Replication Service, FRS) verteiltes Dateisystem zur DFS-Replikation. Außerdem finden Sie hier Informationen zum Fortschritt der Migration und zum ändern Active Directory Domain Services (AD DS)-Objekten zur Unterstützung der Migration.

## <a name="syntax"></a>Syntax

```
dfsrmig [/setglobalstate <state> | /getglobalstate | /getmigrationstate | /createglobalobjects |
/deleterontfrsmember [<read_only_domain_controller_name>] | /deleterodfsrmember [<read_only_domain_controller_name>] | /?]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `/setglobalstate <state>` | Legt den globalen Migrations Zustand der Domäne auf einen Wert fest, der dem durch *State*angegebenen Wert entspricht. Der globale Migrations Zustand kann nur auf einen stabilen Zustand festgelegt werden. Zu den *Zustands* Werten gehören:<ul><li>**0** -Start Status</li><li>**1** -vorbereiteter Zustand</li><li>**2** -umgeleiteter Zustand</li><li>**3** : Zustand wird gelöscht</li></ul> |
| /getglobalstate | Ruft den aktuellen globalen Migrationsstatus für die Domäne aus der lokalen Kopie der AD DS Datenbank ab, wenn Sie auf dem PDC-Emulator ausgeführt wird. Verwenden Sie diese Option, um zu bestätigen, dass Sie den richtigen globalen Migrationsstatus festgelegt haben.<p>**Wichtig:** Sie sollten diesen Befehl nur für den PDC-Emulator ausführen. |
| /getmigrationstate | Ruft den aktuellen Zustand der lokalen Migration für alle Domänen Controller in der Domäne ab und bestimmt, ob diese lokalen Zustände dem aktuellen globalen Migrationsstatus entsprechen. Verwenden Sie diese Option, um zu bestimmen, ob alle Domänen Controller den globalen Migrations Zustand erreicht haben. |
| /createglobalobjects | Erstellt die globalen Objekte und Einstellungen in AD DS, die von DFS-Replikation verwendet werden. Die einzigen Situationen, in denen Sie diese Option verwenden sollten, um Objekte und Einstellungen manuell zu erstellen, sind:<ul><li>**Während der Migration wird ein neuer Schreib geschützter Domänen Controller**herauf gestuft. Wenn ein neuer Schreib geschützter Domänen Controller in der Domäne herauf gestuft wird, nachdem er in den Zustand " **vorbereitet** " versetzt wurde, aber **vor der Migration in den Zustand** "entfernt", werden die Objekte, die dem neuen Domänen Controller entsprechen, nicht erstellt, wodurch die Replikation und die Migration fehlschlagen.</li><li>**Die globalen Einstellungen für den DFS-Replikation Dienst fehlen oder wurden gelöscht**. Wenn diese Einstellungen für einen Domänen Controller fehlen, wird die Migration vom **Start** Status in den Status **vorbereitet** in den Zustand **Vorbereitung** versetzt. **Hinweis:** Da die globalen AD DS Einstellungen für den DFS-Replikation-Dienst für einen schreibgeschützten Domänen Controller auf dem PDC-Emulator erstellt werden, müssen diese Einstellungen auf den schreibgeschützten Domänen Controller aus dem PDC-Emulator repliziert werden, bevor der DFS-Replikation Dienst auf dem schreibgeschützten Domänen Controller diese Einstellungen verwenden kann. Aufgrund Active Directory Replikations Wartezeiten kann diese Replikation einige Zeit in Anspruch nehmen. |
| `/deleterontfrsmember [<read_only_domain_controller_name>]` | Löscht die globalen AD DS Einstellungen für die FRS-Replikation, die dem angegebenen schreibgeschützten Domänen Controller entsprechen, oder löscht die globalen AD DS Einstellungen für die FRS-Replikation für alle schreibgeschützten Domänen Controller, wenn kein Wert für angegeben ist `<read_only_domain_controller_name>` .<p>Diese Option sollte bei einem normalen Migrations Vorgang nicht verwendet werden, da der DFS-Replikation Dienst diese AD DS Einstellungen während der Migration vom **umgeleiteten** in **den Zustand "** entfernt" automatisch löscht. Verwenden Sie diese Option, um die AD DS Einstellungen nur manuell zu löschen, wenn der automatische Löschvorgang auf einem schreibgeschützten Domänen Controller fehlschlägt und den schreibgeschützten Domänen Controller während der Migration vom **umgeleiteten** in den **Zustand "** entfernt" versetzt. |
| `/deleterodfsrmember [<read_only_domain_controller_name>]` | Löscht die globalen AD DS Einstellungen für DFS-Replikation, die dem angegebenen schreibgeschützten Domänen Controller entsprechen, oder löscht die globalen AD DS Einstellungen für DFS-Replikation für alle schreibgeschützten Domänen Controller, wenn kein Wert für angegeben ist `<read_only_domain_controller_name>` .<p>Verwenden Sie diese Option, um die AD DS Einstellungen nur dann manuell zu löschen, wenn der automatische Löschvorgang auf einem schreibgeschützten Domänen Controller fehlschlägt und den schreibgeschützten Domänen Controller für einen längeren Zeitraum anhält, wenn ein Rollback der Migration vom Zustand "vorbereitet" in den Startstatus erfolgt. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Verwenden `/setglobalstate <state>` Sie den Befehl zum Festlegen des globalen Migrations Zustands in AD DS auf dem PDC-Emulator, um den Migrationsprozess zu initiieren und zu steuern. Wenn der PDC-Emulator nicht verfügbar ist, schlägt dieser Befehl fehl.

- **Die Migration** in den Zustand "entfernt" ist nicht rückgängig, und ein Rollback ist nicht möglich. verwenden Sie daher den Wert **3** nur für " *State* ", wenn Sie mit der Verwendung DFS-Replikation für die SYSVOL-Replikation

- Globale Migrations Zustände müssen einen stabilen Migrationsstatus aufweisen.

- Active Directory Replikation repliziert den globalen Status auf andere Domänen Controller in der Domäne, aber aufgrund von Replikations Wartezeiten können Sie Inkonsistenzen erhalten, wenn Sie `dfsrmig /getglobalstate` auf einem anderen Domänen Controller als dem PDC-Emulator ausführen.

- Die Ausgabe von `dsfrmig /getmigrationstate` gibt an, ob die Migration zum aktuellen globalen Status beendet ist. dabei wird der lokale Migrationsstatus für alle Domänen Controller aufgelistet, die den aktuellen globalen Migrationsstatus noch nicht erreicht haben. Der lokale Migrationsstatus für Domänen Controller kann auch Übergangszustände für Domänen Controller einschließen, die den aktuellen globalen Migrationsstatus nicht erreicht haben.

- Schreibgeschützte Domänen Controller können keine Einstellungen aus AD DS löschen, der PDC-Emulator führt diesen Vorgang aus, und die Änderungen werden schließlich nach den anwendbaren Wartezeiten für die Active Directory-Replikation auf die schreibgeschützten Domänen Controller repliziert.

- Der **DFSRMIG** -Befehl wird nur auf Domänen Controllern unterstützt, die auf der Windows Server-Domänen Funktionsebene ausgeführt werden, da die SYSVOL-Migration von FRS zu DFS-Replikation nur auf Domänen Controllern möglich ist, die auf dieser Ebene arbeiten.

- Sie können den **DFSRMIG** -Befehl auf einem beliebigen Domänen Controller ausführen, aber Vorgänge, die AD DS Objekte erstellen oder bearbeiten, sind nur auf Lese-/schreibfähigen Domänen Controllern zulässig (nicht auf schreibgeschützten Domänen Controllern).

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Status der globalen Migration auf "vorbereitet" (**1**) festzulegen und die Migration zu initiieren oder den Status "vorbereitet" zurückzusetzen:

```
dfsrmig /setglobalstate 1
```

Geben Sie Folgendes ein, um den globalen Migrationsstatus auf Start (**0**) festzulegen und den Rollback in den Startzustand zu initiieren:

```
dfsrmig /setglobalstate 0
```

Geben Sie Folgendes ein, um den globalen Migrationsstatus anzuzeigen:

```
dfsrmig /getglobalstate
```

Ausgabe des `dfsrmig /getglobalstate` Befehls:

```
Current DFSR global state: Prepared
Succeeded.
```

Geben Sie Folgendes ein, um Informationen dazu anzuzeigen, ob die lokalen Migrations Zustände auf allen Domänen Controllern dem globalen Migrationsstatus entsprechen und ob lokale Migrations Zustände vorhanden sind, bei denen der lokale Zustand nicht dem globalen Status entspricht, geben Sie Folgendes ein:

```
dfsrmig /GetMigrationState
```

Ausgabe des `dfsrmig /getmigrationstate` Befehls, wenn die lokalen Migrations Zustände auf allen Domänen Controllern dem globalen Migrationsstatus entsprechen:

```
All Domain Controllers have migrated successfully to Global state (Prepared).
Migration has reached a consistent state on all Domain Controllers.
Succeeded.
```

Ausgabe des `dfsrmig /getmigrationstate` Befehls, wenn die lokalen Migrations Zustände auf einigen Domänen Controllern nicht dem globalen Migrationsstatus entsprechen.

```
The following Domain Controllers are not in sync with Global state (Prepared):
Domain Controller (Local Migration State) DC type
=========
CONTOSO-DC2 (start) ReadOnly DC
CONTOSO-DC3 (Preparing) Writable DC
Migration has not yet reached a consistent state on all domain controllers
State information might be stale due to AD latency.
```

Geben Sie Folgendes ein, um die globalen Objekte und Einstellungen zu erstellen, die von DFS-Replikation in AD DS auf Domänen Controllern verwendet werden, auf denen diese Einstellungen während der Migration nicht automatisch erstellt wurden oder deren Einstellungen fehlen:

```
dfsrmig /createglobalobjects
```

Geben Sie Folgendes ein, um die globalen AD DS Einstellungen für die FRS-Replikation für einen schreibgeschützten Domänen Controller mit dem Namen "Configuration Manager" zu löschen, wenn diese Einstellungen beim Migrations Vorgang nicht automatisch gelöscht wurden:

```
dfsrmig /deleterontfrsmember contoso-dc2
```

Wenn Sie die globalen AD DS Einstellungen für die FRS-Replikation für alle schreibgeschützten Domänen Controller löschen möchten, wenn diese Einstellungen vom Migrationsprozess nicht automatisch gelöscht wurden, geben Sie Folgendes ein:

```
dfsrmig /deleterontfrsmember
```

Zum Löschen der globalen AD DS Einstellungen für DFS-Replikation für einen schreibgeschützten Domänen Controller mit dem Namen "" "" "" "" "" "".

```
dfsrmig /deleterodfsrmember contoso-dc2
```

Geben Sie Folgendes ein, um die globalen AD DS Einstellungen für DFS-Replikation für alle schreibgeschützten Domänen Controller zu löschen, wenn diese Einstellungen vom Migrationsprozess nicht automatisch gelöscht wurden:

```
dfsrmig /deleterodfsrmember
```

So zeigen Sie die Hilfe an der Eingabeaufforderung an:

```
dfsrmig
```

```
dfsrmig /?
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](https://go.microsoft.com/fwlink/?LinkId=122056)

- [SYSVOL-Migrations Reihe: Teil 2 dfsrmig.exe: das SYSVOL-Migrations Tool](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-2-8211-dfsrmig-exe-the-sysvol/ba-p/423470)

- [Active Directory Domain Services](../../identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview.md)
