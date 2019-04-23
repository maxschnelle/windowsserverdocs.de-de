---
title: 'Schritt 4: Verschieben von Einstellungen und Daten auf den Zielserver für die Migration zu Windows Server Essentials'
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: e5a8db44f80c333d589e0c1664174c394701f90d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835681"
---
# <a name="step-4-move-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Schritt 4: Verschieben von Einstellungen und Daten auf den Zielserver für die Migration zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver. Verschieben von Einstellungen und Daten auf den Zielserver:  
  
-   [Kopieren von Daten auf den Zielserver](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
-   [Konfigurieren des Netzwerks](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
-   [Ordnen Sie zugelassener Computer zu Benutzerkonten zu](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="BKMK_CopyData"></a> Kopieren von Daten auf den Zielserver  
 Führen Sie die folgenden Aufgaben aus, bevor Sie Daten vom Quellserver zum Zielserver kopieren:  
  
-   Prüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie die Ordner auf dem Zielserver so bzw. passen Sie diese so an, dass sie der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren.  
  
-   Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.  
  
-   Legen Sie für die freigegebenen Ordner auf dem Quellserver für alle Benutzer einen Schreibschutz fest, damit die Festplatte nicht beschrieben werden kann, während Sie Dateien auf den Zielserver kopieren.  
  
-   Der Ordner **Clientcomputersicherung** kann nicht auf den Zielserver migriert werden. Stellen Sie vor der Servermigration sicher, dass alle Clientcomputer fehlerfrei sind. Nach der Servermigration empfiehlt es sich, Sicherungen der Clientcomputer zu konfigurieren und zu starten, um sicherzustellen, dass die Daten für alle wichtigen Clientcomputer gesichert werden.  
  
-   Die **Sicherungen von Dateiversionsverläufen** Ordner kann nicht direkt auf dem Zielserver aufgrund der Ordnerstruktur und geänderter Sicherungsmetadaten in Windows Server Essentials migriert werden. Es ist jedoch möglich, den Ordner **Sicherungen von Dateiversionsverläufen** für einen bestimmten Benutzer auf einem bestimmten Computer zu migrieren. Hierzu suchen Sie den Ordner **Daten** im Ordner **Sicherungen von Dateiversionsverläufen** für den betreffenden Benutzer und Computer und kopieren diesen Ordner **Daten** in den Ordner **Sicherungen von Dateiversionsverläufen** auf dem Zielserver.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver.  
  
1.  Melden Sie sich bei dem Zielserver als Domänenadministrator an, und öffnen Sie ein Eingabeaufforderungsfenster oder eine Windows PowerShell-Eingabeaufforderung.  
  
2.  Wenn Sie das Eingabeaufforderungsfenster verwenden, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  
  
    `robocopy \\<SourceServerName>\<SharedSourceFolderName> "<PathOfTheDestination>\<SharedDestinationFolderName>" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`
  
     Dabei gilt:  
  
    -   \<Quellservername\> ist der Name des Quellservers  
  
    -   \<Namedesfreigegebenenquellordners\> ist der Name des freigegebenen Ordners auf dem Quellserver  
  
    -   \<PathOfTheDestination\> ist der absolute Pfad, in dem Sie den Ordner verschieben möchten,  
  
    -   \<Namedesfreigegebenenzielordners\> ist der Ordner auf dem Zielserver, auf denen die Daten kopiert werden,  
  
     Beispiel:  `robocopy \\sourceserver\MyData "d:\ServerFolders\MyData" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`.  
  
3.  Wenn Sie Windows PowerShell verwenden, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
     `Add-Wssfolder  Path \ -Name  -KeepPermission`  
  
4.  Wiederholen Sie diesen Vorgang für jeden freigegebenen Ordner, den Sie vom Quellserver migrieren.  
  
##  <a name="BKMK_Network"></a> Konfigurieren des Netzwerks  
  
#### <a name="to-configure-the-network"></a>So konfigurieren Sie das Netzwerk  
  
1.  Öffnen Sie auf dem Zielserver das Dashboard.  
  
2.  Klicken Sie auf der Dashboardseite **Home** auf **Setup**, klicken Sie auf **Zugriff überall einrichten**, und wählen Sie dann die Option**Hier klicken, um Zugriff überall zu konfigurieren**.  
  
3.  Der Assistent zum Einrichten von Zugriff überall wird gestartet. Vervollständigen Sie die Anweisungen im Assistenten, um Ihren Router und Domänennamen zu konfigurieren.  
  
 Wenn Ihr Router das UPnP-Framework nicht unterstützt, oder wenn das UPnP-Framework deaktiviert ist, wird möglicherweise ein gelbes Warnsymbol neben dem Namen des Routers angezeigt. Stellen Sie sicher, dass folgende Ports geöffnet sind, und dass sie an die IP-Adresse des Zielservers weitergeleitet werden:  
  
-   Port 80: HTTP-Webdatenverkehr  
  
-   Port 443: HTTPS-Webdatenverkehr  
  
> [!NOTE]
>  Wenn Sie einen öffentlichen Domänennamen auf dem Zielserver konfigurieren möchten, müssen Sie den Domänennamen vom Quellserver zur Vermeidung einer Störung durch das dynamische DNS-Update freigeben.  
  
##  <a name="BKMK_MapPermittedComputers"></a> Ordnen Sie zugelassener Computer zu Benutzerkonten zu  
 Jedes Benutzerkonto, das von früheren Versionen von Windows Small Business Server oder Windows Server Essentials migriert wird, muss einem oder mehreren Computern zugeordnet werden.  
  
#### <a name="to-map-user-accounts-to-computers"></a>So weisen Sie Benutzerkonten Computern zu  
  
1.  Öffnen Sie Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Klicken Sie in der Liste von Benutzerkonten mit der rechten Maustaste auf ein Benutzerkonto, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
4.  Klicken Sie auf der Registerkarte **Zugriff überall** auf **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**.  
  
5.  Klicken Sie auf **freigegebene Ordner**, auf **Computer**, dann auf **Links zur Homepage**, und klicken Sie dann auf **Übernehmen**.  
  
6.  Klicken Sie auf der Registerkarte **Computerzugriff** auf den Namen des Computers, für den Sie Zugriff gewähren möchten.  
  
7.  Wiederholen Sie die Schritte 3, 4, 5 und 6 für jedes Benutzerkonto.  
  
> [!NOTE]
>  Die Konfiguration des Clientcomputers braucht nicht geändert zu werden. Er wird automatisch konfiguriert.  
  
> [!NOTE]
>  Wenn nach abgeschlossener Migration ein Problem beim Erstellen des ersten neuen Benutzerkontos auf dem Zielserver auftritt, entfernen Sie das Benutzerkonto, das Sie hinzugefügt haben, und erstellen Sie es erneut.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Einstellungen und Daten auf den Zielserver verschoben. Wechseln Sie nun zur [Schritt 5: Aktivieren der ordnerumleitung auf dem Zielserver für Windows Server Essentials-Migration](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  
  

Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

