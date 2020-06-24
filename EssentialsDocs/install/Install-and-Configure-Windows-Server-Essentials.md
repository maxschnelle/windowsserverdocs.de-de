---
title: Installieren und Konfigurieren von Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 06/17/2013
ms.prod: windows-server
ms.topic: article
ms.assetid: e95cf219-46a4-4041-bd81-0c4c2a0622cf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 46ee8e19f50b1bce48bd1e7c773bbd802d85b550
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267570"
---
# <a name="install-and-configure-windows-server-essentials"></a>Installieren und Konfigurieren von Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_InstallConfigure"></a>   

 Dieses Dokument enthält schrittweise Anleitungen zum Installieren und Konfigurieren von Windows Server Essentials. Bevor Sie mit der Installation beginnen, überprüfen Sie die Aufgaben, die in beschrieben werden, [bevor Sie Windows Server Essentials installieren](Before-You-Install-Windows-Server-Essentials.md).  

 Dieses Dokument enthält schrittweise Anleitungen zum Installieren und Konfigurieren von Windows Server Essentials. Bevor Sie mit der Installation beginnen, überprüfen Sie die Aufgaben, die in beschrieben werden, [bevor Sie Windows Server Essentials installieren](../install/Before-You-Install-Windows-Server-Essentials.md).  
  
 Windows Server Essentials wird in zwei Schritten installiert und konfiguriert:  
  

1.  [Schritt 1: Installieren des Windows Server Essentials-Betriebssystems](Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation) In diesem Schritt installieren Sie das Betriebssystem auf dem Server.  
  
2.  [Schritt 2: Konfigurieren des Windows Server Essentials-Betriebssystems](Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure) In diesem Schritt schließen Sie die Installation ab, indem Sie Informationen zu Ihrem Unternehmen, den Domänen Einstellungen und dem Netzwerkadministrator bereitstellen. Diese Informationen werden verwendet, um den Server betriebsbereit zu machen.  

  
###  <a name="step-1-install-the-windows-server-essentials-operating-system"></a><a name="BKMK_ManualInstallation"></a>Schritt 1: Installieren des Windows Server Essentials-Betriebssystems  
  
