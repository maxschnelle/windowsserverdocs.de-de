---
title: dfsrmig
description: Das Thema Windows-Befehle für DFSRMIG, das die SYSVOL-Replikation von der Datei Replikations Dienst (FRS) zur verteiltes Dateisystem (DFS)-Replikation migriert, Informationen zum Fortschritt der Migration sowie Active Directory-Domänen Dienste (AD DS) zur Unterstützung der Migration ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d688832169cf216e628fe761f85d708a78103d89
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846163"
---
# <a name="dfsrmig"></a>dfsrmig

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Migriert die SYSVOL-Replikation vom Datei Replikations Dienst (File Replication Service, FRS) verteiltes Dateisystem zur DFS-Replikation, stellt Informationen zum Fortschritt der Migration bereit und ändert die Objekte der Active Directory-Domänen Dienste (AD DS) zur Unterstützung der Migration.

Beispiele für die Verwendung dieses Befehls finden Sie im Abschnitt " [Beispiele](#BKMK_examples) " weiter unten in diesem Dokument.

## <a name="syntax"></a>Syntax

```
dfsrmig [/SetGlobalState <state> | /GetGlobalState | /GetMigrationState | /createGlobalObjects | 
/deleteRoNtfrsMember [<read_only_domain_controller_name>] | /deleteRoDfsrMember [<read_only_domain_controller_name>] | /?]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung | | -----_ | ------ | | /SetGlobalState <state> | Legt den gewünschten globalen Migrationsstatus für die Domäne auf den Zustand fest, der dem durch den *Zustand*angegebenen Wert entspricht.<p>Um die Migration oder die Rollback-Prozesse fortzusetzen, verwenden Sie diesen Befehl, um die gültigen Zustände zu durchlaufen. Mit dieser Option können Sie den Migrationsprozess initiieren und Steuern, indem Sie den globalen Migrationsstatus in AD DS auf dem PDC-Emulator festlegen. Wenn der PDC-Emulator nicht verfügbar ist, schlägt dieser Befehl fehl.<p>Der globale Migrations Zustand kann nur auf einen stabilen Zustand festgelegt werden. Die gültigen Werte für den *Status*sind daher **0** für den Startzustand, **1** für den vorbereiteten Zustand, **2** für den umgeleiteten Zustand und **3** für den Zustand "entfernt".<p>Die Migration in den Zustand "entfernt" ist nicht rückgängig, und ein Rollback von diesem Zustand ist nicht möglich. verwenden Sie daher den Wert **3** nur für " *State* ", wenn Sie vollständig mit DFS-Replikation für die SYSVOL-Replikation zusammen sind. | | /GetGlobalState | Ruft den aktuellen globalen Migrationsstatus für die Domäne aus der lokalen Kopie der AD DS Datenbank ab, wenn Sie auf dem PDC-Emulator ausgeführt wird.<p>Verwenden Sie diese Option, um zu bestätigen, dass Sie den richtigen globalen Migrationsstatus festgelegt haben. Nur stabile Migrations Zustände können globale Migrations Zustände sein. daher entsprechen die Ergebnisse, die der **DFSRMIG** -Befehl mit der **/GetGlobalState** -Option meldet, den Zuständen, die Sie mit der Option **/SetGlobalState** festlegen können.<p>Sie sollten den **DFSRMIG** -Befehl mit der **/GetGlobalState** -Option nur für den PDC-Emulator ausführen. die Active Directory-Replikation repliziert den globalen Status auf die anderen Domänen Controller in der Domäne. Replikations Wartezeiten können jedoch zu Inkonsistenzen führen, wenn Sie den **DFSRMIG** -Befehl mit der **/GetGlobalState** -Option auf einem anderen Domänen Controller als dem PDC Verwenden Sie stattdessen die Option **/GetMigrationState** , um den lokalen Migrationsstatus eines anderen Domänen Controllers als dem PDC-Emulator zu überprüfen. | | /GetMigrationState | Ruft den aktuellen Zustand der lokalen Migration für alle Domänen Controller in der Domäne ab und bestimmt, ob diese lokalen Zustände dem aktuellen globalen Migrationsstatus entsprechen.<p>Verwenden Sie diese Option, um zu bestimmen, ob alle Domänen Controller den globalen Migrations Zustand erreicht haben. Die Ausgabe des Befehls **dsfrmig** bei Verwendung der Option **/GetMigrationState** gibt an, ob die Migration zum aktuellen globalen Status fertiggestellt ist. Außerdem wird der lokale Migrations Zustand für alle Domänen Controller aufgelistet, die den aktuellen globalen Migrationsstatus nicht erreicht haben. Der Status der lokalen Migration von Domänen Controllern kann Übergangszustände für Domänen Controller enthalten, die den aktuellen globalen Migrationsstatus nicht erreicht haben. | | /createGlobalObjects | Erstellt die globalen Objekte und Einstellungen in AD DS, die von DFS-Replikation verwendet werden.<p>Diese Option sollte bei einem normalen Migrations Vorgang nicht verwendet werden, da der DFS-Replikation-Dienst diese AD DS Objekte und-Einstellungen während der Migration vom Startstatus in den vorbereiteten Status automatisch erstellt. Verwenden Sie diese Option, um diese Objekte und Einstellungen in den folgenden Situationen manuell zu erstellen:<p>-  **ein neuer Schreib geschützter Domänen Controller während der Migration**höher gestuft wird. Der DFS-Replikation-Dienst erstellt automatisch die AD DS Objekte und Einstellungen für DFS-Replikation während der Migration vom Startstatus in den vorbereiteten Zustand. Wenn ein neuer Schreib geschützter Domänen Controller nach diesem Übergang in der Domäne herauf gestuft wird, jedoch vor der Migration in den Zustand "entfernt", werden die Objekte, die dem neu aktivierten schreibgeschützten Domänen Controller entsprechen, nicht in AD DS erstellt, wodurch die Replikation und die Migration fehlschlagen.<br />-In diesem Fall können Sie den **DFSRMIG** -Befehl mit der **/createGlobalObjects** -Option ausführen, um die Objekte auf einem schreibgeschützten Domänen Controller, auf dem Sie noch nicht vorhanden sind, manuell zu erstellen. Das Ausführen dieses Befehls hat keine Auswirkungen auf die Domänen Controller, die bereits über die Objekte und Einstellungen für den DFS-Replikation-Dienst verfügen.<p>- **die globalen Einstellungen für den DFS-Replikation Dienst fehlen oder wurden gelöscht**. Wenn diese Einstellungen für einen bestimmten Domänen Controller fehlen, wird beim Vorbereiten des Übergangsstatus für den Domänen Controller eine Migration vom Startstatus zum vorbereiteten Zustand angehalten. In diesem Fall können Sie den **DFSRMIG** -Befehl mit der **/createGlobalObjects** -Option verwenden, um die Einstellungen manuell zu erstellen. **Hinweis:** Da die globalen AD DS Einstellungen für den DFS-Replikation-Dienst für einen schreibgeschützten Domänen Controller auf dem PDC-Emulator erstellt werden, müssen diese Einstellungen auf den schreibgeschützten Domänen Controller aus dem PDC-Emulator repliziert werden, bevor der DFS-Replikation Dienst auf dem schreibgeschützten Domänen Controller diese Einstellungen verwenden kann. Aufgrund der aktiven IsName-Replikations Wartezeiten kann diese Replikation einige Zeit in Anspruch nehmen. | | /deleteRoNtfrsMember [< read_only_domain_controller_name >] | Löscht die globalen AD DS Einstellungen für die FRS-Replikation, die dem angegebenen schreibgeschützten Domänen Controller entsprechen, oder löscht die globalen AD DS Einstellungen für die FRS-Replikation für alle schreibgeschützten Domänen Controller, wenn kein Wert für *read_only_domain_controller_name*angegeben ist.<p>Diese Option sollte bei einem normalen Migrations Vorgang nicht verwendet werden, da der DFS-Replikation Dienst diese AD DS Einstellungen während der Migration vom umgeleiteten in den Zustand "entfernt" automatisch löscht. Da schreibgeschützte Domänen Controller diese Einstellungen nicht aus AD DS löschen können, führt der PDC-Emulator diesen Vorgang aus, und die Änderungen werden schließlich nach den anwendbaren Latenzen für die Active Directory-Replikation auf die schreibgeschützten Domänen Controller repliziert.<p>Mit dieser Option können Sie die AD DS Einstellungen nur manuell löschen, wenn der automatische Löschvorgang auf einem schreibgeschützten Domänen Controller fehlschlägt und den schreibgeschützten Domänen Controller während der Migration vom umgeleiteten in den Zustand "entfernt" versetzt. | | /deleteRoDfsrMember [< read_only_domain_controller_name >] | Löscht die globalen AD DS Einstellungen für DFS-Replikation, die dem angegebenen schreibgeschützten Domänen Controller entsprechen, oder löscht die globalen AD DS Einstellungen für DFS-Replikation für alle schreibgeschützten Domänen Controller, wenn kein Wert für *read_only_domain_controller_name*angegeben ist.<p>Verwenden Sie diese Option, um die AD DS Einstellungen nur dann manuell zu löschen, wenn der automatische Löschvorgang auf einem schreibgeschützten Domänen Controller fehlschlägt und den schreibgeschützten Domänen Controller für einen längeren Zeitraum anhält, wenn ein Rollback der Migration vom Zustand "vorbereitet" in den Startstatus erfolgt. | | /? | Zeigt die Hilfe an der Eingabeaufforderung an. Entspricht der Ausführung von **DFSRMIG** ohne Optionen. |

## <a name="remarks"></a>Hinweise
- DFSRMIG. exe, das Migrationstool für den DFS-Replikation-Dienst, wird mit dem DFS-Replikation-Dienst installiert.
 bei einem neuen Windows Server 2008-Server installiert und startet Dcpromo. exe den DFS-Replikation-Dienst, wenn Sie den Computer auf einen Domänen Controller herauf Stufen. Wenn Sie einen Server von Windows Server 2003 auf Windows Server 2008 aktualisieren, wird der DFS-Replikation Dienst beim Upgradevorgang installiert und gestartet. Sie müssen den DFS-Replikation-Rollen Dienst nicht installieren, damit der DFS-Replikation-Dienst installiert und gestartet wird.
- Das **DFSRMIG** -Tool wird nur auf Domänen Controllern unterstützt, die auf der Domänen Funktionsebene Windows Server 2008 ausgeführt werden, da die SYSVOL-Migration von FRS zu DFS-Replikation nur auf Domänen Controllern möglich ist, die auf der Domänen Funktionsebene von Windows Server 2008 arbeiten
- Sie können den **DFSRMIG** -Befehl auf einem beliebigen Domänen Controller ausführen, aber Vorgänge, die AD DS Objekte erstellen oder bearbeiten, sind nur auf Lese-/schreibfähigen Domänen Controllern zulässig (nicht auf schreibgeschützten Domänen Controllern).
- Wenn Sie **DFSRMIG** ohne Optionen ausführen, wird die Hilfe an der Eingabeaufforderung angezeigt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um den Status der globalen Migration auf vorbereitet (1) festzulegen und**eine**Migration zum bzw
 ```
 dfsrmig /SetGlobalState 1
 ```
 Geben Sie Folgendes ein, um den Status der globalen Migration auf Start (**0**) festzulegen und das Rollback in den Startzustand zu initiieren:
 ```
 dfsrmig /SetGlobalState 0
 ```
 Geben Sie Folgendes ein, um den globalen Migrationsstatus anzuzeigen:
 ```
 dfsrmig /GetGlobalState
 ```
 Dieses Beispiel zeigt eine typische Ausgabe des **DFSRMIG/GetGlobalState** -Befehls.
 ```
 Current DFSR global state: Prepared 
 Succeeded.
 ```
 Geben Sie Folgendes ein, um die Informationen darüber anzuzeigen, ob die lokalen Migrations Zustände auf allen Domänen Controllern mit dem globalen Migrationsstatus und den lokalen Migrations Zuständen für alle Domänen Controller, bei denen der lokale Zustand nicht mit dem globalen Status identisch ist, dem globalen Status entsprechen:
 ```
 dfsrmig /GetMigrationState
 ```
 Dieses Beispiel zeigt eine typische Ausgabe des Befehls **DFSRMIG/GetMigrationState** , wenn die lokalen Migrations Zustände auf allen Domänen Controllern mit dem globalen Migrationsstatus übereinstimmen.
 ```
 All Domain Controllers have migrated successfully to Global state ( Prepared ).
 Migration has reached a consistent state on all Domain Controllers.
 Succeeded.
 ```
 Dieses Beispiel zeigt eine typische Ausgabe des Befehls **DFSRMIG/GetMigrationState** , wenn die lokalen Migrations Zustände auf einigen Domänen Controllern nicht mit dem globalen Migrationsstatus übereinstimmen.
 ```
  The following Domain Controllers are not in sync with Global state ( Prepared ):
  Domain Controller (Local Migration State)  DC type
  =========
  CONTOSO-DC2 ( start )  ReadOnly DC
  CONTOSO-DC3 ( Preparing )  Writable DC
  Migration has not yet reached a consistent state on all domain controllers
  State information might be stale due to AD latency.
 ```
Geben Sie Folgendes ein, um die globalen Objekte und Einstellungen zu erstellen, die von DFS-Replikation in AD DS auf Domänen Controllern verwendet werden, auf denen diese Einstellungen während der Migration nicht automatisch erstellt wurden oder deren Einstellungen fehlen:
```
dfsrmig /createGlobalObjects
```
Geben Sie Folgendes ein, um die globalen AD DS Einstellungen für die FRS-Replikation für einen schreibgeschützten Domänen Controller mit dem Namen "Configuration Manager" zu löschen, wenn diese Einstellungen beim Migrations Vorgang nicht automatisch gelöscht wurden:
```
dfsrmig /deleteRoNtfrsMember contoso-dc2
```
Wenn Sie die globalen AD DS Einstellungen für die FRS-Replikation für alle schreibgeschützten Domänen Controller löschen möchten, wenn diese Einstellungen vom Migrationsprozess nicht automatisch gelöscht wurden, geben Sie Folgendes ein:
```
dfsrmig /deleteRoNtfrsMember
```
Zum Löschen der globalen AD DS Einstellungen für DFS-Replikation für einen schreibgeschützten Domänen Controller mit dem Namen "" "" "" "" "" "".
```
dfsrmig /deleteRoDfsrMember contoso-dc2
```
Geben Sie Folgendes ein, um die globalen AD DS Einstellungen für DFS-Replikation für alle schreibgeschützten Domänen Controller zu löschen, wenn diese Einstellungen vom Migrationsprozess nicht automatisch gelöscht wurden:
```
dfsrmig /deleteRoDfsrMember
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](https://go.microsoft.com/fwlink/?LinkId=122056)

- [SYSVOL-Migrations Reihe: Teil 2 DFSRMIG. exe: das SYSVOL-Migrations Tool](https://go.microsoft.com/fwlink/?LinkID=121757)
