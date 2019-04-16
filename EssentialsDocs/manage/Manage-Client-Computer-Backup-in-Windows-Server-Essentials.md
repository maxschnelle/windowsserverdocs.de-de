---
title: Verwalten der Clientcomputersicherung in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b4776e8-9504-4b98-ae80-11da797d9819
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d184c97e47f04b9d7434aaeb0d328761bcfac1c0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-client-computer-backup-in-windows-server-essentials"></a>Verwalten der Clientcomputersicherung in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
 
 Dieses Thema enthält Informationen zu allgemeinen Sicherungsaufgaben für Clientcomputer, die Sie mithilfe von Windows Server Essentials-Dashboard ausführen können, und die folgenden Abschnitte enthält:  
  
-   [Funktionsweise der Standortreparatur-Assistenten die Sicherungsdatenbank](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Verstehen der Einstellungen für die computersicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Sicherung für einen Client-Computer einrichten](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Ändern der Zeit, dass eine Sicherung geplant ist](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Ändern der Aufbewahrungsrichtlinie](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Sicherung auf Standardeinstellungen zurückgesetzt.](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Verwenden von Reparatur-und Wiederherstellungstools](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Reparieren der Sicherungsdatenbank](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Deaktivieren der Sicherung für einen computer](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Ausführen der sicherungsbereinigungsaufgabe](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Anzeigen von Warnungen in der Taskleiste auf einem Clientcomputer](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Anzeigen des Sicherungsstatus über das Launchpad](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [Beenden einer laufenden Sicherung über das Launchpad](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [Starten einer Sicherung über das Launchpad](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [Funktionsweise der computersicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_15)  
  
-   [Tipps zur Vermeidung von Datenverlust aufgrund einer Beschädigung der clientsicherungsdatenbank zu vermeiden.](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_16)  
  
-   [Wiederherstellen von Dateien oder Ordnern aus einer clientcomputersicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_17)  
  
-   [Grundlegendes zum Dateiversionsverlauf](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_FileHistory)  
  
##  <a name="BKMK_1"></a>Funktionsweise der Standortreparatur-Assistenten die Sicherungsdatenbank  
 Wenn Windows Server Essentials Fehler in der Sicherungsdatenbank erkennt, erhalten Sie eine integritätsbenachrichtigung, und der Warnstatus ändert sich in Rot, womit eine kritische Bedingung gekennzeichnet.  
  
 Klicken Sie auf dem Windows Server Essentials-Dashboard auf das Warnstatus-Symbol, um die Benachrichtigung über einen Fehler der Sicherungsdatenbank finden Sie unter. Die Benachrichtigung umfasst eine **Reparatur** Schaltfläche den Assistenten die Sicherungsdatenbank reparieren startet. Des Assistenten möglicherweise mehrere Stunden in Anspruch nehmen.  
  
 Der Assistent überprüft die Sicherungsdatenbank für den ausgewählten Computer und versucht, die Datenbank zu reparieren, wenn Fehler erkannt werden. In einigen Fällen kann nicht den Assistenten für die gesamte Sicherungsdatenbank reparieren. Bevor Sie den Assistenten starten, stellen Sie sicher, dass alle externen Festplatten, mit denen Sie auf dem Server mit dem Server aktiviert ist und ordnungsgemäß angeschlossen sind. Fehler der Sicherungsdatenbank kann möglicherweise automatisch behoben werden, durch das Wiederherstellen der Verbindung einer fehlenden Festplatte.  
  
> [!CAUTION]
>  Sie sollten die Datenbank sichern, bevor Sie versuchen, es zu reparieren. Je nach Typ der in der Sicherungsdatenbank gefundenen Fehler der Assistent einige Sicherungen wiederherstellen möglicherweise nicht. Einige oder alle Sicherungen sind möglicherweise dauerhaft beschädigt.  
  
##  <a name="BKMK_2"></a>Verstehen der Einstellungen für die computersicherung  
 Nachdem die Sicherung für Clientcomputer konfiguriert ist, können Sie ein anderes Zeitfenster für die Sicherung angeben. Auf ähnliche Weise können Sie eine längere oder kürzere Aufbewahrungszeit als Standard festlegen.  
  
 Die **Standard wiederherstellen** Option können Sie das Sicherungsfenster und die Aufbewahrungsrichtlinie auf die Standardeinstellungen während der anfänglichen Sicherungskonfiguration zurücksetzen.  
  
 Die Standardeinstellungen sind:  
  
|Backup-Einstellung|Standardwert|Beschreibung|  
|--------------------|-------------|-----------------|  
|Startzeit|6:00 UHR|Gibt die Zeit, die die tägliche Sicherung beginnt. Es wird empfohlen, dass Sie diese auf einen Zeitpunkt festlegen Wenn Benutzer ihre Computer nicht verwenden.|  
|Endzeit|09:00 UHR|Gibt die Zeit, die die Sicherung abgeschlossen sein muss. Wenn die Sicherung keine Dauer angegeben erforderlich ist, wird nur den Zeitaufwand für den Computer erfolgreich zu sichern.|  
|Tägliche Sicherungen aufbewahren|5 Tage|Gibt die Anzahl von Tagen, die tägliche Sicherungen aufbewahrt werden. Die Standardeinstellung verwenden, sind z. B. 5 tägliche Sicherungen aufbewahrt werden. 6. Tag und jeden Tag danach wird die älteste tägliche Sicherungsdatei gelöscht.|  
|Wöchentliche Sicherungen aufbewahren|4 Wochen|Gibt die Anzahl der Wochen, die die letzte Sicherung der Woche aufbewahrt wird. Verwenden die Standardeinstellungen, sind z. B. 4 wöchentliche Sicherungen aufbewahrt werden. 5. Woche und jede Woche danach wird die älteste wöchentliche Sicherung gelöscht.|  
|Monatliche Sicherungen aufbewahren|6 Monate|Gibt die Anzahl von Monaten, die die letzte Sicherung des Monats aufbewahrt wird. Die Standardeinstellung verwenden, sind z. B. 6 monatliche Sicherungen aufbewahrt werden. Die 7. Monat und jeden Monat danach wird die älteste monatliche Sicherung gelöscht.|  
  
##  <a name="BKMK_3"></a>Sicherung für einen Client-Computer einrichten  
 Wenn die Sicherung deaktiviert ist, können Sie über dem Dashboard Sicherung für den Computer einrichten. Wenn Sie eine Sicherung für einen Computer einrichten, können Sie alle Dateien auf dem Computer sichern, oder wählen Sie die Volumes und Ordner, die Sie sichern möchten.  
  
> [!NOTE]
>  Der Computer muss für Sie Einrichten der Sicherung online sein.  
  
> [!IMPORTANT]
>   Windows Server Essentials wird nicht unterstützt, Sichern und Wiederherstellen von dynamischen Datenträgern auf Clientcomputern.  
  
#### <a name="to-set-up-backup-for-a-client-computer"></a>Zum Einrichten der Sicherung für einen Clientcomputer  
  
1.  Öffnen der **Dashboard**, und klicken Sie dann auf die **Geräte** Registerkarte.  
  
2.  Klicken Sie auf den Namen des Clientcomputers, die zum Einrichten der Sicherung für, und klicken Sie dann im sollen die **Aufgaben** Bereich, klicken Sie auf **Sicherung für diesen Computer einrichten**.  
  
    > [!NOTE]
    >  Wenn die Sicherung für den Clientcomputer bereits eingerichtet ist **Sicherung für diesen Computer anpassen** steht in den **Aufgaben** Bereich anstelle von **Sicherung für diesen Computer einrichten**.  
  
3.  In der Sicherung Assistenten zum einrichten können Sie alle Ordner sichern oder bestimmte Ordner, die Sie sichern möchten. Folgen Sie den Anweisungen im Assistenten aus.  
  
4.  Klicken Sie auf **schließen** Wenn Sicherung einrichten für den Computer festgelegt ist.  
  
### <a name="critical-system-files"></a>Wichtige Systemdateien  
 Wenn Sie das Windows-Betriebssystem installieren, erstellt das Setupprogramm Ordner auf dem Systemlaufwerk, in dem Dateien gespeichert werden, die das System zum Starten und Ausführen benötigt. Wichtige Systemdateien gehören Dateien mit der DLL-Datei, .exe, .ocx und Sys. Einige dieser Dateien sind True Type-Schriftarten. Darüber hinaus sind Systemstatusdateien, z. B. die systemregistrierung s erforderlich für das Betriebssystem ordnungsgemäß ausgeführt.  
  
### <a name="find-the-file-you-are-looking-for"></a>Suchen Sie die Datei, die Sie suchen  
 Sie können alle Ordner für einen Computer, mehrere Dateien und Ordner, oder eine einzelne Datei oder Ordner aus einer vorhandenen Sicherung wiederherstellen.  
  
 Nachdem Sie die Sicherung, die Sie verwenden auswählen, um aus wiederherstellen möchten, die Sicherungsdatei gelesen, und alle Dateien und Ordner angezeigt. Sie können einen Drilldown auf die Datei oder den Ordner wiederherstellen, indem Sie auf die Ordner der obersten Ebene doppelklicken und dann durchblättern, die Hierarchie der Ordner, bis Sie die Datei suchen, die Sie suchen.  
  
### <a name="why-am-i-unable-to-select-some-items"></a>Warum kann ich nicht einige Elemente auswählen?  
 Das Kontrollkästchen auf der das Auswahlmenü der **Elemente zum Sichern von Seite auswählen** kann verschiedene Status für jeden Ordner angeben. Wenn das Kontrollkästchen ist:  
  
-   **Ausgewählte**, die zugehörigen Ordner und Ordnerinhalte werden für die Sicherung ausgewählt.  
  
-   **Nicht ausgewählte**, die zugehörigen Ordner und Ordnerinhalte werden von der Sicherung ausgeschlossen.  
  
-   **Solid**, die zugehörige Ordner für die Sicherung ausgewählt ist, aber ein oder mehrere Elemente in diesem Ordner werden aus der Sicherung ausgeschlossen.  
  
 Wenn Sie einen bestimmten Ordner auswählen können:  
  
-   Das Volume kann für die Sicherung konfiguriert sein, aber möglicherweise offline. Dies tritt häufig bei USB-Wechseldatenträger. Volumes, die offline sind, werden im grauem Text angezeigt.  
  
-   Sie können nur Daten von einem lokalen Laufwerk sichern, die als NTFS-Dateisystem formatiert sind. Laufwerke, die als FAT-(und FAT32) oder ReFS-Dateisysteme in der Liste der zu sichernden Laufwerke nicht angezeigt werden formatiert.  
  
> [!IMPORTANT]
>  Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) unterstützt nicht das Erstellen einer Schattenkopie eines virtuellen Volumes und des Hostvolumes in demselben Snapshotsatz. VSS unterstützt Erstellen von Snapshots von Volumes auf einer virtuellen Festplatte (VHD), wenn eine Sicherung des virtuellen Volumes erforderlich ist. Weitere Informationen finden Sie unter [warten und Sichern virtueller Festplatten](https://go.microsoft.com/fwlink/p/?LinkId=256577).  
  
##  <a name="BKMK_4"></a>Ändern der Zeit, dass eine Sicherung geplant ist  
 Der Sicherungsvorgang sollten in einer Zeit geplant werden, wenn möglichst wenige Personen ihren Netzwerkcomputer verwenden. Dies ist in der Regel am späten Abend oder frühen morgen. Die Standardeinstellung für die Sicherung ist 18:00 Uhr bis 18:00 Uhr. Der Server versucht, die Clientcomputer nur während der geplanten Zeitfensters zu sichern.  
  
 Wenn Ihr Unternehmen während dieser Arbeitszeiten aktiv ist, sollten Sie diese Standardeinstellungen ändern.  
  
#### <a name="to-change-the-time-that-backup-is-scheduled-to-run"></a>So ändern Sie den Zeitraum für eine geplante Sicherung ausführen  
  
1.  Öffnen Sie den Server **Dashboard**, und klicken Sie dann auf **Geräte**.  
  
2.  In **Geräteaufgaben**, klicken Sie auf **Einstellungen anpassen Computersicherung und Dateiversionsverlauf**.  
  
    > [!NOTE]
    >  In Windows Server Essentials, wurde diese Aufgabe umbenannt **Clientcomputer-Sicherungsaufgaben**.  
  
3.  In **Client Computer backup Einstellungen und Tools für**auf die **Computersicherung** Registerkarte können Sie die Start- und Endzeiten je nach Bedarf ändern.  
  
4.  Klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_5"></a>Ändern der Aufbewahrungsrichtlinie  
 Tägliche Sicherungen von allen Computern gesammelt, auf dem Server mit der Zeit. Um diese Sicherungen verwalten können, können Windows Server Essentials die Datenbank mit computersicherungen zu verwalten. Sie können konfigurieren, wie viele Sicherungen für alle Computer beibehalten.  
  
 Die sicherungsaufbewahrungsrichtlinie bestimmt, wie lange eine Sicherung gespeichert wird, bevor es während des Bereinigungsvorgangs gelöscht wird. Die sicherungsbereinigung wird jeden Samstag um 23:59 Uhr ausgeführt. Es löscht alle Sicherungen, die außerhalb der sicherungsaufbewahrungsrichtlinie liegen. Die Standardeinstellungen für die sicherungsaufbewahrungsrichtlinie sind:  
  
-   **Tägliche Sicherungen 5 Tage lang aufbewahren.** Die erste Sicherung des Tages wird als tägliche Sicherung aufbewahrt. Nach 5 Tagen wird die älteste tägliche Sicherung während des Bereinigungsvorgangs gelöscht.  
  
-   **4 Wochen wöchentliche Sicherung aufbewahren.** Die erste Sicherung der Woche wird als wöchentliche Sicherung aufbewahrt. Nach 4 Wochen wird die älteste wöchentliche Sicherung während des Bereinigungsvorgangs gelöscht.  
  
-   **Monatliche Sicherungen 6 Monate lang aufbewahren.** Die erste Sicherung des Monats wird als monatliche Sicherung aufbewahrt. Nach 6 Monaten wird die älteste monatliche Sicherung während des Bereinigungsvorgangs gelöscht.  
  
#### <a name="to-change-the-computer-backup-retention-policy"></a>So ändern Sie die Aufbewahrungsrichtlinie  
  
1.  Öffnen der **Dashboard**.  
  
2.  Klicken Sie auf **Geräte**.  
  
3.  In der **Geräteaufgaben** Bereich, klicken Sie auf **Einstellungen anpassen Computersicherung und Dateiversionsverlauf**.  
  
    > [!NOTE]
    >  In Windows Server Essentials, wurde diese Aufgabe umbenannt **Clientcomputer-Sicherungsaufgaben**.  
  
4.  In **Client Computer backup Einstellungen und Tools für**in der **Client Computer backup Retention Policy** nehmen die Änderungen an der Aufbewahrungsrichtlinie die Ihren Bedürfnissen entspricht.  
  
5.  Wenn Sie fertig sind, klicken Sie auf **OK** gelten die Änderungen und das Dialogfeld zu schließen. Die aktualisierte Aufbewahrungsrichtlinie wird die beim nächsten Start der sicherungsbereinigung angewendet werden.  
  
    > [!NOTE]
    >  Die aktualisierte Aufbewahrungsrichtlinie gilt für alle Clientcomputer im Netzwerk, die für die Sicherung konfiguriert sind.  
  
##  <a name="BKMK_6"></a>Sicherung auf Standardeinstellungen zurückgesetzt.  
 Nachdem die Sicherung für Clientcomputer konfiguriert ist, kann der Netzwerkadministrator ein anderes Zeitfenster angegeben haben. Auf ähnliche Weise kann der Administrator eine längere oder kürzere Aufbewahrungszeit als die Standardeinstellung angegeben haben. Die **auf Standardeinstellungen zurücksetzen** Schaltfläche können Sie das Sicherungsfenster und die Aufbewahrungsrichtlinie auf die Standardeinstellungen während der anfänglichen Sicherungskonfiguration zurücksetzen.  
  
 Die Standardeinstellungen sind:  
  
-   Startzeit Sicherung: 18:00 Uhr  
  
-   Endzeit: 9:00 Uhr  
  
-   Anzahl von Tagen, die tägliche Sicherungen aufbewahrt werden: 5 Tage  
  
-   Anzahl der Wochen, die die letzte Sicherung der Woche aufbewahrt wird: 4 Wochen  
  
-   Anzahl von Monaten, die die letzte Sicherung des Monats aufbewahrt wird: 6 Monate  
  
#### <a name="to-reset-computer-backup-to-the-default-settings"></a>Sicherung auf die Standardeinstellungen zurücksetzen  
  
1.  Öffnen Sie die **Dashboard**, und öffnen Sie dann die **Geräte** Seite.  
  
2.  In **Geräteaufgaben**, klicken Sie auf **Einstellungen anpassen Computersicherung und Dateiversionsverlauf**.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Clientcomputer-Sicherungsaufgaben**.  
  
3.  Auf der **Computersicherung** auf der Registerkarte der **Client-Computer und Sicherung Einstellungen und Tools für** auf **auf Standardeinstellungen zurücksetzen**.  
  
    > [!NOTE]
    >  Sie möchten Sie den benutzerdefinierten Zeitplan und die aufbewahrungsrichtlinieneinstellungen zu schreiben, da sie nicht mehr vorhanden sind, wenn Sie auf die Standardeinstellungen zurücksetzen.  
  
4.  Klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_7"></a>Verwenden von Reparatur-und Wiederherstellungstools  
 **Sicherungen reparieren:** , wenn die Datenbank mit computersicherungen aus irgendeinem Grund beschädigt oder unbrauchbar wird, können Sie versuchen, mithilfe der Assistenten die Sicherungsdatenbank Reparieren der Datenbank zu reparieren. Der Assistent analysiert die Sicherungsdateien, um festzustellen, ob Probleme auftreten, die nicht repariert werden können. Der Assistent versucht anschließend, Probleme zu beheben, die gefunden werden.  
  
> [!WARNING]
>  Wenn das Problem nicht behoben werden kann, kann der Assistent eine Sicherungsdatei Computer dauerhaft löschen.  
  
 **Computerwiederherstellung:** können einen startbaren USB-Speicherstick verwenden, um einen Computer aus einer vorhandenen Sicherung wiederherzustellen. Sie müssen einen USB-Speicherstick, der 1 GB verwenden oder größer. Nachdem das startbare USB-Flashlaufwerk erstellt wurde, stecken Sie ihn in den Computer, den Sie wiederherstellen möchten, und starten Sie dann mit dem USB-Speicherstick, um die vollständige Systemwiederherstellung zu starten.  
  
##  <a name="BKMK_8"></a>Reparieren der Sicherungsdatenbank  
 Wenn Sie eine Warnung besagt erhalten, dass der Computer Sicherungsdatenbank Probleme aufweist, können Sie versuchen, sie zu reparieren.  
  
#### <a name="to-repair-the-backup-database"></a>Reparieren die Sicherungsdatenbank  
  
1.  Öffnen der **Dashboard**.  
  
2.  Klicken Sie auf **Geräte**.  
  
3.  In der **Geräteaufgaben** Bereich, klicken Sie auf **Einstellungen anpassen Computersicherung und Dateiversionsverlauf.**  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Clientcomputer-Sicherungsaufgaben**.  
  
4.  In **Client Computer backup Einstellungen und Tools für**, klicken Sie auf die **Tools** Registerkarte.  
  
5.  In der **Sicherungen reparieren** auf **jetzt reparieren**. Der Standortreparatur-Assistenten die Sicherungsdatenbank wird geöffnet.  
  
6.  Folgen Sie den Anweisungen in den Assistenten die Sicherungsdatenbank reparieren.  
  
7.  Je nach Umfang kann der Sicherungsdatenbank, die Reparatur der Datenbank mehrere Stunden in Anspruch nehmen. Klicken Sie auf **schließen**, und klicken Sie dann auf **OK** zum Schließen der **Einstellungen anpassen Computersicherung und Dateiversionsverlauf** Seite.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Client Computer backup Einstellungen und Tools für**.  
  
#### <a name="to-review-the-results-of-the-backup-database-repair"></a>So überprüfen die Ergebnisse der Reparatur der Sicherungsdatenbank  
  
1.  Öffnen der **Dashboard**.  
  
2.  Klicken Sie auf **Geräte**.  
  
3.  In der **Geräteaufgaben** Bereich, klicken Sie auf **Einstellungen anpassen Computersicherung und Dateiversionsverlauf.**  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Clientcomputer-Sicherungsaufgaben**.  
  
4.  In **Client Computer backup Einstellungen und Tools für**, klicken Sie auf die **Tools** Registerkarte.  
  
5.  Die Ergebnisse werden angezeigt, dem **Sicherungen reparieren** Abschnitt.  
  
##  <a name="BKMK_9"></a>Deaktivieren der Sicherung für einen computer  
 Verwenden Sie das Dashboard, um Sicherungen für Computer in Ihrem Netzwerk schnell zu deaktivieren.  
  
#### <a name="to-disable-backup-for-a-computer"></a>So deaktivieren Sie Sicherung für einen computer  
  
1.  Öffnen der **Dashboard**.  
  
2.  Klicken Sie auf die **Geräte** Registerkarte.  
  
3.  Klicken Sie auf den Namen des Computers, für die Sie Sicherungen deaktivieren möchten.  
  
4.  Klicken Sie im Bereich Aufgaben auf **Sicherung für den Computer anpassen**. Der Assistent zum Anpassen der Sicherung wird angezeigt.  
  
5.  Klicken Sie auf **deaktiviert die Sicherung für diesen Computer**, und wählen Sie dann, ob Sie die vorhandenen Sicherungsdateien gelöscht oder beibehalten möchten.  
  
6.  Klicken Sie auf **Änderungen speichern**, und klicken Sie dann auf **schließen**.  
  
 Informationen dazu, wie Sie die Sicherung für einen Computer aktivieren, nachdem die Sicherung deaktiviert wurde, finden Sie unter [Sicherung für einen Clientcomputer einrichten](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_3).  
  
##  <a name="BKMK_10"></a>Ausführen der sicherungsbereinigungsaufgabe  
 Die Bereinigungsaufgabe der Client Computer backup ist geplant, um 23:59 Uhr jeden Samstag, nachdem alle Sicherungen durchgeführt wurden ausgeführt. Die Bereinigungsaufgabe löscht Sicherungen aus der Datenbank mit clientcomputersicherungen gemäß der Aufbewahrungsrichtlinie. Die Standardeinstellungen für die sicherungsaufbewahrungsrichtlinie sind:  
  
-   Anzahl von Tagen, die tägliche Sicherungen aufbewahrt werden: 5 Tage  
  
-   Anzahl der Wochen, die die letzte Sicherung der Woche aufbewahrt wird: 4 Wochen  
  
-   Anzahl von Monaten, die die letzte Sicherung des Monats aufbewahrt wird: 6 Monate  
  
 Informationen zum Ändern der sicherungsaufbewahrungsrichtlinie finden Sie unter [Ändern der Aufbewahrungsrichtlinie](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
#### <a name="to-run-the-client-backup-database-cleanup-task"></a>Der Client Sicherungsdatenbank Bereinigungsaufgabe ausführen  
  
1.  Melden Sie sich an den Server mit Ihrem Benutzerkonto und Kennwort an.  
  
2.  Öffnen Sie auf dem Server **Taskplaner**. Sie erreichen die aufgabenplanung über die **Verwaltung** Konsole.  
  
3.  Erweitern Sie im Taskplaner **Aufgabenplanungsbibliothek**, erweitern Sie **Microsoft**, erweitern Sie **Windows**, und klicken Sie dann auf **Windows Server Essentials**.  
  
4.  Klicken Sie auf die **Sicherungsbereinigung** , und klicken Sie dann auf **ausführen** in der **Aktionen** Bereich. Der Status wechselt zu **mit** bis der Vorgang abgeschlossen ist.  
  
##  <a name="BKMK_11"></a>Anzeigen von Warnungen in der Taskleiste auf einem Clientcomputer  
 Sie können eine Sicherung Meldung in der Taskleiste auf Ihrem Computer aus den folgenden Gründen angezeigt:  
  
-   Eine Sicherung wurde gestartet.  
  
-   Eine Sicherung wurde beendet.  
  
-   Es ist keine aktuelle erfolgreiche Sicherung. Die Anzahl der Tage seit die letzte erfolgreiche Sicherung in der Benachrichtigung enthalten ist.  
  
-    Nur Windows Server Essentials: wird ein neues Volume auf Ihrem Computer hinzugefügt. Die Person, die das Netzwerk verwaltet muss der Assistent zum Anpassen von Sicherung einzuschließenden oder schließen Sie das Volume für zukünftige Sicherungen ausgeführt.  
  
##  <a name="BKMK_12"></a>Anzeigen des Sicherungsstatus über das Launchpad  
 Verwenden Sie das Launchpad, um schnell den Sicherungsstatus für den Computer anzuzeigen.  
  
> [!TIP]
>  Bewegen Sie für einen schnellen Überblick den Cursor über das Launchpad-Symbol im Infobereich des Desktops. Der Sicherungsstatus wird als QuickInfo angezeigt.  
  
#### <a name="to-view-status-of-a-backup-for-your-computer"></a>Anzeigen des Sicherungsstatus für Ihren computer  
  
1.  Melden Sie sich bei der **Launchpad** mit Ihrem Benutzernamen und Kennwort.  
  
2.  Klicken Sie auf **Sicherung**.  
  
3.  In der **Eigenschaften der Sicherung** Dialogfeld, in der **Sicherungsstatus** Bereich, den Status der Sicherung wird angezeigt.  
  
    -   **Keine früheren Sicherungen**: entweder Sicherung wurde noch nicht ausgeführt oder der Sicherungsverlauf wurde gelöscht.  
  
    -   **Sicherung ausstehend**: eine Sicherung wartet auf einen anderen Prozess auf dem Server abgeschlossen.  
  
    -   **Herstellen einer Verbindung**: Sicherung stellt eine Verbindung mit dem Server her.  
  
    -   **Kann keine Verbindung herstellen**: Sicherung keine Verbindung mit Windows Server Client Computer Backup Provider Service herstellen.  
  
        > [!NOTE]
        >  Dieser Dienst wurde in Windows Server Essentials, Windows Server Essentials-Verwaltungsdienst umbenannt.  
  
    -   **Sicherung läuft**: Zeigt den abgeschlossenen Prozentsatz der Sicherung.  
  
    -   **Sicherung wurde abgebrochen**: Zeigt das Datum und Uhrzeit, zu der die Sicherung gestartet wurde, wenn Sie oder der Netzwerkadministrator die Sicherung abgebrochen haben.  
  
    -   **Sicherung erfolgreich**: Zeigt das Datum und Uhrzeit, zu der die Sicherung gestartet wurde, wenn die Sicherung erfolgreich abgeschlossen wurde.  
  
    -   **Sicherung war nicht vollständig**: Zeigt das Datum und Uhrzeit, zu der die Sicherung gestartet wurde, wenn die Sicherung nicht erfolgreich abgeschlossen wurde.  
  
    -   **Sicherung war nicht erfolgreich**: Zeigt das Datum und Uhrzeit, zu der die Sicherung gestartet wurde, wenn die Sicherung nicht erfolgreich abgeschlossen wurde.  
  
4.  Klicken Sie auf **OK** zum Schließen der **Eigenschaften der Sicherung** Dialogfeld.  
  
##  <a name="BKMK_13"></a>Beenden einer laufenden Sicherung über das Launchpad  
 Sie können eine Sicherung problemlos beenden, die gerade ausgeführt wird.  
  
#### <a name="to-stop-a-backup-in-progress"></a>Um eine laufende Sicherung beenden  
  
1.  Öffnen der **Launchpad**.  
  
    > [!NOTE]
    >  Wenn Sie aufgefordert werden, melden Sie sich auf die **Launchpad** mit Ihrem Benutzernamen und Kennwort.  
  
2.  Klicken Sie auf **Sicherung**.  
  
3.  In der **Eigenschaften der Sicherung** Dialogfeld, in der **Sicherungsstatus** Abschnitt der **Sicherung starten** Schaltfläche ändert sich in **Sicherung beenden** bei der Sicherung ausgeführt wird. Klicken Sie auf **Sicherung beenden**, und klicken Sie dann auf **Ja** zu bestätigen. Die Sicherung wird weiterhin ausgeführt, bis Sie auf **Ja**.  
  
4.  Wenn Sie eine laufende Sicherung beenden, ändert sich der Status in **Sicherung wurde abgebrochen** mit Datum und Uhrzeit, zu der die Sicherung gestartet wurde. Wenn Sie stattdessen den Status finden Sie unter **erfolgreich**, **unvollständig**, oder **Fehler**, die letzte Sicherung bereits beendet.  
  
5.  Klicken Sie auf **OK** zum Schließen der **Eigenschaften der Sicherung** Dialogfeld.  
  
##  <a name="BKMK_14"></a>Starten einer Sicherung über das Launchpad  
 Möglicherweise gibt es Zeiten, wenn Sie sichern möchten Sie Ihre Dateien und Ordner vor der eigentlich geplanten Zeitpunkt der Sicherung auf dem Server einrichten. Das Launchpad können Sie die Sicherung des Computers manuell initiieren.  
  
#### <a name="to-start-a-backup"></a>So starten Sie eine Sicherung  
  
1.  Öffnen der **Launchpad**.  
  
    > [!NOTE]
    >  Wenn Sie aufgefordert werden, melden Sie sich auf die **Launchpad** mit Ihrem Benutzernamen und Kennwort.  
  
2.  Klicken Sie auf **Sicherung**.  
  
3.  In der **Eigenschaften der Sicherung** Dialogfeld, in der **Sicherungsstatus** auf **Sicherung starten**, und klicken Sie dann auf **OK**.  
  
4.  Geben Sie eine Beschreibung für die Sicherung, und klicken Sie dann auf **OK**. Der Status wechselt zu **Sicherung**, und wählen Sie dann **Sicherung wird ausgeführt** wobei der abgeschlossene Prozentsatz.  
  
5.  Nach der Sicherung gestartet wurde, ändert sich die Schaltfläche zum **Sicherung beenden**. Wenn die Sicherung ausgeführt wird und Sie möchten, beenden, klicken Sie auf **Sicherung beenden**, und klicken Sie dann auf **Ja**. Wenn Sie eine laufende Sicherung beenden, ändert sich der Status in **Sicherung wurde abgebrochen** mit Datum und Uhrzeit, zu der die Sicherung gestartet wurde.  
  
6.  Wenn die Sicherung erfolgreich abgeschlossen wird, ändert sich der Status in **Sicherung erfolgreich** mit Datum und Uhrzeit, zu der die abgeschlossene Sicherung gestartet wurde.  
  
7.  Klicken Sie auf **OK** zum Schließen der **Eigenschaften der Sicherung** Dialogfeld.  
  
##  <a name="BKMK_15"></a>Funktionsweise der computersicherung  
 Während der Sicherung passiert täglich Folgendes:  
  
-   Computern im Netzwerk gesichert werden nacheinander.  
  
-   Eine Sicherung, die in Bearbeitung ist abgeschlossen ist, auch wenn Sie das Sicherungsfenster schließen.  
  
-   Windows-Updates installiert sind, und Windows Server Essentials neu gestartet wird (falls erforderlich).  
  
-   Am Sonntag wird die Sicherungsbereinigung ausgeführt.  
  
> [!IMPORTANT]
>  Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) unterstützt nicht das Erstellen einer Schattenkopie eines virtuellen Volumes und des Hostvolumes in demselben Snapshotsatz. VSS unterstützt Erstellen von Snapshots von Volumes auf einer virtuellen Festplatte (VHD), wenn eine Sicherung des virtuellen Volumes erforderlich ist. Weitere Informationen finden Sie unter [warten und Sichern virtueller Festplatten](https://go.microsoft.com/fwlink/p/?LinkId=256577).  
  
##  <a name="BKMK_16"></a>Tipps zur Vermeidung von Datenverlust aufgrund einer Beschädigung der clientsicherungsdatenbank zu vermeiden.  
 Wenn die clientsicherungsdatenbank beschädigt wird, können Sie wichtige Daten verlieren.  
  
 Um Datenverluste aufgrund einer Beschädigung der clientsicherungsdatenbank zu vermeiden, ist Folgendes zu berücksichtigen:  
  
-   Eine weitere Methode zum Sichern der clientsicherungsdatenbank zu aktivieren. Beispielsweise je nach der Version von Windows Server Essentials, die Sie ausführen, verwenden Sie Serversicherung, Onlinesicherung oder Microsoft Azure Backup, um die Datenbank zu sichern.  
  
    > [!IMPORTANT]
    >  Stellen Sie sicher, dass Sie so sichern Sie alle Dateien in der **Clientcomputersicherungen** Ordner.  
  
-   Für den Fall, dass Sie die Datenbank wiederherstellen müssen, müssen Sie zum Wiederherstellen aller Dateien in der **Clientcomputersicherungen** Ordner. Wenn Sie nicht alle Dateien wiederherstellen, kann die Datenbank inkonsistent geworden.  
  
-   Bevor Sie bereinigen oder die clientsicherungsdatenbank wiederherstellen, stellen Sie sicher, dass alle Clientsicherungen beendet, die derzeit ausgeführt werden.  
  
     Wenn Sie Windows Server Essentials ausgeführt werden, sollten Sie auch die Windows Server Client Computer Backup Service und Windows Server Client Computer Backup Provider Service beenden.  
  
     Wenn Sie Windows Server Essentials ausgeführt werden, sollten Sie auch den Windows Server Backup-Dienst beenden.  
  
     Starten Sie nach Abschluss des Wiederherstellungsvorgangs den Dienst neu.  
  
##  <a name="BKMK_17"></a>Wiederherstellen von Dateien oder Ordnern aus einer clientcomputersicherung  
 Sie können navigieren und einzelne Dateien und Ordner aus einer Sicherung wiederherstellen.  
  
> [!NOTE]
>  Sie können keine Dateien und Ordner auf einem Clientcomputer wiederherstellen, mithilfe des Dashboards auf dem Server. Öffnen Sie das Dashboard auf einem Clientcomputer, um den Vorgang abzuschließen.  
  
> [!IMPORTANT]
>  Sie können keine Dateien und Ordner auf einer Festplatte wiederherstellen, die als dynamischer Datenträger konfiguriert wurde.  
  
#### <a name="to-restore-files-and-folders"></a>Wiederherstellen von Dateien und Ordnern  
  
1.  Öffnen der **Dashboard** auf einem Clientcomputer.  
  
2.  Klicken Sie auf die **Geräte** Registerkarte.  
  
3.  Klicken Sie auf dem Computer für die Sie Dateien und Ordner wiederherstellen, und klicken Sie dann auf möchten **Wiederherstellen von Dateien oder Ordner für den Computer** in der **Aufgaben** Bereich. Das Wiederherstellen von Dateien oder Ordner-Assistent wird geöffnet.  
  
4.  Folgen Sie den Anweisungen im Assistenten aus.  
  
##  <a name="BKMK_FileHistory"></a>Grundlegendes zum Dateiversionsverlauf  
 Die Dateiversionsverlauf-Funktion von Windows Server Essentials sichert automatisch Dateien, die in den Ordnern "Bibliotheken", "Kontakte", "Desktop" und "Favoriten" von Computern im Netzwerk sind, die Dateiversionsverlauf-Funktion aktiviert haben. Wenn die Originaldateien verloren gehen, beschädigt oder gelöscht werden, können Sie diese wiederherstellen. Sie können auch verschiedene Versionen der Dateien von einem bestimmten Punkt Zeitpunkten. Im Laufe der Zeit verfügen Sie über einen vollständigen Verlauf Ihrer Dateien.  
  
 In Windows Server Essentials können Sie Einstellungen für Dateiversionsverlauf von Anpassen der **Dateiversionsverlauf** Seite **Client Computer backup Einstellungen und Tools für**.  
  
 Sie können Einstellungen des Dateiversionsverlaufs in Windows Server Essentials anpassen, indem Sie zu der **Benutzer** Registerkarte, und wählen Sie dann die **ändern Sie die Dateiversionsverlauf-Einstellung** Aufgabe.  
  
 Die Seite "Dateiversionsverlauf" bietet die folgenden Optionen:  
  
|Backup-Einstellung|Standardwert|Beschreibung|  
|--------------------|-------------|-----------------|  
|Einschalten / ausschalten|Auf|Dateiversionsverlauf ist standardmäßig aktiviert, wenn Sie Windows Server Essentials installieren.|  
|Sicherung von Daten|Dokumente und Desktop|Es gibt drei vorkonfigurierte Einstellungen, die Ihnen ermöglichen, eine Vielzahl von sicherungslösungen angeben. Sie können eine der folgenden Optionen auswählen:<br /><br /> -Dokumente und Desktop<br /><br /> -Alle Bibliotheken, Desktop, Kontakte und Favoriten<br /><br /> -Alle Daten in Bibliotheken, Desktop, Kontakte und Favoriten Ausschließen von Daten in der Musik, Videos und Bilder Bibliotheken|  
|Sicherungshäufigkeit|Einmal pro Stunde|Gibt an, wie oft der Dateiversionsverlauf eine Sicherung der ausgewählten Daten erstellt. Sie können dieses Bereichs von 10 Minuten in täglich zwischen mehreren Optionen auswählen.|  
|Aufbewahrungsdauer der Kopien|1 Jahr|Gibt die Zeitspanne, die Dateiversionsverlauf eine Kopie einer Sicherung verfügen.|  
  
 Informationen zu Problemen mit dem Dateiversionsverlauf finden Sie unter [Problembehandlung beim Dateiversionsverlauf](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
