---
title: Installieren und Konfigurieren von Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 06/17/2013
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e95cf219-46a4-4041-bd81-0c4c2a0622cf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cdad118c30fbf303b55ec7ea25bbe3e209c016db
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="install-and-configure-windows-server-essentials"></a>Installieren und Konfigurieren von Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_InstallConfigure"></a>   

 Dieses Dokument enthält eine schrittweise Anleitung zum Installieren und Konfigurieren von Windows Server Essentials. Vor dem Beginn der Installations überprüfen, und führen Sie die Aufgaben, die in beschriebenen [bevor Sie Windows Server Essentials installieren](Before-You-Install-Windows-Server-Essentials.md).  

 Dieses Dokument enthält eine schrittweise Anleitung zum Installieren und Konfigurieren von Windows Server Essentials. Vor dem Beginn der Installations überprüfen, und führen Sie die Aufgaben, die in beschriebenen [bevor Sie Windows Server Essentials installieren](../install/Before-You-Install-Windows-Server-Essentials.md).  
  
 Sie installieren und Konfigurieren von Windows Server Essentials in zwei Schritten:  
  

1.  [Schritt 1: Installieren des Betriebssystems Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation) In diesem Schritt installieren Sie das Betriebssystem auf dem Server.  
  
2.  [Schritt 2: Konfigurieren des Windows Server Essentials-Betriebssystems](Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure) In diesem Schritt schließen Sie die Installation durch die Angabe von Informationen des Unternehmens, der domäneneinstellungen und des Netzwerkadministrators. Diese Informationen werden verwendet, um den Server für die Verwendung vorzubereiten.  

1.  [Schritt 1: Installieren des Betriebssystems Windows Server Essentials](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation) In diesem Schritt installieren Sie das Betriebssystem auf dem Server.  
  
2.  [Schritt 2: Konfigurieren des Windows Server Essentials-Betriebssystems](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure) In diesem Schritt schließen Sie die Installation durch die Angabe von Informationen des Unternehmens, der domäneneinstellungen und des Netzwerkadministrators. Diese Informationen werden verwendet, um den Server für die Verwendung vorzubereiten.  

  
###  <a name="BKMK_ManualInstallation"></a>Schritt 1: Installieren des Betriebssystems Windows Server Essentials  
  
> [!IMPORTANT]
>  Nach der Installation des Betriebssystems Anpassen des Servers, bis Sie vollständig [Schritt2: Konfigurieren des Betriebssystems Windows Server Essentials](#BKMK_Step2Configure).  
  
 **Geschätzte Dauer:** ungefähr 30 Minuten.  
  
> [!NOTE]
>  Die geschätzte Zeiten Vorgangs basiert auf den Mindestanforderungen für Hardware.  
  
##### <a name="to-install-the-operating-system"></a>So installieren Sie das Betriebssystem  
  
1.  Verbinden Sie Ihren Computer mit dem Netzwerk über ein Netzwerkkabel.  
  
    > [!IMPORTANT]
    >  Trennen Sie den Computer nicht über das Netzwerk während der Installation. Auf diese Weise kann fehlschlagen die Installation führen.  
  
2.  Aktivieren Sie auf dem Computer, und legen Sie dann die Windows Server Essentials-DVD in das DVD-Laufwerk.  
  
     Wenn Sie eine unbeaufsichtigte Installation ausführen, schließen Sie das Wechselmedium (z. B. einer Diskette oder einem USB-Speicherstick), die die Antwortdateien enthält. Abhängig vom Inhalt der Antwortdateien können einige oder alle der folgenden Installationsbildschirme nicht angezeigt werden.  
  
3.  Starten Sie den Computer neu. Wenn die Meldung **mit beliebiger Taste zum Starten von CD oder DVD** angezeigt wird, drücken Sie eine beliebige Taste.  
  
    > [!NOTE]
    >  Wenn Ihr Computer nicht von der DVD startet, stellen Sie sicher, dass das CD-ROM-Laufwerk zuerst in der BIOS-Startreihenfolge aufgeführt ist. Weitere Informationen zu den BIOS-Startreihenfolge finden Sie in der Dokumentation des Computerherstellers.  
  
4.  Wählen Sie die **Sprache** , die Sie installieren möchten, **Uhrzeit und Währungsformat**, und **Tastatur oder Eingabemethode**, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf **jetzt installieren**.  
  
6.  In **Geben Sie den Product Key**, geben Sie den Product Key.  
  
7.  Lesen der **Lizenzbedingungen**. Wenn Sie sie akzeptieren, aktivieren Sie die **ich akzeptiere die Lizenzbedingungen** , und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]
    >  Wenn Sie sich nicht entscheiden, die Lizenzbedingungen akzeptieren, wird die Installation nicht fortgesetzt.  
  
