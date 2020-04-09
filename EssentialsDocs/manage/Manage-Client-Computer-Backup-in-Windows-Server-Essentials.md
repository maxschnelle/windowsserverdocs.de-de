---
title: Verwalten der Clientcomputersicherung in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 1b4776e8-9504-4b98-ae80-11da797d9819
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ae59fb050b41cef866a8f0e97d8d07d28b54ca52
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852823"
---
# <a name="manage-client-computer-backup-in-windows-server-essentials"></a>Verwalten der Clientcomputersicherung in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 Dieses Thema enthält Informationen zu allgemeinen Sicherungsaufgaben für Clientcomputer, die Sie mithilfe des Windows Server Essentials-Dashboards ausführen können. Dieses Themas enthält die folgenden Abschnitte:  
  
-   [Funktionsweise des Assistenten zum Reparieren der Sicherungs Datenbank](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Informationen zu den Einstellungen für die Computer Sicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Einrichten der Sicherung für einen Client Computer](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Ändern der Zeit, zu der die Ausführung der Sicherung geplant ist](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Ändern der Aufbewahrungs Richtlinie für die Computer Sicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Sicherung auf Standardeinstellungen zurücksetzen](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Verwenden von Reparatur-und Wiederherstellungs Tools](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Reparieren der Sicherungs Datenbank](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Deaktivieren der Sicherung für einen Computer](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Ausführen der Sicherungs Bereinigungs Aufgabe](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Anzeigen von Warnungen in der Taskleiste auf einem Client Computer](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Anzeigen des Sicherungs Status über das launchpad](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [Beendet eine laufende Sicherung aus dem launchpad.](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [Starten einer Sicherung über das launchpad](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [Funktionsweise der Computer Sicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_15)  
  
-   [Tipps zur Vermeidung von Datenverlusten aufgrund einer Beschädigung der Client Sicherungs Datenbank](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_16)  
  
-   [Wiederherstellen von Dateien oder Ordnern aus einer Client Computer Sicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_17)  
  
-   [Grundlegendes zum Datei Verlauf](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_FileHistory)  
  
##  <a name="how-the-repair-the-backup-database-wizard-works"></a><a name="BKMK_1"></a>Funktionsweise des Assistenten zum Reparieren der Sicherungs Datenbank  
 Wenn Windows Server Essentials einen Fehler in der Sicherungsdatenbank erkennt, erhalten Sie eine Integritätsbenachrichtigung, und der Warnstatus ändert sich in Rot, womit eine kritische Bedingung gekennzeichnet wird.  
  
 Klicken Sie im Windows Server Essentials-Dashboard auf das Warnstatus-Symbol, um die Benachrichtigung über einen Fehler der Sicherungsdatenbank anzuzeigen. Die Benachrichtigung enthält eine Schaltfläche **Reparieren**, über die der Assistent "Die Sicherungsdatenbank reparieren" gestartet werden kann. Es kann möglicherweise mehrere Stunden dauern, bis der Assistent abgeschlossen ist.  
  
 Der Assistent überprüft die Sicherungsdatenbank für den ausgewählten Computer und versucht, die Datenbank zu reparieren, wenn Fehler erkannt werden. In einigen Fällen kann der Assistent nicht die gesamte Sicherungsdatenbank reparieren. Bevor Sie den Assistenten starten, stellen Sie sicher, dass alle externen Festplatten, die Sie verwenden, mit dem Server verbunden und aktiviert sind und ordnungsgemäß funktionieren. Der Fehler der Sicherungsdatenbank kann möglicherweise automatisch behoben werden, indem Sie die Verbindung einer fehlenden Festplatte erneut herstellen.  
  
> [!CAUTION]
>  Sie sollten die Datenbank sichern, bevor Sie versuchen, sie zu reparieren. Je nach Fehlertyp in der Sicherungsdatenbank kann der Assistent unter Umständen einige Sicherungen nicht wiederherstellen. Einige oder alle Sicherungen sind möglicherweise dauerhaft beschädigt.  
  
##  <a name="understand-the-computer-backup-settings"></a><a name="BKMK_2"></a>Informationen zu den Einstellungen für die Computer Sicherung  
 Nachdem die Sicherung für Clientcomputer konfiguriert wurde, können Sie für die Ausführung der Sicherung ein anderes Zeitfenster festlegen. Gleichermaßen können Sie eine längere oder kürzere Aufbewahrungszeit als die Standardzeit festlegen.  
  
 Mithilfe der Option **Standard wiederherstellen** können Sie das Sicherungsfenster und die Aufbewahrungsrichtlinie während der anfänglichen Sicherungskonfiguration auf die Standardeinstellungen zurücksetzen.  
  
 Die Standardwerte sind:  
  
|Sicherungseinstellung|Standard|Beschreibung|  
|--------------------|-------------|-----------------|  
|Startzeit|18:00 Uhr|Gibt die Uhrzeit an, zu der die tägliche Sicherung beginnt. Es wird empfohlen, eine Zeit festzulegen, zu der kein Benutzer seinen Computer verwendet.|  
|Endzeit|9:00 Uhr|Gibt die Zeit an, zu der die Sicherung abgeschlossen sein muss. Wenn für die Sicherung keine Dauer angegeben werden muss, wird nur die Zeit verwendet, die zum erfolgreichen Erstellen einer Sicherungskopie des Computers erforderlich ist.|  
|Tägliche Sicherungen aufbewahren|5 Tage|Gibt die Anzahl an Tagen an, die tägliche Sicherungen aufbewahrt werden. Wenn Sie beispielsweise die Standardeinstellung verwenden, werden 5 tägliche Sicherungen aufbewahrt. Am sechsten Tag und jeden Tag danach wird die jeweils älteste tägliche Sicherungsdatei gelöscht.|  
|Wöchentliche Sicherungen aufbewahren|4 Wochen|Gibt die Anzahl an Wochen an, die die letzte Sicherung der Woche aufbewahrt wird. Wenn Sie beispielsweise die Standardeinstellung verwenden, werden 4 wöchentliche Sicherungen aufbewahrt. In der fünften Woche und jede Woche danach wird die jeweils älteste wöchentliche Sicherung gelöscht.|  
|Monatliche Sicherungen aufbewahren|6 Monate|Gibt die Anzahl an Monaten an, die die letzte Sicherung des Monats aufbewahrt wird. Wenn Sie beispielsweise die Standardeinstellung verwenden, werden 6 monatliche Sicherungen aufbewahrt. Im siebten Monat und jeden Monat danach wird die jeweils älteste monatliche Sicherung gelöscht.|  
  
##  <a name="set-up-backup-for-a-client-computer"></a><a name="BKMK_3"></a>Einrichten der Sicherung für einen Client Computer  
 Wenn die Sicherung deaktiviert ist, können Sie die Sicherung für den Computer über das Dashboard festlegen. Beim Einrichten der Sicherung für einen Computer können Sie festlegen, dass der gesamte Computer oder einzelne Volumes und Ordner gesichert werden sollen.  
  
> [!NOTE]
>  Zum Einrichten der Sicherung muss der Computer online sein.  
  
> [!IMPORTANT]
>   Windows Server Essentials bietet keine Unterstützung für das Sichern und Wiederherstellen dynamischer Datenträger auf Client Computern.  
  
#### <a name="to-set-up-backup-for-a-client-computer"></a>So richten Sie eine Sicherung für einen Clientcomputer ein  
  
1.  Öffnen Sie das **Dashboard**, und klicken Sie auf die Registerkarte **Geräte**.  
  
2.  Klicken Sie auf den Namen des Clientcomputers, für den Sie eine Sicherung einrichten möchten, und klicken Sie dann im Bereich **Aufgaben** auf **Sicherung für den Computer einrichten**.  
  
    > [!NOTE]
    >  Wenn die Sicherung für den Clientcomputer bereits eingerichtet ist, wird im Bereich **Aufgaben** die Option **Sicherung für den Computer anpassen** anstelle von **Sicherung für den Computer einrichten** angezeigt.  
  
3.  Im Assistent "Sicherung einrichten" können Sie auswählen, ob Sie alle Ordner oder bestimmte Ordner sichern möchten. Folgen Sie den Anweisungen im Assistenten.  
  
4.  Klicken Sie auf **Schließen**, wenn die Sicherung für den Computer eingerichtet ist.  
  
### <a name="critical-system-files"></a>Wichtige Systemdateien  
 Wenn Sie das Windows-Betriebssystem installieren, erstellt das Setupprogramm Ordner auf dem Systemlaufwerk, in dem Dateien gespeichert werden, die das System zum Starten und Ausführen benötigt. Zu den wichtigen Systemdateien gehören Dateien mit der Dateierweiterung .dll, .exe, .ocx und .sys. Einige dieser Dateien sind True Type-Schriftarten. Darüber hinaus sind Systemstatus Dateien, z. b. die Registrierung des Systems, erforderlich, damit das Betriebssystem ordnungsgemäß ausgeführt werden kann.  
  
### <a name="find-the-file-you-are-looking-for"></a>Suchen der gewünschten Datei  
 Sie können alle Ordner für einen Computer, mehrere Dateien und Ordner oder eine einzelne Datei oder einen einzelnen Ordner aus einer vorhandenen Sicherung wiederherstellen.  
  
 Nachdem Sie die Sicherung, die Sie zum Wiederherstellen verwenden möchten, ausgewählt haben, wird die Sicherungsdatei gelesen, und alle Dateien und Ordner werden angezeigt. Sie können eine bestimmte Datei oder einen bestimmten Ordner wiederherstellen, indem Sie auf den Ordner der obersten Ebene doppelklicken, und dann die Hierarchie der Ordner durchblättern, bis Sie die gesuchte Datei finden.  
  
### <a name="why-am-i-unable-to-select-some-items"></a>Warum kann ich einige Elemente nicht auswählen?  
 Das Kontrollkästchen im Auswahlmenü auf der Seite **Zu sichernde Elemente auswählen** kann verschiedene Status für jeden Ordner angeben. Status des Kontrollkästchens:  
  
- **Aktiviert**– Die zugehörigen Ordner und Ordnerinhalte werden für die Sicherung ausgewählt.  
  
- **Deaktiviert**– Die zugehörigen Ordner und Ordnerinhalte werden von der Sicherung ausgeschlossen.  
  
- **Einfarbig**– Der zugehörige Ordner wird für die Sicherung ausgewählt, aber ein oder mehrere Elemente in diesem Ordner werden von der Sicherung ausgeschlossen.  
  
  Die Auswahl eines bestimmten Ordners ist nicht möglich:  
  
- Das Volume kann für eine Sicherung konfiguriert sein, ist aber möglicherweise offline. Dies tritt häufig bei USB-Wechseldatenträgern auf. Volumes, die offline sind, werden mit grauem Text angezeigt.  
  
- Sie können nur Daten von einem lokalen Laufwerk sichern, das als NTFS-Dateisystem formatiert ist. Laufwerke, die als FAT- (und FAT32-) oder ReFS-Dateisystem formatiert sind, werden in der Liste der zu sichernden Laufwerke nicht angezeigt.  
  
> [!IMPORTANT]
>  Der Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) unterstützt nicht das Erstellen einer Schattenkopie eines virtuellen Volumes und des Hostvolumes in demselben Snapshotsatz. VSS unterstützt das Erstellen von Snapshots von Volumes auf einer virtuellen Festplatte (VHD), wenn eine Sicherung des virtuellen Volumes erforderlich ist. Weitere Informationen finden Sie unter [Warten und Sichern virtueller Festplatten](https://go.microsoft.com/fwlink/p/?LinkId=256577).  
  
##  <a name="change-the-time-that-backup-is-scheduled-to-run"></a><a name="BKMK_4"></a>Ändern der Zeit, zu der die Ausführung der Sicherung geplant ist  
 Der Sicherungsprozess sollte für eine Zeit geplant werden, wenn möglichst wenige Personen ihren Netzwerkcomputer verwenden. Dies ist in der Regel am späten Abend oder frühen Morgen der Fall. Die Standardzeit für die Sicherung liegt zwischen 18:00 Uhr und 9:00 Uhr. Der Server versucht, die Clientcomputer nur während des geplanten Zeitfensters zu sichern.  
  
 Wenn es während dieser Zeiten, die normalerweise außerhalb der normalen Arbeitszeiten liegen, jedoch Aktivitäten in Ihrem Unternehmen gibt, sollten Sie die Standardeinstellung ändern.  
  
#### <a name="to-change-the-time-that-backup-is-scheduled-to-run"></a>So ändern Sie die Zeit für eine geplante Sicherung  
  
1.  Öffnen Sie das **Dashboard** des Servers, und klicken Sie dann auf **Geräte**.  
  
2.  Klicken Sie im Bereich **Geräteaufgaben** auf **Einstellungen für Computersicherung und Dateiversionsverlauf anpassen**.  
  
    > [!NOTE]
    >  In Windows Server Essentials wurde diese Aufgabe umbenannt in **Client Computer-Sicherungs Tasks**.  
  
3.  Unter **Einstellungen und Tools für die Clientcomputersicherung** auf der Registerkarte **Computersicherung** können Sie die Start- und Endzeiten ändern, um Sie an Ihre Anforderungen anzupassen.  
  
4.  Klicken Sie auf **Übernehmen** und dann auf **OK**.  
  
##  <a name="change-the-computer-backup-retention-policy"></a><a name="BKMK_5"></a>Ändern der Aufbewahrungs Richtlinie für die Computer Sicherung  
 Tägliche Sicherungen von allen Computern sammeln sich mit der Zeit auf Ihrem Server an. Windows Server Essentials hilft Ihnen bei der Verwaltung der Datenbank mit Computersicherungen, um auf diese Weise die Sicherungen zu verwalten. Sie können festlegen, wie viele Sicherungen für alle Computer aufbewahrt werden sollen.  
  
 Die Sicherungsaufbewahrungsrichtlinie bestimmt, wie lange eine Sicherung gespeichert wird, bevor sie während des Bereinigungsvorgangs gelöscht wird. Die Sicherungsbereinigung wird jeden Samstag um 23:59 Uhr ausgeführt. Dabei werden alle Sicherungen gelöscht, die außerhalb der Sicherungsaufbewahrungsrichtlinie liegen. Standardeinstellungen für die Sicherungsaufbewahrungsrichtlinie:  
  
-   **Tägliche Sicherungen 5 Tage lang aufbewahren.** Die erste Sicherung des Tages wird als tägliche Sicherung aufbewahrt. Nach 5 Tagen wird die älteste tägliche Sicherung während des Bereinigungsvorgangs gelöscht.  
  
-   **Wöchentliche Sicherungen 4 Tage lang aufbewahren.** Die erste Sicherung der Woche wird als wöchentliche Sicherung aufbewahrt. Nach 4 Wochen wird die älteste wöchentliche Sicherung während des Bereinigungsvorgangs gelöscht.  
  
-   **Monatliche Sicherungen 6 Monate lang aufbewahren.** Die erste Sicherung des Monats wird als monatliche Sicherung aufbewahrt. Nach 6 Monaten wird die älteste monatliche Sicherung während des Bereinigungsvorgangs gelöscht.  
  
#### <a name="to-change-the-computer-backup-retention-policy"></a>So ändern Sie die Aufbewahrungsrichtlinie für die Computersicherung  
  
1.  Öffnen Sie das **Dashboard**.  
  
2.  Klicken Sie auf **Geräte**.  
  
3.  Klicken Sie im Bereich **Geräteaufgaben** auf **Einstellungen für Computersicherung und Dateiversionsverlauf anpassen**.  
  
    > [!NOTE]
    >  In Windows Server Essentials wurde diese Aufgabe umbenannt in **Client Computer-Sicherungs Tasks**.  
  
4.  Unter **Einstellungen und Tools für die Clientcomputersicherung** im Bereich **Aufbewahrungsrichtlinie für Clientcomputersicherungen** nehmen Sie die Änderungen an der Aufbewahrungsrichtlinie vor, die Ihren Anforderungen entsprechen.  
  
5.  Wenn Sie fertig sind, klicken Sie auf **OK**, um die Änderungen zu übernehmen und das Dialogfeld zu schließen. Die aktualisierte Aufbewahrungsrichtlinie wird beim nächsten Ausführen der Sicherungsbereinigung angewendet.  
  
    > [!NOTE]
    >  Die aktualisierte Aufbewahrungsrichtlinie gilt für alle Clientcomputer in Ihrem Netzwerk, die für die Sicherung konfiguriert wurden.  
  
##  <a name="reset-backup-to-default-settings"></a><a name="BKMK_6"></a>Sicherung auf Standardeinstellungen zurücksetzen  
 Nachdem die Sicherung für Clientcomputer konfiguriert wurde, kann der Netzwerkadministrator ein anderes Zeitfenster angeben. Gleichermaßen kann der Administrator eine längere oder kürzere Aufbewahrungszeit als die Standardzeit festlegen. Mithilfe der Schaltfläche **Standards wiederherstellen** können Sie das Sicherungsfenster und die Aufbewahrungsrichtlinie während der anfänglichen Sicherungskonfiguration auf die Standardeinstellungen zurücksetzen.  
  
 Die Standardwerte sind:  
  
-   Startzeit für die Sicherung: 18:00 Uhr  
  
-   Endzeit: 9:00 Uhr  
  
-   Anzahl von Tagen, die tägliche Sicherungen aufbewahrt werden: 5 Tage  
  
-   Anzahl von Wochen, die die letzte Sicherung der Woche aufbewahrt wird: 4 Wochen  
  
-   Anzahl von Monaten, die die letzte Sicherung des Monats aufbewahrt wird: 6 Monate  
  
#### <a name="to-reset-computer-backup-to-the-default-settings"></a>So setzen Sie die Computersicherung auf die Standardeinstellungen zurück  
  
1.  Öffnen Sie das **Dashboard** und dann die Seite **Geräte**.  
  
2.  Klicken Sie im Bereich **Geräteaufgaben** auf **Einstellungen für Computersicherung und Dateiversionsverlauf anpassen**.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Client Computer-Sicherungs Tasks**.  
  
3.  Klicken Sie auf der Registerkarte **Computersicherung** auf der Seite **Einstellungen und Tools für die Clientcomputersicherung** auf **Standards wiederherstellen**.  
  
    > [!NOTE]
    >  Es empfiehlt sich, den benutzerdefinierten Zeitplan und die Aufbewahrungsrichtlinieneinstellungen zu notieren, da sie nicht mehr vorhanden sind, wenn Sie die Standardeinstellungen wiederherstellen.  
  
4.  Klicken Sie auf **Übernehmen** und dann auf **OK**.  
  
##  <a name="use-repair-and-recovery-tools"></a><a name="BKMK_7"></a>Verwenden von Reparatur-und Wiederherstellungs Tools  
 **Sicherungen reparieren:** Wenn die Datenbank mit Computersicherungen aus irgendeinem Grund beschädigt oder unbrauchbar wird, können Sie versuchen, die Datenbank zu reparieren, indem Sie den Assistenten für die Reparatur der Sicherungsdatenbank verwenden. Der Assistent analysiert die Sicherungsdateien, um festzustellen, ob es Probleme gibt, die repariert werden können. Der Assistent versucht anschließend, die gefundenen Probleme zu beheben.  
  
> [!WARNING]
>  Wenn ein Problem nicht behoben werden kann, löscht der Assistent eine Computersicherungsdatei unter Umständen dauerhaft.  
  
 **Computerwiederherstellung:** Sie können einen startbaren USB-Speicherstick anlegen, um einen Computer aus einer vorhandenen Sicherung wiederherzustellen. Sie müssen einen USB-Speicherstick mit mindestens 1 GB verwenden. Nachdem der startfähige USB-Speicherstick angelegt wurde, stecken Sie ihn in den Computer, den Sie wiederherstellen möchten, und führen Sie dann einen Bootvorgang zum USB-Speicherstick durch, um eine vollständige Systemwiederherstellung zu starten.  
  
##  <a name="repair-the-backup-database"></a><a name="BKMK_8"></a>Reparieren der Sicherungs Datenbank  
 Wenn Sie eine Warnung erhalten, in der Sie auf Probleme mit der Computersicherungsdatenbank hingewiesen werden, können Sie versuchen, sie zu reparieren.  
  
#### <a name="to-repair-the-backup-database"></a>So reparieren Sie die Sicherungsdatenbank  
  
1.  Öffnen Sie das **Dashboard**.  
  
2.  Klicken Sie auf **Geräte**.  
  
3.  Klicken Sie im Bereich **Geräteaufgaben** auf **Einstellungen für Computersicherung und Dateiversionsverlauf anpassen**.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Client Computer-Sicherungs Tasks**.  
  
4.  Klicken Sie unter **Einstellungen und Tools für die Clientcomputersicherung** auf die Registerkarte **Tools**.  
  
5.  Klicken Sie im Bereich **Sicherungen reparieren** auf **Jetzt reparieren**. Der Assistent "Die Sicherungsdatenbank reparieren" wird geöffnet.  
  
6.  Folgen Sie den Anweisungen im Assistenten "Die Sicherungsdatenbank reparieren".  
  
7.  Je nach Umfang der Sicherungsdatenbank kann die Reparatur der Datenbank mehrere Stunden in Anspruch nehmen. Klicken Sie auf **Schließen** und dann auf **OK**, um die Seite **Einstellungen für Computersicherung und Dateiversionsverlauf anpassen** zu schließen.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Einstellungen und Tools für die Client Computer Sicherung**.  
  
#### <a name="to-review-the-results-of-the-backup-database-repair"></a>So überprüfen Sie die Ergebnisse der Reparatur der Sicherungsdatenbank  
  
1.  Öffnen Sie das **Dashboard**.  
  
2.  Klicken Sie auf **Geräte**.  
  
3.  Klicken Sie im Bereich **Geräteaufgaben** auf **Einstellungen für Computersicherung und Dateiversionsverlauf anpassen**.  
  
    > [!NOTE]
    >  Klicken Sie in Windows Server Essentials auf **Client Computer-Sicherungs Tasks**.  
  
4.  Klicken Sie unter **Einstellungen und Tools für die Clientcomputersicherung** auf die Registerkarte **Tools**.  
  
5.  Die Ergebnisse werden im Abschnitt **Sicherungen reparieren** angezeigt.  
  
##  <a name="disable-backup-for-a-computer"></a><a name="BKMK_9"></a>Deaktivieren der Sicherung für einen Computer  
 Verwenden Sie das Dashboard, um Sicherungen für Computer in Ihrem Netzwerk schnell zu deaktivieren.  
  
#### <a name="to-disable-backup-for-a-computer"></a>So deaktivieren Sie die Sicherung für einen Computer  
  
1. Öffnen Sie das **Dashboard**.  
  
2. Klicken Sie auf die Registerkarte **Geräte**.  
  
3. Klicken Sie auf den Namen des Computers an, für den Sie Sicherungen deaktivieren möchten.  
  
4. Klicken Sie im Bereich "Aufgaben" auf **Sicherung für den Computer anpassen**. Der Assistent zum Anpassen der Sicherung wird angezeigt.  
  
5. Klicken Sie auf **Sicherung für den Computer deaktivieren**, und wählen Sie dann, ob die vorhandenen Sicherungsdateien aufbewahrt oder gelöscht werden sollen.  
  
6. Klicken Sie auf **Änderungen speichern** und dann auf **Schließen**.  
  
   Weitere Informationen dazu, wie Sie eine Sicherung für einen Computer aktivieren, nachdem die Sicherung deaktiviert wurde, finden Sie unter [Einrichten der Sicherung für einen Clientcomputer](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_3).  
  
##  <a name="run-the-backup-cleanup-task"></a><a name="BKMK_10"></a>Ausführen der Sicherungs Bereinigungs Aufgabe  
 Die Bereinigungsaufgabe der Clientcomputersicherung ist für 11:59 Uhr jeden Samstag geplant, nachdem alle Sicherungen durchgeführt wurden. Die Bereinigungsaufgabe löscht Sicherungen aus der Datenbank mit Clientcomputersicherungen gemäß der Sicherungsaufbewahrungsrichtlinie. Standardeinstellungen für die Sicherungsaufbewahrungsrichtlinie:  
  
- Anzahl von Tagen, die tägliche Sicherungen aufbewahrt werden: 5 Tage  
  
- Anzahl von Wochen, die die letzte Sicherung der Woche aufbewahrt wird: 4 Wochen  
  
- Anzahl von Monaten, die die letzte Sicherung des Monats aufbewahrt wird: 6 Monate  
  
  Informationen zum Ändern der Sicherungsaufbewahrungsrichtlinie finden Sie unter [Ändern der Aufbewahrungsrichtlinie für die Computersicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
#### <a name="to-run-the-client-backup-database-cleanup-task"></a>So führen Sie die Bereinigungsaufgabe der Clientsicherungsdatenbank aus  
  
1.  Melden Sie sich mit Ihrem Administratorbenutzerkonto und -kennwort beim Server an.  
  
2.  Öffnen Sie auf dem Server die **Aufgabenplanung**. Sie können die Aufgabenplanung über die Konsole **Verwaltung** aufrufen.  
  
3.  Erweitern Sie in der Aufgabenplanung **Aufgabenplanungsbibliothek** und dann **Microsoft** und **Windows**, und klicken Sie auf **Windows Server Essentials**.  
  
4.  Klicken Sie auf die Aufgabe **Sicherungsbereinigung** und dann im Bereich **Aktionen** auf **Ausführen**. Der Status ändert sich in **Wird ausgeführt**, bis die Aufgabe abgeschlossen ist.  
  
##  <a name="view-alerts-in-the-task-bar-on-a-client-computer"></a><a name="BKMK_11"></a>Anzeigen von Warnungen in der Taskleiste auf einem Client Computer  
 In der Taskleiste Ihres Computer wird aus folgenden Gründen ein Hinweis in Bezug auf die Sicherung angezeigt:  
  
-   Eine Sicherung wurde gestartet.  
  
-   Eine Sicherung wurde beendet.  
  
-   Es gibt keine aktuelle erfolgreiche Sicherung. Der Hinweis enthält auch die Anzahl der Tage seit der letzten erfolgreichen Sicherung.  
  
-    Nur Windows Server Essentials: Ihrem Computer wird ein neues Volume hinzugefügt. Die Person, die das Netzwerk verwaltet, muss den Assistenten zum Anpassen der Sicherung ausführen, um das Volume in zukünftige Sicherungen einzuschließen bzw. davon auszuschließen.  
  
##  <a name="view-backup-status-from-the-launchpad"></a><a name="BKMK_12"></a>Anzeigen des Sicherungs Status über das launchpad  
 Verwenden Sie das Launchpad, um schnell den Sicherungsstatus Ihres Computer anzuzeigen.  
  
> [!TIP]
>  Bewegen Sie den Mauszeiger über das Launchpad-Symbol im Infobereich des Desktops, um eine Statusübersicht anzuzeigen. Der Sicherungsstatus wird als QuickInfo angezeigt.  
  
#### <a name="to-view-status-of-a-backup-for-your-computer"></a>So zeigen Sie den Sicherungsstatus für den Computer an  
  
1.  Melden Sie sich mit Ihrem Benutzernamen und Kennwort beim **Launchpad** an.  
  
2.  Klicken Sie auf **Sicherung**.  
  
3.  Der Sicherungsstatus wird im Dialogfeld **Eigenschaften der Sicherung** im Abschnitt **Sicherungsstatus** angezeigt.  
  
    -   **Keine vorherigen Sicherungen:** Entweder wurde noch keine Sicherung ausgeführt, oder der Sicherungsverlauf wurde gelöscht.  
  
    -   **Sicherung ausstehend:** Eine Sicherung wartet darauf, dass ein anderer Prozess auf dem Server abgeschlossen wird.  
  
    -   **Verbindung wird hergestellt**: Die Sicherung stellt eine Verbindung zum Server her.  
  
    -   **Verbindung kann nicht hergestellt werden**: Die Sicherung kann keine Verbindung mit dem Windows Server-Anbieterdienst für die Clientcomputersicherung herstellen.  
  
        > [!NOTE]
        >  In Windows Server Essentials wurde dieser Dienst in Windows Server Essentials Client Computer Management-Dienst umbenannt.  
  
    -   **Sicherung wird ausgeführt**: Zeigt den abgeschlossenen Prozentsatz der Sicherung an.  
  
    -   **Sicherung wurde abgebrochen**: Zeigt das Datum und die Uhrzeit an, an dem bzw. zu der die Sicherung gestartet wurde, wenn Sie oder der Netzwerkadministrator die Sicherung abgebrochen haben.  
  
    -   **Sicherung erfolgreich**: Zeigt das Datum und die Uhrzeit, an dem bzw. zu der die Sicherung gestartet wurde, wenn die Sicherung erfolgreich abgeschlossen wurde.  
  
    -   **Sicherung war nicht vollständig**: Zeigt das Datum und die Uhrzeit, an dem bzw. zu der die Sicherung gestartet wurde, wenn die Sicherung nicht erfolgreich abgeschlossen wurde.  
  
    -   **Sicherung war nicht erfolgreich**: Zeigt das Datum und die Uhrzeit, an dem bzw. zu der die Sicherung gestartet wurde, wenn die Sicherung nicht erfolgreich abgeschlossen wurde.  
  
4.  Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften der Sicherung** zu schließen.  
  
##  <a name="stop-a-backup-in-progress-from-the-launchpad"></a><a name="BKMK_13"></a>Beendet eine laufende Sicherung aus dem launchpad.  
 Sie können eine Sicherung problemlos beenden, die gerade ausgeführt wird.  
  
#### <a name="to-stop-a-backup-in-progress"></a>So beenden Sie eine laufende Sicherung  
  
1.  Öffnen Sie das **Launchpad**.  
  
    > [!NOTE]
    >  Melden Sie sich, wenn Sie dazu aufgefordert werden, mit Ihrem Benutzernamen und Kennwort beim **Launchpad** an.  
  
2.  Klicken Sie auf **Sicherung**.  
  
3.  Im Dialogfeld **Eigenschaften der Sicherung** ändert sich im Abschnitt **Sicherungsstatus** die Schaltfläche **Sicherung starten** in **Sicherung beenden**, wenn die Sicherung gerade ausgeführt wird. Klicken Sie auf **Sicherung beenden** und dann auf **Ja**, um den Vorgang zu bestätigen. Die Sicherung wird weiterhin ausgeführt, bis Sie auf **Ja** klicken.  
  
4.  Wenn Sie eine laufende Sicherung beenden, ändert sich der Status in **Sicherung wurde abgebrochen** mit Datum und Uhrzeit des Sicherungsstarts. Wenn Sie stattdessen den Status **Erfolgreich**, **Unvollständig** oder **Fehler** sehen, wurde die letzte Sicherung bereits beendet.  
  
5.  Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften der Sicherung** zu schließen.  
  
##  <a name="start-a-backup-from-the-launchpad"></a><a name="BKMK_14"></a>Starten einer Sicherung über das launchpad  
 Möglicherweise gibt es Zeiten, wenn Sie Ihre Dateien und Ordner vor der eigentlich geplanten, auf dem Server festgelegten Sicherung sichern möchten. Über das Launchpad können Sie die Sicherung des Computers manuell initiieren.  
  
#### <a name="to-start-a-backup"></a>So starten Sie eine Sicherung  
  
1.  Öffnen Sie das **Launchpad**.  
  
    > [!NOTE]
    >  Melden Sie sich, wenn Sie dazu aufgefordert werden, mit Ihrem Benutzernamen und Kennwort beim **Launchpad** an.  
  
2.  Klicken Sie auf **Sicherung**.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften der Sicherung** im Abschnitt **Sicherungsstatus** auf **Sicherung starten** und dann auf **OK**.  
  
4.  Geben Sie eine Beschreibung für die Sicherung ein, und klicken Sie dann auf **OK**. Der Status ändert sich in **Sicherung wird gestartet** und dann in **Sicherung wird ausgeführt**, wobei der abgeschlossene Prozentsatz angezeigt wird.  
  
5.  Nachdem die Sicherung gestartet wurde, ändert sich der Text auf der Schaltfläche in **Sicherung beenden**. Wenn die Sicherung ausgeführt wird und Sie sie beenden möchten, klicken Sie auf **Sicherung beenden** und dann auf **Ja**. Wenn Sie eine laufende Sicherung beenden, ändert sich der Status in **Sicherung wurde abgebrochen** mit Datum und Uhrzeit des Sicherungsstarts.  
  
6.  Wenn die Sicherung erfolgreich abgeschlossen wird, ändert sich der Status in **Sicherung erfolgreich** mit Datum und Uhrzeit, an dem die abgeschlossene Sicherung gestartet wurde.  
  
7.  Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften der Sicherung** zu schließen.  
  
##  <a name="how-computer-backup-works"></a><a name="BKMK_15"></a>Funktionsweise der Computer Sicherung  
 Bei der täglichen Sicherung werden die folgenden Aufgaben durchgeführt:  
  
-   Die Netzwerkcomputer werden nacheinander gesichert.  
  
-   Eine laufende Sicherung wird abgeschlossen, auch wenn Sie das Sicherungsfenster schließen.  
  
-   Windows-Updates werden installiert und Windows Server Essentials startet (falls erforderlich) neu.  
  
-   Sonntags wird die Sicherungsbereinigung ausgeführt.  
  
> [!IMPORTANT]
>  Der Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) unterstützt nicht das Erstellen einer Schattenkopie eines virtuellen Volumes und des Hostvolumes in demselben Snapshotsatz. VSS unterstützt das Erstellen von Snapshots von Volumes auf einer virtuellen Festplatte (VHD), wenn eine Sicherung des virtuellen Volumes erforderlich ist. Weitere Informationen finden Sie unter [Warten und Sichern virtueller Festplatten](https://go.microsoft.com/fwlink/p/?LinkId=256577).  
  
##  <a name="tips-to-help-prevent-data-loss-due-to-corruption-of-the-client-backup-database"></a><a name="BKMK_16"></a>Tipps zur Vermeidung von Datenverlusten aufgrund einer Beschädigung der Client Sicherungs Datenbank  
 Wenn die Clientsicherungsdatenbank beschädigt wird, können Sie wichtige Daten verlieren.  
  
 Beachten Sie Folgendes, um einen Datenverlust aufgrund einer Beschädigung der Clientsicherungsdatenbank zu vermeiden:  
  
-   Aktivieren Sie eine weitere Sicherungsmethode für die Clientsicherungsdatenbank. Verwenden Sie beispielsweise abhängig von der Version von Windows Server Essentials, die Sie ausführen, die Server Sicherung, die Online Sicherung oder die Microsoft Azure Backup, um die Datenbank zu sichern.  
  
    > [!IMPORTANT]
    >  Stellen Sie sicher, dass Sie alle Dateien im Ordner **Clientcomputersicherungen** auswählen, um sie zu sichern.  
  
-   Wenn Sie die Datenbank wiederherstellen müssen, stellen Sie sicher, dass Sie alle Dateien im Ordner **Clientcomputersicherungen** wiederherstellen. Wenn Sie nicht alle Dateien wiederherstellen, ist die Datenbank womöglich inkonsistent.  
  
-   Bevor Sie die Clientsicherungsdatenbank bereinigen oder wiederherstellen, stellen Sie sicher, dass Sie alle Clientsicherungen beenden, die derzeit ausgeführt werden.  
  
     Wenn Sie Windows Server Essentials ausführen, sollten Sie auch den Windows Server-Dienst für die Client Computer Sicherung und den Anbieter Dienst für die Windows Server-Client Computer Sicherung unterbinden.  
  
     Wenn Sie Windows Server Essentials ausführen, sollten Sie auch den Windows Server-Computer Sicherungsdienst abbrechen.  
  
     Nach Abschluss des Wiederherstellungsvorgangs müssen Sie den Dienst neu starten.  
  
##  <a name="restore-files-or-folders-from-a-client-computer-backup"></a><a name="BKMK_17"></a>Wiederherstellen von Dateien oder Ordnern aus einer Client Computer Sicherung  
 Sie können zu einzelnen Dateien und Ordnern navigieren und sie aus einer Sicherungsdatei wiederherstellen.  
  
> [!NOTE]
>  Mithilfe des Dashboards auf dem Server können Sie keine Dateien und Ordner auf einem Clientcomputer wiederherstellen. Sie müssen das Dashboard auf einem Clientcomputer öffnen, um den Vorgang abzuschließen.  
  
> [!IMPORTANT]
>  Sie können keine Dateien und Ordner auf einer Festplatte wiederherstellen, die als dynamischer Datenträger konfiguriert wurde.  
  
#### <a name="to-restore-files-and-folders"></a>So stellen Sie Dateien und Ordnern wieder her  
  
1.  Öffnen Sie das **Dashboard** auf einem Clientcomputer.  
  
2.  Klicken Sie auf die Registerkarte **Geräte**.  
  
3.  Klicken Sie auf den Computer, für den Sie Dateien und Ordner wiederherstellen möchten, und klicken Sie dann im Bereich **Aufgaben** auf **Dateien oder Ordner für den Computer wiederherstellen**. Der Assistent zum Wiederherstellen von Dateien oder Ordnern wird geöffnet.  
  
4.  Folgen Sie den Anweisungen im Assistenten.  
  
##  <a name="understanding-file-history"></a><a name="BKMK_FileHistory"></a>Grundlegendes zum Datei Verlauf  
 Die Dateiversionsverlauf-Funktion von Windows Server Essentials sichert automatisch Dateien, die sich in den Ordnern "Bibliotheken", "Kontakte", "Desktop" und "Favoriten" auf Netzwerkcomputern befinden, für die die Dateiversionsverlauf-Funktion aktiviert wurde. Wenn ursprüngliche Dateien verloren gegangen sind, beschädigt oder gelöscht wurden, können Sie sie wiederherstellen. Es gibt auch verschiedene Versionen der Dateien von unterschiedlichen Zeitpunkten. Im Laufe der Zeit erhalten Sie einen vollständigen Verlauf der Dateien.  
  
 In Windows Server Essentials können Sie die Einstellungen des Datei Versions Verlaufs auf der Seite **Datei Versionsverlauf** unter **Einstellungen und Tools für die Client Computer Sicherung**anpassen.  
  
 In Windows Server Essentials können Sie die Einstellungen des Datei Versions Verlaufs anpassen, indem Sie auf die Registerkarte **Benutzer** wechseln und dann den Task **Datei Versionsverlauf ändern** auswählen.  
  
 Die Seite "Dateiversionsverlauf" bietet die folgenden Optionen:  
  
|Sicherungseinstellung|Standard|Beschreibung|  
|--------------------|-------------|-----------------|  
|Einschalten/Ausschalten|Ein|Der Dateiversionsverlauf ist bei der Installation von Windows Server Essentials standardmäßig aktiviert.|  
|Sicherungsdaten|Dokumente und Desktop|Es gibt drei vorkonfigurierte Einstellungen, mit denen Sie eine Vielzahl von Sicherungslösungen festlegen können. Sie können eine der folgenden Optionen wählen:<br /><br /> -Dokumente und Desktop<br /><br /> -Alle Bibliotheken, Desktop, Kontakte und Favoriten<br /><br /> -Alle Daten in Bibliotheken, Desktops, Kontakten und Favoriten ohne Daten in den Bibliotheken Musik, Video und Bilder|  
|Sicherungshäufigkeit|Jede Stunde|Gibt an, wie oft der Dateiversionsverlauf eine Sicherung der ausgewählten Daten erstellt. Sie können aus verschiedenen Optionen wählen, von "Jede 10 Minuten" bis hin zu "Täglich".|  
|Aufbewahrungsdauer der Kopien|1 Jahr|Gibt die Dauer an, die eine Sicherungskopie im Dateiversionsverlauf aufbewahrt wird.|  
  
 Informationen zu Problemen mit dem Dateiversionsverlauf finden Sie unter [Problembehandlung für den Dateiversionsverlauf](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md) (womöglich nur in englischer Sprache).  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Sicherungen und Wiederherstellungen](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
