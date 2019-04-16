---
title: Verwalten der Serversicherung in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0302d070-c58a-40f2-b56d-7e7842813d02
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 2b0cd926b15d65e5cd4c784681c40df29b18a48f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manage-server-backup-in-windows-server-essentials"></a>Verwalten der Serversicherung in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
  
 Die folgenden Themen enthalten Informationen zu allgemeinen Sicherungsaufgaben, die Sie mithilfe von Windows Server Essentials-Dashboard ausführen können:  
  
-   [Welche Sicherung soll ich auswählen?](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_WhichBackup)  
  
-   [Einrichten oder Anpassen der serversicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Beenden der aktiven serversicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Remoteverwaltung von Sicherungen](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Deaktivieren der serversicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Weitere Informationen zum Einrichten von Server-Sicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Erneutes Partitionieren einer Festplatte auf dem server](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Wiederherstellen von Dateien und Ordnern aus einer Sicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
##  <a name="BKMK_WhichBackup"></a>Welche Sicherung soll ich auswählen?  
 Auswahl einer Sicherung kann einfach sein, wenn Sie über eine möglichst aktuelle erfolgreiche Sicherung verfügen und Sie wissen, dass die Sicherung alle wichtigen Daten enthält. Wenn Sie auf dem Server oder einen Computer aus einer älteren Sicherung wiederherstellen möchten, Auswählen einer guten Sicherung wiederherstellen, erfordern einige Ermittlungen und möglicherweise einige gefährden.  
  
#### <a name="to-choose-a-backup"></a>So wählen Sie eine Sicherung aus  
  
1.  Überprüfen Sie mit dem Besitzer der Dateien oder Ordner, und notieren Sie die Datums- und Uhrzeitangaben bei dem diese hinzugefügt oder bearbeitet wurden. Verwenden Sie die Datums- und Uhrzeitangaben als Ausgangspunkt verwendet.  
  
2.  Auf der **Wiederherstellungsoption auswählen** Seite das Wiederherstellen von Dateien und Ordner-Assistent, klicken Sie auf **wiederherstellen aus einer Sicherung, die ich auswählen (Erweitert)**.  
  
3.  Je nachdem, ob Sie eine ältere oder neuere Version der Dateien oder Ordner wiederherstellen möchten wählen Sie die Sicherung, die ehesten den Datums- und Uhrzeitangaben in Schritt 1 notiert haben.  
  
4.  Als bewährte Methode Sie können Dateien und Ordner an einem alternativen Speicherort wiederherstellen, und klicken Sie dann den Besitzer der Dateien und Ordner verschieben, über die sie am ursprünglichen Speicherort. Wenn sie fertig sind, können die Dateien und Ordner, die im alternativen Pfad bleiben gelöscht werden.  
  
##  <a name="BKMK_1"></a>Einrichten oder Anpassen der serversicherung  
 Server-Sicherung ist während der Installation nicht automatisch konfiguriert. Sie sollten Ihre Server und dessen Daten automatisch schützen, indem Sie tägliche Sicherungen planen. Es wird empfohlen, einen täglichen Sicherungsplan zu verwalten, da die meisten Organisationen können es sich, Daten zu verlieren, die über mehrere Tage erstellt wurde. Weitere Informationen finden Sie unter [festlegen einrichten oder Anpassen der serversicherung](Set-up-or-customize-server-backup.md).  
  
##  <a name="BKMK_2"></a>Beenden der aktiven serversicherung  
 Ob eine regelmäßig geplante gleichzeitig serversicherung oder eine Server-Sicherung manuell starten, können Sie die laufende Sicherung beenden.  
  
#### <a name="to-stop-a-backup-in-progress"></a>Um eine laufende Sicherung beenden  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie in der Navigationsleiste auf **Geräte**.  
  
3.  Klicken Sie in der Liste der Computer, auf den Server, und klicken Sie dann auf **Sicherung für den Server beenden** in der **Aufgaben** Bereich.  
  
4.  Klicken Sie auf **Ja** Aktion zu bestätigen.  
  
##  <a name="BKMK_3"></a>Remoteverwaltung von Sicherungen  
 Wenn Sie nicht im Büro sind, können Sie Windows Server Essentials-Remotewebzugriff, auf dem Windows Server Essentials-Dashboard zur Verwaltung der Server zugreifen.  
  
#### <a name="to-use-remote-web-access-to-manage-your-server"></a>Verwalten Sie den Server mit Remote Web Access  
  
1.  Öffnen Sie einen Webbrowser.  
  
2.  Geben Sie in das Adressfeld den Namen des Windows Server Essentials-Domäne.  
  
3.  Wenn Sie aufgefordert werden, geben Sie Ihren Benutzernamen und Ihr Kennwort ein.  
  
4.  Wenn Sie den Namen des Servers in Remote Web Access klicken, wird die Anmeldeseite des Dashboards angezeigt.  
  
5.  Melden Sie sich auf dem Dashboard als Administrator, und klicken Sie dann auf **Geräte**.  
  
 Weitere Informationen zum Remotewebzugriff finden Sie unter [Übersicht über Remotewebzugriff](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Overview).  
  
##  <a name="BKMK_4"></a>Deaktivieren der serversicherung  
 Sie sollten Ihre Server und dessen Daten automatisch schützen, indem Sie tägliche Sicherungen planen. Es wird empfohlen, einen täglichen Sicherungsplan zu verwalten, da die meisten Organisationen können es sich, Daten zu verlieren, die über mehrere Tage erstellt wurde.  
  
 Wenn Sie bereits Server-Sicherung konfiguriert haben und später eine Drittanbieter-Anwendung, die zum Sichern des Servers verwenden möchten, können Sie Windows Server Essentials-serversicherung deaktivieren.  
  
#### <a name="to-disable-server-backup"></a>So deaktivieren Sie Server-Sicherung  
  
1.  Melden Sie sich auf die Windows Server Essentials-Dashboard mit einem Administratorkonto und das Kennwort an.  
  
2.  Klicken Sie auf die **Geräte** Registerkarte, und klicken Sie dann auf den Namen des Servers.  
  
3.  Klicken Sie im Bereich Aufgaben auf **Sicherung für den Server anpassen**.  
  
    > [!NOTE]
    >  Die **Sicherung für den Server anpassen** Aufgabe wird angezeigt, nachdem Sie Server-Sicherung mithilfe des Server-Sicherung-Assistenten konfiguriert haben. Weitere Informationen zum Einrichten von Server-Sicherung finden Sie unter [festlegen einrichten oder Anpassen der serversicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1).  
  
4.  Der Assistent zum Anpassen der Serversicherung wird angezeigt.  
  
5.  Auf der **Konfigurationsoptionen** auf **Serversicherung deaktivieren**. Folgen Sie den Anweisungen im Assistenten aus.  
  
##  <a name="BKMK_5"></a>Weitere Informationen zum Einrichten von Server-Sicherung  
 Server-Sicherung ist während der Serverinstallation nicht aktiviert.  
  
> [!NOTE]
>  Wenn Sie Server-Sicherung konfigurieren, sollten Sie mindestens eine externe Festplatte an den Server, die als die Festplatte Sicherungsziel verwendet verbinden.  
  
###  <a name="BKMK_Target"></a>Sicherungsziellaufwerk  
 Sie können zahlreiche externe Speicherlaufwerke für Sicherungen verwenden können, und Sie die Laufwerken zwischen internen und externen Speicherorten. Dies kann die notfallbereitschaft planen Sie die Daten wiederherstellen, wenn die Hardware vor Ort physische Schäden auftritt und verbessern.  
  
 Bei der Auswahl eines Speicherlaufwerks für die serversicherung die folgenden Punkte:  
  
-   Wählen Sie ein Laufwerk, das über genügend Speicherplatz zum Speichern der Daten enthält. Die Speicherlaufwerke sollte mindestens 2,5 Mal die Speicherkapazität der Daten enthalten, die Sie sichern möchten. Die Laufwerke sollten auch groß genug für das zukünftige Wachstum der Serverdaten sein.  
  
-   Wenn das Ziellaufwerk offline-Laufwerke enthält, wird die Sicherungskonfiguration nicht erfolgreich ausgeführt. Um die Konfiguration abzuschließen, wenn das Sicherungsziel auswählen, deaktivieren Sie das Kontrollkästchen, damit Laufwerke ausgeschlossen werden, die offline sind.  
  
-   Wenn Sie ein Laufwerk, die als Sicherungsziel vorherige Sicherungen enthält auszuwählen, kann der Assistent, dass Sie auswählen, wenn Sie die vorherigen Sicherungen beibehalten möchten. Wenn Sie die Sicherungen beibehalten, formatiert der Assistent das Laufwerk nicht.  
  
-   Bei externen Speicherlaufwerks, stellen Sie sicher, dass das Laufwerk leer ist oder nur Daten enthält, die Sie nicht benötigen.  
  
-   Sie auf der Website des Herstellers des externen Speicher ob um sicherzustellen, dass das Sicherungslaufwerk für Computer, die mit Windows Server Essentials unterstützt wird.  
  
> [!CAUTION]
>  Der Server-Sicherung-Assistent formatiert die Speicherlaufwerke, wenn sie für die Sicherung konfiguriert.  
  
### <a name="server-backup-schedule"></a>Serversicherungszeitplan  
 Sie sollten Ihre Server und dessen Daten automatisch schützen, indem Sie tägliche Sicherungen planen. Es wird empfohlen, einen täglichen Sicherungsplan zu verwalten, da die meisten Organisationen können es sich, Daten zu verlieren, die über mehrere Tage erstellt wurde.  
  
 Wenn Sie den Windows Server Essentials-Server-Sicherung-Assistenten verwenden, können Sie zum Sichern der Serverdaten mehrmals am Tag. Da der Assistent differenzielle Sicherungen plant, Sicherung schnell ausgeführt und serverleistung nicht wesentlich beeinträchtigt. In der Standardeinstellung **legen Sie Server-Sicherung** eine Sicherung für die tägliche Ausführung 12:00 Uhr und 23:00 Uhr geplant. Allerdings können Sie den Sicherungszeitplan entsprechend den Anforderungen Ihrer Organisation anpassen. Sie sollten Zeit zu Zeit die Effektivität des Sicherungsplans bewerten, und ändern Sie den Plan nach Bedarf.  
  
> [!NOTE]
>  In der Standardinstallation von Windows Server Essentials ist der Server konfiguriert, dass automatisch einmal pro Woche eine Defragmentierung durchgeführt. Dies kann dazu führen Sicherungen größer als üblich bei Verwendung von Microsoft stammende imaging-Software. Ist es nicht erforderlich, um den Server in regelmäßigen Abständen defragmentieren, können Sie führen Sie die folgenden Schritte aus, um den defragmentierungszeitplan zu deaktivieren:  
>   
>  1.  Drücken Sie die Windows-Taste + W öffnen **Suche**.  
> 2.  Geben Sie in das Textfeld Suchen **Defragmentieren**.  
> 3.  Klicken Sie im Ergebnisabschnitt auf **Laufwerke defragmentieren und optimieren**.  
> 4.  In der **Laufwerkoptimierung** Seite, wählen Sie ein Laufwerk, und klicken Sie dann auf **Einstellungsänderungen**.  
> 5.  In der **optimierungszeitplan** Löschen der **ein Zeitplan (empfohlen)** , und klicken Sie dann auf **OK** um die Änderung zu speichern.  
  
### <a name="items-to-be-backed-up"></a>Elemente gesichert werden.  
 Standardmäßig werden alle Dateien und Ordner für die Sicherung ausgewählt. Sie können auch alle Festplatten, Dateien und Ordner auf dem Server sichern oder nur einzelne Festplatten, Dateien oder Ordner für die Sicherung auswählen. Zum Hinzufügen oder Entfernen von Elementen für die Sicherung führen Sie eine der folgenden Optionen:  
  
-   Um ein Datenlaufwerk in die serversicherung einzuschließen, aktivieren Sie das daneben liegende Kontrollkästchen.  
  
-   Um ein Datenlaufwerk aus der serversicherung auszuschließen, deaktivieren Sie das daneben liegende Kontrollkästchen.  
  
> [!NOTE]
>  Wenn Sie ausschließen möchten die **Betriebssystem** Element aus der Sicherung, müssen Sie zunächst Deaktivieren der **Systemsicherung (empfohlen)** Kontrollkästchen.  
  
 Um die Menge des Festplattenspeichers zu minimieren, die Sicherungen des Servers verwenden, sollten Sie alle Ordner ausschließen, die Dateien, die Sie nicht enthalten unbedingt berücksichtigen.  
  
 Sie können z. B. einen Ordner mit aufgezeichneten TV-Programme verfügen, die zahlreiche Festplatten-Speicherplatz verwendet. Sie können auswählen, diese Dateien sichern, da Sie normalerweise sie nach dem Löschen ohnehin nicht. Alternativ müssen Sie einen Ordner möglicherweise, der temporären Dateien enthält, die Sie nicht behalten möchten.  
  
##  <a name="BKMK_6"></a>Erneutes Partitionieren einer Festplatte auf dem server  
 Wenn eine unformatierte interne Festplatte auf dem Windows Server Essentials-Server erkannt wird, wird eine integritätsstatuswarnung ausgelöst, die einen Link zu der neuen Festplatte Laufwerk Assistenten zum Hinzufügen einer enthält. Die neue Festplatte Laufwerk Assistenten zum Hinzufügen einer führt Sie durch die verschiedenen Optionen zur Formatierung der Festplatte. Wenn der Assistent abgeschlossen ist, wird eine oder mehrere, abhängig von der Größe des Laufwerks, logische formatierte Festplatten auf der Festplatte erstellt und als NTFS formatiert.  
  
 Wenn sie ein Festplattenlaufwerk neu partitionieren erforderlich wird, gehen Sie wie folgt vor:  
  
#### <a name="to-repartition-a-hard-disk-drive"></a>Ein Festplattenlaufwerk neu partitionieren.  
  
1.  Auf der **starten** auf **Verwaltung**, und doppelklicken Sie dann auf **Computerverwaltung**.  
  
2.  Klicken Sie in der Computerverwaltung auf **Speicher**, und doppelklicken Sie dann auf **Datenträgerverwaltung**.  
  
3.  Mit der rechten Maustaste in des Laufwerks, das Sie verwenden möchten, neu zu partitionieren, klicken **Volume löschen**, und klicken Sie dann auf **Ja**.  
  
    > [!NOTE]
    >  Wiederholen Sie diesen Schritt für jede Partition auf der Festplatte.  
  
4.  Mit der rechten Maustaste die **nicht zugeordnet** Festplattenlaufwerk, und klicken Sie dann auf **Neues einfaches Volume**.  
  
5.  In der einfachen Assistenten für neue Volumes erstellen und Formatieren eines Volumes, die 16 TB (16.000.000 MB) oder weniger.  
  
    > [!NOTE]
    >  Wiederholen Sie diesen Schritt, bis sämtlicher nicht zugeordneter Speicherplatz auf der Festplatte verwendet wird.  
  
##  <a name="BKMK_7"></a>Wiederherstellen von Dateien und Ordnern aus einer Sicherung  
 Sie können navigieren und einzelne Dateien und Ordner aus einer Sicherung wiederherstellen.  
  
#### <a name="to-restore-files-and-folders-from-a-server-backup"></a>Wiederherstellen von Dateien und Ordnern aus einer Sicherung  
  
1.  Öffnen Sie das Dashboard, und klicken Sie dann auf die **Geräte** Registerkarte.  
  
2.  Klicken Sie auf den Namen des Servers, und klicken Sie dann auf **Wiederherstellen von Dateien oder Ordner für den Server** in der **Aufgaben** Bereich.  
  
3.  Das Wiederherstellen von Dateien oder Ordner-Assistent wird geöffnet. Führen Sie die Anweisungen im Assistenten, um die Dateien oder Ordner wiederherzustellen.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
