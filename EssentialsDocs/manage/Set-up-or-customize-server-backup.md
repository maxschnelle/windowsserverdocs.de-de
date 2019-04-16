---
title: Einrichten oder Anpassen der serversicherung
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 441c2d6c-435a-42cb-90f2-6d680d279d34
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 727dd74e4bddc52f735969f216914b9d76d1f413
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="set-up-or-customize-server-backup"></a>Einrichten oder Anpassen der serversicherung

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
  
 Server-Sicherung ist während der Installation nicht automatisch konfiguriert. Sie sollten Ihre Server und dessen Daten automatisch schützen, indem Sie tägliche Sicherungen planen. Es wird empfohlen, einen täglichen Sicherungsplan zu verwalten, da die meisten Organisationen können es sich, Daten zu verlieren, die über mehrere Tage erstellt wurde.  
  
 Weitere Informationen finden Sie in den folgenden Abschnitten zum Einrichten oder Anpassen der serversicherung:  
  
-   [Einrichten oder Ändern von serversicherungseinstellungen](Set-up-or-customize-server-backup.md#BKMK_1)  
  
-   [Serversicherungszeitplan](Set-up-or-customize-server-backup.md#BKMK_2)  
  
-   [Sicherungsziellaufwerk](Set-up-or-customize-server-backup.md#BKMK_Target)  
  
-   [Elemente gesichert werden.](Set-up-or-customize-server-backup.md#BKMK_4)  
  
##  <a name="BKMK_1"></a>Einrichten oder Ändern von serversicherungseinstellungen  
  
#### <a name="to-set-up-or-change-server-backup-settings"></a>Einrichten oder Ändern von serversicherungseinstellungen  
  
1.  Öffnen der **Dashboard**, und klicken Sie dann auf die **Geräte** Registerkarte.  
  
2.  Klicken Sie in der Listenansicht auf den Server, um es auszuwählen.  
  
3.  Klicken Sie im Bereich Aufgaben auf **Sicherung für den Server einrichten**.  
  
    > [!NOTE]
    >  Wenn Sie die vorhandenen sicherungseinstellungen ändern möchten, klicken Sie auf **Sicherung für den Server anpassen**.  
  
4.  Folgen Sie den Anweisungen im Assistenten aus.  
  
    > [!NOTE]
    >  Wenn Sie den Assistenten starten, bevor Sie die externe Festplatte anfügen, mit dem Server, klicken Sie auf **Liste aktualisieren** auf die **Sicherungsziel auswählen** Seite nach dem Anschließen der Festplatte.  
  
> [!NOTE]
>  In der Standardinstallation von Windows Server Essentials ist der Server konfiguriert, dass automatisch einmal pro Woche eine Defragmentierung durchgeführt. Dies kann dazu führen Sicherungen größer als üblich bei Verwendung von Microsoft stammende imaging-Software. Ist es nicht erforderlich, um den Server in regelmäßigen Abständen defragmentieren, können Sie führen Sie die folgenden Schritte aus, um den defragmentierungszeitplan zu deaktivieren:  
>   
>  1.  Drücken Sie die Windows-Taste + W öffnen **Suche**.  
> 2.  Geben Sie in das Textfeld Suchen **Defragmentieren**.  
> 3.  Klicken Sie im Ergebnisabschnitt auf **Laufwerke defragmentieren und Optimieren der**.  
> 4.  In der **Laufwerkoptimierung** Seite, wählen Sie ein Laufwerk, und klicken Sie dann auf **Einstellungsänderungen**.  
> 5.  In der **optimierungszeitplan** Löschen der **ein Zeitplan (empfohlen)** , und klicken Sie dann auf **OK** um die Änderung zu speichern.  
  
##  <a name="BKMK_2"></a>Serversicherungszeitplan  
 Wenn Sie den Server-Sicherung-Assistenten oder den Assistenten zum Anpassen von Server-Sicherung verwenden, können Sie zum Sichern der Serverdaten mehrmals am Tag. Da die Assistenten inkrementelle Sicherungen planen, die Sicherungen schnell ausgeführt und serverleistung nicht wesentlich beeinträchtigt. In der Standardeinstellung planen die Assistenten eine Sicherung um 12:00 Uhr und 23:00 Uhr täglich ausgeführt. Allerdings können Sie den Sicherungszeitplan entsprechend den Anforderungen Ihrer Organisation anpassen. Sie sollten Zeit zu Zeit die Effektivität des Sicherungsplans bewerten, und ändern Sie den Plan nach Bedarf.  
  
##  <a name="BKMK_Target"></a>Sicherungsziellaufwerk  
 Sie können zahlreiche externe Speicherlaufwerke für Sicherungen verwenden können, und Sie die Laufwerken zwischen internen und externen Speicherorten. Dies kann die notfallbereitschaft planen Sie die Daten wiederherstellen, wenn die Hardware vor Ort physische Schäden auftritt und verbessern.  
  
 Bei der Auswahl eines Speicherlaufwerks für die serversicherung die folgenden Punkte:  
  
-   Wählen Sie ein Laufwerk, das über genügend Speicherplatz zum Speichern der Daten enthält. Die Speicherlaufwerke sollte mindestens 2,5 Mal die Speicherkapazität der Daten enthalten, die Sie sichern möchten. Die Laufwerke sollten auch groß genug für das zukünftige Wachstum der Serverdaten sein.  
  
-   Wenn Sie ein externes Speicherlaufwerk verwenden, stellen Sie sicher, dass das Laufwerk leer ist oder nur Daten enthält, die Sie nicht benötigen.  
  
    > [!CAUTION]
    >  Der Server-Sicherung-Assistent formatiert die Speicherlaufwerke, wenn sie für die Sicherung konfiguriert.  
  
-   Wenn das speicherziellaufwerk Offline-Laufwerke enthält, wird die Sicherungskonfiguration nicht erfolgreich ausgeführt. Um die Konfiguration abzuschließen, wenn das Sicherungsziel auswählen, deaktivieren Sie das Kontrollkästchen, damit Laufwerke ausgeschlossen werden, die offline sind.  
  
-   Wenn Sie ein Laufwerk, die als Sicherungsziel vorherige Sicherungen enthält auszuwählen, kann der Assistent, dass Sie auswählen, wenn Sie die vorherigen Sicherungen beibehalten möchten. Wenn Sie die Sicherungen beibehalten, formatiert der Assistent das Laufwerk nicht.  
  
-   Sie auf der Website des Herstellers des externen Speicher ob um sicherzustellen, dass das Sicherungslaufwerk für Computer, die mit Windows Server Essentials unterstützt wird.  
  
-   Das Laufwerk kann nicht auf eine Systempartition Extensible Firmware Interface (EFI) enthalten. Wenn eine EFI-Partition auf einem USB-Laufwerk vorhanden ist, wird davon ausgegangen, dass der Datenträger ein Startdatenträger ist. Wenn Sie sicher sind, dass Sie die Daten auf dem Datenträger ist nicht erforderlich Verschlüsselungskennwort, können Sie den Datenträger neu formatieren und für Sicherungen verwenden.  
  
    > [!CAUTION]
    >  Wenn Sie den Datenträger neu formatieren, werden alle Daten gelöscht.  
  
    #### <a name="to-remove-an-efi-system-partition-from-a-usb-disk"></a>So entfernen Sie eine EFI-Systempartition von einem USB-Datenträger  
  
    1.  Öffnen Sie in der Systemsteuerung **System und Sicherheit**.  
  
    2.  Klicken Sie unter **Verwaltung**, klicken Sie auf **erstellen und Formatieren von Festplattenpartitionen**.  
  
    3.  Löschen Sie alle Volumes auf dem USB-Datenträger, oder löschen Sie einfach die EFI-Partition. Der Server-Sicherung Assistenten zum Einrichten, werden alle Volumes gelöscht.  
  
-   Das Laufwerk kann nicht auf alle freigegebenen Serverordner enthalten. Bevor Sie den Datenträger als Sicherungsziel verwenden können, müssen Sie die Freigabe für alle freigegebenen Serverordner beenden. Sie können die Freigabe über das Dashboard oder im Datei-Explorer.  
  
    #### <a name="to-stop-sharing-on-a-server-folder-from-the-dashboard"></a>Zum Beenden der Freigabe eines Serverordners über das Dashboard  
  
    1.  Klicken Sie auf dem Dashboard auf **Speicher**, und klicken Sie dann auf **Serverordner**.  
  
    2.  Wählen Sie den Ordner, dessen Freigabe beendet werden soll, und klicken Sie dann im Aufgabenbereich auf **beenden**.  
  
> [!NOTE]
>  Wenn eine Sicherung nicht erfolgreich ist, weil der Sicherungsdatenträger nicht genügend Speicherplatz bietet, ist der Laufwerkbuchstabe für das Sicherungsziellaufwerk aus der Windows Server Essentials-Datenbank entfernt und das Dashboard wird das Laufwerk nicht angezeigt. Wenn Sie das Laufwerk in zukünftigen Sicherungen verwenden möchten, müssen Sie die Laufwerkbuchstaben mithilfe eines systemeigenen Tools erneut zuweisen.  
>   
>  **Um einen Laufwerkbuchstaben für ein vorhandenes Volume erneut zuweisen.**  
>   
>  1.  Öffnen Sie in der Systemsteuerung **System und Sicherheit**.  
> 2.  Klicken Sie unter **Verwaltung**, klicken Sie auf **erstellen und Formatieren von Festplattenpartitionen**.  
> 3.  Maustaste auf das Laufwerk, und klicken Sie auf **Änderung Laufwerkbuchstaben und -Pfade**.  
> 4.  Klicken Sie auf **hinzufügen**.  
> 5.  Wählen Sie im Dialogfeld hinzufügen Laufwerkbuchstaben oder -Pfad einen Laufwerkbuchstaben zuweisen. (Sie können die gleichen Laufwerkbuchstaben erneut zuweisen.) Klicken Sie dann auf **OK**.  
>   
>      Das Laufwerk wird sofort auf dem Dashboard angezeigt.  
  
##  <a name="BKMK_4"></a>Elemente gesichert werden.  
 Sie können auch alle Laufwerke, Dateien und Ordner auf dem Server sichern, oder wählen Sie nur einzelne Laufwerke, Dateien oder Ordner zum Sichern.  
  
 Wenn Sie hinzufügen oder entfernen Sie ein Laufwerk oder hinzufügen oder entfernen Sie freigegebene Dateien und Ordner, sollten Sie sicherstellen, dass diese Elemente hinzugefügt oder aus der Sicherungskonfiguration entfernt die Serversicherungskonfiguration erneut. Zum Hinzufügen oder Entfernen von Elementen für die Sicherung führen Sie eine der folgenden Optionen:  
  
-   Um ein Datenlaufwerk in die serversicherung einzuschließen, aktivieren Sie das Kontrollkästchen neben  
  
-   Um ein Datenlaufwerk aus der serversicherung auszuschließen, deaktivieren Sie das Kontrollkästchen neben  
  
    > [!NOTE]
    >  Wenn Sie ausschließen möchten die **Betriebssystem** Element aus der Sicherung, müssen Sie zunächst Deaktivieren der **Systemsicherung (empfohlen)** Kontrollkästchen.  
  
 Um die Menge an Serverspeicher zu minimieren, die Sicherungen des Servers verwenden, sollten Sie alle Ordner ausschließen, die Dateien, die Sie nicht enthalten unbedingt berücksichtigen.  
  
 Sie können z. B. einen Ordner mit aufgezeichneten TV-Programme verfügen, die zahlreiche Festplatten-Speicherplatz verwendet. Sie können auswählen, diese Dateien sichern, da Sie normalerweise sie nach dem Löschen ohnehin nicht. Oder Sie haben einen Ordner mit temporären Dateien, die Sie nicht behalten möchten.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Serversicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md)  
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
