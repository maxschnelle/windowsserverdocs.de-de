---
title: Verschieben von Windows Server 2008 Foundation-Einstellungen und Daten auf den Zielserver für die Migration zu Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 3ff7d040-ebd1-421c-80db-765deacedd4c
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: c2426e535ff67b1e76668e5fd2abefbd3f5569bb
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625665"
---
# <a name="move-windows-server-2008-foundation-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Verschieben von Windows Server 2008 Foundation-Einstellungen und Daten auf den Zielserver für die Migration zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Verschieben von Einstellungen und Daten auf den Zielserver:

1. [Kopieren von Daten auf den Zielserver (optional)](#copy-data-to-the-destination-server)

2. [Importieren von Active Directory Benutzerkonten in das Windows Server Essentials-Dashboard (optional)](#import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard)

3. [Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den Router.](#move-the-dhcp-server-role-from-the-source-server-to-the-router)

4. [Netzwerk konfigurieren](#configure-the-network)

5. [Zuordnen zugelassener Computer zu Benutzerkonten](#map-permitted-computers-to-user-accounts)

## <a name="copy-data-to-the-destination-server"></a>Kopieren von Daten auf den Zielserver.
 Führen Sie die folgenden Aufgaben aus, bevor Sie Daten vom Quellserver zum Zielserver kopieren:

- Prüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie die Ordner auf dem Zielserver so bzw. passen Sie diese so an, dass sie der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren.

- Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.

- Machen Sie die freigegebenen Ordner auf dem Quellserver für alle Benutzer schreibgeschützt, damit auf das Laufwerk nicht geschrieben werden kann, während Sie Dateien auf den Zielserver kopieren.

#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver.

1.  Melden Sie sich beim Zielserver als Domänenadministrator an, und öffnen Sie ein Eingabeaufforderungsfenster.

2.  Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`

     Hierbei gilt:
     - \<SourceServerName\> ist der Name des Quellservers
     - \<SharedSourceFolderName\> ist der Name des freigegebenen Ordners auf dem Quellserver
     - \<DestinationServerName\> ist der Name des Zielservers.
     - \<SharedDestinationFolderName\> der freigegebene Ordner auf dem Ziel Server, in den die Daten kopiert werden.

3.  Wiederholen Sie den vorherigen Schritt für jeden freigegebenen Ordner, zu dem Sie die Migration vom Quellserver aus vornehmen.

## <a name="import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard"></a>Importieren von Active Directory Benutzerkonten in das Windows Server Essentials-Dashboard
 Standardmäßig werden alle auf dem Quell Server erstellten Benutzerkonten automatisch auf das Dashboard in Windows Server Essentials migriert. Die automatische Migration eines Active Directory-Benutzerkontos schlägt jedoch fehl, wenn nicht alle Eigenschaften die Migrationsanforderungen erfüllen. Sie können das folgende Windows PowerShell-Cmdlet verwenden, um Active Directory-Benutzer zu importieren.

#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>So importieren Sie ein Active Directory Benutzerkonto in das Windows Server Essentials-Dashboard

1.  Melden Sie sich auf den Zielserver als Domänenadministrator an.

2.  Öffnen Sie Windows PowerShell als Administrator.

3.  Führen Sie das folgende Cmdlet aus, wobei `[AD username]` für den Namen des Active Directory-Benutzerkontos steht, das Sie importieren möchten:

     `Import-WssUser  SamAccountName [AD username]`

## <a name="move-the-dhcp-server-role-from-the-source-server-to-the-router"></a>Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den Router.
 Wenn Ihr Quellserver in der DHCP-Rolle ausgeführt wird, führen Sie die folgenden Schritte aus, um die DHCP-Rolle auf den Router zu verschieben.

#### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>Verschieben der DHCP-Serverrolle vom Quellserver auf den Router.

1.  Deaktivieren Sie wie folgt den DHCP-Dienst auf dem Quellserver:

    1.  Klicken Sie auf dem Quellserver auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Dienste**.

    2.  Klicken Sie in der Liste der zurzeit ausgeführten Dienste mit der rechten Maustaste auf **DHCP-Server**, und klicken Sie dann auf **Eigenschaften**.

    3.  Wählen Sie für **Starttyp** die Option **deaktiviert**.

    4.  Beenden Sie den Dienst.

2.  Aktivieren Sie die DHCP-Rolle auf dem Router.

    1.  Befolgen Sie die Anweisungen in Ihrer Router-Dokumentation, um die DHCP-Serverrolle auf dem Router zu aktivieren.

    2.  Befolgen Sie, um sicherzustellen, dass die vom Quellserver ausgestellten IP-Adressen unverändert bleiben, die Anweisungen in der Routerdokumentation, um den DHCP-Bereich auf den Router so zu konfigurieren, dass er mit dem DHCP-Bereich auf dem Quellserver identisch ist.

        > [!IMPORTANT]
        >  Wenn Sie keine statische IP oder DHCP-Reservierungen auf dem Router für den Zielserver eingerichtet haben, und der DHCP-Bereich nicht identisch mit dem Quellserver ist, ist es möglich, dass der Router eine neue IP-Adresse für den Zielserver ausstellt. Setzen Sie in diesem Fall die Portweiterleitungsregeln des Routers zum Weiterleiten auf die neue IP-Adresse des Zielservers zurück.

## <a name="configure-the-network"></a>Konfigurieren des Netzwerks
 Nachdem Sie die DHCP-Rolle zum Router verschoben haben, konfigurieren Sie die Netzwerkeinstellungen auf dem Zielserver.

#### <a name="to-configure-the-network"></a>So konfigurieren Sie das Netzwerk

1. Öffnen Sie auf dem Zielserver das Dashboard.

2. Klicken Sie auf dem Dashboard **Home** auf **Setup**, klicken Sie auf **"Zugriff überall" einrichten**, und wählen Sie dann die Option **Zum Konfigurieren von "Zugriff überall" klicken** aus.

3. Vervollständigen Sie die Anweisungen im Assistenten, um Ihren Router und Domänennamen zu konfigurieren.

   Wenn Ihr Router das UPnP-Framework nicht unterstützt, oder wenn das UPnP-Framework deaktiviert ist, wird möglicherweise ein gelbes Warnsymbol neben dem Namen des Routers angezeigt. Stellen Sie sicher, dass folgende Ports geöffnet sind, und dass sie an die IP-Adresse des Zielservers weitergeleitet werden:

-   Port 80: HTTP-Webdatenverkehr

-   Port 443: HTTPS-Webdatenverkehr

## <a name="map-permitted-computers-to-user-accounts"></a>Zuordnen zugelassener Computer zu Benutzerkonten
 In Windows Server Essentials muss ein Benutzer explizit einem Computer zugewiesen werden, damit er in Remote Webzugriff angezeigt wird. Jedes Benutzerkonto, das von Windows Server 2008 Foundation migriert wird, muss einem oder mehreren Computern zugeordnet werden.

#### <a name="to-map-user-accounts-to-computers"></a>So weisen Sie Benutzerkonten Computern zu

1.  Öffnen Sie das Windows Server Essentials-Dashboard.

2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3.  Klicken Sie in der Liste von Benutzerkonten mit der rechten Maustaste auf ein Benutzerkonto, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.

4.  Klicken Sie auf der Registerkarte **Zugriff überall** auf **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**.

5.  Wählen Sie **Freigegebene Ordner**, **Computers** und **Links auf der Startseite** aus, und klicken Sie dann auf **Übernehmen**.

6.  Klicken Sie auf der Registerkarte **Computerzugriff** auf den Namen des Computers, für den Sie Zugriff gewähren möchten.

7.  Wiederholen Sie die Schritte 3, 4, 5 und 6 für jedes Benutzerkonto.

> [!NOTE]
> Die Konfiguration des Clientcomputers braucht nicht geändert zu werden. Er wird automatisch konfiguriert.
>
> Wenn nach abgeschlossener Migration ein Problem beim Erstellen des ersten neuen Benutzerkontos auf dem Zielserver auftritt, entfernen Sie das Benutzerkonto, das Sie hinzugefügt haben, und erstellen Sie es erneut.
