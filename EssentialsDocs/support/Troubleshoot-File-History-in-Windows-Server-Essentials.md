---
title: Problembehandlung beim Dateiversionsverlauf in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="troubleshoot-file-history-in-windows-server-essentials"></a>Problembehandlung beim Dateiversionsverlauf in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials 
  
## <a name="troubleshoot-issues-with-user-file-history-backups"></a>Behandeln von Problemen mit dateiversionsverläufen  
 Die folgenden Probleme können auftreten, bei der Verwaltung von dateiversionsverläufen für einen Benutzer oder Computer, der mit einem Server unter Windows Server Essentials hinzugefügt wurde.  
  
### <a name="file-history-data-is-not-automatically-deleted"></a>Dateiversionsverlaufs-Daten werden nicht automatisch gelöscht.  
 Die Dateiversionsverlauf-Daten möglicherweise nicht automatisch gelöscht:  
  
-   Beim Löschen eines Benutzerkontos festlegen, dass das Benutzerkonto s Dateiversionsverlauf-Daten nicht gelöscht, und entscheiden, löschen Sie die Daten manuell aus.  
  
-   Wenn Sie versuchen, die Dateiversionsverlauf-Daten zu löschen, werden die Dateiversionsverlauf-Daten von anderen Prozess verwendet.  
  
 Um dieses Problem zu beheben, müssen Sie den Dateiversionsverlauf mit dem folgenden Verfahren manuell löschen:  
  
####  <a name="BKMK_manuallyDelete"></a>So löschen Sie Sicherungen des Dateiversionsverlaufs für einen Benutzer oder Computer manuell  
  
1.  Melden Sie sich an den Server als Administrator an.  
  
2.  Datei-Explorer als Administrator ausführen.  
  
3.  Navigieren Sie zum Ordner "Sicherungen von Dateiversionsverläufen". Der Standardspeicherort ist C:\ServerFolders\File Sicherungen.  
  
4.  Löschen Sie den freigegebenen Ordner, in der Sicherung des Dateiversionsverlaufs gespeichert:  
  
    -   Um den Dateiversionsverlauf eines Benutzers zu löschen, löschen Sie den Unterordner "Sicherungen von dateiversionsverläufen", der den Benutzernamen des s verfügt.  
  
    -   Um den Dateiversionsverlauf für einen Computer zu löschen, löschen Sie den Unterordner "Sicherungen von dateiversionsverläufen", der Namen des Computers hat. Beispielsweise, wenn ein Benutzer < MyComputer01\ > eingestellt, nach dem sie den neuen Laptop < MyComputer02\ >, funktioniert begonnener Sie würde Löschen C:\ServerFolders\File Verlauf Backups\\ < MyAccount\ > \\ < MyComputer01\ >, nachdem Sie mit dem Benutzer stellen Sie sicher, dass sie alle Dateien und Ordner auf ihren neuen Laptop übertragen wurde und keine Notwendigkeit für den Dateiversionsverlauf in der Zukunft.  
  
### <a name="cannot-apply-file-history-setting-to-a-new-user"></a>Einstellung "Dateiversionsverlauf" kann nicht auf einen neuen Benutzer angewendet werden.  
 Wenn Sie einen neuen Benutzer hinzufügen, dessen Benutzername mit den Benutzernamen eines Benutzers identisch ist, der von Windows Server Essentials gelöscht wurde, kann die Konfiguration des Dateiversionsverlaufs für den neuen Benutzer aufgrund eines Namenskonflikts fehlschlagen, wenn Windows Server Essentials versucht, einen Ordner zum Speichern des dateiversionsverlaufs des neuen Benutzers zu erstellen. Um dieses Problem zu beheben, können Sie den Ordner Dateiversionsverlauf des gelöschten Benutzers umbenennen.  
  
##### <a name="to-locate-user-file-history-on-the-server"></a>Verlauf – Benutzer Datei auf dem Server suchen  
  
1.  Melden Sie sich an den Server als Administrator an.  
  
2.  Klicken Sie auf dem Windows Server Essentials-Dashboard auf **Speicher**.  
  
3.  Auf der **Serverordner** Registerkarte, notieren Sie den Speicherort des Ordners "Sicherungen von Dateiversionsverläufen". Der Standardspeicherort ist %SystemDrive%\ServerFolders\File Verlauf Backups\\.  
  
##### <a name="to-resolve-file-history-issues-for-a-new-user-with-a-name-conflict"></a>Beheben von Problemen mit dem Dateiversionsverlauf für einen neuen Benutzer mit Namenskonflikt  
  
1.  Melden Sie sich an den Server als Administrator an.  
  
2.  Datei-Explorer als Administrator ausführen.  
  
3.  Navigieren Sie zum Ordner "Sicherungen von Dateiversionsverläufen". Der Standardspeicherort ist C:\ServerFolders\File Sicherungen.  
  
     Ordner "Sicherungen von Dateiversionsverläufen" verfügt über einen Unterordner für jedes Benutzerkonto, das mit Windows Server Essentials hinzugefügt wurde. Der Dateiversionsverlauf des Benutzers John Smith würde z.B. in den Unterordner Dateiversionsverlauf Backups\JohnSmith gespeichert werden.  
  
4.  Benennen Sie den Unterordner für den Benutzer, die Sie, z.B. gelöscht **<*Benutzername*> _gelöscht **. Wenn Sie Dateiversionsverlauf des Benutzers nicht mehr benötigen, können Sie den Ordner löschen.  
  

5.  Sie können jetzt den neuen Benutzer hinzufügen. Anweisungen finden Sie unter Hinzufügen eines Benutzerkontos? in [Manage User Accounts](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>Ein Benutzerkonto wurde entfernt, aber der Dateiversionsverlauf des Benutzers bleibt  
 In einigen Fällen können der Netzwerkadministrator einen Benutzer oder Computer vom Server entfernen, aber den Dateiversionsverlauf Sicherung für die zukünftige Verwendung beibehalten. Wenn Sie den Dateiversionsverlauf nicht mehr benötigen, entfernen Sie den Ordner "Sicherungen von Dateiversionsverläufen" für den Benutzer oder den Computer aus freigegebenen Ordnern auf dem Server. Informationen hierzu finden Sie unter [dateiversionsverläufen für einen Benutzer oder Computer manuell löschen](Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete).  

5.  Sie können jetzt den neuen Benutzer hinzufügen. Anweisungen finden Sie unter Hinzufügen eines Benutzerkontos? in [Manage User Accounts](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>Ein Benutzerkonto wurde entfernt, aber der Dateiversionsverlauf des Benutzers bleibt  
 In einigen Fällen können der Netzwerkadministrator einen Benutzer oder Computer vom Server entfernen, aber den Dateiversionsverlauf Sicherung für die zukünftige Verwendung beibehalten. Wenn Sie den Dateiversionsverlauf nicht mehr benötigen, entfernen Sie den Ordner "Sicherungen von Dateiversionsverläufen" für den Benutzer oder den Computer aus freigegebenen Ordnern auf dem Server. Informationen hierzu finden Sie unter [dateiversionsverläufen für einen Benutzer oder Computer manuell löschen](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete).  

  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Clientsicherung](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)  
  

-   [Unterstützung für Windows Server Essentials](Support-Windows-Server-Essentials.md)

-   [Unterstützung für Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

