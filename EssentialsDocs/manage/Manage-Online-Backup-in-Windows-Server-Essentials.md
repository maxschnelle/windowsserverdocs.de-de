---
title: Verwalten der Onlinesicherung in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95a9f593-fad7-4335-bd4d-c7bb8c033efb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 0879f0300892e26e1afb9b33e857ce0e255308ee
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311206"
---
# <a name="manage-online-backup-in-windows-server-essentials"></a>Verwalten der Onlinesicherung in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 Nachdem Sie mit Microsoft Azure Backup integriert haben, wird die Verwaltungsseite für die **Online Sicherung** im Windows Server Essentials-Dashboard angezeigt. Auf der Seite **Onlinesicherung** können Sie allgemeine administrative Aufgaben ausführen. Die Funktionen auf der Seite „Onlinesicherung“ umfassen Folgendes:  
  
- Die folgenden Unterabschnitte:  
  
  -   **Onlinesicherung** Nachdem Sie den Server für die Onlinesicherung registriert haben, werden in diesem Abschnitt der aktuelle Sicherungsstatus, Speicherstatus und Kontoinformationen angezeigt.  
  
  -   **Geschützte Ordner** In diesem Abschnitt werden alle freigegebenen Ordner und alle Datei Versions Verlaufs Ordner auf dem Server sowie alle anderen Ordner aufgelistet, die Sie für die Sicherungskopie in Azure ausgewählt haben. Die Liste enthält den Ordnernamen, Ordnerpfad und Status für jeden freigegebenen Ordner.  
  
  -   **Sicherungsverlauf** In diesem Abschnitt wird eine Liste der zuletzt erstellten Onlinesicherungen angezeigt. Die Liste enthält den Vorgangstyp sowie die Uhrzeit und den Status jeder Sicherung.  
  
- Ein Detailbereich mit weiteren Informationen zu einem ausgewählten Sicherungs- oder Wiederherstellungsauftrag.  
  
