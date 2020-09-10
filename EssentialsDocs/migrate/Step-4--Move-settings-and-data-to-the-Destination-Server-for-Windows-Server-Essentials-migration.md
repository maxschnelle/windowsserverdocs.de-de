---
title: 'Schritt 4: Verschieben von Einstellungen und Daten auf den Zielserver für die Migration zu Windows Server Essentials'
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: e143df43-e227-4629-a4ab-9f70d9bf6e84
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 888ecc5c5ab8fd609264f0f184686a144e2f8ce8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625472"
---
# <a name="step-4-move-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Schritt 4: Verschieben von Einstellungen und Daten auf den Zielserver für die Migration zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver. Verschieben von Einstellungen und Daten auf den Zielserver:

-   [Kopieren von Daten auf den Zielserver.](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)

-   [Netzwerk konfigurieren](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)

-   [Zuordnen zugelassener Computer zu Benutzerkonten](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)

##  <a name="copy-data-to-the-destination-server"></a><a name="BKMK_CopyData"></a> Kopieren von Daten auf den Ziel Server
 Führen Sie die folgenden Aufgaben aus, bevor Sie Daten vom Quellserver zum Zielserver kopieren:

-   Prüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie die Ordner auf dem Zielserver so bzw. passen Sie diese so an, dass sie der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren.

-   Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.

-   Legen Sie für die freigegebenen Ordner auf dem Quellserver für alle Benutzer einen Schreibschutz fest, damit die Festplatte nicht beschrieben werden kann, während Sie Dateien auf den Zielserver kopieren.

-   Der Ordner **Clientcomputersicherung** kann nicht auf den Zielserver migriert werden. Stellen Sie vor der Servermigration sicher, dass alle Clientcomputer fehlerfrei sind. Nach der Servermigration empfiehlt es sich, Sicherungen der Clientcomputer zu konfigurieren und zu starten, um sicherzustellen, dass die Daten für alle wichtigen Clientcomputer gesichert werden.

-   Der Ordner **Sicherungen von Datei** Versions Verläufen kann aufgrund der Ordnerstruktur und der Änderungen der Sicherungs Metadaten in Windows Server Essentials nicht direkt zum Ziel Server migriert werden. Es ist jedoch möglich, den Ordner **Sicherungen von Dateiversionsverläufen** für einen bestimmten Benutzer auf einem bestimmten Computer zu migrieren. Hierzu suchen Sie den Ordner **Daten** im Ordner **Sicherungen von Dateiversionsverläufen** für den betreffenden Benutzer und Computer und kopieren diesen Ordner **Daten** in den Ordner **Sicherungen von Dateiversionsverläufen** auf dem Zielserver.

#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver.

1. Melden Sie sich bei dem Zielserver als Domänenadministrator an, und öffnen Sie ein Eingabeaufforderungsfenster oder eine Windows PowerShell-Eingabeaufforderung.

2. Wenn Sie das Eingabeaufforderungsfenster verwenden, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   `robocopy \\<SourceServerName>\<SharedSourceFolderName> "<PathOfTheDestination>\<SharedDestinationFolderName>" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`

    Hierbei gilt:

   - \<SourceServerName\> ist der Name des Quellservers

   - \<SharedSourceFolderName\> ist der Name des freigegebenen Ordners auf dem Quellserver

   - \<PathOfTheDestination\> ist der absolute Pfad, in dem Sie den Ordner verschieben möchten

   - \<SharedDestinationFolderName\> ist der Ordner auf dem Zielserver, auf den die Daten kopiert werden

     z. B. `robocopy \\sourceserver\MyData "d:\ServerFolders\MyData" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`.

3. Wenn Sie Windows PowerShell verwenden, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

    `Add-Wssfolder  Path \ -Name  -KeepPermission`

4. Wiederholen Sie diesen Vorgang für jeden freigegebenen Ordner, den Sie vom Quellserver migrieren.

##  <a name="configure-the-network"></a><a name="BKMK_Network"></a> Netzwerk konfigurieren

#### <a name="to-configure-the-network"></a>So konfigurieren Sie das Netzwerk

1. Öffnen Sie auf dem Zielserver das Dashboard.

2. Klicken Sie auf der Dashboardseite **Home** auf **Setup**, klicken Sie auf **Zugriff überall einrichten**, und wählen Sie dann die Option**Hier klicken, um Zugriff überall zu konfigurieren**.

3. Der Assistent zum Einrichten von Zugriff überall wird gestartet. Vervollständigen Sie die Anweisungen im Assistenten, um Ihren Router und Domänennamen zu konfigurieren.

   Wenn Ihr Router das UPnP-Framework nicht unterstützt, oder wenn das UPnP-Framework deaktiviert ist, wird möglicherweise ein gelbes Warnsymbol neben dem Namen des Routers angezeigt. Stellen Sie sicher, dass folgende Ports geöffnet sind, und dass sie an die IP-Adresse des Zielservers weitergeleitet werden:

-   Port 80: HTTP-Webdatenverkehr

-   Port 443: HTTPS-Webdatenverkehr

> [!NOTE]
>  Wenn Sie einen öffentlichen Domänennamen auf dem Zielserver konfigurieren möchten, müssen Sie den Domänennamen vom Quellserver zur Vermeidung einer Störung durch das dynamische DNS-Update freigeben.

##  <a name="map-permitted-computers-to-user-accounts"></a><a name="BKMK_MapPermittedComputers"></a> Zuordnen zulässiger Computer zu Benutzerkonten
 Jedes Benutzerkonto, das von früheren Versionen von Windows Small Business Server oder Windows Server Essentials migriert wird, muss einem oder mehreren Computern zugeordnet werden.

#### <a name="to-map-user-accounts-to-computers"></a>So weisen Sie Benutzerkonten Computern zu

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

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
 Sie haben die Einstellungen und Daten auf den Zielserver verschoben. Gehen Sie jetzt zu [Schritt 5: Aktivieren der Ordner Umleitung auf dem Ziel Server für die Migration zu Windows Server Essentials](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md).


Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

