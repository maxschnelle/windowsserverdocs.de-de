---
title: Verwalten der Onlinesicherung in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95a9f593-fad7-4335-bd4d-c7bb8c033efb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 37d59d500a2de1e2b98c848e7484ae13639d09b7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-online-backup-in-windows-server-essentials"></a>Verwalten der Onlinesicherung in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
  
 Nach der Integration in Microsoft Azure Backup der **Onlinesicherung** Verwaltungsseite wird in Windows Server Essentials-Dashboard angezeigt. Die **Onlinesicherung** Seite ermöglicht, allgemeine Verwaltungsaufgaben auszuführen. Die Features auf der Seite "Onlinesicherung" umfassen:  
  
-   Die folgenden Unterabschnitte:  
  
    -   **Online Backup** Nachdem Sie den Server für die Onlinesicherung registriert haben, wird in diesem Abschnittder aktuelle Sicherungsstatus, Speicherstatus und Kontoinformationen.  
  
    -   **Geschützte Ordner** in diesem Abschnittlistet alle freigegebenen und dateiversionsverlaufsordner auf dem Server und alle weiteren Ordner, die Sie in Azure sichern möchten. Die Liste enthält den Ordnernamen, Ordnerpfad und Status für jeden freigegebenen Ordner.  
  
    -   **Sicherungsverlauf** in diesem Abschnittzeigt eine Liste der zuletzt erstellten Onlinesicherungen. Die Liste enthält den Typ der Vorgang, und die Uhrzeit und den Status für jede Sicherung.  
  
-   Ein Detailbereich mit zusätzlichen Informationen zu einem ausgewählten sicherungs- oder Wiederherstellungsauftrag.  
  
