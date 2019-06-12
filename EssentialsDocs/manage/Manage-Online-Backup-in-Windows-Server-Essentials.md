---
title: Verwalten der Onlinesicherung in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: c0357c1a2dc0bebee11355d1e2d1faa2dc80d06a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433293"
---
# <a name="manage-online-backup-in-windows-server-essentials"></a>Verwalten der Onlinesicherung in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 Nach der Integration mit Microsoft Azure Backup die **Onlinesicherung** Management-Seite wird im Windows Server Essentials-Dashboard angezeigt. Auf der Seite **Onlinesicherung** können Sie allgemeine administrative Aufgaben ausführen. Die Funktionen auf der Seite „Onlinesicherung“ umfassen Folgendes:  
  
- Die folgenden Unterabschnitte:  
  
  -   **Onlinesicherung** Nachdem Sie den Server für die Onlinesicherung registriert haben, werden in diesem Abschnitt der aktuelle Sicherungsstatus, Speicherstatus und Kontoinformationen angezeigt.  
  
  -   **Geschützte Ordner** dieser Abschnitt enthält alle freigegebenen und dateiversionsverlaufsordner auf dem Server und alle anderen Ordnern, die Sie ausgewählt haben, die in Azure sichern. Die Liste enthält den Ordnernamen, Ordnerpfad und Status für jeden freigegebenen Ordner.  
  
  -   **Sicherungsverlauf** In diesem Abschnitt wird eine Liste der zuletzt erstellten Onlinesicherungen angezeigt. Die Liste enthält den Vorgangstyp sowie die Uhrzeit und den Status jeder Sicherung.  
  
- Ein Detailbereich mit weiteren Informationen zu einem ausgewählten Sicherungs- oder Wiederherstellungsauftrag.  
  
