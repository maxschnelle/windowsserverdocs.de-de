---
title: 'AD-Gesamtstruktur-Wiederherstellung: einen vollständigen Server sichern'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: fec8de8ea1dadb392f6a3bd1c881e8df2266f404
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846521"
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>AD-Gesamtstruktur-Wiederherstellung: einen vollständigen Server sichern  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Eine vollständige serversicherung wird empfohlen, um für eine Wiederherstellung der Gesamtstruktur vorzubereiten, da sie für unterschiedliche Hardware- oder ein anderes Betriebssystem-Instanz wiederhergestellt werden kann.  Mithilfe von Windows Server-Sicherung können Sie eine vollständige Sicherung des Servers ausführen. 

## <a name="windows-server-backup"></a>Windows Server-Sicherung

Windows Server-Sicherung ist nicht standardmäßig installiert. Installieren Sie in Windows Server 2016 und Windows Server 2012 R2 es über die folgenden Schritte aus.

>[!NOTE]
>Bedenken Sie bitte die Schritte leicht zwischen Windows Server 2016 und Windows Server 2012 R2 variieren.

Schritte zur Installation in Windows Server 2008 und Windows Server 2008 R2, finden Sie unter [Installieren von Windows Server-Sicherung](https://technet.microsoft.com/library/cc771232.aspx).  

### <a name="to-install-windows-server-backup"></a>So installieren Sie Windows Server-Sicherung

1. Open **Server-Manager** , und klicken Sie auf **Rollen und Features hinzufügen**.
2. Auf der **Hinzufügen von Rollen und Features Assistenten** klicken Sie auf **Weiter**.
3. Auf der **Installationstyp** Bildschirm, übernehmen Sie den Standardwert **rollenbasierte oder featurebasierte Installation** , und klicken Sie auf **Weiter**.
4. Auf der **Serverauswahl** auf **Weiter**.
5. Auf der **Serverrollen** Bildschirm auf **Weiter**.
6. Auf der **Features** auf **Windows Server-Sicherung** , und klicken Sie auf **Weiter**
   ![Sicherung installieren](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup2.png)
7. Klicken Sie auf **Installieren**.
8. Nachdem die Installation abgeschlossen ist, klicken Sie auf **schließen**.

### <a name="to-perform-a-backup-with-windows-server-backup"></a>Zum Ausführen einer Sicherung mit Windows Server-Sicherung

1. Open **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Windows Server-Sicherung**.
   - Klicken Sie in Windows Server 2008 R2 und Windows Server 2008, auf **starten**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Windows Server-Sicherung**.

   ![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 

2. Wenn Sie, in aufgefordert werden der **User Account Control** im Dialogfeld Anmeldeinformationen für die Sicherungs-Operator, und klicken Sie dann auf **OK**.
3. Klicken Sie auf **lokale Sicherung**.
4. Klicken Sie im Menü **Aktion** auf **Einmal sichern**.
5. Im Assistenten für die Einmalsicherung auf die **Sicherungsoptionen** auf **Möglichkeiten**, und klicken Sie dann auf **Weiter**.

   ![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. Auf der **wählen Sicherungskonfiguration** auf **vollständiger Server (empfohlen)**, und klicken Sie dann auf **Weiter**.
7. Auf der **Zieltyp angeben** auf **lokale Laufwerke** oder **freigegebener Remoteordner**, und klicken Sie dann auf **Weiter**.
8. Auf der **Sicherungsziel auswählen** Seite, und wählen Sie den Sicherungsspeicherort.  Bei Auswahl der lokalen Laufwerk ein lokales Laufwerk auswählen, oder bei Auswahl der remote eine Netzwerkfreigabe auswählen.
9. Klicken Sie auf dem Bestätigungsbildschirm **Sicherung**.

   ![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)

10. Sobald dies abgeschlossen ist, klicken Sie auf **schließen**.
11. Schließen Sie Windows Server-Sicherung.

>[!NOTE]
>Wenn Sie eine Fehlermeldung erhalten, dass keine Sicherungsspeicherort verfügbar ist, müssen Sie zum Ausschließen eines der Volumes, das ausgewählt wurde, oder fügen ein neues Volume oder eine remote-Freigabe.
>Wenn Sie eine Warnung an, die besagt erhalten, dass das ausgewählte Volume auch in der Liste der zu sichernden Elemente enthalten ist, ermitteln, ob entfernen, und klicken Sie auf **Ok**.

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Verwenden von Wbadmin.exe zum Sichern von WindowsServer

Wbadmin.exe ist ein Befehlszeilen-Hilfsprogramm, mit der Sie zum Sichern und Wiederherstellen von Ihrem Betriebssystem, Volumes, Dateien, Ordner und Anwendungen über eine Eingabeaufforderung.

### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>Zum Ausführen einer vollständigen serversicherung, die mithilfe von Wbadmin.exe
  
- Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie den folgenden Befehl aus, und drücken Sie die EINGABETASTE:  

   ```
   wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:
   ```

   ![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