-   Ein Aufgabenbereich, der eine Reihe von administrativen Aufgaben enthält, die Sie ausführen können.  
  
 Als bewährte Methode sollten Sie die wichtigsten Unternehmens- und Benutzerdaten Daten sichern. Sie sollten z.B. Serverordner sichern, die wichtige Datendateien enthalten. Sie sollten auch den Dateiversionsverlauf für Netzwerkcomputer sichern, die wichtigen Informationen enthalten.  
  
 Bei der Entscheidung, welche Daten Sie online sichern, sollten Sie die Häufigkeit und Aufbewahrungsdauer Sicherungsrichtlinie, die Sie implementieren möchten. Klicken Sie dann überprüfen Sie Ihr Budget, und ermitteln Sie die Menge des Speicherplatzes, die Sie sich leisten können. Wägen Sie Kosten und Volumen des Speichers gegen Ihre Anforderungen, und konfigurieren Sie online Backup größtmöglichen Teil Ihrer wichtigen Daten wie möglich zu schützen. Preise finden Sie unter [Azure Backup – Preise](https://azure.microsoft.com/pricing/details/backup/).  
  
 Den folgenden Abschnitten werden die verschiedenen Aufgaben der Onlinesicherung, die in Windows Server Essentials-Dashboard angezeigt werden können.  
  
## <a name="online-backup-tasks-in-the-dashboard"></a>Aufgaben für die Onlinesicherung im Dashboard  
  
-   [Ein Zertifikat in den Azure Backup-Tresor hochladen](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Konfigurieren der Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Starten einer Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Wiederherstellen von Dateien und Ordnern aus einer Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Registrieren dieses Server für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Registrierung des Servers aufheben](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
###  <a name="BKMK_1"></a>Ein Zertifikat in den Azure Backup-Tresor hochladen  
 Bevor Sie Azure Backup für Onlinesicherungen in Windows Server Essentials verwenden können, müssen Sie ein öffentliches Zertifikat für die Registrierung mit dem sicherungstresor hochladen. Das Zertifikat wird verwendet, die Azure Backup-Bereitstellung (Agent), im Namen des Microsoft Online Services zum Verwalten von Ressourcen, die dem Abonnement zugeordneten fungiert authentifizieren.  
  
> [!NOTE]
>  Bevor Sie das Zertifikat hochladen, müssen Sie die Verfahren in [melden Sie sich für Azure Backup-Dienst](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16).  
  
##### <a name="to-upload-a-certificate-to-use-with-the-azure-backup-service"></a>Ein Zertifikat mit dem Azure Backup-Dienst hochladen  
  
1.  Melden Sie sich bei Windows Server Essentials-Dashboard mit einem Administratorkonto an.  
  
2.  Auf dem Dashboard **Home** auf **ONLINESICHERUNG**.  
  
3.  In der **ONLINESICHERUNG** Bereich, klicken Sie auf **Upload-Zertifikat in Azure Backup-Tresor**.  
  
     Öffnet die **Recovery Services** im Azure-Verwaltungsportal. Wenn Sie t bereits in Azure angemeldet, müssen Sie mit Ihrem Microsoft-Konto anmelden.  
  
4.  Klicken Sie auf den Namen des sicherungstresors, den Sie zum Öffnen für Onlinesicherungen verwenden die **Quick Start** Seite für den sicherungstresor.  
  
5.  Klicken Sie auf **Zertifikat verwalten**.  
  
6.  In der **Zertifikat verwalten** einfügen, wird der Pfad des öffentlichen Zertifikats von Windows Server Essentials generiert. Gehen Sie wie folgt vor, um den Pfad des öffentlichen Zertifikats zu erhalten:  
  
    1.  Klicken Sie auf dem Windows Server Essentials-Dashboard auf der **Onlinesicherung** Registerkarte.  
  
    2.  Auf der **Onlinesicherung** Seite, und kopieren Sie den Pfad des generierten Zertifikats.  
  
    3.  Wechseln Sie im Azure-Verwaltungsportal, und klicken Sie dann in der **Zertifikat verwalten** Dialogfeld fügen den Pfad ein, das generierte öffentliche Zertifikat hochgeladen.  
  
    > [!NOTE]
    >  Sie können auch Ihr eigenes öffentliche Zertifikat verwenden. Wissen, welches Zertifikat erforderlich ist, ist die **Quick Start** auf die **Zertifikat erwerben** Link.  
  
    > [!NOTE]
    >   Azure erfordert ein x. 509 v2-Zertifikat mit einem öffentlichen Schlüssel. Weitere Informationen finden Sie unter [Verwalten von Onlinekonten](https://msdn.microsoft.com/library/azure/dn169036.aspx).  
  
7.  Nachdem Sie das Zertifikat ausgewählt haben, klicken Sie auf **OK** (Häkchen).  
  
8.  Sie kehren zum der **Quick Start** Seite. Klicken Sie auf **Dashboard**, und stellen Sie sicher, dass das Zertifikat erfolgreich hochgeladen wurde. Nachdem das Zertifikat erfolgreich hochgeladen wurde, zeigt das Dashboard das Datum Fingerabdruck und das Ablaufdatum des Zertifikats.  
  
 Führen Sie nach Abschluss dieses Vorgangs folgende Schritteaus:  
  
1.  Registrieren Sie den Server mit dem Azure Backup-Dienst. Weitere Informationen finden Sie unter [registrieren dieses Server für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
2.  Konfigurieren der Onlinesicherung des Servers. Weitere Informationen finden Sie unter [Configure online Backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="BKMK_2"></a>Konfigurieren der Onlinesicherung  
 Nachdem Sie den Server bei Azure Backup registrieren, können Sie Einstellungen für die Onlinesicherung in Windows Server Essentials konfigurieren.  
  
##### <a name="to-configure-online-backup"></a>So konfigurieren Sie die Onlinesicherung  
  
1.  Entweder von der Registrierungs-Assistenten oder von der **Online Backup** Seite des Windows Server Essentials-Dashboards, klicken Sie auf **Configure online Backup**. Der Assistent zum Konfigurieren von Online-Sicherung wird angezeigt.  
  
2.  Auf der **Onlinesicherung konfigurieren** Seite des Assistenten das Kontrollkästchen für jeden Serverordner, die Sie zum Azure-Sicherung sichern möchten. Deaktivieren Sie das Kontrollkästchen für jeden Serverordner, die nicht in die Sicherung aufgenommen werden sollen. Um Ordner hinzuzufügen, die nicht in der Liste angezeigt werden, klicken Sie auf **Ordner hinzufügen**. Wenn Sie Ihre Auswahl beendet haben, klicken Sie auf **Weiter**.  
  
    > [!NOTE]
    >  Sie können keine wählen Sie einen Ordner, die nicht auf dem lokalen Server oder einen Ordner auf einem Laufwerk, das als ReFS formatiert ist.  
  
3.  Auf der **Dateiversionsverlaufssicherungen hinzufügen** Seite des Assistenten können Sie auswählen, ob Sie Dateiversionsverlaufssicherungen für Netzwerkcomputer einschließen, die die Funktion "Dateiversionsverlauf" unterstützen. Klicken Sie dann auf **Weiter** um den Vorgang fortzusetzen.  
  
4.  Auf der **Sicherungszeitplan angeben** Seite des Assistenten konfigurieren Sie Folgendes aus, und klicken Sie dann auf **Weiter** fort:  
  
    -   Wählen Sie oder übernehmen Sie die Tageszeit, wenn die Onlinesicherung ausgeführt werden soll. Die Standardzeit beträgt 10:00 Uhr. Sie können auch eine Zeit für die Ausführung einer zweiten Sicherung angeben.  
  
    -   Wählen Sie aus, oder übernehmen Sie die Tage, wenn die Onlinesicherung ausgeführt werden soll. Standardmäßig wird online Backup montags bis freitags ausgeführt.  
  
5.  Auf der **Geben Sie die Aufbewahrungsrichtlinie für die Sicherung** Seite des Assistenten, wählen Sie die Anzahl der Tage Onlinesicherungen beibehalten, und klicken Sie auf **Weiter**. Der Standardwert ist 7Tage. Sie können auch auswählen, 15 oder 30Tage Onlinesicherungen beibehalten.  
  
    > [!NOTE]
    >   Azure Backup behält immer die neueste Sicherung. Wenn das Sicherungsziel nicht über genügend Speicherplatz zum Speichern der Sicherung verfügt, ist der Sicherungsvorgang nicht erfolgreich. Um dies zu vermeiden, erwerben Sie zusätzlichen Speicherplatz, oder verkürzen Sie die Beibehaltungsdauer der Daten. Preise finden Sie unter [Preisdetails](https://azure.microsoft.com/pricing/details/backup/) für Microsoft Azure Backup.  
  
6.  Auf der **bandbreitennutzung auswählen** Seite des Assistenten Wunsch Internet Bandbreite zu beschränken, die Online-Sicherung, wählen zugewiesen ist **aktivieren Internet-bandbreitennutzung**. Verwenden Sie die Optionen auf der Seite an, wie viel Internetbandbreite von der Onlinesicherung während der Arbeit Arbeitszeit bzw. außerhalb der Arbeitszeit verwenden können. Definieren Sie dann die Geschäftszeiten und Werktagen.  
  
    > [!NOTE]
    >   Azure-Sicherung können Sie anpassen, wie die Netzwerkbandbreite beim Sichern oder Wiederherstellen von Informationen Integrationssoftware. Verwenden eine Technik, die üblicherweise als Einschränkung bezeichnet, können Sie steuern die Menge an Bandbreite, die für die Verwendung durch die Sicherung verfügbar ist und Wiederherstellungsprozesse während bestimmter Tages- und Zeitintervalle. Nach dem Auswählen der **aktivieren Internet-bandbreitennutzung** Kontrollkästchen in den Assistenten für die Onlinesicherung konfigurieren, können Sie angeben, die Arbeitstage und Arbeitszeiten, um die Arbeitsstunden Bandbreitenlimit gilt. Die Grenze nicht Stunden wird bei allen in anderen Fällen verwendet. Sind Bandbreitenbereiche von 256 KBit/s bis unbegrenzt zulässig für beide Grenzwerte.  
  
7.  Wenn die Konfiguration die Onlinesicherung abgeschlossen ist, klicken Sie auf **schließen**.  
  
    > [!TIP]
    >  Nach einer erfolgreichen Sicherung Konfiguration der **Online Backup** Seite zeigt den Status der letzten Onlinesicherung und die Menge an Speicherplatz, die vom sicherungstresor verwendet. Um den Status früherer Sicherungen anzuzeigen, klicken Sie auf **Sicherungsverlauf**.  
  
###  <a name="BKMK_3"></a>Starten einer Onlinesicherung  
  
> [!NOTE]
>  Bevor Sie eine Online-Sicherung starten können, müssen Sie zuerst [registrieren dieses Server für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5), und klicken Sie dann [Configure online Backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
##### <a name="to-start-an-online-backup-immediately"></a>Um eine Onlinesicherung sofort zu starten.  
  
1.  Melden Sie sich auf das Dashboard als Administrator an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  In der **Aufgaben für die Onlinesicherung** Bereich, klicken Sie auf **Backup jetzt starten**.  
  
###  <a name="BKMK_4"></a>Wiederherstellen von Dateien und Ordnern aus einer Onlinesicherung  
 Wiederherstellen von Dateien und Ordner-Assistent führt Sie durch den Prozess der suchen, auswählen und Wiederherstellen von Dateien und Ordnern, die online gesichert werden. Wie Sie mithilfe des Assistenten wechseln, werden die folgenden Aufgaben ausgeführt:  
  
1.  **Wählen Sie eine Online-Sicherung zum Wiederherstellen von Dateien und Ordner aus**  
  
     Wenn Sie das Wiederherstellen von Dateien und Ordner-Assistenten ausführen, wird als Erstes, die Sie durchführen müssen, angeben, wenn Sie Dateien aus einer Onlinesicherung des Servers, der Sie aktuell angemeldet sind, oder aus einer Sicherung von einem anderen Server wiederherstellen möchten.  
  
2.  **Wählen Sie einen Server für die Wiederherstellung von Dateien und Ordnern**  
  
     Wenn Sie Dateien und Ordner von einem anderen Server wiederherstellen möchten, wählen Sie den Server, die Sie verwenden möchten, in der Liste der verfügbaren Server aus wiederherstellen, und klicken Sie dann auf **Weiter**.  
  
3.  **Wählen Sie ein Volume mit den Dateien und Ordner wiederhergestellt werden**  
  
     Onlinesicherungen enthalten Volumes, die Volumes auf dem Quellserver für Sicherungen entsprechen. Nachdem Sie das Volume ausgewählt haben, wählen Sie Datum und Uhrzeit der Sicherung dort wiederherstellen, und klicken Sie dann auf **Weiter**.  
  
4.  **Wählen Sie Dateien und Ordner wiederherstellen**  
  
     Auf der **Wiederherzustellende Elemente** Seite des Assistenten können Sie die verschiedenen Ordnerpfade öffnen und wählen Sie das Kontrollkästchen für die einzelnen Dateien oder Ordner, die Sie wiederherstellen möchten. Wenn Sie die Dateien ausgewählt haben, klicken Sie auf **Weiter**.  
  
5.  **Angeben des Zielspeicherorts für die wiederhergestellten Dateien und Ordner**  
  
     Die **Wiederherstellungsoptionen angeben** auf der Seite des Assistenten können Sie angeben, wo Sie Dateien und Ordner wiederherstellen. Es gibt zwei Optionen:  
  
    -   **Am ursprünglichen Speicherort wiederherstellen**. Wählen Sie diese Option, um Dateien und Ordner an genau dem Speicherort wiederherstellen, von dem die Sicherung erstellt wurde.  
  
    -   **An einem anderen Speicherort wiederherstellen**.  Wählen Sie diese Option aus, geben Sie einen anderen Speicherort auf dem Server, um die Dateien wiederherzustellen.  
  
         In der Standardinstallation eine Datei mit demselben Namen wie die Wiederherstellungsdatei bereits am Zielort vorhanden ist, erstellt der Assistent eine Kopie der ursprünglichen Datei. Darüber hinaus wird die Zugriffssteuerungsliste (ACL) aktualisiert, um aktuelle Dateiberechtigungen zu berücksichtigen. Klicken Sie auf **erweitert** auf die Standardeinstellungen anzupassen.  
  
6.  **Bestätigen der Wiederherstellungsinformationen**  
  
     Die **Wiederherstellungsinformationen bestätigen** Seite enthält eine Zusammenfassung der Wiederherstellung Anweisungen, die Sie angegeben haben. Um die Wiederherstellung der Datei fortzusetzen, müssen Sie die richtige Passphrase für Ihr Onlinesicherungskonto eingeben.  
  
###  <a name="BKMK_5"></a>Registrieren dieses Server für die Sicherung  
 Zum Sichern oder Wiederherstellen von Dateien, Ordner und Dateiversionsverlauf Ihres Windows Server Essentials-Servers auf Azure Backup, müssen Sie zuerst den Server mit dem Microsoft Azure Backup-Dienst registrieren.  
  
> [!NOTE]
>  Bevor Sie den Server registrieren, müssen Sie hochladen ein Zertifikats mit dem sicherungstresor verwenden, die die Onlinesicherungen gespeichert werden. Weitere Informationen finden Sie unter [Hochladen eines Zertifikats in den Azure Backup-Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1).  
  
##### <a name="to-register-your-server-with-azure-backup"></a>So registrieren Sie Ihre Server in Azure Backup  
  
1.  Melden Sie sich an den Server als Administrator, und öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  In der **Onlinesicherung** Unterabschnitt, klicken Sie auf **registrieren**.  
  
4.  Wählen Sie das Zertifikat, das Sie für Ihre Online-Sicherungen mit dem sicherungstresor verwenden möchten. Das Standardzertifikat ist standardmäßig aktiviert. Wenn Sie ein anderes Zertifikat auswählen möchten, verwenden Sie **Durchsuchen**. Klicken Sie dann auf **Weiter**.  
  
5.  Folgen Sie den Anweisungen im Assistenten, um eine Passphrase zu erstellen, und schließen Sie die Registrierung.  
  
###  <a name="BKMK_6"></a>Registrierung des Servers aufheben  
  
> [!CAUTION]
>  Wenn Sie Ihre Windows Server Essentials-Server aus der Microsoft Azure Backup-Dienst die Registrierung aufheben, können den Server nicht mehr Azure Backup sichern. Darüber hinaus werden die Server-Daten, die zuvor hochgeladenen Serverdaten gelöscht. Um Onlinesicherungen fortzusetzen, müssen Sie den Server erneut registrieren.  
  
##### <a name="to-unregister-your-server-with-azure-backup"></a>Aufheben der Registrierung Ihres Servers mit Azure Backup  
  
1.  Melden Sie sich an den [Azure-Verwaltungsportal](https://manage.windowsazure.com).  
  
2.  Klicken Sie auf **Recovery Services**.  
  
3.  In **Recovery Services**, klicken Sie auf den Namen des sicherungstresors.  
  
4.  Von der **Quick Start** Seite für den Tresor, klicken Sie auf **Server**.  
  
5.  Wählen Sie den Server, klicken Sie auf **löschen**, und klicken Sie dann auf **Ja** zur Bestätigung aufgefordert.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Ändern Sie die Richtlinie für die Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Anzeigen der Verwendung der online Backup-Speicher](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Einschließen eines neuen Ordners in die Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Entfernen oder Ausschließen von dateiversionsverlaufssicherungen aus der Richtlinie für die Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Deaktivieren oder erneutes Aktivieren der Onlineserversicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Beendet eine laufende Sicherung Online-Server](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [Anzeigen des Status der Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [Anzeigen und Verwalten von online Backup-Warnungen](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [Online-Sicherung auf Standardeinstellungen zurückgesetzt.](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_15)  
  
-   [Melden Sie sich für Azure Backup-Dienst](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)  
  
-   [Integration von Azure Backup mit Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_17)  
  
-   [Schützen von Ordnern für die Onlinesicherung in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_18)  
  
-   [Verlauf der Onlinesicherung in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_19)  
  
###  <a name="BKMK_7"></a>Ändern Sie die Richtlinie für die Onlinesicherung  
 Es ist einfach so ändern Sie die online Backup-Richtlinie mithilfe von Windows Server Essentials-Dashboard.  
  
##### <a name="to-change-the-online-backup-policy"></a>So ändern Sie die Richtlinie für die Onlinesicherung  
  
1.  Melden Sie sich auf das Dashboard als Administrator an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3.  In der **Aufgaben für die Onlinesicherung** Bereich, klicken Sie auf **Configure online Backup**.  
  
4.  Folgen Sie den Anweisungen im Assistenten zum Anpassen der Richtlinie für der Onlinesicherung.  
  
 Ausführlichere Informationen zu den Einstellungen, die Sie anpassen können, finden Sie unter [Configure online Backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="BKMK_8"></a>Anzeigen der Verwendung der online Backup-Speicher  
  
##### <a name="to-view-the-amount-of-storage-space-that-online-backup-uses"></a>So zeigen Sie die Menge an Speicherplatz an, die Online Backup verwendet  
  
1.  Melden Sie sich auf das Dashboard als Administrator an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Auf der **Onlinesicherung** Registerkarte, die **Speicherstatus** im Informationsbereich angezeigt wird.  
  
###  <a name="BKMK_9"></a>Einschließen eines neuen Ordners in die Onlinesicherung  
  
##### <a name="to-include-a-new-folder-in-the-online-backup-policy"></a>Hinzufügen ein neues Ordners in die online Backup-Richtlinie  
  
1.  Melden Sie sich auf das Dashboard als Administrator an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3.  In der **Aufgaben für die Onlinesicherung** Bereich, klicken Sie auf **Configure online Backup**.  
  
4.  Auf der **ändern oder Entfernen der Sicherungsrichtlinie** auf **passen Sie die Online Backup-Richtlinie**.  
  
5.  Auf der **Onlinesicherung konfigurieren** Seite, wenn der Ordner, die Sie einschließen möchten nicht in der Liste angezeigt wird, klicken Sie auf **Hinzufügen von Ordnern**.  
  
6.  In der **Hinzufügen von Ordnern** Fenster, navigieren Sie zu, und wählen Sie den Ordner, die Sie verwenden möchten, in die Onlinesicherung, und klicken Sie dann auf **OK**.  
  
7.  Auf der **Onlinesicherung konfigurieren** Seite, wählen Sie andere Ordner nach Bedarf, und klicken Sie dann auf **Weiter**.  
  
8.  Folgen Sie den Anweisungen im Assistenten zum Anpassen der Richtlinie für der Onlinesicherung abgeschlossen.  
  
 Ausführlichere Informationen zu anderen Einstellungen, die Sie anpassen können, finden Sie unter [Configure online Backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="BKMK_10"></a>Entfernen oder Ausschließen von dateiversionsverlaufssicherungen aus der Richtlinie für die Onlinesicherung  
  
##### <a name="to-remove-or-exclude-a-folder-from-the-online-backup-policy"></a>So entfernen oder Ausschließen eines Ordners aus der Richtlinie für die Onlinesicherung  
  
1.  Melden Sie sich auf das Dashboard als Administrator an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3.  Klicken Sie auf die **geschützte Ordner** Registerkarte. Klicken Sie im Detailbereich zeigt eine Liste der Ordner mit ihren Status der Onlinesicherung angezeigt.  
  
4.  Wählen Sie den Ordner, die Sie verwenden möchten, von der Richtlinie für die Onlinesicherung ausschließen, und klicken Sie dann im Aufgabenbereich auf **Ordner aus Onlinesicherung entfernen**.  
  
###  <a name="BKMK_11"></a>Deaktivieren oder erneutes Aktivieren der Onlineserversicherung  
 Informationen zur Verwendung von Azure Backup sichern oder Wiederherstellen von Serverdaten finden Sie unter [registrieren dieses Server für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
 Informationen zum Beenden der Verwendung von Azure Backup sichern oder Wiederherstellen von Serverdaten finden Sie unter [Aufheben der serverregistrierung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6).  
  
###  <a name="BKMK_12"></a>Beendet eine laufende Sicherung Online-Server  
  
##### <a name="to-stop-an-online-server-backup-in-progress"></a>So beenden Sie eine Online-Server-Sicherung in Bearbeitung  
  
1.  Melden Sie sich auf das Dashboard als Administrator an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  In der **Aufgaben für die Onlinesicherung** Bereich, klicken Sie auf **Sicherung beenden**.  
  
     Nachdem Sie die Sicherung, Status beendet **Canceled** angezeigt wird, für die Sicherung in der **Sicherungsverlauf** Liste.  
  
###  <a name="BKMK_13"></a>Anzeigen des Status der Onlinesicherung  
  
##### <a name="to-view-the-backup-status"></a>So zeigen Sie den Sicherungsstatus an  
  
1.  Melden Sie sich auf das Dashboard als Administrator an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie auf die **Sicherungsverlauf** Registerkarte. Die Listenansicht zeigt den Status jedes Sicherungsauftrags an. Wählen Sie einen Sicherungsauftrag aus, um weitere Detail zum Auftrag anzuzeigen.  
  
###  <a name="BKMK_14"></a>Anzeigen und Verwalten von online Backup-Warnungen  
 Wie viele andere Warnungen werden Warnungen für Azure Backup in der Meldungsanzeige angezeigt.  
  
##### <a name="to-view-online-backup-alerts-in-the-alert-viewer"></a>Online Backup-Warnungen im Alert Viewer anzeigen  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Führen Sie einen der folgenden:  
  
      Windows Server Essentials: Klicken Sie auf im Navigationsbereich auf das Warnungssymbol \ (möglicherweise kritisch, Warnung oder Informational\). Dadurch wird die Meldungsanzeige geöffnet.  
  
      Windows Server Essentials: Auf die **Home** auf die **Überwachung der Integrität** Registerkarte.  
  
3.  Überprüfen Sie die Liste der Warnungen auf Probleme, die im Zusammenhang mit Azure Backup.  
  
 Weitere Informationen zur Verwendung der Meldungsanzeige oder Überwachung der Integrität Registerkarte zur Verwaltung von Warnungen finden Sie unter [Manage System Health](Manage-System-Health-in-Windows-Server-Essentials.md).  
  
###  <a name="BKMK_15"></a>Online-Sicherung auf Standardeinstellungen zurückgesetzt.  
 Windows Server Essentials enthält einen Assistenten, der Sie die Einstellungen für die Onlinesicherung konfigurieren können. Wenn Sie die Standardeinstellungen wiederherstellen möchten, führen Sie die **Configure online Backup** aus, und wählen Sie die **Richtlinie für die Onlinesicherung entfernen** Option. Führen Sie dann die **Configure online Backup** Aufgabe erneut aus. Die zuvor hochgeladenen Daten bleiben unverändert.  
  
###  <a name="BKMK_16"></a>Melden Sie sich für Azure Backup-Dienst  
 Zum Vorbereiten der Microsoft Azure Backup mit Windows Server Essentials integrieren, werden Sie mit Ihrem Microsoft Online Services-Konto im Azure-Verwaltungsportal anmelden und erstellen Sie einen sicherungstresor zum Speichern der Onlinesicherungen in Azure. Sie erhalten dann Azure Backup-Integrationsmodul herunterladen und verwenden die heruntergeladene Datei zum Installieren des Azure Backup Add-In auf dem Windows Server Essentials-Server. Wenn Sie nicht über ein Microsoft-Konto verfügen, können Sie eine kostenlose Testversion registrieren.  
  
 Zum Ausführen von Setup führen führen Sie die folgenden Aufgaben aus:  
  
1.  Melden Sie sich für ein Microsoft Online Services-Konto und die Vorschau der Sicherung an.  
  
2.  Erstellen Sie einen sicherungstresor zum Speichern von Onlinesicherungen.  
  
3.  Herunterladen des Azure Backup-Agents.  
  
4.  Installieren des Azure Backup Add-In auf dem Server.  
  
####  <a name="BKMK_SignupforaMicrosoftOnlineServiceAccount"></a>Melden Sie sich für ein Microsoft Online Services-Konto und die Vorschau der Sicherung  
  
1.  Melden Sie sich bei Windows Server Essentials-Dashboard.  
  
2.  Auf dem Dashboard **Home** auf die **ADD-INS** Kategorie aus, klicken Sie auf **in Azure Backup integrieren**, und klicken Sie dann auf **klicken Sie zur Anmeldung bei Azure Backup**.  
  
3.  Auf den Azure **Recovery Services** Seite der **Backup (Vorschau)** Abschnitt, überprüfen Sie die Detail.  
  
4.  Wenn Sie nicht über ein Azure-Abonnement verfügen, klicken Sie auf **kostenlose Testversion**, und folgen Sie dann die Anweisungen, um ein Azure-Abonnement erhalten.  
  
     Wenn Sie bereits ein Azure-Abonnement verfügen, klicken Sie auf **Portal** in der oberen rechten Ecke der Webseite zum Azure-Verwaltungsportal wechseln.  
  
5.  Auf der Seite Azure-Verwaltungsportal sehen Sie **Recovery Services** im linken Bereich. S, in dem Sie alles verwalten die Sicherung, Dateidepots, den Store Onlinesicherungen Windows Server Essentials.  
  
####  <a name="BKMK_Createabackupvaulttostoreonlinebackups"></a>Erstellen Sie einen sicherungstresor zum Speichern von Onlinesicherungen  
  
1.  Melden Sie sich an den [Azure-Verwaltungsportal](https://manage.windowsazure.com)über den Webbrowser auf dem Windows Server Essentials-Server.  
  
2.  Klicken Sie in der Azure-Verwaltungsportal auf **neu**, klicken Sie auf **Data Services**, klicken Sie auf **Recovery Services**, klicken Sie auf **Sicherungstresor**, und klicken Sie dann auf **Schnellerfassung**.  
  
3.  Geben Sie einen Namen für den sicherungstresor, wählen Sie die Region, in dem Sie die Sicherungen speichern, und klicken Sie dann auf möchten **Schnellerfassung**.  
  
     Die **Recovery Services** Bereich wird mit der neuen sicherungstresor geöffnet.  
  
####  <a name="BKMK_DownloadtheWindowsAzureBackupAgent"></a>Herunterladen des Azure Backup-Agents  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Auf dem Dashboard **Home** auf die **Einstieg in die** auf die **ADD-INS** Kategorie, klicken Sie auf **in Azure Backup integrieren**, und klicken Sie dann auf **klicken Sie zum Herunterladen von Azure Backup-Integrationsmodul**.  
  
####  <a name="BKMK_InstalltheWindowsAzureBackupAddIn"></a>Installieren des Azure Backup Add-In auf dem Server  
  
1.  Melden Sie sich an den Server mit einem Administratorkonto an, und führen Sie die **OnlineBackupAddin.wssx** -Datei, die Sie im vorherigen Schrittheruntergeladen haben.  
  
2.  Die **Software-Lizenzbedingungen** werden angezeigt. Wenn Sie mit den Bestimmungen einverstanden sind, klicken Sie auf **annehmen** um die Installation fortzusetzen.  
  
3.  Auf der **installieren Sie das Add-In** auf **installieren Sie das Add-In**.  
  
    > [!NOTE]
    >  Möglicherweise müssen Sie den Server neu starten, um die erforderliche Software zu installieren.  
  
     Die **Installation** angezeigt wird. Eine Statusanzeige angezeigt, wenn die Installation beginnt, und den Fortschritt der Installation zeigt. Wenn die Installation abgeschlossen ist, erhalten Sie eine Meldung, dass das Azure Backup Add-In erfolgreich installiert wurde.  
  
4.  Klicken Sie auf **Fertig stellen**.  
  
5.  Schließen Sie und öffnen Sie das Dashboard.  
  
     Eine neue Registerkarte **Onlinesicherung**, wird dem Dashboard hinzugefügt. Auf dieser Registerkarte den Server registrieren, sicherungseinstellungen konfigurieren und öffnen Sie **Recovery Services** im Azure-Verwaltungsportal die sicherungstresore für Ihre Server zu verwalten.  
  
 Führen Sie nach Abschluss dieser Schrittefolgende Schritteaus:  
  
1.  Laden Sie ein Zertifikat für Onlinesicherungen in Windows Server Essentials hoch. Weitere Informationen finden Sie unter [Hochladen eines Zertifikats in den Azure Backup-Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1).  
  
2.  Registrieren Sie den Server mit dem Azure Backup-Tresor. Weitere Informationen finden Sie unter [registrieren dieses Server für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
3.  Konfigurieren der Onlinesicherung des Servers. Weitere Informationen finden Sie unter [Configure online Backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="BKMK_17"></a>Integration von Azure Backup mit Windows Server Essentials  
 Das Microsoft Azure Backup-Integrationsmodul ist ein neues Feature von Windows Server Essentials, mit der Sie zum Verschlüsseln und Sichern von Dateien und Ordner von Ihrem Server mit einem Azure gehosteten Speichersystem von Microsoft bereitgestellt. Azure Backup zum Verschlüsseln und Sichern von Daten auf dem Server verwenden, können Sie folgenschwere Verluste wichtiger Geschäftsdaten aufgrund von Feuer, überschwemmungen, Diebstahl oder anderen Notfällen verhindern. Wenn Sie Azure Backup Sichern von Serverdaten verwenden, werden die Informationen verschlüsselt mithilfe Ihrer Passphrase, bevor sie in ein sicheres Datacenter im Internet hochgeladen werden. Zugriff auf Daten aus einem Online-Sicherung, muss einen Server, der durch ein Zertifikat authentifiziert wird und müssen die Passphrase angeben.  
  
 Nach der Integration und Registrierung des Servers beim Azure Backup, können Sie die Einstellungen für die Onlinesicherung um regelmäßig geplante Sicherungen konfigurieren. Sie können auch eine Onlinesicherung jederzeit initiieren, indem Sie auf die **Backup jetzt starten** Aufgabe im Online Backup-Dashboard.  
  
 Die Einrichtung die Onlinesicherung umfasst die folgenden Schritte:  
  
1.  [Melden Sie sich für Azure Backup-Dienst](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16) – nach der Anmeldung für den Dienst Sie erstellen einen sicherungstresor, heruntergeladen und installiert das Azure Backup-Integrationsmodul.  
  
2.  [Ein Zertifikat in den Azure Backup-Tresor hochladen](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
3.  [Registrieren dieses Server für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
4.  [Konfigurieren der Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
> [!NOTE]
>   Azure-Sicherung verwendet die Passphrase zum Verschlüsseln von Dateien und Ordner für die Onlinesicherung. Ändern die verschlüsselungspassphrase ersetzen Sie die Passphrase, die Sie bei der Registrierung des Servers angegeben haben. Die Passphrase werden nur ASCII-codierte Zeichen akzeptiert.  
  
###  <a name="BKMK_18"></a>Schützen von Ordnern für die Onlinesicherung in Windows Server Essentials  
 Die **geschützte Ordner** Unterabschnitt im Abschnitt "Onlinesicherung" des Dashboards zeigt eine Liste aller freigegebenen Ordner auf dem Server. Die folgende Tabelle enthält die Informationen, die in der Liste enthalten ist.  
  
|Spalte|Beschreibung|  
|------------|-----------------|  
|**Name des Ordners:**|Der Name des Ordners, der in die Onlinesicherung enthalten ist.<br /><br /> Führen Sie zum Hinzufügen oder Ausschließen eines Ordners, der **Configure online Backup** Aufgabe.|  
|**Pfad des Ordners:**|Der Speicherort des Ordners.|  
|**Status:**|Es gibt drei Arten von Status **geschützte**, **nicht geschützt**, und **unbekannte**.|  
  
###  <a name="BKMK_19"></a>Verlauf der Onlinesicherung in Windows Server Essentials  
 Die **Sicherungsverlauf** Unterabschnitt im Abschnitt "Onlinesicherung" des Dashboards wird eine Liste der zuletzt erstellten Onlinesicherungen angezeigt. Erfolgreiche Sicherungen können Sie Dateien und Ordner wiederherstellen. Die folgende Tabelle enthält die Informationen, die in der Liste enthalten ist.  
  
|Spalte|Beschreibung|  
|------------|-----------------|  
|**Vorgang:**|Es gibt zwei Arten von Vorgängen - **Sicherung** und **wiederherstellen**.|  
|**Zeit:**|Dies ist die für den letzten Status protokollierte Uhrzeit.|  
|**Status:**|Es gibt fünf Statusarten **Erfolg**, **In Bearbeitung**, **Canceled**, **Warnung**, und **nicht erfolgreich**.|  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Microsoft Online Services](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
