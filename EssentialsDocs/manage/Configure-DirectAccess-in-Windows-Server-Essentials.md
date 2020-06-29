---
title: Konfigurieren von DirectAccess in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: c959b6fc-c67e-46cd-a9cb-cee71a42fa4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a9ebd7af7f748a1e2af4a47ca5b590137cd33b3d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470905"
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>Konfigurieren von DirectAccess in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Thema enthält Schritt-für-Schritt-Anleitungen zum Konfigurieren von DirectAccess in Windows Server Essentials, damit Mobile Mitarbeiter nahtlos eine Verbindung mit dem Unternehmensnetzwerk von einem beliebigen Remote Standort mit Internet Verbindung herstellen können, ohne dass eine VPN-Verbindung (virtuelles privates Netzwerk) eingerichtet werden muss. DirectAccess bietet mobilen Mitarbeitern die gleichen Konnektivitätsprobleme innerhalb und außerhalb des Büros auf Ihren Windows 8.1-, Windows 8-und Windows 7-Computern.

 Wenn die Domäne in Windows Server Essentials mehr als einen Windows Server Essentials-Server enthält, muss DirectAccess auf dem Domänen Controller konfiguriert werden.

> [!NOTE]
>  Dieses Thema enthält Anweisungen zum Konfigurieren von DirectAccess, wenn der Windows Server Essentials-Server der Domänen Controller ist. Wenn der Windows Server Essentials-Server ein Domänen Mitglied ist, befolgen Sie stattdessen die Anweisungen zum Konfigurieren von DirectAccess auf einem Domänen Mitglied in [Hinzufügen von DirectAccess zu einer vorhandenen Remote Zugriffs Bereitstellung (VPN)](https://technet.microsoft.com/library/jj574220.aspx) .

## <a name="process-overview"></a>Übersicht über den Prozess
 Führen Sie die folgenden Schritte aus, um DirectAccess in Windows Server Essentials zu konfigurieren.

> [!IMPORTANT]
>  Bevor Sie die Verfahren in diesem Handbuch zum Konfigurieren von DirectAccess in Windows Server Essentials verwenden, müssen Sie das VPN auf dem Server aktivieren. Anweisungen hierzu finden Sie unter [Manage VPN](Manage-VPN-in-Windows-Server-Essentials.md).

-   [Schritt 1: Hinzufügen von %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot; zum Server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)

-   [Schritt 2: Ändern der Netzwerkadapteradresse des Servers zu einer statischen IP-Adresse](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)

-   [„Schritt 3: Vorbereiten eines Zertifikats und eines DNS-Eintrags für den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)

    -   [Schritt 3a: Erteilen von vollständigen Berechtigungen für authentifizierte Benutzer für die Zertifikat Vorlage des Webservers](#BKMK_GrantFullPermissions)

    -   [Schritt 3: Registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann](#BKMK_EnrollaCertificate)

    -   [Schritt 3C: Hinzufügen eines neuen Hosts auf dem DNS-Server und Zuordnen des Hosts zur Windows Server Essentials-Server Adresse](#BKMK_MapNewHosttoServerAddress)

-   [Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Clientcomputer](#BKMK_AddSecurityGroup)

-   [Schritt 5: Aktivieren und Konfigurieren von DirectAccess](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)

    -   [Schritt 5a: Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)

    -   [Schritt 5B: Entfernen des ungültigen IPv6Prefix im RRAS-Gruppenrichtlinien Objekt (nur Windows Server Essentials)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)

    -   [Schritt 5c: Aktivieren von Clientcomputern mit Windows 7 Enterprise für DirectAccess](#BKMK_Step4cWindows7Setup)

    -   [Schritt 5d: Konfigurieren des Netzwerkadressenservers](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)

    -   [Schritt 5e: Hinzufügen eines Registrierungsschlüssels zur Umgehung der CA-Zertifizierung beim Einrichten des IPsec-Kanals](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)

-   [Schritt 6: Konfigurieren der Richtlinientabelleneinträge für die Namensauflösung des DirectAccess-Servers](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)

-   [Schritt 7: Konfigurieren der TCP- und UDP-Firewallregeln für die Gruppenrichtlinienobjekte des DirectAccess-Servers](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)

-   [Schritt 8: Ändern der DNS64-Konfiguration zum Abhören der IP-HTTPS-Schnittstelle](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)

-   [Schritt 9: Reservieren von Ports für den WinNat-Dienst](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)

-   [Schritt 10: Neustarten des WinNat-Diensts](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)

> [!NOTE]
>  [Anhang: Einrichten von DirectAccess mithilfe von Windows PowerShell](#BKMK_AppendixBPowerShellScript) bietet ein Windows PowerShell-Skript, mit dem Sie das DirectAccess-Setup ausführen.

##  <a name="step-1-add-remote-access-management-tools-to-your-server"></a><a name="BKMK_AddRAM"></a>Schritt 1: Hinzufügen von Tools für die Remote Zugriffs Verwaltung zum Server

#### <a name="to-add-remote-accregss-management-tools--reg"></a>So fügen Sie Remoteverwaltungs Tools für Remote Dienste hinzu &reg;&reg;

1.  Klicken Sie auf dem Server in der unteren linken Ecke der Startseite auf das Symbol **Server-Manager**.

     In Windows Server Essentials müssen Sie nach Server-Manager suchen, um es zu öffnen. Geben Sie auf der Startseite **Server Manager** ein, und klicken Sie dann auf **Server-Manager** in den Suchergebnissen. Um den Server-Manager an die Startseite anzuheften, klicken Sie mit der rechten Maustaste auf den Server-Manager in den Suchergebnissen, und klicken Sie dann auf **An Startmenü anheften**.

2.  Wenn eine Warnmeldung zur **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**.

3.  Klicken Sie auf dem Server-Manager-Dashboard auf **Verwalten**, und klicken Sie dann auf **Rollen und Features hinzufügen**.

4.  Im Assistenten zum Hinzufügen von Rollen und Features gehen folgendermaßen Sie vor:

    1.  Klicken Sie auf der Seite **Installationstyp** auf **Rollenbasierte oder featurebasierte Installation**.

    2.  Klicken Sie auf der Seite **Server Auswahl** (oder auf der Seite **Ziel Server auswählen** in Windows Server Essentials) auf **einen Server aus dem Server Pool auswählen**.

    3.  Auf der Seite **Features** erweitern Sie **Remoteserver-Verwaltungstools (installiert)**, erweitern Sie **Tools für die Remotezugriffsverwaltung (installiert)**, erweitern Sie **Rollenverwaltungstools (installiert)**, erweitern Sie **Tools für die Remotezugriffsverwaltung**, und wählen Sie dann **Remotezugriffs-GUI und Befehlszeilentools**.

    4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

##  <a name="step-2-change-the-network-adapter-address-of-the-server-to-a-static-ip-address"></a><a name="BKMK_AddStaticIP"></a>Schritt 2: Ändern der Netzwerkadapter Adresse des Servers zu einer statischen IP-Adresse
 DirectAccess erfordert einen Adapter mit einer statischen IP-Adresse. Sie müssen die IP-Adresse für den lokalen Netzwerkadapter auf Ihrem Server ändern.

#### <a name="to-add-a-static-ip-address"></a>So fügen Sie eine statische IP-Adresse hinzu

1.  Öffnen Sie auf der Startseite **Systemsteuerung**.

2.  Klicken Sie auf **Netzwerk und Internet** und dann auf **Netzwerkstatus und -aufgaben anzeigen**.

3.  Klicken Sie im Aufgabenbereich des **Netzwerk- und Freigabecenters** auf **Adaptereinstellungen ändern**.

4.  Klicken Sie mit der rechten Maustaste auf den lokalen Netzwerkadapter, und klicken Sie dann auf **Eigenschaften**.

5.  Klicken Sie auf der Registerkarte **Netzwerk** auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.

6.  Klicken Sie auf der Registerkarte **Allgemein** auf **Folgende IP-Adresse verwenden**, und geben Sie dann die zu verwendende IP-Adresse ein.

     Im Feld **Subnetzmaske** wird automatisch ein Standardwert für die Subnetzmaske angezeigt. Übernehmen Sie entweder den Standardwert, oder geben Sie den gewünschten Subnetzmaskenwert ein.

7.  Geben Sie im Feld **Standardgateway** die IP-Adresse des Standardgateways ein.

8.  Geben Sie im Feld **Bevorzugter DNS-Server** die IP-Adresse des DNS-Servers ein.

    > [!NOTE]
    >  Verwenden Sie die IP-Adresse, die dem Netzwerkadapter von DHCP (z. B. 192.168.X.X) zugewiesen ist, anstatt eines Loopback-Netzwerks (z. B. 127.0.0.1). Um die zugewiesene IP-Adresse herauszufinden, führen Sie **ipconfig** an einer Eingabeaufforderung aus.

9. Geben Sie gegebenenfalls im Feld **Alternativer DNS-Server** die IP-Adresse des alternativen DNS-Servers ein.

10. Klicken Sie auf **OK** und dann auf **Schließen**.

> [!IMPORTANT]
>  Konfigurieren Sie unbedingt den Router für die Weiterleitung der Ports 80 und 443 an die neue statische IP-Adresse des Servers.

##  <a name="step-3-prepare-a-certificate-and-dns-record-for-the-network-location-server"></a><a name="BKMK_DNS"></a>Schritt 3: Vorbereiten eines Zertifikats und eines DNS-Einsatzes für den Netzwerkadressen Server
 Um ein Zertifikat und den DNS-Eintrag für den Netzwerkadressenserver vorzubereiten, führen Sie die folgenden Aufgaben aus:

-   [Schritt 3a: Erteilen von vollständigen Berechtigungen für authentifizierte Benutzer für die Zertifikat Vorlage des Webservers](#BKMK_GrantFullPermissions)

-   [Schritt 3: Registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann](#BKMK_EnrollaCertificate)

-   [Schritt 3c: Hinzufügen eines neuen Hosts auf dem DNS-Server und Zuordnen des Hosts zur Windows Server Essentials-Serveradresse](#BKMK_MapNewHosttoServerAddress)

###  <a name="step-3a-grant-full-permissions-to-authenticated-users-for-the-web-servers-certificate-template"></a><a name="BKMK_GrantFullPermissions"></a>Schritt 3a: Erteilen von vollständigen Berechtigungen für authentifizierte Benutzer für die Zertifikat Vorlage des Webservers
 Ihre erste Aufgabe besteht darin, die vollständigen Berechtigungen zum Authentifizieren von Benutzern für die Zertifikat Vorlage des Webservers in der Zertifizierungsstelle zu erteilen.

####  <a name="to-grant-full-permissions-to-authenticated-users-for-the-web-servers-certificate-template"></a><a name="BKMK_ToGrantFullPermissions"></a>So erteilen Sie authentifizierten Benutzern vollständige Berechtigungen für die Zertifikat Vorlage des Webservers

1.  Auf der Seite **Start** öffnen Sie **Zertifizierungsstelle**.

2.  Erweitern Sie in der Konsolen Struktur unter **Zertifizierungsstelle (lokal)** den **Eintrag<Servername \> -ca**, klicken Sie mit der rechten Maustaste auf **Zertifikat Vorlagen**, und klicken Sie dann auf **Verwalten**.

3.  In **Zertifizierungsstelle (lokal)** klicken Sie mit der rechten Maustaste auf **Webserver**, und klicken Sie dann auf **Eigenschaften**.

4.  In den Webservereigenschaften klicken Sie auf der Registerkarte **Sicherheit** auf **Authentifizierte Benutzer**, wählen Sie **Vollzugriff**, und klicken Sie dann auf **OK**.

5.  Starten Sie **Active Directory-Zertifikatdienste** neu. Öffnen Sie in der Systemsteuerung **Lokale Dienste anzeigen**. Klicken Sie in der Liste der Dienste mit der rechten Maustaste auf **Active Directory-Zertifikatdienste**, und klicken Sie dann auf **Neustarten**.

###  <a name="step-3b-enroll-a-certificate-for-the-network-location-server-with-a-common-name-that-is-unresolvable-from-the-external-network"></a><a name="BKMK_EnrollaCertificate"></a>Schritt 3B: Registrieren eines Zertifikats für den Netzwerkadressen Server mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann
 Anschließend registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann.

####  <a name="to-enroll-a-certificate-for-the-network-location-server"></a><a name="BKMK_ToEnrollaCertificate"></a>So registrieren Sie ein Zertifikat für den Netzwerkadressen Server

1.  Auf der Seite **Start** öffnen Sie **MMC** (Microsoft Management Console).

2.  Wenn eine Warnmeldung zur **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**.

     Die Microsoft Management Console (MMC) wird geöffnet.

3.  Im Menü **Datei** klicken Sie auf **Snap-Ins hinzufügen bzw. entfernen**.

4.  Im Feld **Snap-Ins hinzufügen bzw. entfernen** klicken Sie auf **Zertifikate**, und klicken Sie dann auf **Hinzufügen**.

5.  Klicken Sie auf der Seite **Zertifikat-Snap-In** auf **Computerkonto**, und klicken Sie dann auf **Weiter**.

6.  Klicken Sie auf der Seite **Computer auswählen** auf **Lokaler Computer**, auf **Fertig stellen** und dann auf **OK**.

7.  Erweitern Sie in der Konsolenstruktur **Zertifikate (Lokaler Computer)**, erweitern Sie **Persönlich**, klicken Sie mit der rechten Maustaste auf **Zertifikate**, und klicken Sie dann in **Alle Aufgaben** auf **Neues Zertifikat anfordern**.

8.  Wenn der Zertifikatregistrierungs-Assistent angezeigt wird, klicken Sie auf **Weiter**.

9. Auf der Seite **Zertifikatregistrierungsrichtlinie auswählen** klicken Sie auf **Weiter**.

10. Auf der Seite **Zertifikate anfordern** wählen Sie **Webserver**, und klicken Sie dann auf **Es werden zusätzliche Informationen für diese Zertifikatsregistrierung benötigt**.

11. Im Feld **Zertifikateigenschaften** geben Sie die folgenden Einstellungen für **Antragstellername** ein:

    1.  Für **Typ** wählen Sie **Allgemeiner Name**.

    2.  Für **Wert** geben Sie den Namen des Netzwerkadressenservers (z. B. DirectAccess-NLS.contoso.local) ein, und klicken Sie dann auf **Hinzufügen**.

    3.  Klicken Sie auf **OK**, und klicken Sie dann auf **Registrieren**.

12. Klicken Sie nach Abschluss der Zertifikatregistrierung auf **Fertig stellen**.

###  <a name="step-3c-add-a-new-host-on-the-dns-server-and-map-it-to-the-windows-server-essentials-server-address"></a><a name="BKMK_MapNewHosttoServerAddress"></a>Schritt 3C: Hinzufügen eines neuen Hosts auf dem DNS-Server und Zuordnen des Hosts zur Windows Server Essentials-Server Adresse
 Fügen Sie einen neuen Host auf dem DNS-Server hinzu, und ordnen Sie ihn der Windows Server Essentials-Server Adresse zu, um die DNS-Konfiguration abzuschließen.

####  <a name="to-map-a-new-host-to-the-windows-server-essentials-server-address"></a><a name="BKMK_ToMapNewHosttoServerAddress"></a>So ordnen Sie einen neuen Host der Windows Server Essentials-Server Adresse zu

1.  Öffnen Sie auf der Startseite den DNS-Manager. Suchen Sie zum Öffnen des DNS-Managers nach **dnsmgmt.msc**, und klicken Sie dann auf **dnsmgmt.msc** in den Ergebnissen.

2.  Erweitern Sie in der Konsolen Struktur des DNS-Managers den lokalen Server, erweitern Sie **Forward-Lookupzonen**, klicken Sie mit der rechten Maustaste auf die Zone mit dem Domänen Suffix des Servers, und klicken Sie dann auf **neuer Host (A oder AAAA)**.

3.  Geben Sie den Namen und die IP-Adresse des Servers (z. B. %%amp;quot;DirectAccess-NLS.contoso.local%%amp;quot;) und die entsprechende Serveradresse ein (z. B. 192.168.x.x).

4.  Klicken Sie auf **Host hinzufügen**, klicken Sie auf **OK**, und klicken Sie dann auf **Fertig**.

##  <a name="step-4-create-a-security-group-for-directaccess-client-computers"></a><a name="BKMK_AddSecurityGroup"></a>Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Client Computer
 Anschließend erstellen Sie eine Sicherheitsgruppe für DirectAccess-Clientcomputer, und fügen Sie dann die Computerkonten der Gruppe hinzu.

#### <a name="to-add-a-security-group-for-client-computers-that-use-directaccess"></a>So fügen Sie eine Sicherheitsgruppe für Clientcomputer hinzu, die DirectAccess verwenden

1. Klicken Sie auf dem Server-Manager-Dashboard auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.

   > [!NOTE]
   >  Wenn **Active Directory-Benutzer und -Computer** nicht im Menü **Tools** angezeigt wird, müssen Sie das Feature installieren. Um Active Directory-Benutzer und -Gruppen zu installieren, führen Sie das folgende Windows PowerShell-Cmdlet als Administrator aus: `Install-WindowsFeature RSAT-ADDS-Tools`. Weitere Informationen finden Sie unter [Installieren oder Entfernen der Remoteserver-Verwaltungstools](https://technet.microsoft.com/library/cc730825.aspx).

2. Erweitern Sie in der Konsolenstruktur den Server, klicken Sie mit der rechten Maustaste auf **Benutzer**, klicken Sie auf **Neu**, und klicken Sie dann auf **Gruppe**.

3. Geben Sie einen Gruppennamen, den Gruppenbereich und den Gruppentyp (Erstellen einer Sicherheitsgruppe) ein, und klicken Sie dann auf **OK**.

   Die neue Sicherheitsgruppe wird dem Ordner **Benutzer** hinzugefügt.

#### <a name="to-add-computer-accounts-to-the-security-group"></a>So fügen Sie Computerkonten zur Sicherheitsgruppe hinzu

1.  Klicken Sie auf dem Server-Manager-Dashboard auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.

2.  In der Konsolenstruktur, erweitern Sie den Server, und klicken Sie dann auf **Benutzer**.

3.  Klicken Sie in der Liste von Benutzerkonten und Sicherheitsgruppen auf dem Server mit der rechten Maustaste auf die Sicherheitsgruppe, die Sie für DirectAccess erstellt haben, und klicken Sie dann auf **Eigenschaften**.

4.  Klicken Sie auf der Registerkarte **Mitglieder** auf **Hinzufügen**.

5.  Geben Sie im Dialogfeld die Namen der Computerkonten, die Sie der Gruppe hinzufügen möchten, durch ein Semikolon (;) getrennt ein. Klicken Sie dann auf **Namen überprüfen**.

6.  Nachdem die Computerkonten überprüft wurden, klicken Sie auf **OK**. Klicken Sie dann erneut auf **OK**.

> [!NOTE]
>  Sie können auch die Registerkarte **Mitglied von** in den Eigenschaften des Computerkontos verwenden, um das Konto der Sicherheitsgruppe hinzuzufügen.

##  <a name="step-5-enable-and-configure-directaccess"></a><a name="BKMK_EnableConfigureDA"></a>Schritt 5: Aktivieren und Konfigurieren von DirectAccess
 Zum Aktivieren und Konfigurieren von DirectAccess in Windows Server Essentials müssen Sie die folgenden Schritte ausführen:

-   [Schritt 5a: Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)

-   [Schritt 5B: Entfernen des ungültigen IPv6Prefix im RRAS-Gruppenrichtlinien Objekt (nur Windows Server Essentials)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)

-   [Schritt 5c: Aktivieren von Clientcomputern mit Windows 7 Enterprise für DirectAccess](#BKMK_Step4cWindows7Setup)

-   [Schritt 5d: Konfigurieren des Netzwerkadressenservers](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)

-   [Schritt 5e: Hinzufügen eines Registrierungsschlüssels zur Umgehung der CA-Zertifizierung beim Einrichten des IPsec-Kanals](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)

###  <a name="step-5a-enable-directaccess-by-using-the-remote-access-management-console"></a><a name="BKMK_EnableDA"></a>Schritt 5a: Aktivieren von DirectAccess mithilfe der Remote Zugriffs-Verwaltungskonsole
 Dieser Abschnitt enthält Schritt-für-Schritt-Anleitungen zum Aktivieren von DirectAccess in Windows Server Essentials. Wenn Sie auf dem Server noch kein VPN konfiguriert haben, sollten Sie dies tun, bevor Sie mit diesem Vorgang beginnen. Anweisungen hierzu finden Sie unter [Manage VPN](Manage-VPN-in-Windows-Server-Essentials.md).

##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>So aktivieren Sie DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole

1.  Öffnen Sie auf der Startseite **Remotezugriffsverwaltung**.

2.  Führen Sie im Assistenten zum Aktivieren von DirectAccess folgende Schritte aus:

    1.  Überprüfen Sie **Voraussetzungen für DirectAccess**, und klicken Sie auf **Weiter**.

    2.  Auf der Registerkarte **Gruppen auswählen** fügen Sie die zuvor für DirectAccess-Clients erstellte Sicherheitsgruppe hinzu. (Wenn Sie die Sicherheitsgruppe nicht erstellt haben, finden Sie unter [Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Client Computer](#BKMK_AddSecurityGroup) Anweisungen.)

    3.  Wenn Sie den Remotezugriff auf den Server für mobile Computer über DirectAccess zulassen möchten, klicken Sie auf der Registerkarte **Gruppen auswählen** auf **DirectAccess ausschließlich für mobile Computer aktivieren** und anschließend auf **Weiter**.

    4.  Wählen Sie in **Netzwerktopologie** die Topologie des Servers aus, und klicken Sie dann auf **Weiter**.

    5.  Fügen Sie in **Suchliste für DNS-Suffix** ggf. das zusätzliche DNS-Suffix für die Clientcomputer hinzu, und klicken Sie dann auf **Weiter**.

        > [!NOTE]
        >  Standardmäßig fügt der Assistent zum Aktivieren von DirectAccess bereits das DNS-Suffix für die aktuelle Domäne hinzu. Sie können bei Bedarf jedoch weitere Domänen hinzufügen.

    6.  Überprüfen Sie die anzuwendenden Gruppenrichtlinienobjekte (Group Policy Objects, GPOs), und ändern Sie sie ggf.

    7.  Klicken Sie auf **Weiter**und dann auf **Fertig stellen**.

    8.  Führen Sie den folgenden Windows PowerShell-Befehl im Modus mit erhöhten Rechten aus, um den Remotezugriffsverwaltungs-Dienst neu zu starten:

        ```powershell
        Restart-Service RaMgmtSvc
        ```

###  <a name="step-5b-remove-the-invalid-ipv6prefix-in-rras-gpo-windows-server-essentials-only"></a><a name="BKMK_RemoveIPv6"></a>Schritt 5B: Entfernen des ungültigen IPv6Prefix im RRAS-Gruppenrichtlinien Objekt (nur Windows Server Essentials)
  Dieser Abschnitt gilt für einen Server, auf dem Windows Server Essentials ausgeführt wird.

 Öffnen Sie Windows PowerShell als Administrator, und führen Sie die folgenden Befehle aus:

```powershell
gpupdate
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix
gpupdate
```

###  <a name="step-5c-enable-client-computers-running-windows-7-enterprise-to-use-directaccess"></a><a name="BKMK_Step4cWindows7Setup"></a>Schritt 5C: Aktivieren von Client Computern mit Windows 7 Enterprise für die Verwendung von DirectAccess
 Wenn Sie über Client Computer verfügen, auf denen Windows 7 Enterprise ausgeführt wird, führen Sie das folgende Verfahren zum Aktivieren von DirectAccess von diesen Computern aus.

##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>So aktivieren Sie Windows 7 Enterprise-Computer für die Verwendung von DirectAccess

1.  Öffnen Sie auf der Start Seite des Servers die **Remote Zugriffs Verwaltung**.

2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**. Klicken Sie dann im Bereich **Einstellungsdetails** unter **Schritt 2** auf **Bearbeiten**.

     Der Setup-Assistent für Remotezugriffsserver wird geöffnet.

3.  Wählen Sie auf der Registerkarte **Authentifizierung** das Zertifizierungsstellen Zertifikat (ca) aus, das als vertrauenswürdiges Stamm Zertifikat verwendet werden soll (Sie können das Zertifizierungsstellen Zertifikat des Windows Server Essentials-Servers auswählen). Klicken Sie auf **Für Windows 7-Clientcomputer Verbindungen über DirectAccess zulassen**, und klicken Sie dann auf **Weiter**.

4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.

> [!IMPORTANT]
>  Es gibt ein bekanntes Problem für Windows 7 Enterprise-Computer, die eine Verbindung über DirectAccess herstellen, wenn auf dem Windows Server Essentials-Server nicht UR1 vorinstalliert ist. Um DirectAccess-Verbindungen in dieser Umgebung zu ermöglichen, müssen Sie die folgenden zusätzlichen Schritte ausführen:
>
> 1. Installieren Sie den im [Microsoft Knowledge Base-Artikel 2796394 (KB)](https://support.microsoft.com/kb/2796394) beschriebenen Hotfix auf dem Windows Server Essentials-Server. Starten Sie dann den Server neu.
>    2. Installieren Sie dann den im [Microsoft Knowledge Base-Artikel 2615847](https://support.microsoft.com/kb/2615847) beschriebenen Hotfix auf jedem Computer mit Windows 7.
>
>    Dieses Problem wurde in Windows Server Essentials gelöst.

###  <a name="step-5d-configure-the-network-location-server"></a><a name="BKMK_NLS"></a>Schritt 5d: Konfigurieren des Netzwerkadressen Servers
 Dieser Abschnitt enthält schrittweise Anweisungen zum Konfigurieren der Einstellungen des Netzwerkadressenservers.

> [!NOTE]
>  Bevor Sie beginnen, kopieren Sie den Inhalt des Ordners "<SystemDrive \> \inetpub\wwwroot" in den Ordner "<SystemDrive \> \Program Files\Windows server\bin\webapps\site\insideoutside". Kopieren Sie außerdem die Datei default. aspx aus dem Ordner <SystemDrive \> \Program Files\Windows server\bin\webapps\site in den Ordner <SystemDrive \> \Program Files\Windows server\bin\webapps\site\insideoutside.

##### <a name="to-configure-the-network-location-server"></a>So konfigurieren Sie den Netzwerkadressenserver

1.  Öffnen Sie auf der Startseite **Remotezugriffsverwaltung**.

2.  In der Remotezugriffs-Verwaltungskonsole klicken Sie auf **Konfiguration**, und klicken Sie im Detailbereich **Remotezugriff einrichten** im **Schritt 3** auf **Bearbeiten**.

3.  Im Setup-Assistenten für den Remotezugriffsserver auf der Registerkarte **Netzwerkadressenserver** wählen Sie **Der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt**, und wählen Sie dann das Zertifikat, das zuvor ausgegeben wurde (in [Step 3: Prepare a certificate and DNS record for the network location server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)).

4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen, und klicken Sie dann auf **Fertig stellen**.

###  <a name="step-5e-add-a-registry-key-to-bypass-ca-certification-when-you-establish-an-ipsec-channel"></a><a name="BKMK_CA"></a>Schritt 5E: Hinzufügen eines Registrierungsschlüssels zum Umgehen der Zertifizierungsstellen Zertifizierung beim Einrichten eines IPSec-Kanals
 Im nächsten Schritt konfigurieren Sie den Server, um die CA-Zertifizierung zu umgehen, wenn ein IPsec-Kanal eingerichtet wird.

##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>So fügen Sie einen Registrierungsschlüssel zum Umgehen der CA-Zertifizierung hinzu

1.  Öffnen Sie auf der Startseite **Regedit** (den Registrierungs-Editor).

2.  Erweitern Sie im Registrierungs-Editor **HKEY_LOCAL_MACHINE**, erweitern Sie **System**, erweitern Sie **CurrentControlSet**, erweitern Sie **Services**, und erweitern Sie **IKEEXT**.

3.  Klicken Sie unter **IKEEXT** mit der rechten Maustaste auf **Parameter**, klicken Sie auf **Neu**, und klicken Sie dann auf **DWORD-Wert (32 Bit)**.

4.  Geben Sie dem neu hinzugefügten Wert den Namen **ikeflags**.

5.  Doppelklicken Sie auf **Ikeflags**, geben Sie als **Typ** die Option **Hexadezimal** an, legen Sie als Wert **8000** fest, und klicken Sie dann auf **OK**.

> [!NOTE]
>  Den folgenden Windows PowerShell-Befehl können Sie im erweiterten Modus verwenden, um diesen Registrierungsschlüssel hinzuzufügen:
>
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`

##  <a name="step-6-configure-name-resolution-policy-table-settings-for-the-directaccess-server"></a><a name="BKMK_NRPT"></a>Schritt 6: Konfigurieren der Einstellungen für die Richtlinien Tabelle für die Namensauflösung für den DirectAccess-Server
 Dieser Abschnitt enthält Anweisungen zum Bearbeiten der Namensauflösungseinträge in der Richtlinientabelle für interne Adressen (z. B. Einträge mit dem Suffix "contoso.local") für DirectAccess-Client-Gruppenrichtlinienobjekte und zum Einrichten der IPHTTPS-Schnittstellenadresse.

#### <a name="to-configure-name-resolution-policy-table-entries"></a>So konfigurieren Sie Richtlinientabelleneinträge für die Namensauflösung

1.  Öffnen Sie auf der Startseite **Gruppenrichtlinienverwaltung**.

2.  Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole auf die standardmäßige Gesamtstruktur und Domäne, klicken Sie mit der rechten Maustaste auf **DirectAccess-Clienteinstellungen**, und klicken Sie dann auf **Bearbeiten**.

3.  Klicken Sie auf **Computerkonfigurationen**, klicken Sie auf **Richtlinien**, klicken Sie auf **Windows-Einstellungen**, und klicken Sie dann auf **Namensauflösungsrichtlinie**. Wählen Sie den Eintrag, bei dem der Namespace mit Ihrem DNS-Suffix übereinstimmt, und klicken Sie dann auf **Regel bearbeiten**.

4.  Klicken Sie auf die Registerkarte **DNS-Einstellungen für DirectAccess**, und wählen Sie dann **DNS-Einstellungen für DirectAccess in dieser Regel aktivieren**. Fügen Sie der DNS-Serverliste die IPv6-Adresse für die IP-HTTPS-Schnittstelle hinzu.

    > [!NOTE]
    >  Mit dem folgenden Windows PowerShell-Befehl können Sie die IPv6-Adresse abrufen:
    >
    >  `(Get-NetIPInterface -InterfaceAlias IPHTTPSInterface | Get-NetIPAddress -PrefixLength 128)[1].IPAddress`

##  <a name="step-7-configure-tcp-and-udp-firewall-rules-for-the-directaccess-server-gpos"></a><a name="BKMK_TCPUDP"></a>Schritt 7: Konfigurieren von TCP-und UDP-Firewallregeln für die DirectAccess-Server-Gruppenrichtlinien Objekte
 Dieser Abschnitt enthält schrittweise Anweisungen zum Konfigurieren der TCP- und UDP-Firewallregeln für die Gruppenrichtlinienobjekte des DirectAccess-Servers.

#### <a name="to-configure-firewall-rules"></a>So konfigurieren Sie Firewallregeln

1.  Öffnen Sie auf der Startseite **Gruppenrichtlinienverwaltung**.

2.  Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole auf die standardmäßige Gesamtstruktur und Domäne, klicken Sie mit der rechten Maustaste auf **DirectAccess-Servereinstellungen**, und klicken Sie dann auf **Bearbeiten**.

3.  Klicken Sie auf **Computerkonfiguration**, klicken Sie auf **Richtlinien**, klicken Sie auf **Windows-Einstellungen**, klicken Sie auf **Sicherheitseinstellungen**, klicken Sie auf **Windows-Firewall mit erweiterter Sicherheit**, klicken Sie auf die nächste Ebene **Windows-Firewall mit erweiterter Sicherheit**, und klicken Sie dann auf **Eingehende Regeln**. Klicken Sie mit der rechten Maustaste auf **Domänennamenserver (TCP eingehend)**, und klicken Sie dann auf **Eigenschaften**.

4.  Klicken Sie auf die Registerkarte **Bereich**, und fügen Sie in der Liste **Lokale IP-Adresse** die IPv6-Adresse der IP-HTTPS-Schnittstelle hinzu.

5.  Wiederholen Sie dieses Verfahren für **Domänennamenserver (UDP eingehend)**.

##  <a name="step-8-change-the-dns64-configuration-to-listen-to-the-ip-https-interface"></a><a name="BKMK_DNS64"></a>Schritt 8: Ändern der DNS64-Konfiguration zum lauschen an der IP-HTTPS-Schnittstelle
 Sie müssen die DNS64-Konfiguration mithilfe des folgenden Windows PowerShell so ändern, dass die IP-HTTPS-Schnittstelle abgehört wird:

```powershell
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface
```

##  <a name="step-9-reserve-ports-for-the-winnat-service"></a><a name="BKMK_ExemptPort"></a>Schritt 9: Reservieren von Ports für den winnat-Dienst
 Verwenden Sie den folgenden Windows PowerShell-Befehl, um Ports für des WinNat-Diensts zu reservieren. Ersetzen Sie "192.168.1.100" durch die tatsächliche IPv4-Adresse Ihres Windows Server Essentials-Servers.

```powershell
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")
```

> [!IMPORTANT]
>  Um Portkonflikte mit Anwendungen zu vermeiden, stellen sicher, dass der für den WinNat-Dienst reservierte Portbereich nicht Port 6602 enthält.

##  <a name="step-10-restart-the-winnat-service"></a><a name="BKMK_WinNAT"></a>Schritt 10: Neustarten des winnat-dienstanweises
 Mit dem folgenden Windows PowerShell-Befehl starten Sie den Windows-NAT-Treiberdienst (WinNat)-Dienst neu.

```powershell
Restart-Service winnat
```

##  <a name="appendix-set-up-directaccess-by-using-windows-powershell"></a><a name="BKMK_AppendixBPowerShellScript"></a>Anhang: Einrichten von DirectAccess mithilfe von Windows PowerShell
 In diesem Abschnitt wird das Einrichten und Konfigurieren von DirectAccess mithilfe von Windows PowerShell beschrieben.

### <a name="preparation"></a>Vorbereitung
 Bevor Sie mit der Konfiguration des Servers für DirectAccess beginnen, müssen Sie folgende Schritte ausführen:

1.  Befolgen Sie das Verfahren in [Schritt 3: Vorbereiten eines Zertifikats und eines DNS-Einsatzes für den Netzwerkadressen Server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS) , um ein Zertifikat mit dem Namen **DirectAccess-nls.contoso.com** zu registrieren (wobei **contoso.com** durch den tatsächlichen internen Domänen Namen ersetzt wird) und einen DNS-Datensatz für den Netzwerkadressen Server (Network Location Server, NLS) hinzuzufügen.

2.  Fügen Sie in Active Directory eine Sicherheitsgruppe mit dem Namen **DirectAccessClients** hinzu, und fügen Sie dann Clientcomputer hinzu, auf denen Sie die DirectAccess-Funktionen bereitstellen möchten. Weitere Informationen finden Sie unter [Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Client Computer](#BKMK_AddSecurityGroup).

### <a name="commands"></a>Befehle

> [!IMPORTANT]
>  In Windows Server Essentials müssen Sie das unnötige IPv6-Präfix-Gruppenrichtlinien Objekt nicht entfernen. Löschen Sie den Codeabschnitt mit der folgenden Beschriftung: `# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`.

```powershell
# Add Remote Access role if not installed yet
$ra = Get-WindowsFeature RemoteAccess
If ($ra.Installed -eq $FALSE) { Add-WindowsFeature RemoteAccess }

# Server may need to restart if you installed RemoteAccess role in the above step

# Set the internet domain name to access server, replace contoso.com below with your own domain name
$InternetDomain = "www.contoso.com"
#Set the SG name which you create for DA clients
$DaSecurityGroup = "DirectAccessClients"
#Set the internal domain name
$InternalDomain = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().Name

# Set static IP and DNS settings
$NetConfig = Get-WmiObject Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true"
$CurrentIP = $NetConfig.IPAddress[0]
$SubnetMask = $NetConfig.IPSubnet | Where-Object{$_ -like "*.*.*.*"}
$NetConfig.EnableStatic($CurrentIP, $SubnetMask)
$NetConfig.SetGateways($NetConfig.DefaultIPGateway)
$NetConfig.SetDNSServerSearchOrder($CurrentIP)

# Get physical adapter name and the certificate for NLS server
$Adapter = (Get-WmiObject -Class Win32_NetworkAdapter -Filter "NetEnabled=$true").NetConnectionId
$Certs = dir cert:\LocalMachine\My
$nlscert = $certs | Where-Object{$_.Subject -like "*CN=DirectAccess-NLS*"}

# Add regkey to bypass CA cert for IPsec authentication
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000

# Install DirectAccess.
Install-RemoteAccess -NoPrerequisite -DAInstallType FullInstall -InternetInterface $Adapter -InternalInterface $Adapter -ConnectToAddress $InternetDomain -nlscertificate $nlscert -force

#Restart Remote Access Management service
Restart-Service RaMgmtSvc

# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO

gpupdate
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix
gpupdate

# Enable client computers running Windows 7 to use DirectAccess
$allcertsinroot = dir cert:\LocalMachine\root
$rootcert = $allcertsinroot | Where-Object{$_.Subject -like "*-CAA*"}
Set-DAServer -IPSecRootCertificate $rootcert[0]
Set -DAClient -OnlyRemoteComputers Disabled -Downlevel Enabled

#Set the appropriate security group used for DA client computers. Replace the group name below with the one you created for DA clients
Add-DAClient -SecurityGroupNameList $DaSecurityGroup
Remove-DAClient -SecurityGroupNameList "Domain Computers"

# Gather DNS64 IP address information
$Remoteaccess = get-remoteaccess
$IPinterface = get-netipinterface -InterfaceAlias IPHTTPSInterface | get-netipaddress -PrefixLength 128
$DNS64IP=$IPInterface[1].IPaddress
$Natconfig = Get-NetNatTransitionConfiguration

# Configure TCP and UDP firewall rules for the DirectAccess server GPO
$GpoName = 'GPO:'+$InternalDomain+'\DirectAccess Server Settings'
Get-NetFirewallRule -PolicyStore $GpoName -Displayname "Domain Name Server (TCP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP
Get-NetFirewallrule -PolicyStore $GpoName -Displayname "Domain Name Server (UDP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP

# Configure the name resolution policy settings for the DirectAccess server, replace the DNS suffix below with the one in your domain
$Suffix = '.' + $InternalDomain
set-daclientdnsconfiguration -DNSsuffix $Suffix -DNSIPAddress $DNS64IP

# Change the DNS64 configuration to listen to IP-HTTPS interface
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface

# Copy the necessary files to NLS site folder
XCOPY 'C:\inetpub\wwwroot' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /E /Y
XCOPY 'C:\Program Files\Windows Server\Bin\WebApps\Site\Default.aspx' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /Y

# Reserve ports for the WinNat service
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")

# Restart the WinNat service
Restart-Service winnat
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Verwalten von %%amp;quot;Zugriff überall%%amp;quot;](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
