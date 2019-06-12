---
title: Konfigurieren von DirectAccess in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c959b6fc-c67e-46cd-a9cb-cee71a42fa4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 2081473500a08776a1dc81a4fa443696b6fde0d6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433467"
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>Konfigurieren von DirectAccess in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Thema enthält schrittweise Anweisungen zum Konfigurieren von DirectAccess in Windows Server Essentials zum Aktivieren von mobilen Mitarbeiter zu nahtlos mit dem Unternehmensnetzwerk von einem beliebigen Remotestandort mit Internetanschluss ohne Verbinden einer Virtuelles privates Netzwerk (VPN)-Verbindung. DirectAccess können mobile Mitarbeiter, die gleiche netzwerkanbindung wie innerhalb und außerhalb des Büros auf ihren Computern Windows 8.1, Windows 8 und Windows 7 bieten.  
  
 In Windows Server Essentials auf Wenn eine Domäne mehr als einen Windows Server Essentials-Server muss DirectAccess auf dem Domänencontroller konfiguriert werden.  
  
> [!NOTE]
>  Dieses Thema enthält Anweisungen zum Konfigurieren von DirectAccess, wenn Ihr Windows Server Essentials-Server den Domänencontroller ist. Wenn der Windows Server Essentials-Server Mitglied einer Domäne ist, befolgen Sie die Anweisungen zum Konfigurieren von DirectAccess auf einem Domänenmitglied in [Hinzufügen von DirectAccess zu einer vorhandenen Remotezugriffsbereitstellung (VPN)](https://technet.microsoft.com/library/jj574220.aspx) stattdessen.  
  
## <a name="process-overview"></a>Prozessübersicht  
 Führen Sie die folgenden Schritte aus, um DirectAccess in Windows Server Essentials zu konfigurieren.  
  
> [!IMPORTANT]
>  Bevor Sie die Verfahren in diesem Handbuch zum Konfigurieren von DirectAccess in Windows Server Essentials verwenden, müssen Sie VPN auf dem Server aktivieren. Anweisungen hierzu finden Sie unter [Verwalten des VPN](Manage-VPN-in-Windows-Server-Essentials.md).  
  
-   [Schritt 1: Hinzufügen der Tools für die Remotezugriffsverwaltung zum server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)  
  
-   [Schritt 2: Ändern der Netzwerkadapteradresse des Servers zu einer statischen IP-Adresse](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)  
  
-   [Schritt 3: Vorbereiten eines Zertifikats und DNS-Eintrags für den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)  
  
    -   [Schritt 3a: Gewähren Sie Vollzugriff für die Webserver Zertifikatvorlage zu authentifizierten Benutzern](#BKMK_GrantFullPermissions)  
  
    -   [Schritt 3b: Registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, die aus dem externen Netzwerk nicht aufgelöst werden](#BKMK_EnrollaCertificate)  
  
    -   [Schritt 3c: Hinzufügen eines neuen Hosts auf dem DNS-Server, und ordnen Sie es zur Windows Server Essentials-Serveradresse](#BKMK_MapNewHosttoServerAddress)  
  
-   [Schritt 4: Erstellen Sie eine Sicherheitsgruppe für DirectAccess-Clientcomputer](#BKMK_AddSecurityGroup)  
  
-   [Schritt 5: Aktivieren und Konfigurieren von DirectAccess](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)  
  
    -   [Schritt 5a: Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
    -   [Schritt 5 b: Entfernen Sie die ungültigen IPv6Prefix im RRAS-Gruppenrichtlinienobjekt (nur Windows Server Essentials)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
    -   [Schritt 5c: Aktivieren von Clientcomputern mit Windows 7 Enterprise für DirectAccess](#BKMK_Step4cWindows7Setup)  
  
    -   [Schritt 5D: Konfigurieren des Netzwerkadressenservers](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
    -   [Schritt 5e: Hinzufügen eines Registrierungsschlüssels zur Umgehung der CA-Zertifizierung beim Einrichten eines IPsec-Kanals](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
-   [Schritt 6: Konfigurieren von Einstellungen der Richtlinientabelle für die namensauflösung für den DirectAccess-server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)  
  
-   [Schritt 7: Konfigurieren von TCP- und UDP-Firewallregeln für die Gruppenrichtlinienobjekte des DirectAccess-Servers](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)  
  
-   [Schritt 8: Ändern der DNS64-Konfiguration zum Abhören der IP-HTTPS-Schnittstelle](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)  
  
-   [Schritt 9: Reservieren von Ports für des WinNat-Diensts](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)  
  
-   [Schritt 10: Neustarten des WinNat-Diensts](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)  
  
> [!NOTE]
>  [Anhang: Einrichten von DirectAccess mithilfe von Windows PowerShell](#BKMK_AppendixBPowerShellScript) bietet ein Windows PowerShell-Skript, mit denen Sie das DirectAccess-Setup ausführen.  
  
##  <a name="BKMK_AddRAM"></a> Schritt 1: Hinzufügen von %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot; zum Server  
  
#### <a name="to-add-remote-access-management-tools"></a>So fügen Sie %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot; hinzu  
  
1.  Klicken Sie auf dem Server in der unteren linken Ecke der Startseite auf das Symbol **Server-Manager**.  
  
     In Windows Server Essentials müssen Sie für Server-Manager, um ihn zu öffnen zu suchen. Geben Sie auf der Startseite **Server Manager**ein, und klicken Sie dann auf **Server-Manager** in den Suchergebnissen. Um den Server-Manager an die Startseite anzuheften, klicken Sie mit der rechten Maustaste auf den Server-Manager in den Suchergebnissen, und klicken Sie dann auf **An Startmenü anheften**.  
  
2.  Wenn eine Warnmeldung zur **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**.  
  
3.  Klicken Sie auf dem Server-Manager-Dashboard auf **Verwalten**, und klicken Sie dann auf **Rollen und Features hinzufügen**.  
  
4.  Im Assistenten zum Hinzufügen von Rollen und Features gehen folgendermaßen Sie vor:  
  
    1.  Klicken Sie auf der Seite **Installationstyp** auf **Rollenbasierte oder featurebasierte Installation**.  
  
    2.  Auf der **Serverauswahl** (oder die **Zielserver auswählen** Seite in Windows Server Essentials), klicken Sie auf **wählen Sie einen Server aus dem Serverpool**.  
  
    3.  Auf der Seite **Features** erweitern Sie **Remoteserver-Verwaltungstools (installiert)** , erweitern Sie **Tools für die Remotezugriffsverwaltung (installiert)** , erweitern Sie **Rollenverwaltungstools (installiert)** , erweitern Sie **Tools für die Remotezugriffsverwaltung**, und wählen Sie dann **Remotezugriffs-GUI und Befehlszeilentools**.  
  
    4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
##  <a name="BKMK_AddStaticIP"></a> Schritt 2: Ändern der Netzwerkadapteradresse des Servers zu einer statischen IP-Adresse  
 DirectAccess erfordert einen Adapter mit einer statischen IP-Adresse. Sie müssen die IP-Adresse für den lokalen Netzwerkadapter auf Ihrem Server ändern.  
  
#### <a name="to-add-a-static-ip-address"></a>So fügen Sie eine statische IP-Adresse hinzu  
  
1.  Öffnen Sie auf der Startseite **Systemsteuerung**.  
  
2.  Klicken Sie auf **Netzwerk und Internet**und dann auf **Netzwerkstatus und -aufgaben anzeigen**.  
  
3.  Klicken Sie im Aufgabenbereich des **Netzwerk- und Freigabecenters**auf **Adaptereinstellungen ändern**.  
  
4.  Klicken Sie mit der rechten Maustaste auf den lokalen Netzwerkadapter, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Klicken Sie auf der Registerkarte **Netzwerk** auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
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
  
##  <a name="BKMK_DNS"></a> Schritt 3: Vorbereiten eines Zertifikats und eines DNS-Eintrags für den Netzwerkadressenserver  
 Um ein Zertifikat und den DNS-Eintrag für den Netzwerkadressenserver vorzubereiten, führen Sie die folgenden Aufgaben aus:  
  
-   [Schritt 3a: Gewähren Sie Vollzugriff für die Webserver Zertifikatvorlage zu authentifizierten Benutzern](#BKMK_GrantFullPermissions)  
  
-   [Schritt 3b: Registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, die aus dem externen Netzwerk nicht aufgelöst werden](#BKMK_EnrollaCertificate)  
  
-   [Schritt 3c: Hinzufügen eines neuen Hosts auf dem DNS-Server, und ordnen Sie sie zur Windows Server Essentials-Serveradresse.](#BKMK_MapNewHosttoServerAddress)  
  
###  <a name="BKMK_GrantFullPermissions"></a> Schritt 3a: Gewähren Sie Vollzugriff für die Webserver Zertifikatvorlage zu authentifizierten Benutzern  
 Die erste Aufgabe besteht Vollzugriff zum Authentifizieren von Benutzern für die Webserver Zertifikatvorlage in der Zertifizierungsstelle zu gewähren.  
  
####  <a name="BKMK_ToGrantFullPermissions"></a> Gewähren Sie uneingeschränkte Berechtigungen für authentifizierte Benutzer für die Webserver Zertifikatvorlage  
  
1.  Auf der Seite **Start** öffnen Sie **Zertifizierungsstelle**.  
  
2.  In der Konsolenstruktur unter **Zertifizierungsstelle (lokal)** , erweitern Sie **< Servername\>-CA**, mit der rechten Maustaste **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten**.  
  
3.  In **Zertifizierungsstelle (lokal)** klicken Sie mit der rechten Maustaste auf **Webserver**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  In den Webservereigenschaften klicken Sie auf der Registerkarte **Sicherheit** auf **Authentifizierte Benutzer**, wählen Sie **Vollzugriff**, und klicken Sie dann auf **OK**.  
  
5.  Starten Sie **Active Directory-Zertifikatdienste** neu. Öffnen Sie in der Systemsteuerung **Lokale Dienste anzeigen**. Klicken Sie in der Liste der Dienste mit der rechten Maustaste auf **Active Directory-Zertifikatdienste**, und klicken Sie dann auf **Neustarten**.  
  
###  <a name="BKMK_EnrollaCertificate"></a> Schritt 3 b: Registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann  
 Anschließend registrieren Sie ein Zertifikat für den Netzwerkadressenserver mit einem allgemeinen Namen, der aus dem externen Netzwerk nicht aufgelöst werden kann.  
  
####  <a name="BKMK_ToEnrollaCertificate"></a> Zum Registrieren eines Zertifikats für den Netzwerkadressenserver  
  
1.  Auf der Seite **Start** öffnen Sie **MMC** (Microsoft Management Console).  
  
2.  Wenn eine Warnmeldung zur **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**.  
  
     Die Microsoft Management Console (MMC) wird geöffnet.  
  
3.  Im Menü **Datei** klicken Sie auf **Snap-Ins hinzufügen bzw. entfernen**.  
  
4.  Im Feld **Snap-Ins hinzufügen bzw. entfernen** klicken Sie auf **Zertifikate**, und klicken Sie dann auf **Hinzufügen**.  
  
5.  Klicken Sie auf der Seite **Zertifikat-Snap-In** auf **Computerkonto**, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf der Seite **Computer auswählen** auf **Lokaler Computer**, auf **Fertig stellen**und dann auf **OK**.  
  
7.  Erweitern Sie in der Konsolenstruktur **Zertifikate (Lokaler Computer)** , erweitern Sie **Persönlich**, klicken Sie mit der rechten Maustaste auf **Zertifikate**, und klicken Sie dann in **Alle Aufgaben**auf **Neues Zertifikat anfordern**.  
  
8.  Wenn der Zertifikatregistrierungs-Assistent angezeigt wird, klicken Sie auf **Weiter**.  
  
9. Auf der Seite **Zertifikatregistrierungsrichtlinie auswählen** klicken Sie auf **Weiter**.  
  
10. Auf der Seite **Zertifikate anfordern** wählen Sie **Webserver**, und klicken Sie dann auf **Es werden zusätzliche Informationen für diese Zertifikatsregistrierung benötigt**.  
  
11. Im Feld **Zertifikateigenschaften** geben Sie die folgenden Einstellungen für **Antragstellername** ein:  
  
    1.  Für **Typ** wählen Sie **Allgemeiner Name**.  
  
    2.  Für **Wert**geben Sie den Namen des Netzwerkadressenservers (z. B. DirectAccess-NLS.contoso.local) ein, und klicken Sie dann auf **Hinzufügen**.  
  
    3.  Klicken Sie auf **OK**, und klicken Sie dann auf **Registrieren**.  
  
12. Klicken Sie nach Abschluss der Zertifikatregistrierung auf **Fertig stellen**.  
  
###  <a name="BKMK_MapNewHosttoServerAddress"></a> Schritt 3c: Hinzufügen eines neuen Hosts auf dem DNS-Server und Zuordnen des Hosts zur Windows Server Essentials-Serveradresse  
 Hinzufügen eines neuen Hosts auf dem DNS-Server, und ordnen Sie sie zur Windows Server Essentials-Serveradresse, um die DNS-Konfiguration abzuschließen.  
  
####  <a name="BKMK_ToMapNewHosttoServerAddress"></a> Zuordnen ein neues Hosts zur Windows Server Essentials-Serveradresse  
  
1.  Öffnen Sie auf der Startseite den DNS-Manager. Suchen Sie zum Öffnen des DNS-Managers nach **dnsmgmt.msc**, und klicken Sie dann auf **dnsmgmt.msc** in den Ergebnissen.  
  
2.  In der Konsolenstruktur des DNS-Manager, erweitern Sie in den lokalen Server, erweitern Sie **Forward-Lookupzonen**mit der rechten Maustaste auf die Zone mit dem Domänensuffix des Servers, und klicken Sie dann auf **neuer Host (A oder AAAA)** .  
  
3.  Geben Sie den Namen und die IP-Adresse des Servers (z. B. %%amp;quot;DirectAccess-NLS.contoso.local%%amp;quot;) und die entsprechende Serveradresse ein (z. B. 192.168.x.x).  
  
4.  Klicken Sie auf **Host hinzufügen**, klicken Sie auf **OK**, und klicken Sie dann auf **Fertig**.  
  
##  <a name="BKMK_AddSecurityGroup"></a> Schritt 4: Erstellen einer Sicherheitsgruppe für DirectAccess-Clientcomputer  
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
  
4.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
5.  Geben Sie im Dialogfeld die Namen der Computerkonten, die Sie der Gruppe hinzufügen möchten, durch ein Semikolon (;) getrennt ein. Klicken Sie dann auf **Namen überprüfen**.  
  
6.  Nachdem die Computerkonten überprüft wurden, klicken Sie auf **OK**. Klicken Sie dann erneut auf **OK**.  
  
> [!NOTE]
>  Sie können auch die Registerkarte **Mitglied von** in den Eigenschaften des Computerkontos verwenden, um das Konto der Sicherheitsgruppe hinzuzufügen.  
  
##  <a name="BKMK_EnableConfigureDA"></a> Schritt 5: Aktivieren und Konfigurieren von DirectAccess  
 Zum Aktivieren und Konfigurieren von DirectAccess in Windows Server Essentials, müssen Sie die folgenden Schritte ausführen:  
  
-   [Schritt 5a: Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
-   [Schritt 5 b: Entfernen Sie die ungültigen IPv6Prefix im RRAS-Gruppenrichtlinienobjekt (nur Windows Server Essentials)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
-   [Schritt 5c: Aktivieren von Clientcomputern mit Windows 7 Enterprise für DirectAccess](#BKMK_Step4cWindows7Setup)  
  
-   [Schritt 5D: Konfigurieren des Netzwerkadressenservers](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
-   [Schritt 5e: Hinzufügen eines Registrierungsschlüssels zur Umgehung der CA-Zertifizierung beim Einrichten eines IPsec-Kanals](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
###  <a name="BKMK_EnableDA"></a> Schritt 5a: Aktivieren von DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Aktivieren von DirectAccess in Windows Server Essentials. Wenn Sie auf dem Server noch kein VPN konfiguriert haben, sollten Sie dies tun, bevor Sie mit diesem Vorgang beginnen. Anweisungen hierzu finden Sie unter [Verwalten des VPN](Manage-VPN-in-Windows-Server-Essentials.md).  
  
##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>So aktivieren Sie DirectAccess mithilfe der Remotezugriffs-Verwaltungskonsole  
  
1.  Öffnen Sie auf der Startseite **Remotezugriffsverwaltung**.  
  
2.  Führen Sie im Assistenten zum Aktivieren von DirectAccess folgende Schritte aus:  
  
    1.  Überprüfen Sie **Voraussetzungen für DirectAccess**, und klicken Sie auf **Weiter**.  
  
    2.  Auf der Registerkarte **Gruppen auswählen** fügen Sie die zuvor für DirectAccess-Clients erstellte Sicherheitsgruppe hinzu. (Wenn Sie die Sicherheitsgruppe nicht erstellt haben, finden Sie unter [Schritt 4: Erstellen Sie eine Sicherheitsgruppe für DirectAccess-Client Computern](#BKMK_AddSecurityGroup) Anweisungen.)  
  
    3.  Wenn Sie den Remotezugriff auf den Server für mobile Computer über DirectAccess zulassen möchten, klicken Sie auf der Registerkarte **Gruppen auswählen** auf **DirectAccess ausschließlich für mobile Computer aktivieren** und anschließend auf **Weiter**.  
  
    4.  Wählen Sie in **Netzwerktopologie**die Topologie des Servers aus, und klicken Sie dann auf **Weiter**.  
  
    5.  Fügen Sie in **Suchliste für DNS-Suffix** ggf. das zusätzliche DNS-Suffix für die Clientcomputer hinzu, und klicken Sie dann auf **Weiter**.  
  
        > [!NOTE]
        >  Standardmäßig fügt der Assistent zum Aktivieren von DirectAccess bereits das DNS-Suffix für die aktuelle Domäne hinzu. Sie können bei Bedarf jedoch weitere Domänen hinzufügen.  
  
    6.  Überprüfen Sie die anzuwendenden Gruppenrichtlinienobjekte (Group Policy Objects, GPOs), und ändern Sie sie ggf.  
  
    7.  Klicken Sie auf **Weiter**und dann auf **Fertig stellen**.  
  
    8.  Führen Sie den folgenden Windows PowerShell-Befehl im Modus mit erhöhten Rechten aus, um den Remotezugriffsverwaltungs-Dienst neu zu starten:  
  
        ```powershell  
        Restart-Service RaMgmtSvc   
        ```  
  
###  <a name="BKMK_RemoveIPv6"></a> Schritt 5 b: Entfernen Sie die ungültigen IPv6Prefix im RRAS-Gruppenrichtlinienobjekt (nur Windows Server Essentials)  
  Dieser Abschnitt gilt für einen Server mit Windows Server Essentials.  
  
 Öffnen Sie Windows PowerShell als Administrator, und führen Sie die folgenden Befehle aus:  
  
```powershell  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
```  
  
###  <a name="BKMK_Step4cWindows7Setup"></a> Schritt 5c: Aktivieren von Clientcomputern mit Windows 7 Enterprise für DirectAccess  
 Wenn Sie Clientcomputer mit Windows 7 Enterprise verfügen, führen Sie das folgende Verfahren zum Aktivieren von DirectAccess auf diesen Computern.  
  
##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>So aktivieren Sie Windows 7 Enterprise-Computer für DirectAccess  
  
1.  Öffnen Sie auf der Startseite des Servers **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**. Klicken Sie dann im Bereich **Einstellungsdetails** unter **Schritt 2** auf **Bearbeiten**.  
  
     Der Setup-Assistent für Remotezugriffsserver wird geöffnet.  
  
3.  Auf der **Authentifizierung** Registerkarte, und wählen Sie das Zertifikat der Zertifizierungsstelle-Zertifizierungsstelle (CA), die das vertrauenswürdige Stammzertifikat werden (Sie können das Zertifizierungsstellenzertifikat des Windows Server Essentials-Servers wählen). Klicken Sie auf **Für Windows 7-Clientcomputer Verbindungen über DirectAccess zulassen**, und klicken Sie dann auf **Weiter**.  
  
4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
> [!IMPORTANT]
>  Es gibt ein bekanntes Problem für Windows 7 Enterprise-Computer, die eine Verbindung über DirectAccess herstellen, wenn der Windows Server Essentials-Server nicht mit UR1 vorinstalliert stammt. Um DirectAccess-Verbindungen in dieser Umgebung zu ermöglichen, müssen Sie die folgenden zusätzlichen Schritte ausführen:  
> 
> 1. Installieren Sie den beschriebenen Hotfix [Microsoft Knowledge Base (KB)-Artikel 2796394](https://support.microsoft.com/kb/2796394) auf dem Windows Server Essentials-Server. Starten Sie dann den Server neu.  
>    2. Installieren Sie dann den beschriebenen Hotfix [Microsoft Knowledge Base (KB)-Artikel 2615847](https://support.microsoft.com/kb/2615847) auf jedem Computer Windows 7.  
> 
>    Dieses Problem wurde in Windows Server Essentials gelöst.  
  
###  <a name="BKMK_NLS"></a> Schritt 5D: Konfigurieren des Netzwerkadressenservers  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Konfigurieren der Einstellungen des Netzwerkadressenservers.  
  
> [!NOTE]
>  Bevor Sie beginnen, kopieren Sie den Inhalt von der < SystemDrive\>\inetpub\wwwroot-Ordner, der < SystemDrive\>Ordner "\Program Files\Windows Server\Bin\WebApps\Site\insideoutside". Kopieren Sie außerdem die Datei default.aspx aus dem < SystemDrive\>Ordner "\Program Server\Bin\WebApps\Site" auf der < SystemDrive\>Ordner "\Program Files\Windows Server\Bin\WebApps\Site\insideoutside".  
  
##### <a name="to-configure-the-network-location-server"></a>So konfigurieren Sie den Netzwerkadressenserver  
  
1.  Öffnen Sie auf der Startseite **Remotezugriffsverwaltung**.  
  
2.  In der Remotezugriffs-Verwaltungskonsole klicken Sie auf **Konfiguration**, und klicken Sie im Detailbereich **Remotezugriff einrichten** im **Schritt 3** auf **Bearbeiten**.  
  
3.  In der RAS-Server-Setup-Assistent auf die **Netzwerkadressenserver** Registerkarte **der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt**, und wählen Sie dann das Zertifikat, das war zuvor ausgestellten (in [Schritt 3: Vorbereiten eines Zertifikats und DNS-Eintrags für den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)).  
  
4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen, und klicken Sie dann auf **Fertig stellen**.  
  
###  <a name="BKMK_CA"></a> Schritt 5e: Hinzufügen eines Registrierungsschlüssels zur Umgehung der CA-Zertifizierung beim Einrichten des IPsec-Kanals  
 Im nächsten Schritt konfigurieren Sie den Server, um die CA-Zertifizierung zu umgehen, wenn ein IPsec-Kanal eingerichtet wird.  
  
##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>So fügen Sie einen Registrierungsschlüssel zum Umgehen der CA-Zertifizierung hinzu  
  
1.  Öffnen Sie auf der Startseite **Regedit** (den Registrierungs-Editor).  
  
2.  Erweitern Sie im Registrierungs-Editor **HKEY_LOCAL_MACHINE**, erweitern Sie **System**, erweitern Sie **CurrentControlSet**, erweitern Sie **Services**, und erweitern Sie **IKEEXT**.  
  
3.  Klicken Sie unter **IKEEXT** mit der rechten Maustaste auf **Parameter**, klicken Sie auf **Neu**, und klicken Sie dann auf **DWORD-Wert (32 Bit)** .  
  
4.  Geben Sie dem neu hinzugefügten Wert den Namen **ikeflags**.  
  
5.  Doppelklicken Sie auf **Ikeflags**, geben Sie als **Typ** die Option **Hexadezimal**an, legen Sie als Wert **8000**fest, und klicken Sie dann auf **OK**.  
  
> [!NOTE]
>  Den folgenden Windows PowerShell-Befehl können Sie im erweiterten Modus verwenden, um diesen Registrierungsschlüssel hinzuzufügen:  
>   
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`  
  
##  <a name="BKMK_NRPT"></a> Schritt 6: Konfigurieren der Richtlinientabelleneinträge für die Namensauflösung des DirectAccess-Servers  
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
  
##  <a name="BKMK_TCPUDP"></a> Schritt 7: Konfigurieren der TCP- und UDP-Firewallregeln für die Gruppenrichtlinienobjekte des DirectAccess-Servers  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Konfigurieren der TCP- und UDP-Firewallregeln für die Gruppenrichtlinienobjekte des DirectAccess-Servers.  
  
#### <a name="to-configure-firewall-rules"></a>So konfigurieren Sie Firewallregeln  
  
1.  Öffnen Sie auf der Startseite **Gruppenrichtlinienverwaltung**.  
  
2.  Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole auf die standardmäßige Gesamtstruktur und Domäne, klicken Sie mit der rechten Maustaste auf **DirectAccess-Servereinstellungen**, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfiguration**, klicken Sie auf **Richtlinien**, klicken Sie auf **Windows-Einstellungen**, klicken Sie auf **Sicherheitseinstellungen**, klicken Sie auf **Windows-Firewall mit erweiterter Sicherheit**, klicken Sie auf die nächste Ebene **Windows-Firewall mit erweiterter Sicherheit**, und klicken Sie dann auf **Eingehende Regeln**. Klicken Sie mit der rechten Maustaste auf **Domänennamenserver (TCP eingehend)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf die Registerkarte **Bereich** , und fügen Sie in der Liste **Lokale IP-Adresse** die IPv6-Adresse der IP-HTTPS-Schnittstelle hinzu.  
  
5.  Wiederholen Sie dieses Verfahren für **Domänennamenserver (UDP eingehend)** .  
  
##  <a name="BKMK_DNS64"></a> Schritt 8: Ändern der DNS64-Konfiguration zum Abhören der IP-HTTPS-Schnittstelle  
 Sie müssen die DNS64-Konfiguration mithilfe des folgenden Windows PowerShell so ändern, dass die IP-HTTPS-Schnittstelle abgehört wird:  
  
```powershell  
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface  
```  
  
##  <a name="BKMK_ExemptPort"></a> Schritt 9: Reservieren von Ports für den WinNat-Dienst  
 Verwenden Sie den folgenden Windows PowerShell-Befehl, um Ports für des WinNat-Diensts zu reservieren. Ersetzen Sie "192.168.1.100" durch die tatsächliche IPv4-Adresse Ihres Windows Server Essentials-Servers ein.  
  
```powershell  
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
```  
  
> [!IMPORTANT]
>  Um Portkonflikte mit Anwendungen zu vermeiden, stellen sicher, dass der für den WinNat-Dienst reservierte Portbereich nicht Port 6602 enthält.  
  
##  <a name="BKMK_WinNAT"></a> Schritt 10: Neustarten des WinNat-Diensts  
 Mit dem folgenden Windows PowerShell-Befehl starten Sie den Windows-NAT-Treiberdienst (WinNat)-Dienst neu.  
  
```powershell  
Restart-Service winnat  
```  
  
##  <a name="BKMK_AppendixBPowerShellScript"></a> Anhang: Einrichten von DirectAccess mithilfe von Windows PowerShell  
 In diesem Abschnitt wird das Einrichten und Konfigurieren von DirectAccess mithilfe von Windows PowerShell beschrieben.  
  
### <a name="preparation"></a>Vorbereitung  
 Bevor Sie mit der Konfiguration des Servers für DirectAccess beginnen, müssen Sie folgende Schritte ausführen:  
  
1.  Führen Sie die Verfahren in [Schritt 3: Vorbereiten eines Zertifikats und DNS-Eintrags für den Netzwerkadressenserver](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS) zum Registrieren eines Zertifikats mit dem Namen **DirectAccess-NLS.contoso.com** (wobei **"contoso.com"** wird durch die tatsächliche ersetzt Interner Domänenname), und einen DNS-Eintrag für den Netzwerkadressenserver (NLS) hinzuzufügen.  
  
2.  Fügen Sie in Active Directory eine Sicherheitsgruppe mit dem Namen **DirectAccessClients** hinzu, und fügen Sie dann Clientcomputer hinzu, auf denen Sie die DirectAccess-Funktionen bereitstellen möchten. Weitere Informationen finden Sie unter [Schritt 4: Erstellen Sie eine Sicherheitsgruppe für DirectAccess-Client Computern](#BKMK_AddSecurityGroup).  
  
### <a name="commands"></a>Befehle  
  
> [!IMPORTANT]
>  In Windows Server Essentials müssen Sie nicht das unnötige IPv6-Präfix-Gruppenrichtlinienobjekt zu entfernen. Löschen Sie den Codeabschnitt mit der folgenden Beschriftung: `# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`.  
  
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
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Zugriff überall](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