8.  In **Welche Installationsart soll? **, klicken Sie auf **Benutzerdefiniert: nur Windows installieren (Erweitert)**  
  
9. In **Wo möchten Sie Windows installieren? **, wählen Sie die Festplatte, in dem Sie das Windows-Betriebssystem installieren möchten. Stellen Sie sicher, dass alle Ihre internen Festplatten für die Installation verfügbar sind.  
  
    > [!IMPORTANT]
    >   Windows Server Essentials muss als Volume "c:" installiert werden, und die Größe des Volumes muss mindestens 60 GB sein. Es wird empfohlen, zwei Partitionen auf dem Betriebssystemlaufwerk zu erstellen, und nicht C: (Systempartition) zum Speichern von Geschäftsdaten.  
  
    > [!NOTE]
    >  Wenn eine Festplatte (z. B. eine Festplatte SATA Serial Advanced Technology Attachment ()) nicht aufgeführt ist, müssen Sie die Gerätetreiber für diese Festplatte laden. Erhalten Sie den Treiber des Herstellers, und speichern Sie es auf ein Wechselmedium (z. B. einer Diskette oder einem USB-Speicherstick). Schließen Sie das Wechselmedium an den Computer, und klicken Sie dann auf **Treiber laden**.  
  
     Wenn Sie Partitionen löschen und/oder erstellen müssen, lesen Sie die folgenden Schritte aus:  
  
    1.  Klicken Sie zum Löschen einer Partition wählen Sie die Partition, klicken Sie auf **Laufwerkoptionen (Erweitert)**, und klicken Sie dann auf **löschen**. Nachdem Sie die Systempartition gelöscht haben, erstellen Sie eine neue Partition mithilfe der Anweisungen in Schritt **b** oder Schritt **c**.  
  
        > [!NOTE]
        >  Klicken Sie auf **Laufwerkoptionen (Erweitert)**, die Option nicht mehr angezeigt wird. Überspringen Sie in diesem Fall den Schritt, der den Laufwerkoptionen.  
  
    2.  Zum Erstellen einer Partition aus einem nicht partitionierten Speicherplatz klicken Sie auf der Festplatte, die Sie partitionieren möchten, klicken Sie auf **Laufwerkoptionen (Erweitert)**, klicken Sie auf **neu**, und klicken Sie dann in der **Größe** Text Geben Sie die Größe der Partition erstellt werden soll. Geben Sie z. B. Wenn Sie die empfohlene Partitionsgröße von 120 Gigabyte (GB) verwenden, **122880**, und klicken Sie dann auf **übernehmen**. Nachdem die Partition erstellt wurde, klicken Sie auf **Weiter**. Die Partition wird formatiert, bevor die Installation fortgesetzt wird.  
  
    3.  Zum Erstellen einer Partition, die gesamten nicht partitionierten Speicherplatz verwendet wird, klicken Sie auf der Festplatte, die Sie partitionieren möchten, klicken Sie auf **Laufwerkoptionen (Erweitert)**, klicken Sie auf **neu**, und klicken Sie dann auf **übernehmen** um die standardpartitionsgröße zu übernehmen. Nachdem die Partition erstellt wurde, klicken Sie auf **Weiter**. Die Partition wird formatiert, bevor die Installation fortgesetzt wird.  
  
        > [!IMPORTANT]
        >  Sie können das Betriebssystem in einer anderen Partition verschieben, nachdem Sie diesen Schritt abgeschlossen haben.  
  
 Während der Installation werden temporäre Dateien in einen Installationsordner auf Ihrem Computer kopiert, die dauert ungefähr 30 Minuten. Nach der Installation des Betriebssystems Windows Server Essentials startet den Computer neu. Jetzt können Sie das Betriebssystem Windows Server Essentials konfigurieren.  
  
###  <a name="BKMK_Step2Configure"></a>Schritt 2: Konfigurieren des Windows Server Essentials-Betriebssystems  
  
