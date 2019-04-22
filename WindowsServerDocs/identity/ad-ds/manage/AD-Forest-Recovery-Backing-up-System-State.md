---
title: 'AD-Gesamtstruktur-Wiederherstellung: einen vollständigen Server sichern'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adds
ms.openlocfilehash: a5306960bb2dca3849bdb4fc7304781af3f25335
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815871"
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>Wiederherstellung der Active Directory-Gesamtstruktur - Sicherung der Systemstatusdaten  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren, um eine Sicherung des Systemstatus auf einem Domänencontroller ausführen, mithilfe von Windows Server-Sicherung oder wbadmin.exe.  

## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>Zum Ausführen einer systemstatussicherung mithilfe von Windows Server-Sicherung

1. Open **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Windows Server-Sicherung**.
   - Klicken Sie in Windows Server 2008 R2 und Windows Server 2008, auf **starten**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Windows Server-Sicherung**. 

   ![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png)

2. Wenn Sie, in aufgefordert werden der **User Account Control** im Dialogfeld Anmeldeinformationen für die Sicherungs-Operator, und klicken Sie dann auf **OK**.
3. Klicken Sie auf **lokale Sicherung**.
4. Klicken Sie im Menü **Aktion** auf **Einmal sichern**.
5. Im Assistenten für die Einmalsicherung auf die **Sicherungsoptionen** auf **Möglichkeiten**, und klicken Sie dann auf **Weiter**.

   ![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. Auf der **wählen Sicherungskonfiguration** auf **benutzerdefinierte)**, und klicken Sie dann auf **Weiter**.
7. Auf der **Elemente für Sicherung auswählen** auf **Elemente hinzufügen** , und wählen Sie **Systemstatus** , und klicken Sie auf **Ok**.
   - Wählen Sie in Windows Server 2008 R2 und Windows Server 2008 die Volumes in die Sicherung eingeschlossen werden sollen. Bei Auswahl der **Aktivieren der Wiederherstellung des Systems** Kontrollkästchen alle wichtigen Volumes ausgewählt werden. 

   ![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  

8. Auf der **Zieltyp angeben** auf **lokale Laufwerke** oder **freigegebener Remoteordner**, und klicken Sie dann auf **Weiter**.  Wenn Sie auf einem freigegebenen Remoteordner sichern, führen Sie folgende Schritte aus:  
   - Geben Sie den Pfad zum freigegebenen Ordner.
   - Klicken Sie unter **Zugriffssteuerung**Option **erben keine** oder **erben** steuern den Zugriff auf die Sicherung aus, und klicken Sie dann auf **Weiter**.  
   - In der **Benutzeranmeldeinformationen für die Sicherung** Dialogfeld Geben Sie den Benutzernamen und das Kennwort für einen Benutzer, die Schreibzugriff auf den freigegebenen Ordner verfügt, und klicken Sie dann auf **OK**.

9. Für Windows Server 2008 R2 und Windows Server 2008 auf die **Geben Sie erweiterte Optionen** Seite **VSS kopiesicherung** , und klicken Sie dann auf **Weiter**.
10. Auf der **Sicherungsziel auswählen** Seite, und wählen Sie den Sicherungsspeicherort.  Bei Auswahl der lokalen Laufwerk ein lokales Laufwerk auswählen, oder bei Auswahl der remote eine Netzwerkfreigabe auswählen.
11. Klicken Sie auf dem Bestätigungsbildschirm **Sicherung**.
12. Sobald dies abgeschlossen ist, klicken Sie auf **schließen**.
13. Schließen Sie Windows Server-Sicherung.

## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>Zum Ausführen einer Sicherung des Systemstatus mithilfe von Wbadmin.exe

Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie den folgenden Befehl aus, und drücken Sie die EINGABETASTE:  
  
   ```
   wbadmin start systemstatebackup -backuptarget:<targetDrive>:
   ```

   ![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
