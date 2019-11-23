---
title: 'AD-Gesamtstruktur Wiederherstellung: Sichern eines vollständigen Servers'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: 4377c1d993b4f6d30cf8ca8a7d149b741d7f8d2f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369361"
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>AD-Gesamtstruktur Wiederherstellung: Sichern eines vollständigen Servers  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Eine vollständige Server Sicherung wird empfohlen, um eine Wiederherstellung der Gesamtstruktur vorzubereiten, da Sie auf einer anderen Hardware oder einer anderen Betriebssystem Instanz wieder hergestellt werden kann.  Mithilfe Windows Server-Sicherung können Sie eine vollständige Sicherung des Servers ausführen. 

## <a name="windows-server-backup"></a>Windows Server-Sicherung

Windows Server-Sicherung wird nicht standardmäßig installiert. In Windows Server 2016 und Windows Server 2012 R2 installieren Sie es, indem Sie die folgenden Schritte ausführen.

>[!NOTE]
>Beachten Sie, dass die Schritte zwischen Windows Server 2016 und Windows Server 2012 R2 möglicherweise geringfügig abweichen.

Schritte zur Installation in Windows Server 2008 und Windows Server 2008 R2 finden Sie unter [Installieren von Windows Server-Sicherung](https://technet.microsoft.com/library/cc771232.aspx).  

### <a name="to-install-windows-server-backup"></a>So installieren Sie Windows Server-Sicherung

1. Öffnen Sie **Server-Manager** , und klicken Sie auf **Rollen und Features hinzufügen**.
2. Klicken Sie im **Assistenten zum Hinzufügen von Rollen und Features** auf **weiter**.
3. Belassen Sie auf dem Bildschirm **Installationstyp** die Standard **rollenbasierte oder featurebasierte Installation** , und klicken Sie auf **weiter**.
4. Klicken Sie auf dem Bildschirm **Server Auswahl** auf **weiter**.
5. Klicken Sie auf dem Bildschirm **Server Rollen** auf **weiter**.
6. Wählen Sie auf dem Bildschirm **Features** die Option **Windows Server-Sicherung** aus, und klicken Sie auf **weiter**
   ![Sicherung installieren](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup2.png)
7. Klicken Sie auf **Installieren**.
8. Klicken Sie nach Abschluss der Installation auf **Schließen**.

### <a name="to-perform-a-backup-with-windows-server-backup"></a>So führen Sie eine Sicherung mit Windows Server-Sicherung aus

1. Öffnen Sie **Server-Manager**, **Klicken Sie**auf Extras, und klicken Sie dann auf **Windows Server-Sicherung**.
   - Klicken Sie unter Windows Server 2008 R2 und Windows Server 2008 auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Windows Server-Sicherung**.

   ![Installieren der Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 

2. Wenn Sie dazu aufgefordert werden, geben Sie im Dialogfeld **Benutzerkontensteuerung** die Anmelde Informationen für den Sicherungs Operator an, und klicken Sie dann auf **OK**.
3. Klicken Sie auf **lokale Sicherung**.
4. Klicken Sie im Menü **Aktion** auf **Einmal sichern**.
5. Klicken Sie im Assistenten für die einmalige Sicherung auf der Seite **Sicherungs Optionen** auf **verschiedene Optionen**, und klicken Sie dann auf **weiter**.

   ![Installieren der Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. Klicken Sie auf der Seite **Sicherungs Konfiguration auswählen** auf **vollständiger Server (empfohlen)** , und klicken Sie dann auf **weiter**.
7. Klicken Sie auf der Seite **Zieltyp angeben** auf **lokale Laufwerke** oder frei gegebener **Remote Ordner**, und klicken Sie dann auf **weiter**.
8. Wählen Sie auf der Seite **Sicherungs Ziel auswählen** den Speicherort der Sicherung aus.  Wenn Sie lokales Laufwerk ausgewählt haben, wählen Sie ein lokales Laufwerk aus, oder wählen Sie Remote Freigabe eine Netzwerkfreigabe aus.
9. Klicken Sie auf dem Bestätigungsbildschirm auf **Sicherung**.

   ![Installieren der Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)

10. Klicken Sie nach Abschluss des Vorgangs auf **Schließen**.
11. Schließen Sie Windows Server-Sicherung.

>[!NOTE]
>Wenn Sie eine Fehlermeldung erhalten, dass kein Sicherungs Speicherort verfügbar ist, müssen Sie entweder eines der ausgewählten Volumes ausschließen oder ein neues Volume oder eine Remote Freigabe hinzufügen.
>Wenn eine Warnung angezeigt wird, die besagt, dass das ausgewählte Volume auch in der Liste der zu sichernden Elemente enthalten ist, legen Sie fest, ob Sie entfernt werden sollen, und klicken Sie auf **OK**.

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Verwenden von "Wbadmin. exe" zum Sichern eines Windows-Servers

Wbadmin. exe ist ein Befehlszeilenprogramm, mit dem Sie das Betriebssystem, die Volumes, Dateien, Ordner und Anwendungen über eine Eingabeaufforderung sichern und wiederherstellen können.

### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>So führen Sie eine vollständige Server Sicherung mithilfe von "Wbadmin. exe" aus
  
- Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie den folgenden Befehl ein, und drücken Sie Eingabe  

   ```
   wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:
   ```

   ![Installieren der Sicherung](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
