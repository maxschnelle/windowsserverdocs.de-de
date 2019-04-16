---
title: "Verschieben von Windows Server 2008 Foundation-Einstellungen und Daten auf den Zielserver für Windows Server Essentials-migration"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ff7d040-ebd1-421c-80db-765deacedd4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 80e70ba954d981985caa5329379661d978456c7f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="move-windows-server-2008-foundation-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Verschieben von Windows Server 2008 Foundation-Einstellungen und Daten auf den Zielserver für Windows Server Essentials-migration

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Verschieben von Einstellungen und Daten wie folgt auf den Zielserver: 

1.  [Kopieren von Daten auf dem Zielserver (optional)](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
2.  [Importieren von Active Directory-Benutzerkonten in Windows Server Essentials-Dashboard (optional)](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_ImportADaccounts)  
  
3.  [Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den router](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MoveDHCP)  
  
4.  [Konfigurieren des Netzwerks](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
5.  [Ordnen Sie zugelassener Computer zu Benutzerkonten zu](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="BKMK_CopyData"></a>Kopieren von Daten auf dem Zielserver (optional)  
 Bevor Sie Daten vom Quellserver auf den Zielserver kopieren, werden führen Sie die folgenden Aufgaben aus:  
  
-   Überprüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie oder passen Sie der Ordner auf dem Zielserver, der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren an.  
  
-   Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.  
  
-   Stellen Sie die freigegebenen Ordner auf dem Quellserver nur Lesezugriff für alle Benutzer daher nicht geschrieben werden kann, auf das Laufwerk, während Sie Dateien auf den Zielserver kopieren.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver  
  
1.  Melden Sie sich auf dem Zielserver als Domänenadministrator an, und öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     Dabei gilt:
     - \ < SourceServerName\ > ist der Name des Quellservers
     - \ < SharedSourceFolderName\ > ist der Name des freigegebenen Ordners auf dem Quellserver
     - \ < DestinationServerName\ > ist der Name des Zielservers,
     - \ < SharedDestinationFolderName\ > ist der freigegebene Ordner auf dem Zielserver, der die Daten kopiert werden.  
  
3.  Wiederholen Sie den vorherigen Schritt für jeden freigegebenen Ordner, den Sie vom Quellserver migrieren.  
  
##  <a name="BKMK_ImportADaccounts"></a>Importieren von Active Directory-Benutzerkonten in Windows Server Essentials-Dashboard (optional)  
 Standardmäßig werden alle auf dem Quellserver erstellte Benutzerkonten automatisch auf das Dashboard in Windows Server Essentials migriert. Automatische Migration eines Active Directory-Benutzerkontos schlägt jedoch fehl, wenn es sich bei nicht alle Eigenschaften die migrationsanforderungen erfüllen. Das folgende Windows PowerShell-Cmdlet können Sie um Active Directory-Benutzer zu importieren.  
  
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
  
2.  Aktivieren Sie die DHCP-Serverrolle auf dem Router.  
  
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
  
##  <a name="BKMK_MapPermittedComputers"></a>Ordnen Sie zugelassener Computer zu Benutzerkonten zu  
 In Windows Server Essentials muss ein Benutzer explizit einem Computer, damit er in Remote Web Access angezeigt werden zugewiesen werden. Jedes Benutzerkonto, das von Windows Server 2008 Foundation migriert wird, muss einem oder mehreren Computern zugeordnet werden.  
  
#### <a name="to-map-user-accounts-to-computers"></a>So weisen Sie Benutzerkonten für Computer  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie in der Navigationsleiste auf **Benutzer**.  
  
3.  Klicken Sie in der Liste der Benutzerkonten, Maustaste auf ein Benutzerkonto, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
4.  Klicken Sie auf die **"Zugriff überall"** Registerkarte, und klicken Sie dann auf **ermöglichen den Remotewebzugriff und Zugriff auf Webdienstanwendungen**.  
  
5.  Wählen Sie **freigegebene Ordner**wählen **Computer**wählen **Links auf der Startseite**, und klicken Sie dann auf **übernehmen**.  
  
6.  Klicken Sie auf die **Zugriff auf den Computer** Registerkarte, und klicken Sie dann auf den Namen des Computers, zu dem Sie den Zugriff zulassen möchten.  
  
7.  Wiederholen Sie die Schritte 3, 4, 5 und 6 für jedes Benutzerkonto.  
  
> [!NOTE]
>  Sie müssen nicht zum Ändern der Konfiguration des Client-Computers. Es wird automatisch konfiguriert.  
  
> [!NOTE]
>  Nach der Migration durchführen, wenn Sie ein Problem auftritt, bei der Erstellung des ersten neuen Benutzerkontos auf dem Zielserver entfernen Sie das Benutzerkonto an, das Sie hinzugefügt haben, und erstellen Sie es erneut.
