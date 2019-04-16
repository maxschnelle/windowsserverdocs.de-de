---
title: "Wiederherstellung des AD-Gesamtstruktur - einen vollständigen Server sichern"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adfs
ms.openlocfilehash: a86d61536f8b426e1a5258c661d4e53da63d4162
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>AD-Gesamtstruktur Recovery - Sicherung der Systemstatusdaten  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2
 
Verwenden Sie das folgende Verfahren zum Ausführen einer Sicherung des Systemstatus auf einem Domänencontroller mit Windows Server-Sicherung oder wbadmin.exe.  
  
## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>Um eine Sicherung des Systemstatus mithilfe von Windows Server-Sicherung  
1. Öffnen **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Windows Server-Sicherung**.
    - Klicken Sie in Windows Server2008 R2 und Windows Server2008, auf **starten**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Windows Server-Sicherung**. 
![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 
2. Wenn Sie, in aufgefordert werden der **User Account Control** Dialogfeld Sicherungsoperatoren Anmeldeinformationen, und klicken Sie dann auf **OK**.
3. Klicken Sie auf **lokale Sicherung**.
4. Auf der **Aktion** Menü klicken Sie auf **Einmalsicherung**.
5. Im Assistent für die Einmalsicherung auf die **Sicherungsoptionen** auf **unterschiedliche Optionen**, und klicken Sie dann auf **Weiter**.
![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)
6. Auf der **wählen Sicherungskonfiguration** auf **benutzerdefinierte)**, und klicken Sie dann auf **Weiter**.
7. Auf der **Elemente für Sicherung auswählen** auf **Add Items**, und wählen Sie **Systemstatus**, und klicken Sie auf **Ok**.
    - Wählen Sie in Windows Server2008 R2 und Windows Server2008 Volumes in die Sicherung einschließen. Bei Auswahl der **Aktivieren der Wiederherstellung des Systems** Kontrollkästchen, alle wichtigen Volumes ausgewählt sind. 
![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  
8. Auf der **Zieltyp angeben** auf **lokale Laufwerke** oder **freigegebenen Remoteordner**, und klicken Sie dann auf **Weiter**.  Wenn Sie sich in einem freigegebenen Remoteordner sichern möchten, führen Sie folgende Schritteaus:  
  
 1.  Geben Sie den Pfad zum freigegebenen Ordner.  
 2.  Unter **Access Control**Option **erben keine** oder **erben** bestimmen den Zugriff auf die Sicherung, und klicken Sie auf **Weiter**.  
 3.  In der **Geben Sie Anmeldeinformationen für die Sicherung** Dialogfeld Geben Sie den Benutzernamen und das Kennwort für einen Benutzer, der Schreibzugriff auf den freigegebenen Ordner verfügt, und klicken Sie dann auf **OK**.
9. Für Windows Server2008 R2 und Windows Server2008 auf die **angeben, die erweiterte Option** Seite **VSS-Sicherung**, und klicken Sie dann auf **Weiter**.
10. Auf der **Sicherungsziel auswählen** Seite, und wählen Sie den Sicherungsspeicherort an.  Bei Auswahl von lokalen Laufwerk ein lokales Laufwerk auszuwählen, oder bei Auswahl von remote eine Netzwerkfreigabe auswählen.
11. Klicken Sie auf dem Bestätigungsbildschirm auf **Sicherung**.
12. Sobald dies abgeschlossen ist Klicken Sie auf **schließen**.
13. Schließen Sie Windows Server-Sicherung.

  
## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>Um eine Sicherung des Systemstatus mithilfe von Wbadmin.exe  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, geben Sie folgenden Befehl ein, und drücken Sie die EINGABETASTE:  
  
    ```  
    wbadmin start systemstatebackup -backuptarget:<targetDrive>:
    ```  
![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