> [!IMPORTANT]
>  Wenn Sie zu Windows Server Essentials aus einer früheren Version von Windows Small Business Server migrieren, müssen Sie ein anderes Verfahren ausführen. Informationen zu migrationsinstallationen finden Sie in der folgenden:  
>   
>  -   [Migration von Windows SBS 2003](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
> -   [Migration von Windows SBS 2008](../migrate/Migrate-Windows-Small-Business-Server-2008-to-Windows-Server-Essentials.md)  
  
 In dieser Phase der Installation werden Sie aufgefordert, einige Fragen zu Ihrer Organisation zu beantworten. Diese Informationen werden verwendet, um das Betriebssystem konfigurieren.  
  
> [!IMPORTANT]
>  Stellen Sie vor der Ausführung dieses Schritts sicher, dass der lokale Netzwerkadapter angeschlossen mit einem Router oder einem Switch, der eingeschaltet ist ist und funktioniert ordnungsgemäß.  
  
 **Geschätzte Dauer:** ungefähr 30 Minuten  
  
##### <a name="to-configure-the-operating-system"></a>So konfigurieren Sie das Betriebssystem  
  
1.  Auf der **überprüfen Sie das Datum und Uhrzeit** auf **ändern das Systemdatum und die Uhrzeit** die Einstellungen für Datum, Uhrzeit und Zeitzone für den Server auswählen. Wenn Sie fertig sind, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]
    >  Wenn Sie Windows Server Essentials auf einem virtuellen Computer installieren, stellen Sie sicher, dass Sie die gleichen Einstellungen für die Zeitzone auswählen, die vom Betriebssystem Hosts verwendet werden. Wenn die Einstellungen für die Zeitzone voneinander abweichen, kann die Server-Installation nicht erfolgreich.  
  
2.  Auf der **Installationsmodus auswählen** eine der folgenden Optionen:  
  
    1.  Wählen Sie **Neuinstallation** , um eine vollständig neue Installation von Windows Server Essentials Server einzurichten.  
  
    2.  Wählen Sie **Servermigration** zum Installieren von Windows Server Essentials und den Server zu einer vorhandenen Windows-Domäne hinzuzufügen.  
  
3.  Auf der **Server personalisieren** geben den Namen Ihrer Organisation, einen internen Domänennamen und den Namen des Servers.  
  
    > [!IMPORTANT]
    >  Der Servername muss einen eindeutigen Namen in Ihrem Netzwerk sein. Sie können den Servernamen oder den internen Domänennamen ändern, nachdem Sie diesen Schritt abgeschlossen haben.  
  
4.  Klicken Sie auf **Weiter**.  
  
5.  Auf der **bieten Informationen zu Ihrem Konto Administrator** geben die Informationen für ein neues Administratorkonto.  
  
    > [!CAUTION]
    >  Nicht den Namen der netzwerkadministratorkonto oder Netzwerkadministrator. Diese Kontonamen sind zur Verwendung durch das System reserviert.  
  
6.  Auf der **Geben Sie Ihre Kontoinformationen Standardbenutzer** Seite Geben Sie die Informationen für ein neues Standardbenutzerkonto, und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **den Server automatisch auf dem neuesten Stand halten** Seite, wählen Sie, wie Sie möchten die Windows-Updates für Ihren Server empfangen, und klicken Sie dann auf **Weiter**.  
  
8.  Die **aktualisieren und Vorbereiten des Servers** Seite wird der Status des letzten Installationsvorgangs angezeigt. Diese Zeit in Anspruch nimmt, und Ihr Computer mehrmals neu gestartet.  
  
9. Nach dem letzten Neustart der **der Server kann jetzt verwendet werden** Seite wird angezeigt. Klicken Sie auf **schließen **.  
  
10. Klicken Sie auf der Dashboard-Kachel auf der **starten** Bildschirm, und schließen Sie dann auf dem Dashboard die **eigenen Server einrichten** Aufgaben für die **Home** Seite. Sie sollten diese Aufgaben ausführen, direkt nach Abschluss die Installation von Windows Server Essentials.  
  
