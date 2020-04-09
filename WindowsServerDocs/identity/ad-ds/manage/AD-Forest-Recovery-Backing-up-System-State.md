---
title: 'AD-Gesamtstruktur Wiederherstellung: Sichern eines vollständigen Servers'
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adds
ms.openlocfilehash: 321f927a3efc4f2391daff92ac4c8b7acb47c055
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824282"
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>AD-Gesamtstruktur Wiederherstellung: Sichern der System Statusdaten  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren, um eine Systemstatus Sicherung auf einem DC mithilfe von Windows Server-Sicherung oder Wbadmin. exe auszuführen.  

## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>So führen Sie eine Systemstatus Sicherung mithilfe von Windows Server-Sicherung aus

1. Öffnen Sie **Server-Manager**, **Klicken Sie**auf Extras, und klicken Sie dann auf **Windows Server-Sicherung**.
   - Klicken Sie unter Windows Server 2008 R2 und Windows Server 2008 auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Windows Server-Sicherung**. 

   ![Installieren der Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png)

2. Wenn Sie dazu aufgefordert werden, geben Sie im Dialogfeld **Benutzerkontensteuerung** die Anmelde Informationen für den Sicherungs Operator an, und klicken Sie dann auf **OK**.
3. Klicken Sie auf **lokale Sicherung**.
4. Klicken Sie im Menü **Aktion** auf **Einmal sichern**.
5. Klicken Sie im Assistenten für die einmalige Sicherung auf der Seite **Sicherungs Optionen** auf **verschiedene Optionen**, und klicken Sie dann auf **weiter**.

   ![Installieren der Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. Klicken Sie auf der Seite **Sicherungs Konfiguration auswählen** auf **Benutzer**definiert, und klicken Sie dann auf **weiter**.
7. Klicken Sie auf dem Bildschirm **Elemente für Sicherung auswählen** auf **Elemente hinzufügen** , wählen Sie **System Status** aus, und klicken Sie auf **OK**.
   - Wählen Sie unter Windows Server 2008 R2 und Windows Server 2008 die Volumes aus, die in die Sicherung aufgenommen werden sollen. Wenn Sie das Kontrollkästchen **Systemwiederherstellung aktivieren aktivieren** , werden alle wichtigen Volumes ausgewählt. 

   ![Installieren der Sicherung](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  

8. Klicken Sie auf der Seite **Zieltyp angeben** auf **lokale Laufwerke** oder frei gegebener **Remote Ordner**, und klicken Sie dann auf **weiter**.  Wenn Sie die Sicherung in einem freigegebenen Remote Ordner durchführen, gehen Sie folgendermaßen vor:  
   - Geben Sie den Pfad zum freigegebenen Ordner ein.
   - Wählen Sie unter **Access Control**die Option **nicht erben** oder **erben** aus, um den Zugriff auf die Sicherung zu bestimmen, und klicken Sie dann auf **weiter**.  
   - Geben Sie im Dialogfeld **Benutzer Anmelde Informationen für die Sicherung angeben** den Benutzernamen und das Kennwort für einen Benutzer an, der über Schreibzugriff auf den freigegebenen Ordner verfügt, und klicken Sie dann auf **OK**.

9. Wählen Sie für Windows Server 2008 R2 und Windows Server 2008 auf der Seite **Erweiterte Option angeben die Option** **VSS Kopier Sicherung** aus, und klicken Sie dann auf **weiter**.
10. Wählen Sie auf der Seite **Sicherungs Ziel auswählen** den Speicherort der Sicherung aus.  Wenn Sie lokales Laufwerk ausgewählt haben, wählen Sie ein lokales Laufwerk aus, oder wählen Sie Remote Freigabe eine Netzwerkfreigabe aus.
11. Klicken Sie auf dem Bestätigungsbildschirm auf **Sicherung**.
12. Klicken Sie nach Abschluss des Vorgangs auf **Schließen**.
13. Schließen Sie Windows Server-Sicherung.

## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>So führen Sie eine Systemstatus Sicherung mithilfe von "Wbadmin. exe" aus

Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie den folgenden Befehl ein, und drücken Sie Eingabe  
  
   ```
   wbadmin start systemstatebackup -backuptarget:<targetDrive>:
   ```

   ![Installieren der Sicherung](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