- Ein Aufgabenbereich, der eine Reihe administrativer Aufgaben enthält, die Sie ausführen können.  
  
  Es wird empfohlen, die wichtigsten Unternehmens- und Benutzerdaten zu sichern. Sie sollten z. B. Serverordner sichern, die wichtige Datendateien enthalten. Sie sollten auch den Dateiversionsverlauf für Netzwerkcomputer sichern, die wichtige Informationen enthalten.  
  
  Bei der Entscheidung, welche Daten Sie online sichern, sollten Sie die Sicherungshäufigkeit und die Aufbewahrungsrichtlinie für Sicherungen berücksichtigen, die Sie implementieren möchten. Überprüfen Sie dann Ihr Budget, und ermitteln Sie die Menge des Speicherplatzes, den Sie sich leisten können. Wägen Sie Kosten und Volumen des Speichers gegen Ihre Anforderungen ab, und konfigurieren Sie die Onlinesicherung so, dass ein größtmöglicher Teil Ihrer wichtigen Daten geschützt ist. Preise finden Sie unter [Backup – Preise](https://azure.microsoft.com/pricing/details/backup/).  
  
  In den folgenden Abschnitten werden die verschiedenen Aufgaben der Onlinesicherung beschrieben, die im Windows Server Essentials-Dashboard angezeigt werden können.  
  
## <a name="online-backup-tasks-in-the-dashboard"></a>Aufgaben für die Onlinesicherung im Dashboard  
  
-   [Hochladen eines Zertifikats in Azure Backup-Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Konfigurieren der onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Starten einer onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Wiederherstellen von Dateien und Ordnern aus einer onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Registrieren Sie Ihres Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Serverregistrierung aufheben](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
###  <a name="BKMK_1"></a> Hochladen eines Zertifikats in Azure Backup-Tresor  
 Bevor Sie Azure Backup für onlinesicherungen in Windows Server Essentials verwenden können, müssen Sie für den sicherungstresor zu registrieren ein öffentliches Zertifikat hochladen. Das Zertifikat wird verwendet, um die Azure Backup-Bereitstellung (Agent), im Namen des Abonnementbesitzers Microsoft Online Services-Abonnement zum Verwalten von Ressourcen, die dem Abonnement zugeordneten zu authentifizieren.  
  
> [!NOTE]
>  Bevor Sie das Zertifikat hochladen, müssen Sie die Schritte unter [Sign up for Azure Backup Service](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)ausführen.  
  
##### <a name="to-upload-a-certificate-to-use-with-the-azure-backup-service"></a>So laden Sie ein Zertifikat für die Verwendung mit dem Azure Backup-Dienst hoch  
  
1. Melden Sie sich mit einem Administratorkonto beim Windows Server Essentials-Dashboard an.  
  
2. Klicken Sie auf der **Startseite** des Dashboards auf **ONLINESICHERUNG**.  
  
3. Klicken Sie im Bereich **ONLINESICHERUNG** auf **Zertifikat in den Azure Backup-Tresor hochladen**.  
  
    Öffnet **Wiederherstellungsdienste** im Azure-Verwaltungsportal. Wenn Sie bereits in Azure angemeldet sind, müssen Sie sich mit Ihrem Microsoft-Konto anmelden.  
  
4. Klicken Sie auf den Namen des Sicherungstresors, den Sie für Onlinesicherungen verwenden, um die Seite **Schnellstart** für den Sicherungstresor zu öffnen.  
  
5. Klicken Sie auf **Zertifikat verwalten**.  
  
6. Fügen Sie im Dialogfeld **Zertifikat verwalten** den Pfad des öffentlichen Zertifikats ein, das von Windows Server Essentials generiert wurde. Führen Sie folgende Schritte aus, um den Pfad des öffentlichen Zertifikats zu erhalten:  
  
   1.  Klicken Sie im Windows Server Essentials-Dashboard auf die Registerkarte **Onlinesicherung** .  
  
   2.  Kopieren Sie auf der Seite **Onlinesicherung** den Pfad des generierten Zertifikats.  
  
   3.  Wechseln Sie im Azure-Verwaltungsportal und klicken Sie dann in der **Zertifikat verwalten** Dialogfeld fügen Sie den Pfad, um das generierte öffentliche Zertifikat hochgeladen.  
  
   > [!NOTE]
   >  Sie können auch Ihr eigenes öffentliches Zertifikat verwenden. Um zu erfahren, welches Zertifikat erforderlich ist, klicken Sie auf der Seite **Schnellstart** auf den Link **Zertifikat erwerben**.  
  
   > [!NOTE]
   >   Azure erfordert ein x. 509 v2-Zertifikat mit einem öffentlichen Schlüssel an. Weitere Informationen finden Sie unter [Verwalten von Onlinekonten](https://msdn.microsoft.com/library/azure/dn169036.aspx).  
  
7. Nachdem Sie das Zertifikat ausgewählt haben, klicken Sie auf **OK** (Häkchen).  
  
8. Sie kehren zur Seite **Schnellstart** zurück. Klicken Sie auf **Dashboard**, und stellen Sie sicher, dass das Zertifikat erfolgreich hochgeladen wurde. Nachdem das Zertifikat erfolgreich hochgeladen wurde, zeigt das Dashboard den Fingerabdruck und das Ablaufdatum des Zertifikats an.  
  
   Führen Sie nach Abschluss dieses Vorgangs folgende Schritte aus:  
  
9. Registrieren Sie den Server, mit dem Azure Backup-Dienst. Weitere Informationen finden Sie unter [Registrieren Ihres Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
10. Konfigurieren Sie die Onlinesicherung des Servers. Weitere Informationen finden Sie unter [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="BKMK_2"></a> Konfigurieren der onlinesicherung  
 Nachdem Sie den Server mit Azure Backup registrieren, können Sie Einstellungen für die onlinesicherung in Windows Server Essentials konfigurieren.  
  
##### <a name="to-configure-online-backup"></a>So konfigurieren Sie die Onlinesicherung  
  
1.  Klicken Sie im Registrierungs-Assistenten oder auf der Seite **Onlinesicherung** des Windows Server Essentials-Dashboards auf **Onlinesicherung konfigurieren**. Der Assistent zum Konfigurieren der Onlinesicherung wird angezeigt.  
  
2.  Auf der **Onlinesicherung konfigurieren** Seite des Assistenten das Kontrollkästchen jedes einzelnen Serverordners, die in Azure Backup gesichert werden sollen. Deaktivieren Sie das Kontrollkästchen für jeden Serverordner, der nicht in die Sicherung aufgenommen werden soll. Zum Hinzufügen von Ordnern, die nicht in der Liste angezeigt werden, klicken Sie auf **Ordner hinzufügen**. Nachdem Sie Ihre Auswahl beendet haben, klicken Sie auf **Weiter**.  
  
    > [!NOTE]
    >  Sie können keinen Ordner auswählen, der sich nicht auf dem lokalen Server befindet bzw. in einem Ordner auf einem ReFS-Laufwerk gespeichert ist.  
  
3.  Auf der Seite **Dateiversionsverlaufssicherungen hinzufügen** des Assistenten können Sie auswählen, ob Sie Dateiversionsverlaufssicherungen für Netzwerkcomputer einschließen möchten, die die Funktion "Dateiversionsverlauf" unterstützen. Klicken Sie dann auf **Weiter**, um den Vorgang fortzusetzen.  
  
4.  Konfigurieren Sie auf der Seite **Sicherungszeitplan angeben** des Assistenten die folgenden Einstellungen, und klicken Sie dann auf **Weiter**, um den Vorgang fortzusetzen:  
  
    -   Wählen oder übernehmen Sie die Tageszeit, zur der die Onlinesicherung ausgeführt werden soll. Die Standardzeit beträgt 10:00 Uhr. Sie können auch eine Zeit zur Ausführung einer zweiten Sicherung angeben.  
  
    -   Wählen oder übernehmen Sie die Tage, an denen die Onlinesicherung ausgeführt werden soll. Die Onlinesicherung wird standardmäßig von montags bis freitags ausgeführt.  
  
5.  Wählen Sie auf der Seite **Aufbewahrungsrichtlinie für die Sicherung angeben** des Assistenten die Anzahl der Tage aus, die die Onlinesicherungen beibehalten werden sollen, und klicken Sie anschließend auf **Weiter**. Der Standardwert ist sieben Tage. Sie können Onlinesicherungen auch 15 oder 30 Tage aufbewahren.  
  
    > [!NOTE]
    >   Azure Backup behält immer die letzte Sicherung bei. Wenn das Sicherungsziel nicht über genügend Speicherplatz zum Speichern der Sicherung verfügt, ist der Sicherungsvorgang nicht erfolgreich. Um dies zu vermeiden, erwerben Sie entweder zusätzlichen Speicherplatz, oder verkürzen Sie die Beibehaltungsdauer der Daten. Weitere Informationen zu den Preisen finden Sie unter [Preisdetails](https://azure.microsoft.com/pricing/details/backup/) für Microsoft Azure Backup.  
  
6.  Wenn Sie auf der Seite **Bandbreitennutzung auswählen** des Assistenten die Internetbandbreite einschränken möchten, die der Onlinesicherung zugewiesen ist, wählen Sie **Internet-Bandbreitennutzung aktivieren**aus. Geben Sie mithilfe der Optionen auf der Seite an, wie viel Internetbandbreite von der Onlinesicherung während der Arbeitszeit bzw. außerhalb der Arbeitszeit genutzt werden darf. Definieren Sie dann die Geschäftszeiten und -tage.  
  
    > [!NOTE]
    >   Azure Backup können Sie anpassen, wie die Integration der Software für die Netzwerkbandbreite beim Sichern oder Wiederherstellen von Informationen nutzt. Verwenden eine Technik, die im Allgemeinen als Einschränkung bezeichnet, können Sie steuern, die Menge an Netzwerkbandbreite, die für die Verwendung durch die Sicherung verfügbar ist und Wiederherstellungsprozesse während bestimmter Tages- und Zeitintervalle. Nach dem Aktivieren des Kontrollkästchens **Internet-Bandbreitennutzung aktivieren** im Assistenten zum Konfigurieren der Onlinesicherung können Sie angeben, für welche Arbeitstage und Arbeitszeiten das Bandbreitenlimit gilt. Alle übrigen Zeiten unterliegen dem Grenzwert für arbeitsfreie Stunden. Für beide Grenzwerte sind Bandbreitenbereiche von 256 Kbit/s bis unbegrenzt zulässig.  
  
7.  Nachdem die Konfiguration der Onlinesicherung abgeschlossen ist, klicken Sie auf **Schließen**.  
  
    > [!TIP]
    >  Nach einer erfolgreichen Konfiguration der Sicherung wird auf der Seite **Onlinesicherung** der Status der letzten Onlinesicherung und die vom Sicherungstresor belegte Speicherkapazität angezeigt. Um den Status früherer Sicherungen anzuzeigen, klicken Sie auf **Sicherungsverlauf**.  
  
###  <a name="BKMK_3"></a> Starten einer onlinesicherung  
  
> [!NOTE]
>  Bevor eine Onlinesicherung gestartet werden kann, müssen Sie zuerst die Schritte unter [Registrieren Ihres Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5) und dann [Konfigurieren einer Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2) ausführen.  
  
##### <a name="to-start-an-online-backup-immediately"></a>So starten Sie eine Onlinesicherung sofort  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie im Bereich **Aufgaben für die Onlinesicherung** auf **Sicherung jetzt starten**.  
  
###  <a name="BKMK_4"></a> Wiederherstellen von Dateien und Ordnern aus einer onlinesicherung  
 Der Assistent zum Wiederherstellen von Dateien und Ordnern führt Sie durch die Suche, Auswahl und Wiederherstellung von Dateien und Ordnern, die online gesichert sind. Im Assistenten führen Sie die folgenden Aufgaben aus:  
  
1.  **Auswählen einer onlinesicherung aus der Dateien und Ordner wiederherstellen**  
  
     Wenn Sie den Assistenten zum Wiederherstellen von Dateien und Ordnern ausführen, geben Sie zunächst an, von wo Sie Dateien wiederherstellen möchten: aus einer Onlinesicherung des Servers, bei dem Sie aktuell angemeldet sind, oder aus einer Sicherung eines anderen Servers.  
  
2.  **Wählen Sie einen Server aus der Dateien und Ordner wiederherstellen**  
  
     Wenn Sie Dateien und Ordner von einem anderen Server wiederherstellen möchten, wählen Sie den betreffenden Server aus der Liste der verfügbaren Server aus, und klicken Sie dann auf **Weiter**.  
  
3.  **Wählen Sie ein Volume mit den Dateien und Ordner wiederhergestellt werden**  
  
     Onlinesicherungen enthalten Volumes, die den Volumes auf dem Quellserver für Sicherungen entsprechen. Nachdem Sie das Volume ausgewählt haben, wählen Sie Datum und Uhrzeit der für die Wiederherstellung verwendeten Sicherung aus, und klicken Sie dann auf **Weiter**.  
  
4.  **Wählen Sie Dateien und Ordner wiederherstellen**  
  
     Auf der Seite **Wiederherzustellende Elemente auswählen** des Assistenten können Sie die verschiedenen Ordnerpfade öffnen und das Kontrollkästchen jeder Datei bzw. jedes Ordners aktivieren, die bzw. den Sie wiederherstellen möchten. Nachdem Sie die Dateien ausgewählt haben, klicken Sie auf **Weiter**.  
  
5.  **Geben Sie den Zielspeicherort für die wiederhergestellten Dateien und Ordner**  
  
     Auf der Seite **Wiederherstellungsoptionen angeben** des Assistenten können Sie angeben, an welchem Ort die Dateien und Ordner wiederhergestellt werden sollen. Es gibt zwei Optionen:  
  
    -   **Am ursprünglichen Speicherort wiederherstellen**. Wählen Sie diese Option aus, um Dateien und Ordner an genau dem Speicherort wiederherzustellen, an dem die Sicherung erstellt wurde.  
  
    -   **An einem anderen Speicherort wiederherstellen**.  Wählen Sie diese Option, um einen anderen Speicherort auf dem Server anzugeben, an dem die Dateien wiederhergestellt werden sollen.  
  
         Wenn in der Standardinstallation eine Datei mit dem gleichen Namen wie die Wiederherstellungsdatei bereits am Zielort vorhanden ist, erstellt der Assistent eine Kopie der ursprünglichen Datei. Darüber hinaus wird die Zugriffssteuerungsliste (ACL) aktualisiert, um aktuelle Dateiberechtigungen zu berücksichtigen. Klicken Sie auf **Erweitert**, um die Standardeinstellungen anzupassen.  
  
6.  **Bestätigen der Wiederherstellungsinformationen**  
  
     Die Seite **Wiederherstellungsinformationen bestätigen** enthält eine Zusammenfassung der Wiederherstellungsanweisungen, die Sie angegeben haben. Um die Wiederherstellung der Datei fortzusetzen, müssen Sie die richtige Passphrase für Ihr Onlinesicherungskonto eingeben.  
  
###  <a name="BKMK_5"></a> Registrieren Sie Ihres Servers für die Sicherung  
 Zum Sichern oder Wiederherstellen von Dateien, Ordner und Dateiversionsverlauf Ihres Windows Server Essentials-Servers in Azure Backup, müssen Sie zuerst den Server mit dem Microsoft Azure Backup-Dienst registrieren.  
  
> [!NOTE]
>  Bevor Sie den Server registrieren, müssen Sie ein Zertifikat hochladen, das mit dem Sicherungstresor verwendet wird, in dem die Onlinesicherungen gespeichert werden. Weitere Informationen finden Sie unter [Hochladen eines Zertifikats in den Azure Backup-Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1).  
  
##### <a name="to-register-your-server-with-azure-backup"></a>So registrieren Sie den Server bei Azure Backup  
  
1.  Melden Sie sich als Administrator beim Server an, und öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie im Unterabschnitt **Onlinesicherung** auf **Registrieren**.  
  
4.  Wählen Sie das Zertifikat aus, das Sie mit dem Sicherungstresor für die Onlinesicherungen verwenden möchten. Das Standardzertifikat ist automatisch aktiviert. Wenn Sie ein anderes Zertifikat auswählen möchten, wählen Sie **Durchsuchen**. Klicken Sie dann auf **Weiter**.  
  
5.  Folgen Sie den Anweisungen im Assistenten, um eine Passphrase zu erstellen, und schließen Sie dann die Registrierung ab.  
  
###  <a name="BKMK_6"></a> Serverregistrierung aufheben  
  
> [!CAUTION]
>  Wenn Sie Aufheben der Registrierung Ihrer Windows Server Essentials-Servers aus dem Microsoft Azure Backup-Dienst kann Azure Backup Server nicht mehr sichern. Darüber hinaus werden die zuvor hochgeladenen Serverdaten gelöscht. Um Onlinesicherungen fortzusetzen, müssen Sie den Server erneut registrieren.  
  
##### <a name="to-unregister-your-server-with-azure-backup"></a>So heben Sie die Serverregistrierung bei Azure Backup auf  
  
1.  Melden Sie sich beim [Azure-Verwaltungsportal](https://manage.windowsazure.com)an.  
  
2.  Klicken Sie auf **Recovery Services**.  
  
3.  Klicken Sie in **Recovery Services**auf den Namen des Sicherungstresors.  
  
4.  Klicken Sie auf der Seite **Schnellstart** des Tresors auf **Server**.  
  
5.  Wählen Sie den Server aus, klicken Sie auf **Löschen**, und klicken Sie dann zur Bestätigung auf **Ja**.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Ändern Sie die Richtlinie für die onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Anzeigen der Verwendung der online backup-Speicher](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Einschließen eines neuen Ordners in die onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Entfernen oder Ausschließen von dateiversionsverlaufssicherungen aus der Richtlinie für die onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Deaktivieren oder erneutes Aktivieren der onlineserversicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Beenden einer online-Server-Sicherung wird ausgeführt](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [Anzeigen des Status der onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [Anzeigen und Verwalten von Warnungen zur onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [Online-Sicherung auf Standardeinstellungen zurücksetzen](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_15)  
  
-   [Melden Sie sich für Azure Backup-Dienst](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)  
  
-   [Integration von Azure Backup mit Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_17)  
  
-   [Schützen von Ordnern für die onlinesicherung in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_18)  
  
-   [Verlauf der onlinesicherung in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_19)  
  
###  <a name="BKMK_7"></a> Ändern Sie die Richtlinie für die onlinesicherung  
 Im Windows Server Essentials-Dashboard können Sie die Richtlinie für die Onlinesicherung ganz einfach ändern.  
  
##### <a name="to-change-the-online-backup-policy"></a>So ändern Sie die Richtlinie für die Onlinesicherung  
  
1. Melden Sie sich als Administrator beim Dashboard an.  
  
2. Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3. Klicken Sie im Bereich **Aufgaben für die Onlinesicherung** auf **Onlinesicherung konfigurieren**.  
  
4. Folgen Sie den Anweisungen im Assistenten, um die Richtlinie für die Onlinesicherung anzupassen.  
  
   Ausführlichere Informationen zu den Einstellungen, die Sie anpassen können, finden Sie unter [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="BKMK_8"></a> Anzeigen der Verwendung der online backup-Speicher  
  
##### <a name="to-view-the-amount-of-storage-space-that-online-backup-uses"></a>So zeigen Sie die Menge des von der Onlinesicherung verwendeten Speicherplatzes an  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Auf der Registerkarte **Onlinesicherung** wird der **Speicherstatus** im Informationsbereich angezeigt.  
  
###  <a name="BKMK_9"></a> Einschließen eines neuen Ordners in die onlinesicherung  
  
##### <a name="to-include-a-new-folder-in-the-online-backup-policy"></a>So schließen Sie einen neuen Ordner in die Richtlinie für die Onlinesicherung ein  
  
1. Melden Sie sich als Administrator beim Dashboard an.  
  
2. Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3. Klicken Sie im Bereich **Aufgaben für die Onlinesicherung** auf **Onlinesicherung konfigurieren**.  
  
4. Klicken Sie auf der Seite **Sicherungsrichtlinie ändern oder entfernen** auf **Richtlinie für die Onlinesicherungen anpassen**.  
  
5. Wenn der gewünschte Ordner auf der Seite **Onlinesicherung konfigurieren** nicht in der Liste angezeigt wird, klicken Sie auf **Ordner hinzufügen**.  
  
6. Navigieren Sie im Fenster **Ordner hinzufügen** zum Ordner, den Sie in die Onlinesicherung aufnehmen möchten, und wählen Sie ihn aus. Klicken Sie dann auf **OK**.  
  
7. Wählen Sie auf der Seite **Onlinesicherung konfigurieren** andere Ordner nach Bedarf aus, und klicken Sie dann auf **Weiter**.  
  
8. Folgen Sie den Anweisungen im Assistenten, um die Richtlinie für die Onlinesicherung anzupassen.  
  
   Ausführlichere Informationen zu anderen Einstellungen, die Sie anpassen können, finden Sie unter [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="BKMK_10"></a> Entfernen oder Ausschließen von dateiversionsverlaufssicherungen aus der Richtlinie für die onlinesicherung  
  
##### <a name="to-remove-or-exclude-a-folder-from-the-online-backup-policy"></a>So entfernen oder schließen Sie einen Ordner aus der Richtlinie für die Onlinesicherung aus  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3.  Klicken Sie auf die Registerkarte **Geschützte Ordner**. Im Detailbereich wird eine Liste der Ordner mit dem entsprechenden Status der Onlinesicherung angezeigt.  
  
4.  Wählen Sie den Ordner, den Sie aus der Richtlinie für die Onlinesicherung ausschließen möchten, aus, und klicken Sie dann im Aufgabenbereich auf **Ordner aus Onlinesicherung entfernen**.  
  
###  <a name="BKMK_11"></a> Deaktivieren oder erneutes Aktivieren der onlineserversicherung  
 Anweisungen zur Verwendung von Azure Backup zu sichern oder Wiederherstellen von Serverdaten finden Sie [registrieren dieses Server für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
 Anweisungen zum Beenden der Verwendung von Azure Backup zu sichern oder Wiederherstellen von Serverdaten finden Sie [Aufheben der serverregistrierung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6).  
  
###  <a name="BKMK_12"></a> Beenden einer online-Server-Sicherung wird ausgeführt  
  
##### <a name="to-stop-an-online-server-backup-in-progress"></a>So beenden Sie eine laufende Onlineserversicherung  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie im Bereich **Aufgaben für die Onlinesicherung** auf **Sicherung beenden**.  
  
     Nachdem Sie die Sicherung beendet haben, wird in der Liste **Sicherungsverlauf** der Status **Abgebrochen** für die Sicherung angezeigt.  
  
###  <a name="BKMK_13"></a> Anzeigen des Status der onlinesicherung  
  
##### <a name="to-view-the-backup-status"></a>So zeigen Sie den Sicherungsstatus an  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie auf die Registerkarte **Sicherungsverlauf** . Die Liste zeigt den Status jedes Sicherungsauftrags an. Wählen Sie einen Sicherungsauftrag aus, um weitere Details zum Auftrag anzuzeigen.  
  
###  <a name="BKMK_14"></a> Anzeigen und Verwalten von Warnungen zur onlinesicherung  
 Wie viele andere Warnungen werden Warnungen für Azure Backup in der Meldungsanzeige angezeigt.  
  
##### <a name="to-view-online-backup-alerts-in-the-alert-viewer"></a>So zeigen Sie Warnungen für die Onlinesicherung in der Meldungsanzeige an  
  
1. Öffnen Sie das Dashboard.  
  
2. Führen Sie eines der folgenden Verfahren aus:  
  
     Windows Server Essentials: Klicken Sie auf im Navigationsbereich auf das Symbol "Benachrichtigungen" \(möglicherweise kritisch, Warnung oder Information\). Daraufhin wird die Meldungsanzeige geöffnet.  
  
     Windows Server Essentials: Klicken Sie auf der **Startseite** auf die Registerkarte **Systemüberwachung**.  
  
3. Überprüfen Sie die Liste der Warnungen auf Probleme, die im Zusammenhang mit Azure Backup aus.  
  
   Weitere Informationen zur Verwendung der Meldungsanzeige oder Überwachung der Integrität Registerkarte zum Verwalten von Warnungen finden Sie unter [Manage System Health](Manage-System-Health-in-Windows-Server-Essentials.md).  
  
###  <a name="BKMK_15"></a> Online-Sicherung auf Standardeinstellungen zurücksetzen  
 Windows Server Essentials enthält einen Assistenten, mit dem Sie die Einstellungen für die Onlinesicherung konfigurieren können. Wenn Sie die Standardeinstellungen wiederherstellen möchten, führen Sie die Aufgabe **Onlinesicherung konfigurieren** aus, und wählen Sie die Option **Richtlinie für die Onlinesicherung entfernen** aus. Führen Sie dann die Aufgabe **Onlinesicherung konfigurieren** erneut aus. Die zuvor hochgeladenen Daten bleiben unverändert.  
  
###  <a name="BKMK_16"></a> Melden Sie sich für Azure Backup-Dienst  
 Zum Vorbereiten der Microsoft Azure Backup mit Windows Server Essentials integrieren, Sie melden Sie sich bei Azure-Verwaltungsportal mit Ihrem Microsoft Online Services-Konto, und klicken Sie dann einen sicherungstresor zum Speichern der onlinesicherungen in Azure zu erstellen. Sie müssen dann das Azure Backup-Integrationsmodul herunterladen und verwenden die heruntergeladene Datei zum Installieren des Azure Backup-Add-Ins auf dem Windows Server Essentials-Server. Wenn Sie nicht über ein Microsoft-Konto verfügen, können Sie sich für eine kostenlose Testversion registrieren.  
  
 Zum Ausführen von Setup führen Sie die folgenden Aufgaben aus:  
  
1.  Registrieren Sie sich für ein Microsoft Online Services-Konto und die Vorschau der Sicherung.  
  
2.  Erstellen Sie einen Sicherungstresor zum Speichern von Onlinesicherungen.  
  
3.  Laden Sie Azure Backup-Agent herunter.  
  
4.  Installieren des Azure Backup-Add-Ins auf dem Server.  
  
####  <a name="BKMK_SignupforaMicrosoftOnlineServiceAccount"></a> Melden Sie sich für ein Microsoft Online Services-Konto und die Vorschau der Sicherung  
  
1.  Melden Sie sich beim Windows Server Essentials-Dashboard an.  
  
2.  Klicken Sie auf der **Startseite** des Dashboards auf die Kategorie **ADD-INS**, klicken Sie auf **In Azure Backup integrieren**, und klicken Sie dann auf **Zur Registrierung für Azure Backup klicken**.  
  
3.  Auf den über Azure **Wiederherstellungsdienste** auf der Seite die **Backup (Vorschau)** Abschnitt, überprüfen Sie die Details.  
  
4.  Wenn Sie nicht über ein Azure-Abonnement verfügen, klicken Sie auf **kostenlose Testversion**, und befolgen Sie dann die Anweisungen zum Abrufen eines Azure-Abonnements.  
  
     Wenn Sie bereits über ein Azure-Abonnement verfügen, klicken Sie auf **Portal** in der oberen rechten Ecke der Webseite, um das Azure-Verwaltungsportal aufzurufen.  
  
5.  Klicken Sie auf der Seite Azure-Verwaltungsportal sehen Sie **Wiederherstellungsdienste** im linken Bereich. Das ist, in dem Sie die backup-Tresor verwalten möchten, die Speichern der onlinesicherungen in Windows Server Essentials.  
  
####  <a name="BKMK_Createabackupvaulttostoreonlinebackups"></a> Erstellen Sie einen sicherungstresor zum Speichern von onlinesicherungen  
  
1.  Melden Sie sich über den Webbrowser Ihres Windows Server Essentials-Servers beim [Azure-Verwaltungsportal](https://manage.windowsazure.com)an.  
  
2.  Klicken Sie in der Azure-Verwaltungsportal auf **neu**, klicken Sie auf **Datendienste**, klicken Sie auf **Wiederherstellungsdienste**, klicken Sie auf **Backup-Tresor**, und klicken Sie dann Klicken Sie auf **Schnellerfassung**.  
  
3.  Geben Sie einen Namen für den Sicherungstresor ein, wählen Sie die Region aus, in der Sie die Sicherungen speichern möchten, und klicken Sie dann auf **Schnellerfassung**.  
  
     Der Bereich **Recovery Services** wird mit dem neuen Sicherungstresor geöffnet.  
  
####  <a name="BKMK_DownloadtheWindowsAzureBackupAgent"></a> Azure Backup-Agent herunterladen  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der **Startseite** des Dashboards auf die Registerkarte **Erste Schritte**, auf die Kategorie **ADD-INS**, auf **In Azure Backup integrieren** und auf **Zum Herunterladen des Azure Backup-Integrationsmoduls klicken**.  
  
####  <a name="BKMK_InstalltheWindowsAzureBackupAddIn"></a> Installieren des Azure Backup-Add-Ins auf dem server  
  
1. Melden Sie sich mit einem Administratorkonto bei Ihrem Server an, und führen Sie die Datei **OnlineBackupAddin.wssx** aus, die Sie im vorherigen Schritt heruntergeladen haben.  
  
2. Die **Software-Lizenzbedingungen** werden angezeigt. Wenn Sie den Bedingungen zustimmen, klicken Sie auf **Annehmen**, um die Installation fortzusetzen.  
  
3. Klicken Sie auf der Seite **Add-In installieren** auf **Add-In installieren**.  
  
   > [!NOTE]
   >  Sie müssen den Server u. U. neu starten, um die erforderliche Software zu installieren.  
  
    Die Seite **Installation** wird angezeigt. Eine Statusleiste zeigt den Beginn und den Fortschritt der Installation an. Wenn die Installation abgeschlossen ist, erhalten Sie eine Meldung, dass das Azure Backup-Add-in erfolgreich installiert wurde.  
  
4. Klicken Sie auf **Fertig stellen**.  
  
5. Schließen Sie das Dashboard, und öffnen Sie es erneut.  
  
    Eine neue Registerkarte **Onlinesicherung**wird dem Dashboard hinzugefügt. Auf dieser Registerkarte können Sie den Server registrieren, sicherungseinstellungen konfigurieren und öffnen Sie **Wiederherstellungsdienste** in das Azure-Verwaltungsportal, um die sicherungstresore für Ihre Server zu verwalten.  
  
   Führen Sie nach Abschluss dieses Vorgangs folgende Schritte aus:  
  
6. Laden Sie ein Zertifikat für onlinesicherungen in Windows Server Essentials hoch. Weitere Informationen finden Sie unter [Hochladen eines Zertifikats in den Azure Backup-Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1).  
  
7. Registrieren Sie den Server mit Azure Backup-Tresor ein. Weitere Informationen finden Sie unter [Registrieren Ihres Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
8. Konfigurieren Sie die Onlinesicherung des Servers. Weitere Informationen finden Sie unter [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="BKMK_17"></a> Integration von Azure Backup mit Windows Server Essentials  
 Das Microsoft Azure Backup-Integrationsmodul ist ein neues Feature von Windows Server Essentials, mit der Sie zum Verschlüsseln und Sichern von Dateien und Ordnern von Ihrem Server mit einem Azure gehosteten Speichersystem, die von Microsoft bereitgestellt werden. Azure Backup zum Verschlüsseln und Sichern Sie Daten auf dem Server verwenden, können Sie folgenschwere Verluste wichtiger Geschäftsdaten aufgrund von Feuer, Überflutung, Diebstahl oder anderen Notfällen verhindern. Wenn Sie Azure Backup zum Sichern der Serverdaten verwenden, werden die Informationen verschlüsselt mithilfe Ihrer Passphrase aus, bevor sie in ein sicheres Datacenter im Internet hochgeladen werden. Um auf Daten aus einer Onlinesicherung zuzugreifen, benötigen Sie einen Server, der durch ein Zertifikat authentifiziert wird, und Sie müssen die Passphrase angeben.  
  
 Nach der Integration und Registrierung des Servers mit Azure Backup, können Sie Einstellungen für die onlinesicherung zum Ausführen von regelmäßig geplanter Sicherungen konfigurieren. Sie können eine Onlinesicherung auch jederzeit initiieren, indem Sie im Dashboard für die Onlinesicherung auf die Aufgabe **Backup jetzt starten** klicken.  
  
 Die Einrichtung der Onlinesicherung umfasst die folgenden Schritte:  
  
1.  [Melden Sie sich für Azure Backup-Dienst](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16) – nach der Anmeldung für den Backup-Dienst, einen sicherungstresor erstellen, laden Sie und der Azure Backup-Integrationsmodul installieren.  
  
2.  [Hochladen eines Zertifikats in Azure Backup-Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
3.  [Registrieren Sie Ihres Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
4.  [Konfigurieren der onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
> [!NOTE]
>   Azure Backup verwendet die Passphrase zum Verschlüsseln von Dateien und Ordner für die onlinesicherung. Indem Sie die Verschlüsselungs-Passphrase ändern, ersetzen Sie die Passphrase, die Sie bei der Registrierung des Servers angegeben haben. Für die Passphrase werden nur ASCII-codierte Zeichen akzeptiert.  
  
###  <a name="BKMK_18"></a> Schützen von Ordnern für die onlinesicherung in Windows Server Essentials  
 Der Unterabschnitt **Geschützte Ordner** im Abschnitt „Onlinesicherung“ des Dashboards enthält eine Liste aller freigegebenen Ordner auf dem Server. Die folgende Tabelle beschreibt die Informationen, die in der Liste enthalten sind.  
  
|Spalte|Beschreibung|  
|------------|-----------------|  
|**Ordnername:**|Der Name des Ordners, der in die Onlinesicherung eingeschlossen wurde.<br /><br /> Führen Sie zum Hinzufügen oder Ausschließen eines Ordners die Aufgabe **Onlinesicherung konfigurieren** aus.|  
|**Ordnerpfad:**|Der Speicherort des Ordners.|  
|**Status:**|Es gibt drei Statusarten – **geschützte**, **nicht geschützt**, und **unbekannte**.|  
  
###  <a name="BKMK_19"></a> Verlauf der onlinesicherung in Windows Server Essentials  
 Der Unterabschnitt **Sicherungsverlauf** des Abschnitts „Onlinesicherung“ im Dashboard enthält eine Liste der zuletzt erstellten Onlinesicherungen. Erfolgreiche Sicherungen können zum Wiederherstellen von Dateien und Ordnern verwendet werden. Die folgende Tabelle beschreibt die Informationen, die in der Liste enthalten sind.  
  
|Spalte|Beschreibung|  
|------------|-----------------|  
|**Vorgang:**|Es gibt zwei Arten von Vorgängen - **Sichern** und **Wiederherstellen**.|  
|**Zeit:**|Dies ist die für den letzten Status protokollierte Uhrzeit.|  
|**Status:**|Es gibt fünf Statusarten – **Erfolg**, **In Bearbeitung**, **Canceled**, **Warnung**, und **nicht erfolgreich**.|  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten der Sicherung und Wiederherstellung](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Microsoft Online Services](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