> [!NOTE]
>  Nach Abschluss der Installation werden Sie automatisch mit dem Server mit dem neuen Administratorkonto angemeldet, die Sie während der Installation hinzugefügt. Das Kennwort des integrierte Administratorkontos auf dasselbe Kennwort wie das neue Administratorkonto festgelegt ist, und klicken Sie dann das integrierte Administratorkonto deaktiviert ist.  
  
 Sie können den neu installierten Server für einen begrenzten Zeitraum (bekannt als der Evaluierungszeitraum) verwenden, ohne Eingabe eines Product Keys. Nach Ablauf des Evaluierungszeitraums müssen Sie einen Product Key zum Aktivieren des Servers oder Erweitern des Evaluierungszeitraums eingeben. Sie können den Evaluierungszeitraum maximal zweimal verlängern. Wenn Sie die maximale Anzahl von Tagen für den Evaluierungszeitraum abgelaufen erreichen, müssen Sie den Server mit einem Product Key aktivieren.  
  
### <a name="customize-windows-server-essentials"></a>Anpassen von Windows Server Essentials  
 Die **Home** Seite des Windows Server Essentials-Dashboards enthält links zu **SETUP** Aufgaben, die Sie direkt nach dem ausführen sollten den Server installiert. Durch Ausführen dieser Aufgaben hilft Ihnen, Schutz von Informationen, die auf dem Server gespeichert sind, und aktivieren die Features, die in Windows Server Essentials verfügbar sind.  
  
 Wenn Sie nicht die Aufgaben ausführen, können Benutzer nicht auf bestimmte Netzwerkfunktionen zugreifen. Damit diese Aufgaben später wieder, zurück, zu Windows Server Essentials-Dashboard **Home** Seite.  
  
 In der folgende Tabelle sind die Elemente, die angezeigt werden, können in der Liste der Setupaufgaben definiert.  
  
|Aufgabe|Beschreibung
|----------|-----------------|  
|Abrufen von Updates für andere Microsoft-Produkte|Klicken Sie auf diese Aufgabe, um einen Link zuzugreifen, der ein Tool ausgeführt, mit dem Sie wird angeben, wenn Sie Microsoft Update zum Abrufen von Updates automatisch für Windows Server Essentials und andere Microsoft-Produkte wie z. B. Office verwenden möchten.  
|Hinzufügen von Benutzerkonten|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Hinzufügen von Benutzerkonten anzuzeigen. Ein Link zum Ausführen der **Benutzer Konto Assistenten zum Hinzufügen eines** bereitgestellt wird. Weitere Informationen finden Sie unter [Hinzufügen eines Benutzerkontos](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1).  
|Serverordner hinzufügen|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Hinzufügen von Serverordnern anzuzeigen. Ein Link zum Ausführen der **Ordner Assistenten zum Hinzufügen eines** bereitgestellt wird. Außerdem ist ein Link zu einem Onlinehilfethema zur Verwendung von Serverordnern. Weitere Informationen finden Sie unter [hinzufügen oder Verschieben eines Serverordners](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5). 
|Richten Sie Server-Sicherung|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zur Verwendung von Server-Sicherung zum Schutz Ihrer Daten anzuzeigen. Ein Link zum Ausführen der **Server-Sicherung Assistenten zum Einrichten von** bereitgestellt wird. Weitere Informationen finden Sie unter [festlegen einrichten oder Anpassen der serversicherung](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1). 
|Einrichten von "Zugriff überall"|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung der Funktion "Zugriff überall" in Windows Server Essentials anzeigen. Ein Link zu den **Einstellungen für Zugriff überall** Seite wird zur Verfügung gestellt. Weitere Informationen finden Sie unter [Manage Anywhere Access](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md). 
|Richten Sie e-Mail-Benachrichtigung|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zu e-Mail-Benachrichtigung anzuzeigen. Ein Link zum Ausführen der **e-Mail-Benachrichtigungen für Warnungen einrichten** Tool bereitgestellt wird. Weitere Informationen finden Sie unter [e-Mail-Benachrichtigungen für Warnungen einrichten](../manage/Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email).  
|Medienserver einrichten|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Freigeben von Musik, Videos und Bilddateien über den Medienserver anzuzeigen. Ein Link zu der **Medieneinstellungen** Seite wird zur Verfügung gestellt. Außerdem ist ein Link zu einem Onlinehilfethema erfahren Sie mehr über den Medienserver. Weitere Informationen finden Sie unter [Verwalten von Digitalmedien](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md). 
|Verbinden von Computern|Klicken Sie auf diese Aufgabe, um eine kurze Beschreibung zum Verbinden von eines Computers im Netzwerk mit dem Server anzuzeigen. Weitere Informationen finden Sie unter [Verbinden von Computern mit dem Server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).
  
## <a name="see-also"></a>Siehe auch  
  
-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

