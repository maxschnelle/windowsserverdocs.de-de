---
title: "Schritt4: Verschieben von Einstellungen und Daten auf den Zielserver für Windows Server Essentials-Migration"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e143df43-e227-4629-a4ab-9f70d9bf6e84
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: db1169a5415039498718a7988c711d068945b4b7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="step-4-move-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Schritt4: Verschieben von Einstellungen und Daten auf den Zielserver für Windows Server Essentials-Migration

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver. Verschieben von Einstellungen und Daten wie folgt auf den Zielserver:  
  
-   [Kopieren von Daten auf dem Zielserver](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
-   [Konfigurieren des Netzwerks](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
-   [Ordnen Sie zugelassener Computer zu Benutzerkonten zu](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="BKMK_CopyData"></a>Kopieren von Daten auf dem Zielserver  
 Bevor Sie Daten vom Quellserver auf den Zielserver kopieren, werden führen Sie die folgenden Aufgaben aus:  
  
-   Überprüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie oder passen Sie der Ordner auf dem Zielserver, der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren an.  
  
-   Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.  
  
-   Stellen Sie die freigegebenen Ordner auf dem Quellserver Read-only für alle Benutzer, damit keine Schreibvorgänge auf der Festplatte während der stattfinden können Sie kopieren Dateien auf den Zielserver.  
  
-   Die **Clientcomputersicherung** Ordner kann nicht auf den Zielserver migriert werden. Vor der Servermigration sicher, dass alle Clientcomputer fehlerfrei sind. Nach der Servermigration empfiehlt es sich, dass konfigurieren und starten Sie die clientcomputersicherung, um sicherzustellen, dass die Daten für alle wichtigen Clientcomputer gesichert ist.  
  
-   Die **Dateiversionsverläufen** Ordner nicht direkt auf den Zielserver aufgrund der Ordnerstruktur und geänderter Sicherungsmetadaten in Windows Server Essentials migriert werden. Es ist jedoch möglich, migrieren die **Dateiversionsverläufen** Ordner für einen bestimmten Benutzer auf einem bestimmten Computer. Hierzu Suchen der **Daten** Ordner in der **Sicherungen von Dateiversionsverläufen** Ordner für die Benutzer und Computer, und kopieren diesen **Daten** Ordner die **Sicherungen von Dateiversionsverläufen** Ordner auf dem Zielserver.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver  
  
1.  Melden Sie sich auf den Zielserver als Domänenadministrator an, und öffnen Sie ein Eingabeaufforderungsfenster oder eine Windows PowerShell-Eingabeaufforderung.  
  
2.  Wenn Sie das Eingabeaufforderungsfenster verwenden, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  
  
    `robocopy \\<SourceServerName>\<SharedSourceFolderName> "<PathOfTheDestination>\<SharedDestinationFolderName>" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`
  
     Dabei gilt:  
  
    -   \ < SourceServerName\ > ist der Name des Quellservers  
  
    -   \ < SharedSourceFolderName\ > ist der Name des freigegebenen Ordners auf dem Quellserver  
  
    -   \ < PathOfTheDestination\ > ist der absolute Pfad, in dem Sie möchten den Ordner verschieben,  
  
    -   \ < SharedDestinationFolderName\ > ist der Ordner auf dem Zielserver, der die Daten kopiert werden,  
  
     Z. B.`robocopy \\sourceserver\MyData "d:\ServerFolders\MyData" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`.  
  
3.  Wenn Sie Windows PowerShell verwenden, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE.  
  
     `Add-Wssfolder  Path \ -Name  -KeepPermission`  
  
4.  Wiederholen Sie diesen Vorgang für jeden freigegebenen Ordner, den Sie vom Quellserver migrieren.  
  
##  <a name="BKMK_Network"></a>Konfigurieren des Netzwerks  
  
#### <a name="to-configure-the-network"></a>Konfigurieren des Netzwerks  
  
1.  Öffnen Sie das Dashboard, auf dem Zielserver.  
  
2.  Auf dem Dashboard **Home** auf **Setup**, klicken Sie auf **"Zugriff überall" einrichten**, und wählen Sie dann die **zum Konfigurieren von "Zugriff überall"** Option.  
  
3.  Wird angezeigt, die überall den Assistenten zum einrichten. Führen Sie die Anweisungen im Assistenten so konfigurieren Sie den Router und Domänennamen.  
  
 Wenn Ihr Router das UPnP-Framework nicht unterstützt oder wenn das UPnP-Framework deaktiviert ist, kann ein gelbes Warnsymbol neben dem Namen des Routers angezeigt werden. Stellen Sie sicher, dass folgende Ports geöffnet sind und sie an die IP-Adresse des Zielservers weitergeleitet werden:  
  
-   Port 80: HTTP-Webdatenverkehr  
  
-   Port 443: HTTPS-Webdatenverkehr  
  
> [!NOTE]
>  Wenn Sie einen öffentlichen Domänennamen auf dem Zielserver konfigurieren möchten, müssen Sie den Domänennamen freigeben, vom Quellserver Wettbewerb des dynamischen DNS-Updates zu vermeiden.  
  
##  <a name="BKMK_MapPermittedComputers"></a>Ordnen Sie zugelassener Computer zu Benutzerkonten zu  
 Jedes Benutzerkonto, das von früheren Versionen von Windows Small Business Server oder Windows Server Essentials migriert wird, muss einem oder mehreren Computern zugeordnet werden.  
  
#### <a name="to-map-user-accounts-to-computers"></a>So weisen Sie Benutzerkonten für Computer  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie in der Navigationsleiste auf **Benutzer**.  
  
3.  Klicken Sie in der Liste der Benutzerkonten, Maustaste auf ein Benutzerkonto, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
4.  Klicken Sie auf die **"Zugriff überall"** Registerkarte, und klicken Sie dann auf **ermöglichen den Remotewebzugriff und Zugriff auf Webdienstanwendungen**.  
  
5.  Klicken Sie auf **freigegebene Ordner**, klicken Sie auf**Computer**, klicken Sie auf **Links auf der Startseite**, und klicken Sie dann auf **übernehmen**.  
  
6.  Klicken Sie auf die **Zugriff auf den Computer** Registerkarte, und klicken Sie dann auf den Namen des Computers, zu dem Sie den Zugriff zulassen möchten.  
  
7.  Wiederholen Sie die Schritte 3, 4, 5 und 6 für jedes Benutzerkonto.  
  
> [!NOTE]
>  Sie müssen nicht zum Ändern der Konfiguration des Client-Computers. Es wird automatisch konfiguriert.  
  
> [!NOTE]
>  Nach der Migration durchführen, wenn Sie ein Problem auftritt, bei der Erstellung des ersten neuen Benutzerkontos auf dem Zielserver entfernen Sie das Benutzerkonto an, das Sie hinzugefügt haben, und erstellen Sie es erneut.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Einstellungen und Daten auf den Zielserver verschoben. Lesen Sie jetzt [Schritt5: Aktivieren der ordnerumleitung auf dem Zielserver für Windows Server Essentials-Migration](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  
  

Alle Schrittefinden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

