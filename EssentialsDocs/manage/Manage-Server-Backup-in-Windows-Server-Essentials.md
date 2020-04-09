---
title: Verwalten der Serversicherung in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 0302d070-c58a-40f2-b56d-7e7842813d02
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 91edef97780be5805f13445e6c8311594dbfadc4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852753"
---
# <a name="manage-server-backup-in-windows-server-essentials"></a>Verwalten der Serversicherung in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 Die folgenden Themen betreffen Informationen zu allgemeinen Sicherungsaufgaben, die Sie über das Windows Server Essentials Dashboard ausführen können:  
  
-   [Welche Sicherung soll ausgewählt werden?](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_WhichBackup)  
  
-   [Einrichten oder Anpassen der Serversicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Die Server Sicherung wird beendet.](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Remote Verwaltung Ihrer Sicherungen](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Deaktivieren der Server Sicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Weitere Informationen zum Einrichten der Server Sicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Neupartitionieren einer Festplatte auf dem Server](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Wiederherstellen von Dateien und Ordnern aus einer Server Sicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
##  <a name="which-backup-should-i-choose"></a><a name="BKMK_WhichBackup"></a>Welche Sicherung soll ausgewählt werden?  
 Die Auswahl einer Sicherung kann ganz einfach sein, wenn eine aktuelle, erfolgreich ausgeführte Datensicherung mit allen wichtigen Daten vorliegt. Wenn Sie versuchen, eine Wiederherstellung aus einer älteren Sicherung auf dem Server oder einem Computer auszuführen, erfordert die Auswahl einer geeigneten Sicherung für die Wiederherstellung einige Ermittlungen und möglicherweise einige Kompromisse.  
  
#### <a name="to-choose-a-backup"></a>So wählen Sie eine Sicherung aus  
  
1.  Fragen Sie beim Besitzer der Dateien oder Ordner nach, und notieren Sie Datum und Uhrzeit des Zeitpunkts, zu dem diese hinzugefügt oder bearbeitet wurden. Wählen Sie eine Sicherung ausgehend von diesen Datums- und Uhrzeitangaben aus.  
  
2.  Klicken Sie im Assistenten zum Wiederherstellen von Dateien und Ordnern auf der Seite **Wiederherstellungsoption auswählen** auf **Aus einer ausgewählten Sicherung wiederherstellen (erweitert)** .  
  
3.  Je nachdem, ob eine ältere oder neuere Version der Dateien oder Ordner wiederhergestellt werden soll, wählen Sie die Sicherung aus, die am ehesten den Datums- und Uhrzeitangaben entspricht, die Sie in Schritt 1 notiert haben.  
  
4.  Als bewährte Methode können Sie Dateien und Ordner an einem anderen Speicherort wiederherstellen. Die erforderlichen Dateien und Ordner lassen Sie dann von ihrem Besitzer an den ursprünglichen Speicherort verschieben. Wenn der Vorgang abgeschlossen ist, können die am alternativen Speicherort verbleibenden Dateien und Ordner gelöscht werden.  
  
##  <a name="set-up-or-customize-server-backup"></a><a name="BKMK_1"></a>Einrichten oder Anpassen der Server Sicherung  
 Die Serversicherung wird während der Installation nicht automatisch konfiguriert. Sie sollten den Server und dessen Daten automatisch schützen, indem Sie tägliche Sicherungen planen. Es wird empfohlen, einen täglichen Sicherungsplan zu verwalten, da die meisten Organisationen es sich nicht leisten können, die im Verlauf von mehreren Tagen erstellten Daten zu verlieren. Weitere Informationen finden Sie unter [Einrichten oder Anpassen der Serversicherung](Set-up-or-customize-server-backup.md).  
  
##  <a name="stop-server-backup-in-progress"></a><a name="BKMK_2"></a>Die Server Sicherung wird beendet.  
 Unabhängig davon, ob eine Serversicherung regelmäßig zu einem geplanten Zeitpunkt erfolgt oder Sie die Serversicherung manuell starten, können Sie die aktive Sicherung beenden.  
  
#### <a name="to-stop-a-backup-in-progress"></a>So beenden Sie eine laufende Sicherung  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie in der Navigationsleiste auf **Geräte**.  
  
3.  Klicken Sie in der Liste der Computer auf den Server, und klicken Sie dann im Bereich **Tasks** auf **Sicherung für den Server beenden**.  
  
4.  Klicken Sie auf **Ja**, um die Aktion zu bestätigen.  
  
##  <a name="remotely-manage-your-backups"></a><a name="BKMK_3"></a>Remote Verwaltung Ihrer Sicherungen  
 Wenn Sie nicht im Büro sind, können Sie den Windows Server Essentials-Remotewebzugriff verwenden, um zur Verwaltung der Server auf das Windows Server Essentials-Dashboard zuzugreifen.  
  
#### <a name="to-use-remote-web-access-to-manage-your-server"></a>So verwalten Sie den Server mithilfe des Remotewebzugriffs  
  
1. Öffnen Sie einen Webbrowser.  
  
2. Geben Sie im Adressfeld den Namen der Windows Server Essentials-Domäne ein.  
  
3. Wenn Sie aufgefordert werden, geben Sie Ihren Benutzernamen und das Kennwort ein.  
  
4. Wenn Sie in Remote Webzugriff auf den Namen des Servers klicken, wird die Anmeldeseite für das Dashboard angezeigt.  
  
5. Melden Sie sich auf dem Dashboard als Administrator an, und klicken Sie dann auf **Geräte**.  
  
   Weitere Informationen zu Remote Webzugriff finden Sie unter [Übersicht über Remote Webzugriff](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Overview).  
  
##  <a name="disable-server-backup"></a><a name="BKMK_4"></a>Deaktivieren der Server Sicherung  
 Sie sollten den Server und dessen Daten automatisch schützen, indem Sie tägliche Sicherungen planen. Es wird empfohlen, einen täglichen Sicherungsplan zu verwalten, da die meisten Organisationen es sich nicht leisten können, die im Verlauf von mehreren Tagen erstellten Daten zu verlieren.  
  
 Wenn Sie die Serversicherung bereits konfiguriert haben und später eine Drittanbieteranwendung für die Sicherung des Servers verwenden möchten, können Sie die Windows Server Essentials-Serversicherung deaktivieren.  
  
#### <a name="to-disable-server-backup"></a>So deaktivieren Sie die Serversicherung  
  
1.  Melden Sie sich am Windows Server Essentials-Dashboard mit einem Administratorkonto und dem zugehörigen Kennwort an.  
  
2.  Klicken Sie auf die Registerkarte **Geräte**, und klicken Sie dann auf den Namen des Servers.  
  
3.  Klicken Sie im Aufgabenbereich auf **Sicherung für den Server anpassen**.  
  
    > [!NOTE]
    >  Die Aufgabe **Sicherung für den Server anpassen** wird angezeigt, nachdem Sie die Serversicherung mithilfe des Assistenten zum Einrichten der Serversicherung konfiguriert haben. Weitere Informationen zum Einrichten der Serversicherung finden Sie unter [Einrichten oder Anpassen der Serversicherung](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1).  
  
4.  Der Assistent zum Anpassen der Serversicherung wird angezeigt.  
  
5.  Klicken Sie auf der Seite **Konfigurationsoptionen** auf **Serversicherung deaktivieren**. Folgen Sie den Anweisungen im Assistenten.  
  
##  <a name="learn-more-about-setting-up-server-backup"></a><a name="BKMK_5"></a>Weitere Informationen zum Einrichten der Server Sicherung  
 Die Serversicherung ist während der Einrichtung des Servers nicht aktiviert.  
  
> [!NOTE]
>  Beim Konfigurieren der Serversicherung sollten Sie mindestens eine externe Festplatte an den Server anschließen, die Sie als Sicherungsziel verwenden.  
  
###  <a name="backup-destination-drive"></a><a name="BKMK_Target"></a>Sicherungs Ziellaufwerk  
 Sie können zahlreiche externe Speicherlaufwerke für Sicherungen verwenden, und Sie können bei den Laufwerken zwischen internen und externen Speicherorten wechseln. Dadurch können Sie Ihre Vorbereitung auf Notfälle besser planen und sind in der Lage, die Daten wiederherzustellen, wenn die Hardware vor Ort physische Schäden erleidet.  
  
 Bei der Auswahl eines Speicherlaufwerks für die Serversicherung ist Folgendes zu berücksichtigen:  
  
-   Wählen Sie ein Laufwerk mit ausreichend Speicherplatz zum Speichern der Daten. Die Speicherlaufwerke sollte mindestens 2,5 Mal die Speicherkapazität der Daten enthalten, die Sie sichern möchten. Die Laufwerke sollten auch groß genug sein, ein zukünftiges Wachstum der Serverdaten aufnehmen zu können.  
  
-   Wenn das Ziellaufwerk der Sicherung auch Laufwerke einbezieht, die offline sind, kann die Sicherungskonfiguration nicht erfolgreich ausgeführt werden. Um die Konfiguration abzuschließen, deaktivieren Sie beim Auswählen des Sicherungsziels das Kontrollkästchen, damit Laufwerke ausgeschlossen werden, die offline sind.  
  
-   Wenn Sie ein Laufwerk als Sicherungsziel auswählen, das vorherige Sicherungen enthält, bietet Ihnen der Assistent die Option, die vorherigen Sicherungen zu behalten. Wenn Sie die Sicherungen beibehalten, formatiert der Assistent das Laufwerk nicht.  
  
-   Stellen Sie bei der Wiederverwendung eines externen Speicherlaufwerks sicher, dass das Laufwerk leer ist oder nur Daten enthält, die nicht länger erforderlich sind.  
  
-   Prüfen Sie auf der Website des Herstellers des externen Speicherlaufwerks, ob das Sicherungslaufwerk von Computern unterstützt wird, auf denen Windows Server Essentials ausgeführt wird.  
  
> [!CAUTION]
>  Der Assistent zum Einrichten der Serversicherung formatiert die Speicherlaufwerke während der Sicherungskonfiguration.  
  
### <a name="server-backup-schedule"></a>Serversicherungszeitplan  
 Sie sollten den Server und dessen Daten automatisch schützen, indem Sie tägliche Sicherungen planen. Es wird empfohlen, einen täglichen Sicherungsplan zu verwalten, da die meisten Organisationen es sich nicht leisten können, die im Verlauf von mehreren Tagen erstellten Daten zu verlieren.  
  
 Wenn Sie den Windows Server Essentials-Assistenten zum Einrichten der Serversicherung verwenden, können Sie auswählen, dass Serverdaten mehrmals täglich gesichert werden. Da der Assistent differenzielle Sicherungen plant, wird die Sicherung schnell ausgeführt, und die Serverleistung wird nicht merklich beeinträchtigt. Die Option **Serversicherung einrichten** legt die tägliche Ausführung einer Sicherung für 12:00 Uhr und 23:00 Uhr fest. Sie können den Sicherungszeitplan jedoch entsprechend den Anforderungen Ihrer Organisation anpassen. Sie sollten von Zeit zu Zeit die Effektivität des Sicherungsplans bewerten und diesen nach Bedarf ändern.  
  
> [!NOTE]
>  In der Standardinstallation von Windows Server Essentials ist der Server für die wöchentliche automatische Defragmentierung konfiguriert. Dadurch können die Sicherungen größer als üblich ausfallen, wenn Sie nicht von Microsoft stammende Imaging-Software verwenden. Wenn die regelmäßige Defragmentierung des Servers nicht erforderlich ist, führen Sie die folgenden Schritte aus, um den Defragmentierungszeitplan zu deaktivieren:  
> 
> 1. Drücken Sie WINDOWS+W, um die **Suche** zu öffnen.  
>    2. Geben Sie im Suchfeld **Defragment** ein.  
>    3. Klicken Sie im Ergebnisbereich auf **Laufwerke defragmentieren und optimieren**.  
>    4. Wählen Sie auf der Seite **Laufwerke optimieren** ein Laufwerk aus, und klicken Sie dann auf **Einstellungen ändern**.  
>    5. Deaktivieren Sie im Fenster **Optimierungszeitplan** das Kontrollkästchen **Nach Zeitplan ausführen (empfohlen)** , und klicken Sie dann auf **OK**, um die Änderung zu speichern.  
  
### <a name="items-to-be-backed-up"></a>Zu sichernde Elemente  
 Standardmäßig werden alle Betriebssystemdateien und -ordner für die Sicherung ausgewählt. Sie können auch alle Festplatten, Dateien und Ordner auf dem Server sichern oder nur einzelne Festplatten, Dateien oder Ordner für die Sicherung auswählen. Führen Sie einen der folgenden Schritte aus, um Elemente für die Sicherung hinzuzufügen oder zu entfernen:  
  
-   Um ein Datenlaufwerk in die Serversicherung einzuschließen, aktivieren Sie das nebenstehende Kontrollkästchen.  
  
-   Um ein Datenlaufwerk aus der Serversicherung auszuschließen, deaktivieren Sie das nebenstehende Kontrollkästchen.  
  
> [!NOTE]
>  Wenn Sie das **Betriebssystem** aus der Sicherung ausschließen möchten, müssen Sie zuerst das Kontrollkästchen **Systemsicherung (empfohlen)** deaktivieren.  
  
 Um den Umfang des erforderlichen Festplattenspeichers für die Sicherungen des Servers zu minimieren, können Sie alle Ordner ausschließen, die nicht unbedingt erforderliche Dateien enthalten.  
  
 So können Sie beispielsweise über einen Ordner verfügen, der aufgezeichnete Fernsehsendungen enthält und viel Festplattenspeicherplatz belegt. Sie können festlegen, dass diese Dateien nicht gesichert werden, da sie normalerweise nach einmaliger Wiedergabe ohnehin gelöscht werden. Alternativ verfügen Sie möglicherweise über einen Ordner, der temporäre Dateien enthält, die Sie nicht behalten möchten.  
  
##  <a name="repartition-a-hard-drive-on-the-server"></a><a name="BKMK_6"></a>Neupartitionieren einer Festplatte auf dem Server  
 Wenn eine unformatierte interne Festplatte auf dem Windows Server Essentials-Server erkannt wird, wird eine Integritätsstatuswarnung ausgelöst, die eine Verknüpfung zum Assistenten zum Hinzufügen neuer Festplatten enthält. Der Assistent zum Hinzufügen neuer Festplatten führt Sie durch die verschiedenen Optionen zur Formatierung der Festplatte. Nachdem der Assistent abgeschlossen ist, werden eine oder mehrere (in Abhängigkeit von der Laufwerksgröße) logische formatierte Festplatten auf der Festplatte erstellt und mit NTFS formatiert.  
  
 Wenn ein Festplattenlaufwerk neu partitioniert werden muss, gehen Sie wie folgt vor:  
  
#### <a name="to-repartition-a-hard-disk-drive"></a>So partitionieren Sie ein Festplattenlaufwerk neu  
  
1.  Klicken Sie auf dem Bildschirm **Start** auf **Verwaltung**, und doppelklicken Sie dann auf **Computerverwaltung**.  
  
2.  Klicken Sie in "Computerverwaltung" auf **Speicher**, und doppelklicken Sie dann auf **Datenträgerverwaltung**.  
  
3.  Klicken Sie mit der rechten Maustaste auf das neu zu partitionierende Laufwerk, klicken Sie dann auf **Volume löschen**, und klicken Sie anschließend auf **Ja**.  
  
    > [!NOTE]
    >  Wiederholen Sie diesen Schritt für jede Partition auf dem Festplattenlaufwerk.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Festplattenlaufwerk **Nicht zugeordnet**, und klicken Sie dann auf **Neues einfaches Volume**.  
  
5.  Erstellen Sie im Assistenten für neue einfache Volumes ein Volume mit 16 TB (16.000.000 MB) oder weniger, und formatieren Sie es anschließend.  
  
    > [!NOTE]
    >  Wiederholen Sie diesen Schritt, bis sämtlicher nicht zugeordneter Speicherplatz auf der Festplatte verwendet wird.  
  
##  <a name="restore-files-and-folders-from-a-server-backup"></a><a name="BKMK_7"></a>Wiederherstellen von Dateien und Ordnern aus einer Server Sicherung  
 Sie können einzelne Dateien und Ordner in einer Serversicherung suchen und wiederherstellen.  
  
#### <a name="to-restore-files-and-folders-from-a-server-backup"></a>So stellen Sie Dateien und Ordner über eine Server-Sicherung wieder her  
  
1.  Öffnen Sie das Dashboard, und klicken Sie dann auf die Registerkarte **Geräte**.  
  
2.  Klicken Sie auf den Namen des Servers und anschließend auf **Wiederherstellen von Dateien oder Ordnern für den Server** im Bereich **Aufgaben**.  
  
3.  Der Assistent zum Wiederherstellen von Dateien oder Ordnern wird geöffnet. Befolgen Sie die Anweisungen im Assistenten, um die Dateien oder Ordner wiederherzustellen.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Sicherungen und Wiederherstellungen](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
