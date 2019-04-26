---
title: Problembehandlung beim Dateiversionsverlauf in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed062945-27e9-4572-b1bb-6c8cf1b9c2f4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 34442565b54b089064c1fa19317a24f591e44fda
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868601"
---
# <a name="troubleshoot-file-history-in-windows-server-essentials"></a>Problembehandlung beim Dateiversionsverlauf in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
## <a name="troubleshoot-issues-with-user-file-history-backups"></a>Problembehandlung bei Sicherungen von Dateiversionsverläufen  
 Beim Verwalten von Sicherungen von Dateiversionsverläufen für einen Benutzer oder Computer, der einem Server mit Windows Server Essentials hinzugefügt wurde, können die folgenden Probleme auftreten.  
  
### <a name="file-history-data-is-not-automatically-deleted"></a>Dateiversionsverlaufs-Daten werden nicht automatisch gelöscht.  
 Die Dateiversionsverlaufs-Daten werden möglicherweise in folgenden Fällen nicht automatisch gelöscht:  
  
-   Wenn Sie ein Benutzerkonto zu löschen, Sie das Benutzerkonto, das s Dateiversionsverlauf-Daten nicht gelöscht werden, und angeben, dass die Daten manuell löschen.  
  
-   Wenn Sie versuchen, die Dateiversionsverlauf-Daten zu löschen, diese aber von einem anderen Prozess verwendet werden.  
  
 Um dieses Problem zu beheben, müssen Sie den Dateiversionsverlauf mit dem folgenden Verfahren manuell löschen:  
  
####  <a name="BKMK_manuallyDelete"></a> Sicherungen von Dateiversionsverläufen für einen Benutzer oder Computer manuell zu löschen  
  
1.  Melden Sie sich am Server als Administrator an.  
  
2.  Führen Sie den Datei-Explorer als Administrator aus.  
  
3.  Navigieren Sie zum Ordner "Sicherungen von Dateiversionsverläufen". Der Standardspeicherort ist "C:\ServerFolders\Sicherungen von Dateiversionsverläufen".  
  
4.  Löschen Sie den freigegebenen Ordner, in dem die Sicherung des Dateiversionsverlaufs gespeichert ist:  
  
    -   Um den Dateiversionsverlauf für einen Benutzer löschen, löschen Sie den Dateiversionsverlauf-Sicherungen von dateiversionsverläufen-Ordner, die den Benutzernamen für die s.  
  
    -   Um den Dateiversionsverlauf eines Computers zu löschen, löschen Sie den Unterordner "Sicherungen von Dateiversionsverläufen", der den Namen des Computers hat. Beispielsweise wenn ein Benutzer außer Kraft gesetzt < Meincomputer01\> nach dem sie arbeiten auf dem neuen Laptop, begann < Meincomputer02\>, würden Sie Sicherungen von Dateiversionsverläufen C:\ServerFolders\File löschen\\< MyAccount\> \\ < Meincomputer01\> mit dem Benutzer zu überprüfen, ob sie alle Dateien und Ordner auf den neuen Laptop übertragen hat und keine Notwendigkeit für den Dateiversionsverlauf in der Zukunft hat.  
  
### <a name="cannot-apply-file-history-setting-to-a-new-user"></a>Die Einstellung "Dateiversionsverlauf" kann nicht auf einen neuen Benutzer angewendet werden  
 Wenn Sie einen neuen Benutzer hinzufügen, dessen Benutzername mit dem Benutzernamen eines Benutzers identisch ist, der aus Windows Server Essentials gelöscht wurde, kann die Konfiguration des Dateiversionsverlaufs für den neuen Benutzer ggf. aufgrund eines Namenskonflikts misslingen, sobald Windows Server Essentials versucht, einen Ordner zum Speichern des Dateiversionsverlaufs des neuen Benutzers zu erstellen. Um dieses Problem zu beheben, können Sie die Ordner mit dem Dateiversionsverlauf des gelöschten Benutzers umbenennen.  
  
##### <a name="to-locate-user-file-history-on-the-server"></a>So finden Sie den Dateiversionsverlauf eines Benutzers auf dem Server  
  
1.  Melden Sie sich am Server als Administrator an.  
  
2.  Klicken Sie im Windows Server Essentials-Dashboard auf **Speicher**.  
  
3.  Notieren Sie sich auf der Registerkarte **Serverordner** den Speicherort des Ordners "Sicherungen von Dateiversionsverläufen". Der Standardspeicherort ist der Sicherungen von Dateiversionsverläufen %SystemDrive%\ServerFolders\File\\.  
  
##### <a name="to-resolve-file-history-issues-for-a-new-user-with-a-name-conflict"></a>So beheben Sie Probleme mit dem Dateiversionsverlauf bei einem neuen Benutzer mit Namenskonflikt  
  
1.  Melden Sie sich am Server als Administrator an.  
  
2.  Führen Sie den Datei-Explorer als Administrator aus.  
  
3.  Navigieren Sie zum Ordner "Sicherungen von Dateiversionsverläufen". Der Standardspeicherort ist "C:\ServerFolders\Sicherungen von Dateiversionsverläufen".  
  
     Der Ordner "Sicherungen von Dateiversionsverläufen" verfügt über einen Unterordner für jedes Benutzerkonto, das Windows Server Essentials hinzugefügt wurde. Der Dateiversionsverlauf des Benutzers Johann Schmitz wird beispielsweise im Unterordner "Sicherungen von Dateiversionsverläufen\JohannSchmitz" gespeichert.  
  
4.  Benennen Sie den Unterordner für den Benutzer, die Sie, z. B. gelöscht  **< *Benutzername*> _gelöscht**. Wenn Sie den Dateiversionsverlauf des Benutzers nicht mehr benötigen, können Sie den Ordner löschen.  
  

5.  Sie können jetzt den neuen Benutzer hinzufügen. Anleitungen hierzu finden Sie unter "Hinzufügen eines Benutzerkontos"? in [Verwalten von Benutzerkonten](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>Ein Benutzerkonto wurde entfernt, aber der Dateiversionsverlauf des Benutzers bleibt erhalten  
 Nach Wunsch kann der Netzwerkadministrator einen Benutzer oder Computer vom Server entfernen, aber den Dateiversionsverlauf für eine künftige Nutzung aufbewahren. Wenn Sie den Dateiversionsverlauf nicht mehr benötigen, entfernen Sie den Ordner "Sicherungen von Dateiversionsverläufen" des Benutzers oder Computers aus freigegebenen Ordnern auf dem Server. Weitere Informationen dazu finden Sie unter [To manually delete File History backups for a user or a computer](Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete).  

5.  Sie können jetzt den neuen Benutzer hinzufügen. Anleitungen hierzu finden Sie unter "Hinzufügen eines Benutzerkontos"? in [Verwalten von Benutzerkonten](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>Ein Benutzerkonto wurde entfernt, aber der Dateiversionsverlauf des Benutzers bleibt erhalten  
 Nach Wunsch kann der Netzwerkadministrator einen Benutzer oder Computer vom Server entfernen, aber den Dateiversionsverlauf für eine künftige Nutzung aufbewahren. Wenn Sie den Dateiversionsverlauf nicht mehr benötigen, entfernen Sie den Ordner "Sicherungen von Dateiversionsverläufen" des Benutzers oder Computers aus freigegebenen Ordnern auf dem Server. Weitere Informationen dazu finden Sie unter [To manually delete File History backups for a user or a computer](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete).  

  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Clientsicherung](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)  
  

-   [Unterstützung für Windows Server Essentials](Support-Windows-Server-Essentials.md)

-   [Unterstützung für Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

