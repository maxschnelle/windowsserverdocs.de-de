---
title: Problembehandlung beim Dateiversionsverlauf in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: ed062945-27e9-4572-b1bb-6c8cf1b9c2f4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 51043013320a3fc6faeb9342ac93c010c859bae5
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470175"
---
# <a name="troubleshoot-file-history-in-windows-server-essentials"></a>Problembehandlung beim Dateiversionsverlauf in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

## <a name="troubleshoot-issues-with-user-file-history-backups"></a>Problembehandlung bei Sicherungen von Dateiversionsverläufen
 Beim Verwalten von Sicherungen von Dateiversionsverläufen für einen Benutzer oder Computer, der einem Server mit Windows Server Essentials hinzugefügt wurde, können die folgenden Probleme auftreten.

### <a name="file-history-data-is-not-automatically-deleted"></a>Dateiversionsverlaufs-Daten werden nicht automatisch gelöscht.
 Die Dateiversionsverlaufs-Daten werden möglicherweise in folgenden Fällen nicht automatisch gelöscht:

- Beim Löschen eines Benutzerkontos haben Sie die Möglichkeit, die Datei Versionsverlauf-Daten des Benutzerkontos nicht zu löschen und die Daten manuell zu löschen.

- Wenn Sie versuchen, die Dateiversionsverlauf-Daten zu löschen, diese aber von einem anderen Prozess verwendet werden.

  Um dieses Problem zu beheben, müssen Sie den Dateiversionsverlauf mit dem folgenden Verfahren manuell löschen:

####  <a name="to-manually-delete-file-history-backups-for-a-user-or-a-computer"></a><a name="BKMK_manuallyDelete"></a>So löschen Sie Sicherungen von Datei Versions Verläufen für einen Benutzer oder Computer manuell

1.  Melden Sie sich beim Server als Administrator an.

2.  Führen Sie den Datei-Explorer als Administrator aus.

3.  Navigieren Sie zum Ordner "Sicherungen von Dateiversionsverläufen". Der Standardspeicherort ist "C:\ServerFolders\Sicherungen von Dateiversionsverläufen".

4.  Löschen Sie den freigegebenen Ordner, in dem die Sicherung des Dateiversionsverlaufs gespeichert ist:

    -   Um den Datei Versionsverlauf eines Benutzers zu löschen, löschen Sie den untergeordneten Ordner für die Datei Versions Verlaufs Sicherung mit dem Namen des Benutzers.

    -   Um den Dateiversionsverlauf eines Computers zu löschen, löschen Sie den Unterordner "Sicherungen von Dateiversionsverläufen", der den Namen des Computers hat. Wenn ein Benutzer beispielsweise <meincomputer01 \> nach der Arbeit mit dem neuen Laptop <meincomputer02 gelöscht hat, \> Löschen Sie c:\serverfolders\dateiverlaufsicherungen \\<MyAccount \> \\<meincomputer01, \> nachdem Sie mit dem Benutzer überprüft haben, dass er alle Dateien und Ordner auf den neuen Laptop übertragen hat und in Zukunft nicht mehr benötigt wird.

### <a name="cannot-apply-file-history-setting-to-a-new-user"></a>Die Einstellung "Dateiversionsverlauf" kann nicht auf einen neuen Benutzer angewendet werden
 Wenn Sie einen neuen Benutzer hinzufügen, dessen Benutzername mit dem Benutzernamen eines Benutzers identisch ist, der aus Windows Server Essentials gelöscht wurde, kann die Konfiguration des Dateiversionsverlaufs für den neuen Benutzer ggf. aufgrund eines Namenskonflikts misslingen, sobald Windows Server Essentials versucht, einen Ordner zum Speichern des Dateiversionsverlaufs des neuen Benutzers zu erstellen. Um dieses Problem zu beheben, können Sie die Ordner mit dem Dateiversionsverlauf des gelöschten Benutzers umbenennen.

##### <a name="to-locate-user-file-history-on-the-server"></a>So finden Sie den Dateiversionsverlauf eines Benutzers auf dem Server

1.  Melden Sie sich beim Server als Administrator an.

2.  Klicken Sie im Windows Server Essentials-Dashboard auf **Speicher**.

3.  Notieren Sie sich auf der Registerkarte **Serverordner** den Speicherort des Ordners "Sicherungen von Dateiversionsverläufen". Der Standard Speicherort ist "%SystemDrive%\serverfolders\file History Backups" \\ .

##### <a name="to-resolve-file-history-issues-for-a-new-user-with-a-name-conflict"></a>So beheben Sie Probleme mit dem Dateiversionsverlauf bei einem neuen Benutzer mit Namenskonflikt

1.  Melden Sie sich beim Server als Administrator an.

2.  Führen Sie den Datei-Explorer als Administrator aus.

3.  Navigieren Sie zum Ordner "Sicherungen von Dateiversionsverläufen". Der Standardspeicherort ist "C:\ServerFolders\Sicherungen von Dateiversionsverläufen".

     Der Ordner "Sicherungen von Dateiversionsverläufen" verfügt über einen Unterordner für jedes Benutzerkonto, das Windows Server Essentials hinzugefügt wurde. Der Dateiversionsverlauf des Benutzers Johann Schmitz wird beispielsweise im Unterordner "Sicherungen von Dateiversionsverläufen\JohannSchmitz" gespeichert.

4.  Benennen Sie den Unterordner für den Benutzer um, den Sie gelöscht haben, z. b. ** < *username*>_Deleted**. Wenn Sie den Dateiversionsverlauf des Benutzers nicht mehr benötigen, können Sie den Ordner löschen.

5. Sie können jetzt den neuen Benutzer hinzufügen. Anweisungen finden Sie unter Hinzufügen eines Benutzerkontos. unter [Verwalten von Benutzerkonten](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md).

### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>Ein Benutzerkonto wurde entfernt, aber der Dateiversionsverlauf des Benutzers bleibt erhalten
 Nach Wunsch kann der Netzwerkadministrator einen Benutzer oder Computer vom Server entfernen, aber den Dateiversionsverlauf für eine künftige Nutzung aufbewahren. Wenn Sie den Dateiversionsverlauf nicht mehr benötigen, entfernen Sie den Ordner "Sicherungen von Dateiversionsverläufen" des Benutzers oder Computers aus freigegebenen Ordnern auf dem Server. Weitere Informationen dazu finden Sie unter [To manually delete File History backups for a user or a computer](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete).


## <a name="see-also"></a>Siehe auch

-   [Verwalten der Clientsicherung](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)

-   [Unterstützung von Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

