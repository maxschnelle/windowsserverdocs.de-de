---
title: Verschieben von Windows SBS 2011 Essentials-Einstellungen und -Daten auf den Zielserver für die Migration zu Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47548994-9fa0-42e0-afa4-c2ccbd063acb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 506975db4238abca6ba2d07845281e936e82a76e
ms.sourcegitcommit: 9a4ab3a0d00b06ff16173aed616624c857589459
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2019
ms.locfileid: "66828564"
---
# <a name="move-windows-sbs-2011-essentials-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Verschieben von Windows SBS 2011 Essentials-Einstellungen und -Daten auf den Zielserver für die Migration zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Verschieben von Einstellungen und Daten auf den Zielserver:  
  

1.  [Kopieren von Daten auf den Zielserver](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_CopyData)  
  
2.  [Importieren von Active Directory-Benutzerkonten in Windows Server Essentials-Dashboard (optional)](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_ImportADaccounts)  
  
3.  [Konfigurieren des Netzwerks](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_Network)  
  
4.  [Ordnen Sie zugelassener Computer zu Benutzerkonten zu](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_MapPermittedComputers)  
 
##  <a name="BKMK_CopyData"></a> Kopieren von Daten auf den Zielserver  
 Führen Sie die folgenden Aufgaben aus, bevor Sie Daten vom Quellserver zum Zielserver kopieren:  
  
-   Prüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie die Ordner auf dem Zielserver so bzw. passen Sie diese so an, dass sie der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren.  
  
-   Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.  
  
-   Machen Sie die freigegebenen Ordner auf dem Quellserver für alle Benutzer schreibgeschützt, damit auf das Laufwerk nicht geschrieben werden kann, während Sie Dateien auf den Zielserver kopieren.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver.  
  
1.  Melden Sie sich beim Zielserver als Domänenadministrator an, und öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     Erläuterungen:
     - \<Quellservername\> ist der Name des Quellservers
     - \<Namedesfreigegebenenquellordners\> ist der Name des freigegebenen Ordners auf dem Quellserver
     - \<Zielservername\> ist der Name des Zielservers,
     - \<Namedesfreigegebenenzielordners\> ist der freigegebene Ordner auf dem Zielserver, auf denen die Daten kopiert werden.  
        
3.  Wiederholen Sie den vorherigen Schritt für jeden freigegebenen Ordner, zu dem Sie die Migration vom Quellserver aus vornehmen.  
  
##  <a name="BKMK_ImportADaccounts"></a> Importieren von Active Directory-Benutzerkonten in Windows Server Essentials-Dashboard (optional)  
 Standardmäßig werden alle auf dem Quellserver erstellte Benutzerkonten automatisch an das Dashboard in Windows Server Essentials migriert. Die automatische Migration eines Active Directory-Benutzerkontos schlägt jedoch fehl, wenn nicht alle Eigenschaften die Migrationsanforderungen erfüllen. Sie können das folgende Windows PowerShell-Cmdlet verwenden, um Active Directory-Benutzer zu importieren.  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>So importieren Sie ein Active Directory-Benutzerkonto in Windows Server Essentials-Dashboard  
  
1.  Melden Sie sich auf den Zielserver als Domänenadministrator an.  
  
2.  Öffnen Sie die Windows PowerShell als Administrator.  
  
3.  Führen Sie das folgende Cmdlet aus, wobei `[AD username]` für den Namen des Active Directory-Benutzerkontos steht, das Sie importieren möchten:  
  
     `Import-WssUser  SamAccountName [AD username]`  
  
##  <a name="BKMK_Network"></a> Konfigurieren des Netzwerks  
  
#### <a name="to-configure-the-network"></a>So konfigurieren Sie das Netzwerk  
  
1. Öffnen Sie auf dem Zielserver das Dashboard.  
  
2. Klicken Sie auf dem Dashboard **Home** auf **Setup**, klicken Sie auf **"Zugriff überall" einrichten**, und wählen Sie dann die Option **Zum Konfigurieren von "Zugriff überall" klicken** aus.  
  
3. Vervollständigen Sie die Anweisungen im Assistenten, um Ihren Router und Domänennamen zu konfigurieren.  
  
   Wenn Ihr Router das UPnP-Framework nicht unterstützt, oder wenn das UPnP-Framework deaktiviert ist, wird möglicherweise ein gelbes Warnsymbol neben dem Namen des Routers angezeigt. Stellen Sie sicher, dass folgende Ports geöffnet sind, und dass sie an die IP-Adresse des Zielservers weitergeleitet werden:  
  
-   Port 80: HTTP-Webdatenverkehr  
  
-   Port 443: HTTPS-Webdatenverkehr  
  
##  <a name="BKMK_MapPermittedComputers"></a> Ordnen Sie zugelassener Computer zu Benutzerkonten zu  
 Jedes Benutzerkonto, das von Windows Small Business Server 2011 Essentials migriert wird, muss einem oder mehreren Computern zugeordnet werden.  
  
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
