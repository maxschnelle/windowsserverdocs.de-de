---
title: Verschieben von Windows SBS 2003-Einstellungen und -Daten auf den Zielserver für die Migration zu Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 67087ccb-d820-4642-8ca2-7d2d38714014
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 427f695b36f7a062bdc570ba816560a6a1721b90
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180586"
---
# <a name="move-windows-sbs-2003-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Verschieben von Windows SBS 2003-Einstellungen und -Daten auf den Zielserver für die Migration zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Verschieben von Einstellungen und Daten auf den Zielserver:

1. [Kopieren von Daten auf den Zielserver.](#copy-data-to-the-destination-server)

2. [Importieren von Active Directory Benutzerkonten in das Windows Server Essentials-Dashboard (optional)](#import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard)

3. [Entfernen alter Anmeldeskripts (optional)](#remove-old-logon-scripts)

4. [Entfernen von älteren Active Directory-Gruppenrichtlinienobjekten (optional)](#remove-legacy-active-directory-group-policy-objects)

5. [Konfigurieren des Netzwerks](#configure-the-network)

6. [Zuordnen zugelassener Computer zu Benutzerkonten](#map-permitted-computers-to-user-accounts)

## <a name="copy-data-to-the-destination-server"></a>Kopieren von Daten auf den Zielserver.
Führen Sie die folgenden Aufgaben aus, bevor Sie Daten vom Quellserver zum Zielserver kopieren:

- Prüfen Sie die Liste der freigegebenen Ordner auf dem Quellserver, einschließlich der Berechtigungen für jeden Ordner. Erstellen Sie die Ordner auf dem Zielserver so bzw. passen Sie diese so an, dass sie der Ordnerstruktur entsprechen, die Sie vom Quellserver migrieren.

- Überprüfen Sie die Größe der einzelnen Ordner, und stellen Sie sicher, dass der Zielserver ausreichend Speicherplatz aufweist.

- Machen Sie die freigegebenen Ordner auf dem Quellserver für alle Benutzer schreibgeschützt, damit auf das Laufwerk nicht geschrieben werden kann, während Sie Dateien auf den Zielserver kopieren.

#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>Kopieren von Daten vom Quellserver auf den Zielserver.

1. Melden Sie sich auf den Zielserver als Domänenadministrator an.

2. Klicken Sie auf **Start**, geben Sie **cmd** in das Suchfeld ein, und drücken Sie dann die EINGABETASTE.

3. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`

Hierbei gilt Folgendes:
 - \<SourceServerName\> ist der Name des Quellservers
 - \<SharedSourceFolderName\> ist der Name des freigegebenen Ordners auf dem Quellserver
 - \<DestinationServerName\>ist der Name des Zielservers.
 - \<SharedDestinationFolderName\>der freigegebene Ordner auf dem Ziel Server, in den die Daten kopiert werden.

4. Wiederholen Sie den vorherigen Schritt für jeden freigegebenen Ordner, zu dem Sie die Migration vom Quellserver aus vornehmen.

## <a name="import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard"></a>Importieren von Active Directory Benutzerkonten in das Windows Server Essentials-Dashboard
 Standardmäßig werden alle auf dem Quell Server erstellten Benutzerkonten automatisch auf das Dashboard in Windows Server Essentials migriert. Die automatische Migration eines Active Directory-Benutzerkontos schlägt jedoch fehl, wenn einige Eigenschaften den Migrationsanforderungen nicht entsprechen. Sie können das folgende Windows PowerShell-Cmdlet verwenden, um Active Directory-Benutzer zu importieren.

#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>So importieren Sie ein Active Directory Benutzerkonto in das Windows Server Essentials-Dashboard

1. Melden Sie sich auf den Zielserver als Domänenadministrator an.

2. Öffnen Sie Windows PowerShell als Administrator.

3. Führen Sie das folgende Cmdlet aus, wobei `[AD username]` für den Namen des Active Directory-Benutzerkontos steht, das Sie importieren möchten:

    `Import-WssUser SamAccountName [AD username]`

## <a name="remove-old-logon-scripts"></a>Alte Anmelde Skripts entfernen
Windows SBS 2003 verwendet Anmeldeskripts für Aufgaben wie das Installieren von Software und das Anpassen von Desktops. Windows Server Essentials ersetzt die Windows SSB 2003-Anmelde Skripts durch eine Kombination aus Anmelde Skripts und Gruppenrichtlinie Objekten.

> [!NOTE]
> Wenn Sie die Windows SBS 2003-Anmeldeskripts geändert haben, sollten Sie die Skripts umbenennen, um Ihre Anpassungen beizubehalten.
>
> Windows SBS 2003-Anmeldeskripts gelten nur für Benutzerkonten, die mithilfe des **Assistent zum Hinzufügen neuer Benutzer**hinzugefügt wurden.

#### <a name="to-remove-the-windows-sbs-2003-logon-scripts"></a>So entfernen Sie die Windows SBS 2003-Anmeldeskripts

1. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.

2. Erweitern Sie in **Active Directory-Benutzer und -Computer** Ihr Netzwerk, und klicken Sie dann auf **Benutzer**.

3. Klicken Sie mit der rechten Maustaste auf einen Benutzernamen, klicken Sie auf **Eigenschaften** und dann auf die Registerkarte **Profil**.

4. Löschen Sie die Inhalte des Textfelds **Anmeldeskript**, und klicken Sie dann auf **OK**.

5. Wiederholen Sie die Schritte 3 und 4 für jeden Benutzer.

## <a name="remove-legacy-active-directory-group-policy-objects"></a>Entfernen von Legacy-Active Directory Gruppenrichtlinie Objekten
Die Gruppenrichtlinie Objekte (GPOs) werden für Windows Server Essentials aktualisiert. Sie sind eine Untergruppe der Windows SBS 2003-Gruppenrichtlinienobjekte. Für Windows Server Essentials müssen eine Reihe von Windows SSB 2003-GPOs und-Windows-Verwaltungsinstrumentation-Filtern (WMI) manuell gelöscht werden, um Konflikte mit den Windows Server Essentials-Gruppenrichtlinien Objekten und WMI-Filtern zu verhindern.

> [!NOTE]
> Wenn Sie die ursprünglichen Windows SBS 2003-Gruppenrichtlinienobjekte geändert haben, sollten Sie Kopien davon an einem anderen Speicherort speichern und sie dann aus Windows SBS 2003 entfernen.

#### <a name="to-remove-old-group-policy-objects-from-windows-sbs-2003"></a>So entfernen Sie alte Gruppenrichtlinienobjekte aus Windows SBS 2003

1. Melden Sie sich beim Quellserver mit einem Administratorkonto an.

2. Klicken Sie auf **Start** und anschließend auf **Serververwaltung**.

3. Klicken Sie im Navigationsbereich auf **Erweiterte Verwaltung**, klicken Sie auf **Gruppenrichtlinie Verwaltung**, und klicken Sie dann auf Gesamtstruktur **:** _<yourDomainName \> _.

4. Klicken Sie auf **Domänen**, klicken Sie auf *<\> yourDomainName*, und klicken Sie dann auf **Gruppenrichtlinie Objekte**.

5. Klicken Sie mit der rechten Maustaste auf **Small Business Server Auditing Policy**, klicken Sie auf **Löschen** und dann auf **OK**.

6. Wiederholen Sie Schritt 5, um die folgenden Gruppenrichtlinienobjekte zu löschen, die für Ihr Netzwerk gelten:

 - Small Business Server-Clientcomputer

 - Small Business Server-Domänenkennwortrichtlinie

Es wird empfohlen, die Kenn Wort Richtlinie in Windows Server Essentials zu konfigurieren, um sichere Kenn Wörter zu erzwingen. Um die Kennwortrichtlinie zu konfigurieren, verwenden Sie das Dashboard, das die Konfiguration in die Standarddomänenrichtlinie schreibt. Die Konfiguration der Kennwortrichtlinie wird nicht in das Small Business Server Domain Password-Richtlinienobjekt geschrieben, wie es in Windows SBS 2003 der Fall war.

 - Small Business Server-Internetverbindungsfirewall

 - Small Business Server-Kontosperrungsrichtlinie

 - Small Business Server-Remoteunterstützungsrichtlinie

 - Small Business Server-Windows-Firewall

 - Small Business Server Update Services-Clientcomputerrichtlinie

 Dieses Gruppenrichtlinienobjekt ist vorhanden, wenn Sie von Windows SBS 2003 R2 migrieren.

 - Small Business Server Update Services Common Settings Policy

 Dieses Gruppenrichtlinienobjekt ist vorhanden, wenn Sie von Windows SBS 2003 R2 migrieren.

 - Small Business Server Update Services-Servercomputerrichtlinie

 Dieses Gruppenrichtlinienobjekt ist vorhanden, wenn Sie von Windows SBS 2003 R2 migrieren.

7. Stellen Sie sicher, dass alle Gruppenrichtlinienobjekte gelöscht werden.

#### <a name="to-remove-wmi-filters-from-windows-sbs-2003"></a>So entfernen Sie WMI-Filter aus Windows SBS 2003

1. Melden Sie sich beim Quellserver mit einem Administratorkonto an.

2. Klicken Sie auf **Start** und anschließend auf **Serververwaltung**.

3. Klicken Sie im Navigationsbereich auf **Erweiterte Verwaltung**, klicken Sie auf **Gruppenrichtlinie Verwaltung**, und klicken Sie dann auf Gesamtstruktur **:** _<yournetworkdomainname \> _

4. Klicken Sie auf **Domänen**, klicken Sie auf *<yournetworkdomainname \> *, und klicken Sie dann auf **WMI-Filter**.

5. Klicken Sie mit der rechten Maustaste auf **PostSP2**, klicken Sie auf **Löschen** und dann auf **Ja**.

6. Klicken Sie mit der rechten Maustaste auf **PreSP2**, klicken Sie auf **Löschen** und dann auf **Ja**.

7. Stellen Sie sicher, dass diese drei WMI-Filter gelöscht werden.

## <a name="configure-the-network"></a>Konfigurieren des Netzwerks

#### <a name="to-configure-the-network"></a>So konfigurieren Sie das Netzwerk

1. Öffnen Sie auf dem Zielserver das Dashboard.

2. Klicken Sie auf dem Dashboard **Home** auf **Setup**, klicken Sie auf **"Zugriff überall" einrichten**, und wählen Sie dann die Option **Zum Konfigurieren von "Zugriff überall" klicken** aus.

3. Folgen Sie den Anweisungen im **"Zugriff überall" einrichten**-Assistenten zum Konfigurieren von Router und Domänenname.

 Wenn Ihr Router das UPnP-Framework nicht unterstützt, oder wenn das UPnP-Framework deaktiviert ist, wird möglicherweise ein gelbes Warnsymbol neben dem Namen des Routers angezeigt. Stellen Sie sicher, dass folgende Ports geöffnet sind, und dass sie an die IP-Adresse des Zielservers weitergeleitet werden:

- Port 80: HTTP-Webdatenverkehr

- Port 443: HTTPS-Webdatenverkehr

> [!NOTE]
> Wenn Sie einen lokalen Exchange-Server auf einem zweiten Server eingerichtet haben, müssen Sie sicherstellen, dass auch Port 25 (SMTP) geöffnet ist und an die IP-Adresse des lokalen Exchange-Server umgeleitet wird.

## <a name="map-permitted-computers-to-user-accounts"></a>Zuordnen zugelassener Computer zu Benutzerkonten
 Wenn ein Benutzer in Windows SBS 2003 eine Verbindung mit Remote Web Access herstellt, werden alle Computer im Netzwerk angezeigt. Dies kann Computer umfassen, für die der Benutzer keine Zugriffsberechtigung hat. In Windows Server Essentials muss ein Benutzer explizit einem Computer zugewiesen werden, damit er in Remote Webzugriff angezeigt wird. Jedes Benutzerkonto, das von Windows SBS 2003 migriert werden, muss mindestens einem Computer zugeordnet werden.

#### <a name="to-map-user-accounts-to-computers"></a>So weisen Sie Benutzerkonten Computern zu

1. Öffnen Sie auf dem Ziel Server das Windows Server Essentials-Dashboard.

2. Klicken Sie auf der Navigationsleiste auf **Benutzer**.

3. Klicken Sie in der Liste von Benutzerkonten mit der rechten Maustaste auf ein Benutzerkonto, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.

4. Klicken Sie auf die Registerkarte **Zugriff überall**, und klicken Sie dann auf **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**.

5. Klicken Sie auf **Freigegebene Ordner**, klicken Sie auf **Computer**, klicken Sie auf **Homepagelinks**, und klicken Sie dann auf **Übernehmen**.

6. Klicken Sie auf die Registerkarte **Computerzugriff**, und klicken Sie auf den Namen des Computers, für den Sie den Zugriff zulassen möchten.

7. Wiederholen Sie die Schritte 3, 4, 5 und 6 für jedes Benutzerkonto.

> [!NOTE]
> Die Konfiguration des Clientcomputers braucht nicht geändert zu werden. Er wird automatisch konfiguriert.
>
> Wenn nach abgeschlossener Migration ein Problem beim Erstellen des ersten neuen Benutzerkontos auf dem Zielserver auftritt, entfernen Sie das Benutzerkonto, das Sie hinzugefügt haben, und erstellen Sie es erneut.