> [!IMPORTANT]
>  Passen Sie den Server nach der Installation des Betriebssystems erst an, wenn Sie [Schritt 2: Konfigurieren des Betriebssystems Windows Server Essentials](#BKMK_Step2Configure)abgeschlossen haben.  
  
 **Geschätzte Dauer:** Ungefähr 30 Minuten.  
  
> [!NOTE]
>  Die jeweils geschätzte Zeit bis zum Abschließen des Vorgangs basiert auf den Mindesthardwareanforderungen.  
  
##### <a name="to-install-the-operating-system"></a>So installieren Sie das Betriebssystem  
  
1. Verbinden Sie den Computer über ein Netzwerkkabel mit dem Netzwerk.  
  
   > [!IMPORTANT]
   >  Trennen Sie den Computer während der Installation nicht vom Netzwerk. Dies kann zu einem Fehler bei der Installation führen.  
  
2. Schalten Sie den Computer ein, und legen Sie dann die Windows Server Essentials-DVD in das DVD-Laufwerk ein.  
  
    Wenn Sie eine unbeaufsichtigte Installation ausführen, stellen Sie eine Verbindung mit dem Wechselmedium (z. B. einer Diskette oder einem USB-Speicherstick) her, auf dem sich die Antwortdateien befinden. Je nach Inhalt der Antwortdateien sind einige oder alle der folgenden Installationsbildschirme für Sie nicht sichtbar.  
  
3. Starten Sie den Computer neu. Drücken Sie eine Taste, wenn Sie aufgefordert werden,**** zum Starten von CD oder DVD eine beliebige Taste zu drücken.  
  
   > [!NOTE]
   >  Wenn der Computer nicht über das DVD-Laufwerk startet, stellen Sie sicher, dass das CD-ROM-Laufwerk in der BIOS-Startreihenfolge an oberster Stelle steht. Weitere Informationen zur BIOS-Startreihenfolge finden Sie in der Dokumentation des Computerherstellers.  
  
4. Wählen Sie die **Sprache** aus, die Sie installieren möchten, das **Zeit- und Währungsformat** und die **Tastatur oder Eingabemethode**, und klicken Sie dann auf **Weiter**.  
  
5. Klicken Sie auf **Jetzt installieren**.  
  
6. Geben Sie in **Product Key eingeben** den Product Key ein.  
  
7. Lesen Sie die **Lizenzbedingungen**. Wenn Sie sie akzeptieren, aktivieren Sie das Kontrollkästchen **Ich akzeptiere die Lizenzbestimmungen**, und klicken Sie auf **Weiter**.  
  
   > [!NOTE]
   >  Wenn Sie die Lizenzbestimmungen nicht akzeptieren, wird die Installation nicht fortgesetzt.  
  
8. Klicken Sie in **Wählen Sie eine Installationsart aus** auf **Benutzerdefiniert: nur Windows installieren (für fortgeschrittene Benutzer)**.  
  
9. Wählen Sie in **Wo möchten Sie Windows installieren?** die Festplatte aus, auf der Sie das Windows-Betriebssystem installieren möchten. Stellen Sie sicher, dass die internen Festplatten für die Installation verfügbar sind.  
  
    > [!IMPORTANT]
    >   Windows Server Essentials muss als Volume "C:" installiert sein, und die Volumegröße muss mindestens 60 GB betragen. Es wird empfohlen, zwei Partitionen auf dem Betriebssystemlaufwerk zu erstellen und ":C" (Systempartition) nicht zum Speichern von Geschäftsdaten zu verwenden.  
  
    > [!NOTE]
    >  Wenn eine Festplatte nicht aufgeführt ist (z. B. eine SATA-Festplatte (Serial Advanced Technology Attachment)), müssen Sie die Gerätetreiber für diese Festplatte laden. Rufen Sie den Gerätetreiber beim Hersteller ab, und speichern Sie ihn auf einem Wechselmedium (z. B. einer Diskette oder einem USB-Speicherstick). Verbinden Sie das Wechselmedium mit dem Computer, und klicken Sie dann auf **Treiber laden**.  
  
     Wenn Sie Partitionen löschen und/oder erstellen müssen, führen Sie folgende Schritte aus:  
  
    1.  Zum Löschen einer Partition wählen Sie die Partition aus, klicken Sie auf **Laufwerkoptionen (erweitert)** und dann auf **Löschen**. Wenn Sie die Systempartition gelöscht haben, erstellen Sie eine neue Partition, indem Sie die Anweisungen in Schritt **b** oder Schritt **c** befolgen.  
  
        > [!NOTE]
        >  Nachdem Sie auf **Laufwerkoptionen (erweitert)** geklickt haben, wird diese Option nicht mehr angezeigt. Überspringen Sie in diesem Fall den Schritt mit den Laufwerkoptionen.  
  
    2.  Zum Erstellen einer Partition aus einem nicht partitionierten Speicherplatz klicken Sie auf die Festplatte, die Sie partitionieren möchten, klicken nacheinander auf **Laufwerkoptionen (erweitert)** und **Neu** und geben dann im Textfeld **Größe** die Partitionsgröße ein, die Sie erstellen möchten. Geben Sie z. B., wenn Sie die empfohlene Partitionsgröße von 120 GB verwenden möchten, **122880**ein, und klicken Sie dann auf **Übernehmen**. Klicken Sie auf **Weiter**, wenn die Partition erstellt wurde. Die Partition wird formatiert, bevor die Installation fortgesetzt wird.  
  
    3.  Zum Erstellen einer Partition, die den gesamten nicht partitionierten Speicherplatz verwendet, klicken Sie auf die Festplatte, die Sie partitionieren möchten, klicken Sie nacheinander auf **Laufwerkoptionen (erweitert)** und **Neu** und dann auf **Übernehmen**, um die Standardpartitionsgröße zu übernehmen. Klicken Sie auf **Weiter**, wenn die Partition erstellt wurde. Die Partition wird formatiert, bevor die Installation fortgesetzt wird.  
  
        > [!IMPORTANT]
        >  Sie können das Betriebssystem nicht in eine andere Partition verschieben, nachdem Sie diesen Schritt ausgeführt haben.  
  
   Während der Installation werden temporäre Dateien in einen Installationsordner auf dem Computer kopiert. Dieser Vorgang dauert ungefähr 30 Minuten. Nachdem das Windows Server Essentials-Betriebssystem installiert wurde, wird der Computer neu gestartet. Nun können Sie das Betriebssystem Windows Server Essentials konfigurieren.  
  
###  <a name="step-2-configure-the-windows-server-essentials-operating-system"></a><a name="BKMK_Step2Configure"></a>Schritt 2: Konfigurieren des Windows Server Essentials-Betriebssystems  
  
> [!IMPORTANT]
>  Wenn Sie von einer früheren Version von Windows Small Business Server zu Windows Server Essentials migrieren, müssen Sie einen anderen Prozess befolgen. Informationen zu Migrationsinstallationen finden Sie unter folgenden Themen:  
> 
> - [Migration von Windows SBS 2003](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
>   -   [Migration von Windows SBS 2008](../migrate/Migrate-Windows-Small-Business-Server-2008-to-Windows-Server-Essentials.md)  
  
 In dieser Phase der Installation werden Sie aufgefordert, einige Fragen zu Ihrer Organisation zu beantworten. Diese Informationen werden zum Konfigurieren des Betriebssystems verwendet.  
  
> [!IMPORTANT]
>  Stellen Sie vor der Ausführung dieses Schritts sicher, dass der lokale Netzwerkadapter mit einem Router oder Switch verbunden ist, der eingeschaltet ist und ordnungsgemäß funktioniert.  
  
 **Geschätzte Beendigungs Zeit:** Ungefähr 30 Minuten  
  
##### <a name="to-configure-the-operating-system"></a>So konfigurieren Sie das Betriebssystem  
  
1.  Klicken Sie auf der Seite **Einstellungen für Datum und Uhrzeit überprüfen** auf **Einstellungen für Systemdatum und -uhrzeit ändern**, um die Einstellungen für Datum und Uhrzeit und die Zeitzone für den Server auszuwählen. Wenn Sie fertig sind, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]
    >  Wenn Sie Windows Server Essentials auf einem virtuellen Computer installieren, stellen Sie sicher, dass Sie die gleichen Zeitzoneneinstellungen auswählen, die auch vom Host Betriebssystem verwendet werden. Wenn die Einstellungen für die Zeitzone voneinander abweichen, kann die Serverinstallation möglicherweise nicht erfolgreich ausgeführt werden.  
  
2.  Führen Sie auf der Seite **Installationsmodus auswählen** eine der folgenden Aktionen aus:  
  
    1.  Wählen **Sie Neuinstallation aus** , um eine vollständige Neuinstallation der Windows Server Essentials-Server Software einzurichten.  
  
    2.  Wählen Sie **Server Migration** aus, um Windows Server Essentials zu installieren und diesen Server einer vorhandenen Windows-Domäne hinzuzufügen.  
  
3.  Geben Sie auf der Seite **Server personalisieren** den Namen der Organisation, einen internen Domänennamen und den Servernamen ein.  
  
    > [!IMPORTANT]
    >  Der Servername muss ein eindeutiger Name im Netzwerk sein. Wenn Sie diesen Schritt ausgeführt haben, können Sie den Servernamen oder den internen Domänennamen nicht mehr ändern.  
  
4.  Klicken Sie auf **Weiter**.  
  
5.  Geben Sie auf der Seite **Administratorinformationen angeben** die Informationen für ein neues Administratorkonto ein.  
  
    > [!CAUTION]
    >  Benennen Sie den Netzwerkadministrator Konto Administrator oder Netzwerkadministrator nicht. Diese Kontonamen sind zur Verwendung durch das System reserviert.  
  
6.  Geben Sie auf der Seite **Standardbenutzerinformationen angeben** die Informationen für ein neues Standardbenutzerkonto ein, und klicken Sie dann auf **Weiter**.  
  
7.  Wählen Sie auf der Seite **Server automatisch auf dem neuesten Stand halten** aus, wie Sie Windows-Updates für den Server erhalten möchten, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der Seite **Der Server wird aktualisiert und vorbereitet** wird der Status des letzten Installationsvorgangs angezeigt. Der Abschluss dieses Vorgangs dauert eine Weile. Möglicherweise wird währenddessen der Computer mehrere Male neu gestartet.  
  
9. Nach dem letzten Serverneustart wird die Seite **Der Server kann jetzt verwendet werden** angezeigt. Klicken Sie auf **Schließen**.  
  
10. Klicken Sie auf dem Startbildschirm auf die Kachel **Dashboard **, und führen Sie im Dashboard dann auf der Seite **Start** die Aufgaben unter **Eigenen Server einrichten** aus. Sie sollten diese Aufgaben unmittelbar nach Abschluss der Windows Server Essentials-Installation ausführen.  
  
> [!NOTE]
>  Wenn die Installation abgeschlossen ist, werden Sie beim Server automatisch mit dem neuen Administratorkonto angemeldet, das Sie während der Installation hinzugefügt haben. Das Kennwort für das integrierte Administratorkonto wird auf dasselbe Kennwort wie das neue Administratorkonto festgelegt, und dann wird das integrierte Administratorkonto deaktiviert.  
  
 Sie können den neu installierten Server für einen begrenzten Zeitraum (auch als Evaluierungszeitraum bezeichnet) verwenden, ohne eine Product Key einzugeben. Nach Ablauf des Evaluierungszeitraums müssen Sie einen Product Key eingeben, um den Server zu aktivieren oder den Evaluierungszeitraum zu verlängern. Sie können den Evaluierungszeitraum maximal zweimal verlängern. Wenn die maximal zulässige Anzahl von Tagen für den Evaluierungszeitraum abgelaufen ist, müssen Sie den Server mit einem Product Key aktivieren.  
  
### <a name="customize-windows-server-essentials"></a>Anpassen von Windows Server Essentials  
 Auf der **Start** Seite des Windows Server Essentials-Dashboards finden Sie Links zu **Einrichtungs** Aufgaben, die Sie unmittelbar nach der Installation des Servers ausführen sollten. Durch Ausführen dieser Aufgaben können Sie Informationen schützen, die auf dem Server gespeichert sind, und die in Windows Server Essentials verfügbaren Features aktivieren.  
  
 Wenn Sie die Aufgaben nicht ausführen, haben die Benutzer möglicherweise keinen Zugriff auf bestimmte Netzwerkfunktionen. Um später zu diesen Aufgaben zurückzukehren, kehren Sie zur **Start** Seite des Windows Server Essentials-Dashboards zurück.  
  
 In der folgenden Tabelle sind die Elemente definiert, die in der Liste der Setupaufgaben angezeigt werden können.  
  
|Aufgabe|BESCHREIBUNG
|----------|-----------------|  
|Updates für weitere Microsoft-Produkte abrufen|Klicken Sie auf diese Aufgabe, um auf einen Link zuzugreifen, über den ein Tool ausgeführt wird, mit dem Sie angeben können, ob Sie Microsoft Update zum automatischen Abrufen von Updates für Windows Server Essentials und andere Microsoft-Produkte wie Office verwenden möchten.  
|Benutzerkonten hinzufügen|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Hinzufügen von Benutzerkonten anzuzeigen. Es wird ein Link zum Ausführen des **Assistenten zum Hinzufügen eines Benutzerkontos** bereitgestellt. Weitere Informationen finden Sie unter [Hinzufügen eines Benutzerkontos](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1).  
|Serverordner hinzufügen|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Hinzufügen von Serverordnern anzuzeigen. Es wird ein Link zum Ausführen des **Assistenten zum Hinzufügen eines Ordners** bereitgestellt. Zudem wird ein Link zu einem Onlinehilfethema zur Verwendung von Serverordnern bereitgestellt. Weitere Informationen finden Sie unter [Hinzufügen oder Verschieben eines Serverordners](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5). 
|Serversicherung einrichten|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Schützen Ihrer Dateien mithilfe der Serversicherung anzuzeigen. Es wird ein Link zum Ausführen des **Assistenten zum Einrichten der Serversicherung** bereitgestellt. Weitere Informationen finden Sie unter [Einrichten oder Anpassen der Serversicherung](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1). 
|Zugriff überall|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung der Funktion "Zugriff überall" in Windows Server Essentials anzuzeigen. Es wird ein Link zur Seite **Einstellungen für Zugriff überall** bereitgestellt. Weitere Informationen finden Sie unter [Verwalten von "Zugriff überall](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)". 
|E-Mail-Benachrichtigungen für Warnungen einrichten|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zu E-Mail-Benachrichtigungen für Warnungen anzuzeigen. Es wird ein Link zum Ausführen des Tools **E-Mail-Benachrichtigungen für Warnungen einrichten** bereitgestellt. Weitere Informationen finden Sie unter [Einrichten von E-Mail-Benachrichtigungen für Warnungen](../manage/Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email).  
|Medienserver einrichten|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Freigeben von Musik, Videos und Bilddateien über den Medienserver anzuzeigen. Es wird ein Link zur Seite  **Medieneinstellungen** bereitgestellt. Zudem wird ein Link zu einem Onlinehilfethema mit Informationen über den Medienserver bereitgestellt. Weitere Informationen finden Sie unter [Verwalten von digitalen Medien](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md). 
|Computer verbinden|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Verbinden eines Netzwerkcomputers mit dem Server anzuzeigen. Weitere Informationen finden Sie unter [Verbinden von Computern mit dem Server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).
  
## <a name="see-also"></a>Weitere Informationen  
  
-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

