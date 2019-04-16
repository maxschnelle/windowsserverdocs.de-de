---
title: "Wiederherstellung des AD-Gesamtstruktur - einen vollständigen Server sichern"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adfs
ms.openlocfilehash: b1af97c2eb23d65c2d106906bc0f5bb1f10b23ec
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>Wiederherstellung des AD-Gesamtstruktur - einen vollständigen Server sichern  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

Eine vollständige Sicherung wird empfohlen, um für eine Wiederherstellung der Gesamtstruktur vorzubereiten, da sie für unterschiedliche Hardware oder ein anderes Betriebssystem-Instanz wiederhergestellt werden kann.  Windows Server-Sicherung können Sie eine vollständige Sicherung des Servers ausführen. 

## <a name="windows-server-backup"></a>Windows Server-Sicherung
Windows Server-Sicherung ist nicht standardmäßig installiert. Installieren Sie in Windows Server2016 und Windows Server2012 R2 es anhand der folgenden Schritteaus.

>[!NOTE]
>Bitte beachten Sie, dass die Schritteetwas zwischen Windows Server2016 und Windows Server2012 R2 variieren können.

So installieren Sie es in Windows Server2008 und Windows Server2008 R2 finden Sie unter [Installieren von Windows Server-Sicherung](https://technet.microsoft.com/library/cc771232.aspx).  

### <a name="to-install-windows-server-backup"></a>So installieren Sie Windows Server-Sicherung
1. Öffnen **Server-Manager**, und klicken Sie auf **Hinzufügen von Rollen und Features**.
2. Auf der **Hinzufügen von Rollen und Features Assistenten** klicken Sie auf **Weiter**.
3. Auf der **Installationstyp** Bildschirm, behalten Sie den Standardwert **rollenbasierte oder featurebasierte Installation**, und klicken Sie auf **Weiter**.
4. Auf der **Serverauswahl** auf **Weiter**.
5. Auf der **Serverrollen** Bildschirm auf **Weiter**.
6. Auf der **Features** wählen **Windows Server-Sicherung**, und klicken Sie auf **Weiter**<ph x="4">
! [</ph> Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup2.png)
7. Klicken Sie auf **installieren**.
8. Nachdem die Installation abgeschlossen ist, klicken Sie auf **schließen**.


### <a name="to-perform-a-backup-with-windows-server-backup"></a>Zum Ausführen einer Sicherung mit Windows Server-Sicherung

1. Öffnen **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie dann auf **Windows Server-Sicherung**.
    - Klicken Sie in Windows Server2008 R2 und Windows Server2008, auf **starten**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Windows Server-Sicherung**. 
![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 
2. Wenn Sie, in aufgefordert werden der **User Account Control** Dialogfeld Sicherungsoperatoren Anmeldeinformationen, und klicken Sie dann auf **OK**.
3. Klicken Sie auf **lokale Sicherung**.
4. Auf der **Aktion** Menü klicken Sie auf **Einmalsicherung**.
5. Im Assistent für die Einmalsicherung auf die **Sicherungsoptionen** auf **unterschiedliche Optionen**, und klicken Sie dann auf **Weiter**.
![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)
6. Auf der **wählen Sicherungskonfiguration** auf **vollständiger Server (empfohlen)**, und klicken Sie dann auf **Weiter**.
7. Auf der **Zieltyp angeben** auf **lokale Laufwerke** oder **freigegebenen Remoteordner**, und klicken Sie dann auf **Weiter**.
8. Auf der **Sicherungsziel auswählen** Seite, und wählen Sie den Sicherungsspeicherort an.  Bei Auswahl von lokalen Laufwerk ein lokales Laufwerk auszuwählen, oder bei Auswahl von remote eine Netzwerkfreigabe auswählen.
9. Klicken Sie auf dem Bestätigungsbildschirm auf **Sicherung**.
![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)
10. Sobald dies abgeschlossen ist Klicken Sie auf **schließen**.
11. Schließen Sie Windows Server-Sicherung.

>[!NOTE]
>Wenn Sie die Fehlermeldung besagt, dass keine Sicherungsspeicherort verfügbar ist, müssen Sie zum Ausschließen eines der Volumes, die ausgewählt wurde, oder fügen ein neues Volume oder einer Remotefreigabe.
>Wenn Sie eine Warnung an, die besagt erhalten, dass das ausgewählte Volume auch in der Liste der zu sichernden Elemente enthalten ist, bestimmen, ob entfernen, und klicken Sie auf **Ok**.

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Verwendung von Wbadmin.exe zum Sichern von Windows Server
Wbadmin.exe ist ein Befehlszeilenprogramm, mit dem Sie sichern und Wiederherstellen von Ihrem Betriebssystem, Volumes, Dateien, Ordner und Anwendungen von einer Befehlszeile aus.

#### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>Zum Ausführen einer vollständigen Sicherung mit Wbadmin.exe  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, geben Sie folgenden Befehl ein, und drücken Sie die EINGABETASTE:  

        wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:

![Installieren Sie die Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
