---
title: Verschieben von Windows SBS 2011 Standard-Einstellungen und -Daten auf den Zielserver für die Migration zu Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16b24026-2fe3-4bd0-b82f-900e1564be99
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b0ee150be2452fdf4c31c6a2a372958640fa5e4a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868401"
---
# <a name="move-windows-sbs-2011-standard-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Verschieben von Windows SBS 2011 Standard-Einstellungen und -Daten auf den Zielserver für die Migration zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Verschieben von Einstellungen und Daten auf den Zielserver:  
  

1.  [Kopieren von Daten auf den Zielserver](Move-Windows-SBS-2011-Standard-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
2.  [Importieren von Active Directory-Benutzerkonten in Windows Server Essentials-Dashboard (optional)](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_ImportADaccounts)  
  
3.  [Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den router](Move-Windows-SBS-2011-Standard-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MoveDHCP)  
  
4.  [Konfigurieren des Netzwerks](Move-Windows-SBS-2011-Standard-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
5.  [Entfernen Sie älterer Active Directory Group Policy Objects (optional)](Move-Windows-SBS-2011-Standard-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_RemoveLegacyADGPO)  
  
6.  [Ordnen Sie zugelassener Computer zu Benutzerkonten zu](Move-Windows-SBS-2011-Standard-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="BKMK_CopyData"></a> Kopieren von Daten auf den Zielserver  
 Führen Sie die folgenden Aufgaben aus, bevor Sie Daten vom Quellserver zum Zielserver kopieren:  
  
-   Prüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie die Ordner auf dem Zielserver so bzw. passen Sie diese so an, dass sie der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren.  
  
-   Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.  
  
-   Machen Sie die freigegebenen Ordner auf dem Quellserver für alle Benutzer schreibgeschützt, damit auf das Laufwerk nicht geschrieben werden kann, während Sie Dateien auf den Zielserver kopieren.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver.  
  
1.  Melden Sie sich am Zielserver als ein Domänenadministrator an, und öffnen Sie dann ein Befehlsfenster.  
  
2.  Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     Dabei gilt:
     - \<Quellservername\> ist der Name des Quellservers
     - \<Namedesfreigegebenenquellordners\> ist der Name des freigegebenen Ordners auf dem Quellserver
     - \<Zielservername\> ist der Name des Zielservers,
     - \<Namedesfreigegebenenzielordners\> ist der freigegebene Ordner auf dem Zielserver, auf denen die Daten kopiert werden.  
  
3.  Wiederholen Sie den vorherigen Schritt für jeden freigegebenen Ordner, zu dem Sie die Migration vom Quellserver aus vornehmen.  
  
##  <a name="BKMK_ImportADaccounts"></a> Importieren von Active Directory-Benutzerkonten in Windows Server Essentials-Dashboard (optional)  
 Standardmäßig werden alle auf dem Quellserver erstellte Benutzerkonten automatisch an das Dashboard in Windows Server Essentials migriert. Die automatische Migration eines Active Directory-Benutzerkontos schlägt jedoch fehl, wenn einige Eigenschaften den Migrationsanforderungen nicht entsprechen. Sie können das folgende Windows PowerShell-Cmdlet verwenden, um Active Directory-Benutzer zu importieren.  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>So importieren Sie ein Active Directory-Benutzerkonto in Windows Server Essentials-Dashboard  
  
1.  Melden Sie sich auf den Zielserver als Domänenadministrator an.  
  
2.  Öffnen Sie die Windows PowerShell als Administrator.  
  
3.  Führen Sie das folgende Cmdlet aus, wobei `[AD username]` für den Namen des Active Directory-Benutzerkontos steht, das Sie importieren möchten:  
  
     `Import-WssUser  SamAccountName [AD username]`  
  
##  <a name="BKMK_MoveDHCP"></a> Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den router  
 Wenn Ihr Quellserver in der DHCP-Rolle ausgeführt wird, führen Sie die folgenden Schritte aus, um die DHCP-Rolle auf den Router zu verschieben.  
  
#### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>Verschieben der DHCP-Serverrolle vom Quellserver auf den Router.  
  
1.  Deaktivieren Sie wie folgt den DHCP-Dienst auf dem Quellserver:  
  
    1.  Klicken Sie auf dem Quellserver auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Dienste**.  
  
    2.  Klicken Sie in der Liste der zurzeit ausgeführten Dienste mit der rechten Maustaste auf **DHCP-Server**, und klicken Sie dann auf **Eigenschaften**.  
  
    3.  Wählen Sie für **Starttyp**die Option **deaktiviert**.  
  
    4.  Halten Sie den Dienst an.  
  
2.  Aktivieren Sie die DHCP-Rolle auf dem Router.  
  
    1.  Befolgen Sie die Anweisungen in Ihrer Router-Dokumentation, um die DHCP-Serverrolle auf dem Router zu aktivieren.  
  
    2.  Befolgen Sie, um sicherzustellen, dass die vom Quellserver ausgestellten IP-Adressen unverändert bleiben, die Anweisungen in der Routerdokumentation, um den DHCP-Bereich auf den Router so zu konfigurieren, dass er mit dem DHCP-Bereich auf dem Quellserver identisch ist.  
  
        > [!IMPORTANT]
        >  Wenn Sie keine statische IP oder DHCP-Reservierungen auf dem Router für den Zielserver eingerichtet haben, und der DHCP-Bereich nicht identisch mit dem Quellserver ist, ist es möglich, dass der Router eine neue IP-Adresse für den Zielserver ausstellt. Setzen Sie in diesem Fall die Portweiterleitungsregeln des Routers zum Weiterleiten auf die neue IP-Adresse des Zielservers zurück.  
  
##  <a name="BKMK_Network"></a> Konfigurieren des Netzwerks  
 Nachdem Sie die DHCP-Rolle zum Router verschoben haben, konfigurieren Sie die Netzwerkeinstellungen auf dem Zielserver.  
  
#### <a name="to-configure-the-network"></a>So konfigurieren Sie das Netzwerk  
  
1.  Öffnen Sie auf dem Zielserver das Dashboard.  
  
2.  Klicken Sie auf der **Startseite** auf **SETUP**, und wählen Sie **"Zugriff überall" einrichten** und dann **Hier klicken, um "Zugriff überall" zu konfigurieren** aus.  
  
3.  Vervollständigen Sie die Anweisungen im Assistenten, um Ihren Router und Domänennamen zu konfigurieren.  
  
 Wenn Ihr Router das UPnP-Framework nicht unterstützt, oder wenn das UPnP-Framework deaktiviert ist, wird möglicherweise ein gelbes Warnsymbol neben dem Namen des Routers angezeigt. Stellen Sie sicher, dass folgende Ports geöffnet sind, und dass sie an die IP-Adresse des Zielservers weitergeleitet werden:  
  
-   Port 80: HTTP-Webdatenverkehr  
  
-   Port 443: HTTPS-Webdatenverkehr  
  
> [!NOTE]
>  Wenn Sie einen lokalen Exchange-Server auf einem zweiten Server eingerichtet haben, müssen Sie sicherstellen, dass auch Port 25 (SMTP) geöffnet ist und an die IP-Adresse des lokalen Exchange-Server umgeleitet wird.  
  
##  <a name="BKMK_RemoveLegacyADGPO"></a> Entfernen Sie älterer Active Directory Group Policy Objects (optional)  
 Die Gruppenrichtlinienobjekte (GPOs) werden für Windows Server Essentials aktualisiert. Sie stellen eine Obermenge der Windows Small Business Server 2011-Gruppenrichtlinienobjekte dar. Für Windows Server Essentials muss eine Reihe von Windows Small Business Server 2011-Gruppenrichtlinienobjekten und Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) manuell gelöscht werden, um Konflikte mit dem Windows Server Essentials-Gruppenrichtlinienobjekten und WMI-Filtern zu verhindern.  
  
> [!NOTE]
>  Wenn Sie die ursprünglichen Windows Small Business Server 2011-Gruppenrichtlinienobjekte geändert haben, sollten Sie Kopien davon an einem anderen Speicherort ablegen und diese anschließend von Windows Small Business Server 2011 entfernen.  
  
#### <a name="to-remove-old-group-policy-objects-from-windows-small-business-server-2011"></a>So entfernen Sie die alten Gruppenrichtlinienobjekte von Windows Small Business Server 2011  
  
1.  Melden Sie sich beim Quellserver mit einem Administratorkonto an.  
  
2.  Klicken Sie auf **Start** und anschließend auf **Serververwaltung**.  
  
3.  Klicken Sie im Navigationsbereich auf **Advanced Management**, klicken Sie auf **Gruppenrichtlinienverwaltung**, und klicken Sie dann auf **Gesamtstruktur: *** < IhrDomänenname\>*.  
  
4.  Klicken Sie auf **Domänen**, klicken Sie auf *< IhrDomänenname\>*, und klicken Sie dann auf **Group Policy Objects**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Small Business Server Auditing Policy**, klicken Sie auf **Löschen** und dann auf **OK**.  
  
6.  Wiederholen Sie Schritt 5, um die folgenden Gruppenrichtlinienobjekte zu löschen, die für Ihr Netzwerk gelten:  
  
    -   Windows SBS-Client Windows 7 und Windows Vista-Richtlinie  
  
    -   Windows SBS-Client Windows XP-Richtlinie  
  
    -   Windows SBS-CSE-Richtlinie  
  
    -   Windows SBS-Benutzerrichtlinie  
  
    -   Update Services Client-Computerrichtlinie  
  
    -   Richtlinie für die allgemeinen Einstellungen für Update Services  
  
    -   Update Services Server-Computerrichtlinie  
  
7.  Stellen Sie sicher, dass alle Gruppenrichtlinienobjekte gelöscht werden.  
  
#### <a name="to-remove-wmi-filters-from-the-source-server"></a>So entfernen Sie WMI-Filter vom Quellserver  
  
1.  Melden Sie sich beim Quellserver mit einem Administratorkonto an.  
  
2.  Klicken Sie auf **Start** und anschließend auf **Serververwaltung**.  
  
3.  Klicken Sie im Navigationsbereich auf **Features**, klicken Sie auf **Gruppenrichtlinienverwaltung**, und klicken Sie dann auf **Gesamtstruktur: *** < Ihrnetzwerkdomänenname\>*  
  
4.  Klicken Sie auf **Domänen**, klicken Sie auf *< Ihrnetzwerkdomänenname\>*, und klicken Sie dann auf **WMI-Filter**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Windows SBS-Client**, wählen Sie **Löschen** aus, und klicken Sie dann auf **Ja**.  
  
6.  Mit der rechten Maustaste **Windows SBS-Client Windows 7 und Windows Vista**, klicken Sie auf **löschen**, und klicken Sie dann auf **Ja**.  
  
7.  Mit der rechten Maustaste **Windows SBS-Client Windows XP**, klicken Sie auf **löschen**, und klicken Sie dann auf **Ja**.  
  
8.  Stellen Sie sicher, dass diese drei WMI-Filter gelöscht werden.  
  
##  <a name="BKMK_MapPermittedComputers"></a> Ordnen Sie zugelassener Computer zu Benutzerkonten zu  
 Wenn ein Benutzer in Windows Small Business Server 2011 eine Verbindung mit dem Remotewebzugriff herstellt, werden alle Computer im Netzwerk angezeigt. Dies kann Computer umfassen, für die der Benutzer keine Zugriffsberechtigung hat. In Windows Server Essentials muss ein Benutzer einen Computer für die er in Remote Web Access angezeigt werden explizit zugewiesen werden. Jedes Benutzerkonto, das von Windows Small Business Server 2011 migriert wird, muss einem oder mehreren Computern zugeordnet werden.  
  
#### <a name="to-map-user-accounts-to-computers"></a>So weisen Sie Benutzerkonten Computern zu  
  
1.  Öffnen Sie Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Klicken Sie in der Liste von Benutzerkonten mit der rechten Maustaste auf ein Benutzerkonto, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
4.  Klicken Sie auf der Registerkarte **Zugriff überall** auf **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**.  
  
5.  Wählen Sie **Freigegebene Ordner**, **Computers**und **Links auf der Startseite**aus, und klicken Sie dann auf **Übernehmen**.  
  
6.  Klicken Sie auf der Registerkarte **Computerzugriff** auf den Namen des Computers, für den Sie Zugriff gewähren möchten.  
  
7.  Wiederholen Sie die Schritte 3, 4, 5 und 6 für jedes Benutzerkonto.  
  
> [!NOTE]
>  Die Konfiguration des Clientcomputers braucht nicht geändert zu werden. Er wird automatisch konfiguriert.  
  
> [!NOTE]
>  Wenn nach abgeschlossener Migration ein Problem beim Erstellen des ersten neuen Benutzerkontos auf dem Zielserver auftritt, entfernen Sie das Benutzerkonto, das Sie hinzugefügt haben, und erstellen Sie es erneut.
