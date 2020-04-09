---
title: Einrichten oder Anpassen der Serversicherung
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 441c2d6c-435a-42cb-90f2-6d680d279d34
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 364ba61d42fcb2ae5bc4f91a71083b880eb36ab8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852623"
---
# <a name="set-up-or-customize-server-backup"></a>Einrichten oder Anpassen der Serversicherung

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 Die Serversicherung wird während der Installation nicht automatisch konfiguriert. Sie sollten den Server und dessen Daten automatisch schützen, indem Sie tägliche Sicherungen planen. Es wird empfohlen, einen täglichen Sicherungsplan zu verwalten, da die meisten Organisationen es sich nicht leisten können, die im Verlauf von mehreren Tagen erstellten Daten zu verlieren.  
  
 Die folgenden Abschnitte enthalten Informationen zum Einrichten oder Anpassen der Serversicherung:  
  
-   [Einrichten oder Ändern von Einstellungen für die Server Sicherung](Set-up-or-customize-server-backup.md#BKMK_1)&reg;
  
-   [Zeitplan für die Server Sicherung](Set-up-or-customize-server-backup.md#BKMK_2)  
  
-   [Sicherungs Ziellaufwerk](Set-up-or-customize-server-backup.md#BKMK_Target)  
  
-   [Zu sichernde Elemente](Set-up-or-customize-server-backup.md#BKMK_4)  
  
##  <a name="set-up-or-change-server-backup-settings"></a><a name="BKMK_1"></a>Einrichten oder Ändern von Server Sicherungs Einstellungen  
  
#### <a name="to-set-up-or-change-server-backup-settings"></a>So richten Sie Serversicherungseinstellungen ein oder ändern sie  
  
1.  Öffnen Sie das **Dashboard**, und klicken Sie auf die Registerkarte **Geräte**.  
  
2.  Klicken Sie in der Listenansicht auf den Server, um ihn auszuwählen.  
  
3.  Klicken Sie im Aufgabenbereich auf **Sicherung für den Server einrichten**.  
  
    > [!NOTE]
    >  Wenn Sie die vorhandenen Sicherungseinstellungen ändern möchten, klicken Sie auf **Sicherung für den Server anpassen**.  
  
4.  Folgen Sie den Anweisungen im Assistenten.  
  
    > [!NOTE]
    >  Wenn Sie den Assistenten starten, bevor Sie das externe Festplattenlaufwerk an den Server angehängt haben, klicken Sie auf **Liste aktualisieren** auf der Seite **Sicherungsziel auswählen**, nachdem Sie das Festplattenlaufwerk angehängt haben.  
  
> [!NOTE]
>  In der Standardinstallation von Windows Server Essentials ist der Server so konfiguriert, dass einmal pro Woche automatisch eine Defragmentierung durchgeführt wird. Dadurch können die Sicherungen größer als üblich ausfallen, wenn Sie nicht von Microsoft stammende Imaging-Software verwenden. Wenn die regelmäßige Defragmentierung des Servers nicht erforderlich ist, führen Sie die folgenden Schritte aus, um den Defragmentierungszeitplan zu deaktivieren:  
> 
> 1. Drücken Sie WINDOWS+W, um die **Suche** zu öffnen.  
>    2. Geben Sie im Suchfeld **Defragment** ein.  
>    3. Klicken Sie im Ergebnisabschnitt auf **Laufwerke defragmentieren und optimieren**.  
>    4. Wählen Sie auf der Seite **Laufwerke optimieren** ein Laufwerk aus, und klicken Sie dann auf **Einstellungen ändern**.  
>    5. Deaktivieren Sie im Fenster **Optimierungszeitplan** das Kontrollkästchen **Nach Zeitplan ausführen (empfohlen)** , und klicken Sie dann auf **OK**, um die Änderung zu speichern.  
  
##  <a name="server-backup-schedule"></a><a name="BKMK_2"></a>Zeitplan für die Server Sicherung  
 Wenn Sie den Assistenten zum Einrichten der Serversicherung oder den Assistenten zum Anpassen der Serversicherung verwenden, können Sie wählen, die Serverdaten zu verschiedenen Zeitpunkten täglich zu sichern. Da die Assistenten inkrementelle Sicherungen planen, werden die Sicherungen schnell ausgeführt und die Serverleistung nicht wesentlich beeinträchtigt. Standardmäßig wird von den Assistenten eine tägliche Sicherung um 12 Uhr und um 23 Uhr geplant. Sie können den Sicherungszeitplan jedoch entsprechend den Anforderungen Ihrer Organisation anpassen. Sie sollten von Zeit zu Zeit die Effektivität des Sicherungsplans bewerten und diesen nach Bedarf ändern.  
  
##  <a name="backup-target-drive"></a><a name="BKMK_Target"></a>Sicherungs Ziellaufwerk  
 Sie können zahlreiche externe Speicherlaufwerke für Sicherungen verwenden, und Sie können bei den Laufwerken zwischen internen und externen Speicherorten wechseln. Dadurch können Sie Ihre Vorbereitung auf Notfälle besser planen und sind in der Lage, die Daten wiederherzustellen, wenn die Hardware vor Ort physische Schäden erleidet.  
  
 Bei der Auswahl eines Speicherlaufwerks für die Serversicherung ist Folgendes zu berücksichtigen:  
  
-   Wählen Sie ein Laufwerk mit ausreichend Speicherplatz zum Speichern der Daten. Die Speicherlaufwerke sollte mindestens 2,5 Mal die Speicherkapazität der Daten enthalten, die Sie sichern möchten. Die Laufwerke sollten auch groß genug sein, ein zukünftiges Wachstum der Serverdaten aufnehmen zu können.  
  
-   Wenn ein externes Speicherlaufwerk verwendet wird, stellen Sie sicher, dass das Laufwerk leer ist oder nur Daten enthält, die Sie nicht benötigen.  
  
    > [!CAUTION]
    >  Der Assistent zum Einrichten der Serversicherung formatiert die Speicherlaufwerke während der Sicherungskonfiguration.  
  
-   Wenn das Speicherziellaufwerk Offline-Laufwerke umfasst, kann die Sicherungskonfiguration nicht erfolgreich verlaufen. Deaktivieren Sie zum Abschluss der Konfiguration bei der Auswahl des Sicherungsziels das Kontrollkästchen, um Offline-Laufwerke auszuschließen.  
  
-   Wenn Sie ein Laufwerk als Sicherungsziel auswählen, das vorherige Sicherungen enthält, können Sie im Assistenten wählen, ob Sie die vorherigen Sicherungen beibehalten möchten. Wenn Sie die Sicherungen beibehalten, formatiert der Assistent das Laufwerk nicht.  
  
-   Besuchen Sie die Website für Ihren externen Speicher Laufwerk Hersteller, um sicherzustellen, dass Ihr Sicherungs Laufwerk auf Computern unter Windows Server Essentials unterstützt wird.  
  
-   Das Laufwerk darf keine EFI-Systempartition (Extensible Firmware Interface) enthalten. Wenn eine EFI-Partition auf einem USB-Laufwerk vorhanden ist, wird davon ausgegangen, dass der Datenträger ein Startdatenträger ist. Wenn Sie sicher sind, dass Sie die Daten auf dem Datenträger nicht benötigen, können Sie den Datenträger neu formatieren und für Sicherungen verwenden.  
  
    > [!CAUTION]
    >  Wenn Sie den Datenträger neu formatieren, werden alle Daten gelöscht.  
  
    #### <a name="to-remove-an-efi-system-partition-from-a-usb-disk"></a>So entfernen Sie eine EFI-Systempartition von einem USB-Datenträger  
  
    1.  Öffnen Sie in der Systemsteuerung **System und Sicherheit**.  
  
    2.  Klicken Sie unter **Verwaltung** auf **Festplattenpartitionen erstellen und formatieren**.  
  
    3.  Löschen Sie alle Volumes auf dem USB-Datenträger, oder löschen Sie einfach die EFI-Partition. Der Assistent zum Einrichten der Serversicherung löscht alle Volumes.  
  
-   Der Datenträger darf keine freigegebenen Serverordner enthalten. Bevor Sie den Datenträger als Sicherungsziel verwenden können, müssen Sie die Freigabe für alle freigegebenen Serverordner beenden. Sie können die Freigabe über das Dashboard oder im Datei-Explorer beenden.  
  
    #### <a name="to-stop-sharing-on-a-server-folder-from-the-dashboard"></a>So beenden Sie die Freigabe eines Serverordners über das Dashboard  
  
    1.  Klicken Sie auf dem Dashboard auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
    2.  Wählen Sie den Ordner, dessen Freigabe Sie beenden möchten, und klicken Sie im Aufgabenbereich auf **Beenden**.  
  
> [!NOTE]
>  Wenn eine Sicherung nicht erfolgreich ist, weil auf dem Sicherungs Laufwerk nicht genügend Speicherplatz vorhanden ist, wird der Laufwerk Buchstabe für das Sicherungs Ziellaufwerk aus der Windows Server Essentials-Datenbank entfernt, und das Laufwerk wird nicht auf dem Dashboard angezeigt. Wenn Sie das Laufwerk in zukünftigen Sicherungen verwenden möchten, müssen Sie mithilfe eines systemeigenen Tools den Laufwerkbuchstaben erneut zuweisen.  
> 
>  **So weisen Sie einen Laufwerk Buchstaben für ein vorhandenes Volume erneut zu**  
> 
> 1. Öffnen Sie in der Systemsteuerung **System und Sicherheit**.  
>    2. Klicken Sie unter **Verwaltung** auf **Festplattenpartitionen erstellen und formatieren**.  
>    3. Klicken Sie mit der rechten Maustaste auf das Laufwerk, und klicken Sie auf **Laufwerkbuchstaben und -pfade ändern...** .  
>    4. Klicken Sie auf **Hinzufügen**.  
>    5. Wählen Sie im Dialogfeld Laufwerkbuchstaben oder -pfad hinzufügen“ einen Laufwerkbuchstaben für die Zuweisung aus. (Sie können den gleichen Laufwerk Buchstaben erneut zuweisen.) Klicken Sie dann auf **OK**.  
> 
>    Das Laufwerk wird sofort auf dem Dashboard angezeigt.  
  
##  <a name="items-to-be-backed-up"></a><a name="BKMK_4"></a>Zu sichernde Elemente  
 Sie können wählen, alle Laufwerke, Dateien und Ordner auf dem Server zu sichern oder nur einzelne Laufwerke, Dateien oder Ordner für die Sicherung auswählen.  
  
 Wenn Sie ein Laufwerk oder freigegebene Dateien und Ordner hinzufügen oder entfernen, müssen Sie die Serversicherungskonfiguration erneut überprüfen, um sicherzustellen, dass diese Elemente der Sicherungskonfiguration hinzugefügt oder daraus entfernt wurden. Führen Sie einen der folgenden Schritte aus, um Elemente für die Sicherung hinzuzufügen oder zu entfernen:  
  
- Um ein Datenlaufwerk in die Serversicherung einzuschließen, aktivieren Sie das daneben liegende Kontrollkästchen.  
  
- Um ein Datenlaufwerk aus der Serversicherung auszuschließen, deaktivieren Sie das daneben liegende Kontrollkästchen.  
  
  > [!NOTE]
  >  Wenn Sie das **Betriebssystem** aus der Sicherung ausschließen möchten, müssen Sie zuerst das Kontrollkästchen **Systemsicherung (empfohlen)** deaktivieren.  
  
  Um den Serverspeicher zu minimieren, den die Serversicherungen verwenden, sollten Sie alle Ordner ausschließen, die Dateien enthalten, die Sie nicht für wertvoll oder besonders wichtig halten.  
  
  So können Sie beispielsweise über einen Ordner verfügen, der aufgezeichnete Fernsehsendungen enthält und viel Festplattenspeicherplatz belegt. Sie können festlegen, dass diese Dateien nicht gesichert werden, da sie normalerweise nach einmaliger Wiedergabe ohnehin gelöscht werden. Ein weiteres Beispiel ist ein Ordner mit temporären Dateien, die Sie nicht aufbewahren möchten.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Server Sicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Sicherungen und Wiederherstellungen](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
