---
title: "Verschieben von Windows SBS 2008-Einstellungen und Daten auf den Zielserver für Windows Server Essentials-migration"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4950469d-d800-430d-8d10-53bafc4a9932
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 14a9ab8b4cc18f9c71af6207b854f34af3fa3d17
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="move-windows-sbs-2008-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Verschieben von Windows SBS 2008-Einstellungen und Daten auf den Zielserver für Windows Server Essentials-migration

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Verschieben von Einstellungen und Daten wie folgt auf den Zielserver:  
  

1.  [Kopieren von Daten auf dem Zielserver](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
2.  [Importieren von Active Directory-Benutzerkonten in Windows Server Essentials-Dashboard (optional)](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_ImportADaccounts)  
  
3.  [Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den router](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MoveDHCP)  
  
4.  [Konfigurieren des Netzwerks](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
5.  [Entfernen Sie älterer Active Directory-Gruppenrichtlinien-Objekte (optional)](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_RemoveLegacyADGPO)  
  
6.  [Ordnen Sie zugelassener Computer zu Benutzerkonten zu](Move-Windows-SBS-2008-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="BKMK_CopyData"></a>Kopieren von Daten auf dem Zielserver  
 Bevor Sie Daten vom Quellserver auf den Zielserver kopieren, werden führen Sie die folgenden Aufgaben aus:  
  
-   Überprüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie oder passen Sie der Ordner auf dem Zielserver, der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren an.  
  
-   Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.  
  
-   Stellen Sie die freigegebenen Ordner auf dem Quellserver nur Lesezugriff für alle Benutzer daher nicht geschrieben werden kann, auf das Laufwerk, während Sie Dateien auf den Zielserver kopieren.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver  
  
1.  Melden Sie sich auf den Zielserver als Domänenadministrator an, und öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     Dabei gilt:
     - \ < SourceServerName\ > ist der Name des Quellservers
     - \ < SharedSourceFolderName\ > ist der Name des freigegebenen Ordners auf dem Quellserver
     - \ < DestinationServerName\ > ist der Name des Zielservers,
     - \ < SharedDestinationFolderName\ > ist der freigegebene Ordner auf dem Zielserver, der die Daten kopiert werden.  
  
3.  Wiederholen Sie den vorherigen Schritt für jeden freigegebenen Ordner, den Sie vom Quellserver migrieren.  
  
##  <a name="BKMK_ImportADaccounts"></a>Importieren von Active Directory-Benutzerkonten in Windows Server Essentials-Dashboard (optional)  
 Standardmäßig werden alle auf dem Quellserver erstellte Benutzerkonten automatisch auf das Dashboard in Windows Server Essentials migriert. Jedoch wird die automatische Migration eines Active Directory-Benutzerkontos fehl, wenn einige Eigenschaften die migrationsanforderungen nicht erfüllen. Das folgende Windows PowerShell-Cmdlet können Sie um Active Directory-Benutzer zu importieren.  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>So importieren Sie ein Active Directory-Benutzerkonto in Windows Server Essentials-Dashboard  
  
1.  Melden Sie sich an den Zielserver als Domänenadministrator an.  
  
2.  Öffnen Sie Windows PowerShell als Administrator.  
  
3.  Führen Sie das folgende Cmdlet, in denen `[AD username]` ist der Name des Active Directory-Benutzerkonto an, die Sie importieren möchten:  
  
     `Import-WssUser  SamAccountName [AD username]`  
  
##  <a name="BKMK_MoveDHCP"></a>Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den router  
 Wenn der Quellserver die DHCP-Serverrolle ausgeführt wird, führen Sie die folgenden Schritte aus, um die DHCP-Serverrolle auf den Router verschieben.  
  
#### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>Um die DHCP-Serverrolle vom Quellserver auf den Router zu verschieben.  
  
1.  Deaktivieren Sie den DHCP-Dienst auf dem Quellserver wie folgt aus:  
  
    1.  Klicken Sie auf dem Quellserver auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Dienste**.  
  
    2.  In der Liste der derzeit ausgeführten Dienste mit der rechten Maustaste **DHCP-Server**, und klicken Sie dann auf **Eigenschaften**.  
  
    3.  Für **Starttyp**Option **deaktiviert**.  
  
    4.  Beenden Sie den Dienst.  
  
2.  Die DHCP-Serverrolle auf dem Router aktivieren  
  
    1.  Führen Sie die Anweisungen in der Routerdokumentation, um die DHCP-Serverrolle auf dem Router aktivieren.  
  
    2.  Folgen Sie den Anweisungen in der Routerdokumentation so konfigurieren Sie den DHCP-Bereich auf dem Router für den DHCP-Bereich auf dem Quellserver identisch sein, um sicherzustellen, dass vom Quellserver ausgestellte IP-Adressen unverändert bleiben.  
  
        > [!IMPORTANT]
        >  Wenn Sie keine statische IP-Adresse oder DHCP-Reservierungen auf dem Router, für den Zielserver eingerichtet haben, und der DHCP-Bereich identisch mit dem Quellserver ist, ist es möglich, dass der Router eine neue IP-Adresse für den Zielserver ausstellt. In diesem Fall die portweiterleitungsregeln des Routers zum Weiterleiten der neuen IP-Adresse des Zielservers zurückgesetzt.  
  
##  <a name="BKMK_Network"></a>Konfigurieren des Netzwerks  
 Nachdem Sie die DHCP-Serverrolle auf den Router verschieben, konfigurieren Sie die Netzwerkeinstellungen auf dem Zielserver.  
  
#### <a name="to-configure-the-network"></a>Konfigurieren des Netzwerks  
  
1.  Öffnen Sie das Dashboard, auf dem Zielserver.  
  
2.  Auf dem Dashboard **Home** auf **SETUP**, klicken Sie auf **"Zugriff überall" einrichten**, und wählen Sie dann die **zum Konfigurieren von "Zugriff überall"** Option.  
  
3.  Führen Sie die Anweisungen im Assistenten so konfigurieren Sie den Router und Domänennamen.  
  
 Wenn Ihr Router das UPnP-Framework nicht unterstützt oder wenn das UPnP-Framework deaktiviert ist, kann ein gelbes Warnsymbol neben dem Namen des Routers angezeigt werden. Stellen Sie sicher, dass folgende Ports geöffnet sind und sie an die IP-Adresse des Zielservers weitergeleitet werden:  
  
-   Port 80: HTTP-Webdatenverkehr  
  
-   Port 443: HTTPS-Webdatenverkehr  
  
> [!NOTE]
>  Wenn Sie einen lokalen Exchange-Server auf einem zweiten Server eingerichtet haben, müssen Sie sicherstellen, auch Port 25 (SMTP) geöffnet ist und dass es an die IP-Adresse der lokalen Exchange-Server umgeleitet wird.  
  
##  <a name="BKMK_RemoveLegacyADGPO"></a>Entfernen Sie älterer Active Directory-Gruppenrichtlinien-Objekte (optional)  
 Die Gruppenrichtlinienobjekte (GPOs) sind für Windows Server Essentials aktualisiert. Sie sind eine Obermenge der Windows SBS 2008-Gruppenrichtlinienobjekte. Für Windows Server Essentials muss eine Reihe von Windows SBS 2008-Gruppenrichtlinienobjekten und Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) manuell gelöscht werden, um Konflikte mit den Windows Server Essentials-Gruppenrichtlinienobjekten und WMI-Filtern zu verhindern.  
  
> [!NOTE]
>  Wenn Sie die ursprünglichen Windows SBS 2008-Gruppenrichtlinien-Objekte geändert haben, sollten Sie Kopien davon an einem anderen Speicherort speichern und sie dann aus Windows SBS 2008 löschen.  
  
#### <a name="to-remove-old-group-policy-objects-from-windows-sbs-2008"></a>So entfernen Sie alte Gruppenrichtlinienobjekte aus Windows SBS 2008  
  
1.  Melden Sie sich auf dem Quellserver mit einem Administratorkonto an.  
  
2.  Klicken Sie auf **starten**, und klicken Sie dann auf **Serververwaltung**.  
  
3.  Klicken Sie im Navigationsbereich auf **Erweiterte Verwaltung**, klicken Sie auf **Gruppenrichtlinienverwaltung**, und klicken Sie dann auf **Gesamtstruktur:***< YourDomainName\ >*.  
  
4.  Klicken Sie auf **Domänen**, klicken Sie auf *< YourDomainName\ >*, und klicken Sie dann auf **Group Policy Objects**.  
  
5.  Mit der rechten Maustaste **Small Business Server Auditing Policy**, klicken Sie auf **löschen**, und klicken Sie dann auf **OK**.  
  
6.  Wiederholen Sie Schritt 5, um die folgenden Gruppenrichtlinienobjekte zu löschen, die für Ihr Netzwerk gelten:  
  
    -   Small Business Server-Clientcomputer  
  
    -   Small Business Server Domain Password Policy  
  
         Es wird empfohlen, die Sie konfigurieren die Kennwortrichtlinie in Windows Server Essentials um sichere Kennwörter zu erzwingen. Um die Kennwortrichtlinie zu konfigurieren, verwenden Sie das Dashboard, das die Konfiguration in die Standarddomänenrichtlinie schreibt. Die Konfiguration der Kennwortrichtlinie wird nicht in das Small Business Server Domain Password Policy-Objekt geschrieben, wie dies in Windows SBS 2008 war.  
  
    -   Small Business Server-Internetverbindungsfirewall  
  
    -   Small Business Server-Kontosperrungsrichtlinie  
  
    -   Small Business Server-Remoteunterstützungsrichtlinie  
  
    -   Small Business Server-Windows-Firewall  
  
    -   Small Business Server Update Services-Clientcomputerrichtlinie  
  
         Dieses Gruppenrichtlinienobjekt ist vorhanden sein, wenn Sie von Windows SBS 2008 R2 migrieren.  
  
    -   Small Business Server Update Services Allgemeine Einstellungen-Richtlinie  
  
         Dieses Gruppenrichtlinienobjekt ist vorhanden sein, wenn Sie von Windows SBS 2008 R2 migrieren.  
  
    -   Small Business Server Update Services-Server-Computerrichtlinie  
  
         Dieses Gruppenrichtlinienobjekt ist vorhanden sein, wenn Sie von Windows SBS 2008 R2 migrieren.  
  
7.  Stellen Sie sicher, dass alle Gruppenrichtlinienobjekte gelöscht werden.  
  
#### <a name="to-remove-wmi-filters-from-windows-sbs-2008"></a>So entfernen Sie WMI-Filter aus Windows SBS 2008  
  
1.  Melden Sie sich auf dem Quellserver mit einem Administratorkonto an.  
  
2.  Klicken Sie auf **starten**, und klicken Sie dann auf **Serververwaltung**.  
  
3.  Klicken Sie im Navigationsbereich auf **Erweiterte Verwaltung**, klicken Sie auf **Gruppenrichtlinienverwaltung**, und klicken Sie dann auf **Gesamtstruktur:***< YourNetworkDomainName\ >*  
  
4.  Klicken Sie auf **Domänen**, klicken Sie auf *< YourNetworkDomainName\ >*, und klicken Sie dann auf **WMI-Filter**.  
  
5.  Mit der rechten Maustaste **PostSP2**, klicken Sie auf **löschen**, und klicken Sie dann auf **Ja**.  
  
6.  Mit der rechten Maustaste **PreSP2**, klicken Sie auf **löschen**, und klicken Sie dann auf **Ja**.  
  
7.  Stellen Sie sicher, dass diese drei WMI-Filter gelöscht werden.  
  
##  <a name="BKMK_MapPermittedComputers"></a>Ordnen Sie zugelassener Computer zu Benutzerkonten zu  
 Wenn ein Benutzer eine Verbindung mit Remote Web Access herstellt, werden alle Computer im Netzwerk in Windows SBS 2008 angezeigt. Dies kann Computer umfassen, die der Benutzer nicht über die Berechtigung zum Zugriff auf. In Windows Server Essentials muss ein Benutzer explizit einem Computer, damit er in Remote Web Access angezeigt werden zugewiesen werden. Jedes Benutzerkonto, das aus Windows SBS 2008 migriert wird, muss einem oder mehreren Computern zugeordnet werden.  
  
#### <a name="to-map-user-accounts-to-computers"></a>So weisen Sie Benutzerkonten für Computer  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie in der Navigationsleiste auf **Benutzer**.  
  
3.  Klicken Sie in der Liste der Benutzerkonten, Maustaste auf ein Benutzerkonto, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
4.  Klicken Sie auf die **"Zugriff überall"** Registerkarte, und klicken Sie dann auf **ermöglichen den Remotewebzugriff und Zugriff auf Webdienstanwendungen. **.  
  
5.  Wählen Sie **freigegebene Ordner**wählen **Computer**wählen **Links auf der Startseite**, und klicken Sie dann auf **übernehmen**.  
  
6.  Klicken Sie auf die **Zugriff auf den Computer** Registerkarte, und klicken Sie dann auf den Namen des Computers, zu dem Sie den Zugriff zulassen möchten.  
  
7.  Wiederholen Sie die Schritte 3, 4, 5 und 6 für jedes Benutzerkonto.  
  
> [!NOTE]
>  Sie müssen nicht zum Ändern der Konfiguration des Client-Computers. Es wird automatisch konfiguriert.  
  
> [!NOTE]
>  Nach der Migration durchführen, wenn Sie ein Problem auftritt, bei der Erstellung des ersten neuen Benutzerkontos auf dem Zielserver entfernen Sie das Benutzerkonto an, das Sie hinzugefügt haben, und erstellen Sie es erneut.