- Ein Aufgabenbereich, der eine Reihe administrativer Aufgaben enthält, die Sie ausführen können.  
  
  Es wird empfohlen, die wichtigsten Unternehmens- und Benutzerdaten zu sichern. Sie sollten z. B. Serverordner sichern, die wichtige Datendateien enthalten. Sie sollten auch den Dateiversionsverlauf für Netzwerkcomputer sichern, die wichtige Informationen enthalten.  
  
  Bei der Entscheidung, welche Daten Sie online sichern, sollten Sie die Sicherungshäufigkeit und die Aufbewahrungsrichtlinie für Sicherungen berücksichtigen, die Sie implementieren möchten. Überprüfen Sie dann Ihr Budget, und ermitteln Sie die Menge des Speicherplatzes, den Sie sich leisten können. Wägen Sie Kosten und Volumen des Speichers gegen Ihre Anforderungen ab, und konfigurieren Sie die Onlinesicherung so, dass ein größtmöglicher Teil Ihrer wichtigen Daten geschützt ist. Preise finden Sie unter [Backup – Preise](https://azure.microsoft.com/pricing/details/backup/).  
  
  In den folgenden Abschnitten werden die verschiedenen Aufgaben der Onlinesicherung beschrieben, die im Windows Server Essentials-Dashboard angezeigt werden können.  
  
## <a name="online-backup-tasks-in-the-dashboard"></a>Aufgaben für die Onlinesicherung im Dashboard  
  
-   [Hochladen eines Zertifikats in den Azure Backup Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Konfigurieren der Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Starten einer Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Wiederherstellen von Dateien und Ordnern aus einer Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Diesen Server für die Sicherung registrieren](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Aufheben der Registrierung des Servers](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
###  <a name="upload-a-certificate-to-the-azure-backup-vault"></a><a name="BKMK_1"></a>Hochladen eines Zertifikats in den Azure Backup Tresor  
 Bevor Sie Azure Backup für Online Sicherungen in Windows Server Essentials verwenden können, müssen Sie ein öffentliches Zertifikat hochladen, um sich beim Sicherungs Tresor zu registrieren. Das Zertifikat wird verwendet, um die Azure Backup Bereitstellung (den Agent) zu authentifizieren, die im Auftrag des Microsoft Online Services-Abonnement Besitzers fungiert, um die dem Abonnement zugeordneten Ressourcen zu verwalten.  
  
> [!NOTE]
>  Bevor Sie das Zertifikat hochladen, müssen Sie die Schritte unter [Registrieren für den Azure Backup-Dienst](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16) ausführen.  
  
##### <a name="to-upload-a-certificate-to-use-with-the-azure-backup-service"></a>So laden Sie ein Zertifikat für die Verwendung mit dem Azure Backup-Dienst hoch  
  
1. Melden Sie sich mit einem Administratorkonto beim Windows Server Essentials-Dashboard an.  
  
2. Klicken Sie auf der **Startseite** des Dashboards auf **ONLINESICHERUNG**.  
  
3. Klicken Sie im Bereich **ONLINESICHERUNG** auf **Zertifikat in den Azure Backup-Tresor hochladen**.  
  
    Damit wird **Recovery Services** im Azure-Verwaltungsportal geöffnet. Wenn Sie noch nicht bei Azure angemeldet sind, müssen Sie sich mit Ihrem Microsoft-Konto anmelden.  
  
4. Klicken Sie auf den Namen des Sicherungstresors, den Sie für Onlinesicherungen verwenden, um die Seite **Schnellstart** für den Sicherungstresor zu öffnen.  
  
5. Klicken Sie auf **Zertifikat verwalten**.  
  
6. Fügen Sie im Dialogfeld **Zertifikat verwalten** den Pfad des öffentlichen Zertifikats ein, das von Windows Server Essentials generiert wurde. Führen Sie folgende Schritte aus, um den Pfad des öffentlichen Zertifikats zu erhalten:  
  
   1.  Klicken Sie im Windows Server Essentials-Dashboard auf die Registerkarte **Onlinesicherung**.  
  
   2.  Kopieren Sie auf der Seite **Onlinesicherung** den Pfad des generierten Zertifikats.  
  
   3.  Wechseln Sie zum Azure-Verwaltungsportal, und fügen Sie dann im Dialogfeld **Zertifikat verwalten** den Pfad ein, in den das generierte öffentliche Zertifikat hochgeladen werden soll.  
  
   > [!NOTE]
   >  Sie können auch Ihr eigenes öffentliches Zertifikat verwenden. Um zu erfahren, welches Zertifikat erforderlich ist, klicken Sie auf der Seite **Schnellstart** auf den Link **Zertifikat erwerben**.  
  
   > [!NOTE]
   >   Azure erfordert ein x. 509 v2-Zertifikat mit einem öffentlichen Schlüssel. Weitere Informationen finden Sie unter [Verwalten von Onlinekonten](https://msdn.microsoft.com/library/azure/dn169036.aspx).  
  
7. Nachdem Sie das Zertifikat ausgewählt haben, klicken Sie auf **OK** (Häkchen).  
  
8. Sie kehren zur Seite **Schnellstart** zurück. Klicken Sie auf **Dashboard**, und stellen Sie sicher, dass das Zertifikat erfolgreich hochgeladen wurde. Nachdem das Zertifikat erfolgreich hochgeladen wurde, zeigt das Dashboard den Fingerabdruck und das Ablaufdatum des Zertifikats an.  
  
   Führen Sie nach Abschluss dieses Vorgangs folgende Schritte aus:  
  
9. Registrieren Sie den Server beim Azure Backup-Dienst. Weitere Informationen finden Sie unter [Registrieren Ihres Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
10. Konfigurieren Sie die Onlinesicherung des Servers. Weitere Informationen finden Sie unter [Konfigurieren einer Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="configure-online-backup"></a><a name="BKMK_2"></a>Konfigurieren der Online Sicherung  
 Nachdem Sie den Server bei Azure Backup registriert haben, können Sie die Einstellungen für die Online Sicherung in Windows Server Essentials konfigurieren.  
  
##### <a name="to-configure-online-backup"></a>So konfigurieren Sie die Onlinesicherung  
  
1.  Klicken Sie im Registrierungs-Assistenten oder auf der Seite **Onlinesicherung** des Windows Server Essentials-Dashboards auf **Onlinesicherung konfigurieren**. Der Assistent zum Konfigurieren der Onlinesicherung wird angezeigt.  
  
2.  Aktivieren Sie auf der Seite **Online Sicherung konfigurieren** des Assistenten das Kontrollkästchen für jeden Server Ordner, den Sie auf Azure Backup sichern möchten. Deaktivieren Sie das Kontrollkästchen für jeden Serverordner, der nicht in die Sicherung aufgenommen werden soll. Zum Hinzufügen von Ordnern, die nicht in der Liste angezeigt werden, klicken Sie auf **Ordner hinzufügen**. Nachdem Sie Ihre Auswahl beendet haben, klicken Sie auf **Weiter**.  
  
    > [!NOTE]
    >  Sie können keinen Ordner auswählen, der sich nicht auf dem lokalen Server befindet bzw. in einem Ordner auf einem ReFS-Laufwerk gespeichert ist.  
  
3.  Auf der Seite **Dateiversionsverlaufssicherungen hinzufügen** des Assistenten können Sie auswählen, ob Sie Dateiversionsverlaufssicherungen für Netzwerkcomputer einschließen möchten, die die Funktion "Dateiversionsverlauf" unterstützen. Klicken Sie dann auf **Weiter**, um den Vorgang fortzusetzen.  
  
4.  Konfigurieren Sie auf der Seite **Sicherungszeitplan angeben** des Assistenten die folgenden Einstellungen, und klicken Sie dann auf **Weiter**, um den Vorgang fortzusetzen:  
  
    -   Wählen oder übernehmen Sie die Tageszeit, zur der die Onlinesicherung ausgeführt werden soll. Die Standardzeit beträgt 10:00 Uhr. Sie können auch eine Zeit zur Ausführung einer zweiten Sicherung angeben.  
  
    -   Wählen oder übernehmen Sie die Tage, an denen die Onlinesicherung ausgeführt werden soll. Die Onlinesicherung wird standardmäßig von montags bis freitags ausgeführt.  
  
5.  Wählen Sie auf der Seite **Aufbewahrungsrichtlinie für die Sicherung angeben** des Assistenten die Anzahl der Tage aus, die die Onlinesicherungen beibehalten werden sollen, und klicken Sie anschließend auf **Weiter**. Der Standardwert ist sieben Tage. Sie können Onlinesicherungen auch 15 oder 30 Tage aufbewahren.  
  
    > [!NOTE]
    >   Azure Backup behält immer die letzte Sicherung bei. Wenn das Sicherungsziel nicht über genügend Speicherplatz zum Speichern der Sicherung verfügt, ist der Sicherungsvorgang nicht erfolgreich. Um dies zu vermeiden, erwerben Sie entweder zusätzlichen Speicherplatz, oder verkürzen Sie die Beibehaltungsdauer der Daten. Preisinformationen finden Sie unter [Preis Details](https://azure.microsoft.com/pricing/details/backup/) für Microsoft Azure Backup.  
  
6.  Wenn Sie auf der Seite **Bandbreitennutzung auswählen** des Assistenten die Internetbandbreite einschränken möchten, die der Onlinesicherung zugewiesen ist, wählen Sie **Internet-Bandbreitennutzung aktivieren** aus. Geben Sie mithilfe der Optionen auf der Seite an, wie viel Internetbandbreite von der Onlinesicherung während der Arbeitszeit bzw. außerhalb der Arbeitszeit genutzt werden darf. Definieren Sie dann die Geschäftszeiten und -tage.  
  
    > [!NOTE]
    >   Mit Azure Backup können Sie anpassen, wie die Netzwerkbandbreite beim Sichern oder Wiederherstellen von Informationen von der Integrationssoftware verwendet wird. Mithilfe eines Verfahrens, das häufig als Drosselung bezeichnet wird, können Sie den Umfang der Netzwerkbandbreite steuern, der für die Sicherungs-und Wiederherstellungs Prozesse während bestimmter Tages-und Zeitintervalle verfügbar ist. Nach dem Aktivieren des Kontrollkästchens **Internet-Bandbreitennutzung aktivieren** im Assistenten zum Konfigurieren der Onlinesicherung können Sie angeben, für welche Arbeitstage und Arbeitszeiten das Bandbreitenlimit gilt. Alle übrigen Zeiten unterliegen dem Grenzwert für arbeitsfreie Stunden. Für beide Grenzwerte sind Bandbreitenbereiche von 256 Kbit/s bis unbegrenzt zulässig.  
  
7.  Nachdem die Konfiguration der Onlinesicherung abgeschlossen ist, klicken Sie auf **Schließen**.  
  
    > [!TIP]
    >  Nach einer erfolgreichen Konfiguration der Sicherung wird auf der Seite **Onlinesicherung** der Status der letzten Onlinesicherung und die vom Sicherungstresor belegte Speicherkapazität angezeigt. Um den Status früherer Sicherungen anzuzeigen, klicken Sie auf **Sicherungsverlauf**.  
  
###  <a name="start-an-online-backup"></a><a name="BKMK_3"></a>Starten einer Online Sicherung  
  
> [!NOTE]
>  Bevor eine Onlinesicherung gestartet werden kann, müssen Sie zuerst die Schritte unter [Registrieren Ihres Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5) und dann [Konfigurieren einer Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2) ausführen.  
  
##### <a name="to-start-an-online-backup-immediately"></a>So starten Sie eine Onlinesicherung sofort  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie im Bereich **Aufgaben für die Onlinesicherung** auf **Sicherung jetzt starten**.  
  
###  <a name="restore-files-and-folders-from-an-online-backup"></a><a name="BKMK_4"></a>Wiederherstellen von Dateien und Ordnern aus einer Online Sicherung  
 Der Assistent zum Wiederherstellen von Dateien und Ordnern führt Sie durch die Suche, Auswahl und Wiederherstellung von Dateien und Ordnern, die online gesichert sind. Im Assistenten führen Sie die folgenden Aufgaben aus:  
  
1.  **Auswählen einer Online Sicherung, aus der Dateien und Ordner wieder hergestellt werden**  
  
     Wenn Sie den Assistenten zum Wiederherstellen von Dateien und Ordnern ausführen, geben Sie zunächst an, von wo Sie Dateien wiederherstellen möchten: aus einer Onlinesicherung des Servers, bei dem Sie aktuell angemeldet sind, oder aus einer Sicherung eines anderen Servers.  
  
2.  **Auswählen eines Servers, von dem Dateien und Ordner wieder hergestellt werden sollen**  
  
     Wenn Sie Dateien und Ordner von einem anderen Server wiederherstellen möchten, wählen Sie den betreffenden Server aus der Liste der verfügbaren Server aus, und klicken Sie dann auf **Weiter**.  
  
3.  **Wählen Sie ein Volume aus, das die wiederherzustellenden Dateien und Ordner enthält.**  
  
     Onlinesicherungen enthalten Volumes, die den Volumes auf dem Quellserver für Sicherungen entsprechen. Nachdem Sie das Volume ausgewählt haben, wählen Sie Datum und Uhrzeit der für die Wiederherstellung verwendeten Sicherung aus, und klicken Sie dann auf **Weiter**.  
  
4.  **Dateien und Ordner für die Wiederherstellung auswählen**  
  
     Auf der Seite **Wiederherzustellende Elemente auswählen** des Assistenten können Sie die verschiedenen Ordnerpfade öffnen und das Kontrollkästchen jeder Datei bzw. jedes Ordners aktivieren, die bzw. den Sie wiederherstellen möchten. Nachdem Sie die Dateien ausgewählt haben, klicken Sie auf **Weiter**.  
  
5.  **Geben Sie den Ziel Speicherort für wiederhergestellte Dateien und Ordner an.**  
  
     Auf der Seite **Wiederherstellungsoptionen angeben** des Assistenten können Sie angeben, an welchem Ort die Dateien und Ordner wiederhergestellt werden sollen. Es stehen zwei Optionen zur Verfügung:  
  
    -   **Am ursprünglichen Speicherort wiederherstellen**. Wählen Sie diese Option aus, um Dateien und Ordner an genau dem Speicherort wiederherzustellen, an dem die Sicherung erstellt wurde.  
  
    -   **An einem anderen Speicherort wiederherstellen**.  Wählen Sie diese Option, um einen anderen Speicherort auf dem Server anzugeben, an dem die Dateien wiederhergestellt werden sollen.  
  
         Wenn in der Standardinstallation eine Datei mit dem gleichen Namen wie die Wiederherstellungsdatei bereits am Zielort vorhanden ist, erstellt der Assistent eine Kopie der ursprünglichen Datei. Darüber hinaus wird die Zugriffssteuerungsliste (ACL) aktualisiert, um aktuelle Dateiberechtigungen zu berücksichtigen. Klicken Sie auf **Erweitert**, um die Standardeinstellungen anzupassen.  
  
6.  **Wiederherstellungs Informationen bestätigen**  
  
     Die Seite **Wiederherstellungsinformationen bestätigen** enthält eine Zusammenfassung der Wiederherstellungsanweisungen, die Sie angegeben haben. Um die Wiederherstellung der Datei fortzusetzen, müssen Sie die richtige Passphrase für Ihr Onlinesicherungskonto eingeben.  
  
###  <a name="register-this-server-for-backup"></a><a name="BKMK_5"></a>Diesen Server für die Sicherung registrieren  
 Zum Sichern oder Wiederherstellen von Dateien, Ordnern und Datei Versions Verläufen auf dem Windows Server Essentials-Server für Azure Backup müssen Sie zuerst den Server beim Microsoft Azure Backup-Dienst registrieren.  
  
> [!NOTE]
>  Bevor Sie den Server registrieren, müssen Sie ein Zertifikat hochladen, das mit dem Sicherungstresor verwendet wird, in dem die Onlinesicherungen gespeichert werden. Weitere Informationen finden Sie unter [Hochladen eines Zertifikats in den Azure Backup-Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1).  
  
##### <a name="to-register-your-server-with-azure-backup"></a>So registrieren Sie den Server bei Azure Backup  
  
1.  Melden Sie sich als Administrator beim Server an, und öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie im Unterabschnitt **Onlinesicherung** auf **Registrieren**.  
  
4.  Wählen Sie das Zertifikat aus, das Sie mit dem Sicherungstresor für die Onlinesicherungen verwenden möchten. Das Standardzertifikat ist automatisch aktiviert. Wenn Sie ein anderes Zertifikat auswählen möchten, wählen Sie **Durchsuchen**. Klicken Sie dann auf **Weiter**.  
  
5.  Folgen Sie den Anweisungen im Assistenten, um eine Passphrase zu erstellen, und schließen Sie dann die Registrierung ab.  
  
###  <a name="unregister-server"></a><a name="BKMK_6"></a>Aufheben der Registrierung des Servers  
  
> [!CAUTION]
>  Wenn Sie die Registrierung Ihres Windows Server Essentials-Servers beim Microsoft Azure Backup-Dienst aufheben, kann Azure Backup den Server nicht mehr sichern. Darüber hinaus werden die zuvor hochgeladenen Serverdaten gelöscht. Um Onlinesicherungen fortzusetzen, müssen Sie den Server erneut registrieren.  
  
##### <a name="to-unregister-your-server-with-azure-backup"></a>So heben Sie die Serverregistrierung bei Azure Backup auf  
  
1.  Melden Sie sich beim [Azure-Verwaltungsportal](https://manage.windowsazure.com)an.  
  
2.  Klicken Sie auf **Recovery Services**.  
  
3.  Klicken Sie in **Recovery Services** auf den Namen des Sicherungstresors.  
  
4.  Klicken Sie auf der Seite **Schnellstart** des Tresors auf **Server**.  
  
5.  Wählen Sie den Server aus, klicken Sie auf **Löschen**, und klicken Sie dann zur Bestätigung auf **Ja**.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Ändern der Richtlinie für die Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Anzeigen der Speicherauslastung für die Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Einschließen eines neuen Ordners in die Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Entfernen oder Ausschließen von Datei Versions Verlaufs Sicherungen aus der Online Sicherungs Richtlinie](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Deaktivieren oder erneutes Aktivieren der Online Server Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Beenden einer laufenden Online Server Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [Anzeigen des Status der Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [Anzeigen und Verwalten von Warnungen für die Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [Zurücksetzen der Online Sicherung auf die Standardeinstellungen](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_15)  
  
-   [Registrieren für Azure Backup-Dienst](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)  
  
-   [Integrieren von Azure Backup in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_17)  
  
-   [Schützen von Ordnern für die Online Sicherung in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_18)  
  
-   [Verlauf der Online Sicherung in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_19)  
  
###  <a name="change-the-online-backup-policy"></a><a name="BKMK_7"></a>Ändern der Richtlinie für die Online Sicherung  
 Im Windows Server Essentials-Dashboard können Sie die Richtlinie für die Onlinesicherung ganz einfach ändern.  
  
##### <a name="to-change-the-online-backup-policy"></a>So ändern Sie die Richtlinie für die Onlinesicherung  
  
1. Melden Sie sich als Administrator beim Dashboard an.  
  
2. Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3. Klicken Sie im Bereich **Aufgaben für die Onlinesicherung** auf **Onlinesicherung konfigurieren**.  
  
4. Folgen Sie den Anweisungen im Assistenten, um die Richtlinie für die Onlinesicherung anzupassen.  
  
   Ausführlichere Informationen zu den Einstellungen, die Sie anpassen können, finden Sie unter [Konfigurieren einer Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="view-online-backup-storage-usage"></a><a name="BKMK_8"></a>Anzeigen der Speicherauslastung für die Online Sicherung  
  
##### <a name="to-view-the-amount-of-storage-space-that-online-backup-uses"></a>So zeigen Sie die Menge des von der Onlinesicherung verwendeten Speicherplatzes an  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Auf der Registerkarte **Onlinesicherung** wird der **Speicherstatus** im Informationsbereich angezeigt.  
  
###  <a name="include-a-new-folder-in-online-backup"></a><a name="BKMK_9"></a>Einschließen eines neuen Ordners in die Online Sicherung  
  
##### <a name="to-include-a-new-folder-in-the-online-backup-policy"></a>So schließen Sie einen neuen Ordner in die Richtlinie für die Onlinesicherung ein  
  
1. Melden Sie sich als Administrator beim Dashboard an.  
  
2. Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3. Klicken Sie im Bereich **Aufgaben für die Onlinesicherung** auf **Onlinesicherung konfigurieren**.  
  
4. Klicken Sie auf der Seite **Sicherungsrichtlinie ändern oder entfernen** auf **Richtlinie für die Onlinesicherungen anpassen**.  
  
5. Wenn der gewünschte Ordner auf der Seite **Onlinesicherung konfigurieren** nicht in der Liste angezeigt wird, klicken Sie auf **Ordner hinzufügen**.  
  
6. Navigieren Sie im Fenster **Ordner hinzufügen** zum Ordner, den Sie in die Onlinesicherung aufnehmen möchten, und wählen Sie ihn aus. Klicken Sie dann auf **OK**.  
  
7. Wählen Sie auf der Seite **Onlinesicherung konfigurieren** andere Ordner nach Bedarf aus, und klicken Sie dann auf **Weiter**.  
  
8. Folgen Sie den Anweisungen im Assistenten, um die Richtlinie für die Onlinesicherung anzupassen.  
  
   Ausführlichere Informationen zu weiteren Einstellungen, die Sie anpassen können, finden Sie unter [Konfigurieren einer Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="remove-or-exclude-file-history-backups-from-the-online-backup-policy"></a><a name="BKMK_10"></a>Entfernen oder Ausschließen von Datei Versions Verlaufs Sicherungen aus der Online Sicherungs Richtlinie  
  
##### <a name="to-remove-or-exclude-a-folder-from-the-online-backup-policy"></a>So entfernen oder schließen Sie einen Ordner aus der Richtlinie für die Onlinesicherung aus  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Onlinesicherung**.  
  
3.  Klicken Sie auf die Registerkarte **geschützte Ordner** . Im Detailbereich wird eine Liste der Ordner mit dem Status der Online Sicherung angezeigt.  
  
4.  Wählen Sie den Ordner, den Sie aus der Richtlinie für die Onlinesicherung ausschließen möchten, aus, und klicken Sie dann im Aufgabenbereich auf **Ordner aus Onlinesicherung entfernen**.  
  
###  <a name="disable-or-re-enable-online-server-backup"></a><a name="BKMK_11"></a>Deaktivieren oder erneutes Aktivieren der Online Server Sicherung  
 Anweisungen zum Verwenden von Azure Backup zum Sichern oder Wiederherstellen von Serverdaten finden Sie unter [Registrieren des Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
 Anweisungen zum Deaktivieren der Verwendung von Azure Backup zum Sichern oder Wiederherstellen von Serverdaten finden Sie unter Aufheben der [Registrierung des Servers](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6).  
  
###  <a name="stop-an-online-server-backup-in-progress"></a><a name="BKMK_12"></a>Beenden einer laufenden Online Server Sicherung  
  
##### <a name="to-stop-an-online-server-backup-in-progress"></a>So beenden Sie eine laufende Onlineserversicherung  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie im Bereich **Aufgaben für die Onlinesicherung** auf **Sicherung beenden**.  
  
     Nachdem Sie die Sicherung beendet haben, wird in der Liste **Sicherungsverlauf** der Status **Abgebrochen** für die Sicherung angezeigt.  
  
###  <a name="view-online-backup-status"></a><a name="BKMK_13"></a>Anzeigen des Status der Online Sicherung  
  
##### <a name="to-view-the-backup-status"></a>So zeigen Sie den Sicherungsstatus an  
  
1.  Melden Sie sich als Administrator beim Dashboard an.  
  
2.  Klicken Sie auf der Navigationsleiste auf **ONLINESICHERUNG**.  
  
3.  Klicken Sie auf die Registerkarte **Sicherungs Verlauf** . Die Listenansicht zeigt den Status jedes Sicherungsauftrags an. Wählen Sie einen Sicherungsauftrag aus, um weitere Details zum Auftrag anzuzeigen.  
  
###  <a name="view-and-manage-online-backup-alerts"></a><a name="BKMK_14"></a>Anzeigen und Verwalten von Warnungen für die Online Sicherung  
 Wie viele andere Warnungen werden Warnungen für Azure Backup in der Meldungs Anzeige angezeigt.  
  
##### <a name="to-view-online-backup-alerts-in-the-alert-viewer"></a>So zeigen Sie Warnungen für die Onlinesicherung in der Meldungsanzeige an  
  
1. Öffnen Sie das Dashboard.  
  
2. Führen Sie eine der folgenden Aktionen aus:  
  
     Windows Server Essentials: Klicken Sie im Navigationsbereich auf das Symbol Warnungen, \(möglicherweise kritisch, Warnung oder Information\). Daraufhin wird die Meldungsanzeige geöffnet.  
  
     Windows Server Essentials: Klicken Sie auf der **Start** Seite auf die Registerkarte System **Überwachung** .  
  
3. Überprüfen Sie die Liste der Warnungen auf Probleme im Zusammenhang mit Azure Backup.  
  
   Weitere Informationen zum Verwalten von Warnungen mithilfe der Meldungs Anzeige oder der Registerkarte "System Überwachung" finden Sie unter [Verwalten der System](Manage-System-Health-in-Windows-Server-Essentials.md)Integrität.  
  
###  <a name="reset-online-backup-to-default-settings"></a><a name="BKMK_15"></a>Zurücksetzen der Online Sicherung auf die Standardeinstellungen  
 Windows Server Essentials enthält einen Assistenten, mit dem Sie die Einstellungen für die Onlinesicherung konfigurieren können. Wenn Sie die Standardeinstellungen wiederherstellen möchten, führen Sie die Aufgabe **Onlinesicherung konfigurieren** aus, und wählen Sie die Option **Richtlinie für die Onlinesicherung entfernen** aus. Führen Sie dann die Aufgabe **Onlinesicherung konfigurieren** erneut aus. Die zuvor hochgeladenen Daten bleiben unverändert.  
  
###  <a name="sign-up-for-azure-backup-service"></a><a name="BKMK_16"></a>Registrieren für Azure Backup-Dienst  
 Um die Integration von Microsoft Azure Backup in Windows Server Essentials vorzubereiten, melden Sie sich mit Ihrem Microsoft Online Services-Konto bei der Azure-Verwaltungsportal an, und erstellen Sie dann einen Sicherungs Tresor, in dem Ihre Online Sicherungen in Azure gespeichert werden. Anschließend laden Sie das Azure Backup-Integrationsmodul herunter und verwenden die heruntergeladene Datei, um das Azure Backup-Add-in auf Ihrem Windows Server Essentials-Server zu installieren. Wenn Sie nicht über ein Microsoft-Konto verfügen, können Sie sich für eine kostenlose Testversion registrieren.  
  
 Zum Ausführen von Setup führen Sie die folgenden Aufgaben aus:  
  
1.  Registrieren Sie sich für ein Microsoft Online Services-Konto und die Vorschau der Sicherung.  
  
2.  Erstellen Sie einen Sicherungstresor zum Speichern von Onlinesicherungen.  
  
3.  Laden Sie den Azure Backup-Agent herunter.  
  
4.  Installieren Sie das Azure Backup-Add-in auf dem Server.  
  
####  <a name="sign-up-for-a-microsoft-online-services-account-and-the-backup-preview"></a><a name="BKMK_SignupforaMicrosoftOnlineServiceAccount"></a>Registrieren für ein Microsoft Online Services-Konto und die Backup-Vorschau  
  
1.  Melden Sie sich beim Windows Server Essentials-Dashboard an.  
  
2.  Klicken Sie auf der **Startseite** des Dashboards auf die Kategorie **ADD-INS**, klicken Sie auf **In Azure Backup integrieren**, und klicken Sie dann auf **Zur Registrierung für Azure Backup klicken**.  
  
3.  Überprüfen Sie auf der Seite Azure- **Recovery Services** im Abschnitt **Backup (Vorschau)** die Details.  
  
4.  Wenn Sie nicht über ein Azure-Abonnement verfügen, klicken Sie auf **Kostenlose Testversion**, und befolgen Sie dann die Anweisungen, um ein Azure-Abonnement zu erhalten.  
  
     Wenn Sie bereits über ein Azure-Abonnement verfügen, klicken Sie in der oberen rechten Ecke der Webseite auf **Portal** , um zum Azure-Verwaltungsportal zu gelangen.  
  
5.  Auf der Seite Azure-Verwaltungsportal werden **Recovery Services** im linken Bereich angezeigt. Hier verwalten Sie die Sicherungs Tresore, in denen Ihre Online Sicherungen aus Windows Server Essentials gespeichert werden.  
  
####  <a name="create-a-backup-vault-to-store-online-backups"></a><a name="BKMK_Createabackupvaulttostoreonlinebackups"></a>Erstellen eines Sicherungs Tresors zum Speichern von Online Sicherungen  
  
1.  Melden Sie sich über den Webbrowser Ihres Windows Server Essentials-Servers beim [Azure-Verwaltungsportal](https://manage.windowsazure.com)an.  
  
2.  Klicken Sie im Azure-Verwaltungsportal auf **neu**, klicken Sie auf **Data Services**, klicken Sie auf **Recovery Services**, klicken Sie auf **Sicherungs**Tresor, und klicken Sie dann auf **schneller**Fassung.  
  
3.  Geben Sie einen Namen für den Sicherungstresor ein, wählen Sie die Region aus, in der Sie die Sicherungen speichern möchten, und klicken Sie dann auf **Schnellerfassung**.  
  
     Der Bereich **Recovery Services** wird mit dem neuen Sicherungstresor geöffnet.  
  
####  <a name="download-the-azure-backup-agent"></a><a name="BKMK_DownloadtheWindowsAzureBackupAgent"></a>Herunterladen des Azure Backup-Agents  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der **Startseite** des Dashboards auf die Registerkarte **Erste Schritte**, auf die Kategorie **ADD-INS**, auf **In Azure Backup integrieren** und auf **Zum Herunterladen des Azure Backup-Integrationsmoduls klicken**.  
  
####  <a name="install-the-azure-backup-add-in-on-the-server"></a><a name="BKMK_InstalltheWindowsAzureBackupAddIn"></a>Installieren des Azure Backup-Add-Ins auf dem Server  
  
1. Melden Sie sich mit einem Administratorkonto bei Ihrem Server an, und führen Sie die Datei **OnlineBackupAddin.wssx** aus, die Sie im vorherigen Schritt heruntergeladen haben.  
  
2. Die **Software-Lizenzbedingungen** werden angezeigt. Wenn Sie den Bedingungen zustimmen, klicken Sie auf **Annehmen**, um die Installation fortzusetzen.  
  
3. Klicken Sie auf der Seite **Add-In installieren** auf **Add-In installieren**.  
  
   > [!NOTE]
   >  Sie müssen den Server u. U. neu starten, um die erforderliche Software zu installieren.  
  
    Die Seite **Installation** wird angezeigt. Eine Fortschrittsanzeige wird mit Beginn der Installation eingeblendet. Wenn die Installation abgeschlossen ist, erhalten Sie eine Meldung, dass das Azure Backup-Add-in erfolgreich installiert wurde.  
  
4. Klicken Sie auf **Fertig stellen**.  
  
5. Schließen Sie das Dashboard, und öffnen Sie es erneut.  
  
    Eine neue Registerkarte **Onlinesicherung** wird dem Dashboard hinzugefügt. Auf dieser Registerkarte können Sie den Server registrieren, Sicherungs Einstellungen konfigurieren und **Recovery Services** im Azure-Verwaltungsportal öffnen, um die Sicherungs Tresore für Ihre Server zu verwalten.  
  
   Führen Sie nach Abschluss dieses Vorgangs folgende Schritte aus:  
  
6. Laden Sie in Windows Server Essentials ein Zertifikat hoch, das für Online Sicherungen verwendet werden soll. Weitere Informationen finden Sie unter [Hochladen eines Zertifikats in den Azure Backup-Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1).  
  
7. Registrieren Sie den Server beim Azure Backup-Tresor. Weitere Informationen finden Sie unter [Registrieren Ihres Servers für die Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).  
  
8. Konfigurieren Sie die Onlinesicherung des Servers. Weitere Informationen finden Sie unter [Konfigurieren einer Onlinesicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).  
  
###  <a name="integrate-azure-backup-with-windows-server-essentials"></a><a name="BKMK_17"></a>Integrieren von Azure Backup in Windows Server Essentials  
 Das Microsoft Azure Backup-Integrationsmodul ist ein neues Feature von Windows Server Essentials, mit dem Sie Dateien und Ordner auf Ihrem Server in einem von Microsoft bereitgestellten, von Azure gehosteten Speichersystem verschlüsseln und sichern können. Wenn Sie Azure Backup zum Verschlüsseln und Sichern von Daten auf dem Server verwenden, können Sie einen schwerwiegenden Verlust wichtiger Geschäftsdaten aufgrund von Feuer, Überschwemmungen, Diebstahl oder anderen Notfällen verhindern. Wenn Sie Azure Backup zum Sichern von Serverdaten verwenden, werden die Informationen mithilfe Ihrer Passphrase verschlüsselt, bevor Sie in ein sicheres Daten Center im Internet hochgeladen werden. Um auf Daten aus einer Onlinesicherung zuzugreifen, benötigen Sie einen Server, der durch ein Zertifikat authentifiziert wird, und Sie müssen die Passphrase angeben.  
  
 Nachdem Sie den Server in Azure Backup integriert und registriert haben, können Sie die Einstellungen für die Online Sicherung konfigurieren, um regelmäßig geplante Sicherungen auszuführen. Sie können eine Onlinesicherung auch jederzeit initiieren, indem Sie im Dashboard für die Onlinesicherung auf die Aufgabe **Backup jetzt starten** klicken.  
  
 Die Einrichtung der Onlinesicherung umfasst die folgenden Schritte:  
  
1.  [Registrieren für Azure Backup-Dienst](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16) : Nachdem Sie sich für den Sicherungsdienst angemeldet haben, erstellen Sie einen Sicherungs Tresor, laden das Azure Backup-Integrationsmodul herunter und installieren es.  
  
2.  [Hochladen eines Zertifikats in den Azure Backup Tresor](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
3.  [Diesen Server für die Sicherung registrieren](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
4.  [Konfigurieren der Online Sicherung](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
> [!NOTE]
>   Azure Backup verwendet die Passphrase zum Verschlüsseln von Dateien und Ordnern für die Online Sicherung. Indem Sie die Verschlüsselungs-Passphrase ändern, ersetzen Sie die Passphrase, die Sie bei der Registrierung des Servers angegeben haben. Für die Passphrase werden nur ASCII-codierte Zeichen akzeptiert.  
  
###  <a name="protect-folders-for-online-backup-in-windows-server-essentials"></a><a name="BKMK_18"></a>Schützen von Ordnern für die Online Sicherung in Windows Server Essentials  
 Der Unterabschnitt **Geschützte Ordner** im Abschnitt „Onlinesicherung“ des Dashboards enthält eine Liste aller freigegebenen Ordner auf dem Server. Die folgende Tabelle beschreibt die Informationen, die in der Liste enthalten sind.  
  
|Spalte|Beschreibung|  
|------------|-----------------|  
|**Ordner Name:**|Der Name des Ordners, der in die Onlinesicherung eingeschlossen wurde.<br /><br /> Führen Sie zum Hinzufügen oder Ausschließen eines Ordners die Aufgabe **Onlinesicherung konfigurieren** aus.|  
|**Ordner Pfad:**|Der Speicherort des Ordners.|  
|**Status:**|Es gibt drei Typen von Status **geschützt**, **nicht geschützt**und **unbekannt**.|  
  
###  <a name="online-backup-history-in-windows-server-essentials"></a><a name="BKMK_19"></a>Verlauf der Online Sicherung in Windows Server Essentials  
 Der Unterabschnitt **Sicherungsverlauf** des Abschnitts „Onlinesicherung“ im Dashboard enthält eine Liste der zuletzt erstellten Onlinesicherungen. Erfolgreiche Sicherungen können zum Wiederherstellen von Dateien und Ordnern verwendet werden. Die folgende Tabelle beschreibt die Informationen, die in der Liste enthalten sind.  
  
|Spalte|Beschreibung|  
|------------|-----------------|  
|**Betriebs**|Es gibt zwei Arten von Vorgängen - **Sichern** und **Wiederherstellen**.|  
|**Zeit**|Dies ist die für den letzten Status protokollierte Uhrzeit.|  
|**Status:**|Es gibt fünf Arten von Status: **Erfolg**, **wird**ausgeführt, **abgebrochen**, **Warnung**und nicht **erfolgreich**.|  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Sicherungen und Wiederherstellungen](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Microsoft Online Services](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
