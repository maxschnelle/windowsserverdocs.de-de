---
title: Integration eines lokalen Exchange-Servers in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b56a21e2-c9e3-4ba9-97d9-719ea6a0854b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c2020e08b94800a9750f095a2f772afb14ba5f0b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="integrate-an-on-premises-exchange-server-with-windows-server-essentials"></a>Integration eines lokalen Exchange-Servers in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Handbuch enthält Informationen und grundlegende Anweisungen zur Einrichtung und Integration eines lokalen Servers, das Exchange-Server mit einem Server ausgeführt wird, auf denen Windows Server Essentials ausgeführt wird, und.  
  
 Sie sollten dieses Handbuch lesen, vor dem Bereitstellen von eines lokalen Servers, auf der Exchange Server auf einem Windows Server Essentials-Netzwerk ausgeführt wird.  
  
> [!NOTE]
>  Exchange Server 2010 unterstützt keine Installation auf Computern, auf denen Windows Server 2012 ausgeführt werden.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Stellen Sie vor der Installation von Exchange Server auf einem Windows Server Essentials-Netzwerk sicher, dass Sie die in diesem Abschnitt beschriebenen Aufgaben ausführen.  
  
-   [Einrichten eines Servers, auf denen Windows Server Essentials ausgeführt wird](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SetUpSBS8)  
  
-   [Vorbereiten eines zweiten Servers auf dem Exchange-Server installiert.](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SecondServer)  
  
-   [Konfigurieren des Internetdomänennamens](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_DomainNames)  
  
###  <a name="BKMK_SetUpSBS8"></a>Einrichten eines Servers, auf denen Windows Server Essentials ausgeführt wird  
 Sie müssen bereits ein Server eingerichtet haben, auf denen Windows Server Essentials ausgeführt wird. Dies ist der Domänencontroller für den Server, die Exchange Server ausgeführt wird. Informationen zur Vorgehensweise beim Einrichten von Windows Server Essentials finden Sie unter [Installieren von Windows Server Essentials](../install/Install-Windows-Server-Essentials.md).  
  
###  <a name="BKMK_SecondServer"></a>Vorbereiten eines zweiten Servers auf dem Exchange-Server installiert.  
 Sie müssen Exchange Server auf einem zweiten Server, auf der eine Version des Betriebssystems Windows Server ausgeführt wird, die die Ausführung von Exchange Server 2010 offiziell unterstützt oder Exchange Server 2013 installieren. Sie müssen dann den zweiten Server mit der Windows Server Essentials-Domäne beitreten.  
  
 Informationen dazu, wie Sie einen zweiten Server mit Windows Server Essentials-Domäne zu verknüpfen, finden Sie unter Verbinden eines zweiten Servers mit dem Netzwerk in [Herstellen einer Verbindung](../use/Get-Connected-in-Windows-Server-Essentials.md).  
  
> [!NOTE]
>  Microsoft unterstützt nicht die Installation von Exchange Server auf einem Server, auf der Windows Server Essentials ausgeführt wird.  
  
###  <a name="BKMK_DomainNames"></a>Konfigurieren des Internetdomänennamens  
 Um einen lokalen Server zu integrieren, die Exchange-Server mit Windows Server Essentials ausgeführt wird, Sie müssen registriert haben einen gültigen Internetdomänennamen für Ihr Unternehmen (z. B. *"contoso.com"*). Außerdem müssen Sie gemeinsam mit Ihrem domänennamenanbieter die DNS-Ressourceneinträge erstellen, die Exchange-Server erforderlich sind.  
  
 Wenn Ihr Unternehmen Internetdomänenname "contoso.com" und den vollständig qualifizierten Domänennamen (FQDN) des verwenden möchten z. B. *mail.contoso.com* um den lokalen Server verweisen, auf denen Exchange Server ausgeführt wird, funktioniert mit Ihrem domänennamenanbieter die DNS-Ressourceneinträge in der folgenden Tabelle zu erstellen.  
  
|Name des Ressourceneintrags|Typ des Ressourcendatensatzes|Notieren Sie die Einstellung|Beschreibung|  
|--------------------------|-----------------|--------------------|-----------------|  
|e-Mail-Nachrichten|Host (A)|Address =*öffentliche IP-Adresse vom Internetdienstanbieter zugewiesen*|Exchange-Server wird an %% amp;quot;Mail.contoso.com%%amp;quot; adressierte e-Mails empfangen.<br /><br /> Sie können einen anderen Namen wählen.|  
|MX|Mail-Exchanger (MX)|Hostname = @<br /><br /> Address=Mail.contoso.com<br /><br /> Einstellung = 0|Ermöglicht routing von e-Mail-Nachrichten für email@contoso.com ankommen von Ihrem lokalen Server, auf denen Exchange Server ausgeführt wird.|  
|SPF|Text (TXT)|V spf1 einen Mx = ~ alle|Ressourceneintrag, mit dem wird verhindert, dass die e-Mail-Nachricht von Ihrem Server, die als Spam identifiziert werden.|  
|autodiscover._tcp|Dienste (SRV)|Service: _autodiscover<br /><br /> Protokoll: _tcp<br /><br /> Priorität: 0<br /><br /> Gewicht: 0<br /><br /> Port: 443<br /><br /> Ziel-Host: "Mail.contoso.com"|Ermöglicht Microsoft Office Outlook und mobilen Geräten, auf den lokalen Server automatisch zu ermitteln, auf der Exchange Server ausgeführt wird.<br /><br /> **Hinweis:** können Sie auch einen Ressourceneintrag für die AutoErmittlung Host (A) konfigurieren und zeigen Sie den Eintrag auf die öffentliche IP-Adresse des lokalen Servers, auf denen Exchange Server ausgeführt wird. Wenn Sie diese Option implementieren, Sie müssen jedoch auch angeben, Betreff Alternativer Antragstellername (SAN) SSL-Zertifikat, das sowohl die "Mail.contoso.com" als auch %% amp;quot;autodiscover.contoso.com%%amp;quot; unterstützt.|  
  
> [!NOTE]
>  -   Ersetzen Sie die Instanzen von *"contoso.com"* in diesem Beispiel wird mit den Domänennamen, die Sie registriert.  
  
 Sie müssen einen anderen FQDN für den lokalen Server auswählen, die Exchange-Server als den FQDN ausgeführt wird, die Sie für den Server verwenden, auf denen Windows Server Essentials ausgeführt wird. Sie können beispielsweise auswählen, verwenden *remote.contoso.com* als FQDN wählen, mit dem Computer auf den Server mit Windows Server Essentials über das Internet zugreifen. Sie können *mail.contoso.com* als FQDN wählen, die verwendet wird, zum Weiterleiten von e-Mails an den lokalen Server, auf denen Exchange Server ausgeführt wird.  
  
## <a name="install-exchange-server"></a>Installieren Sie Exchange Server  
 Das Exchange Server-Integrationsfeature unter Windows Server Essentials unterstützt die folgenden Versionen von Exchange Server:  
  
-   Exchange Server 2013  
  
-   Exchange Server 2010 mit Servicepack 1 (SP1)  
  
 Bevor Sie den Exchange-Server auf dem zweiten Server installieren, müssen Sie zuerst das aktuelle Administratorkonto zum Hinzufügen der **Organisations-Admins** Gruppe.  
  
#### <a name="to-add-the-current-administrator-account-to-the-enterprise-admins-group"></a>So fügen Sie das aktuelle Administratorkonto der Gruppe "Organisations-Admins" hinzu  
  
1.  Melden Sie sich mit Windows Server Essentials als Administrator an.  
  
2.  Windows PowerShell als Administrator ausführen.  
  
3.  Geben Sie an der Windows PowerShell-Eingabeaufforderung **Add-ADGroupMember ˜Enterprise Admins $env: Username**, und drücken Sie dann die EINGABETASTE.  
  
#### <a name="to-install-exchange-server"></a>So installieren Sie Exchange Server  
  
1.  Melden Sie sich an den zweiten Server als Administrator an.  
  
2.  Öffnen Sie den Internetbrowser, und navigieren Sie zu den [Bereitstellung Assistenten für Exchange Server](https://go.microsoft.com/fwlink/p/?LinkID=249163) Website.  
  
3.  Klicken Sie auf **On-Premises Only**.  
  
4.  Klicken Sie auf die Option zur Neuinstallation für die Version von Exchange Server, die Sie installieren möchten.  
  
    > [!NOTE]
    >  Wenn Sie von einer Installation von Windows Small Business Server migrieren, sollten Sie die entsprechende upgradeoption auswählen, die den Migrationsschritten aus.  
  
5.  Die Standardeinstellungen übernehmen Sie auf der nächsten Seite, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]
    >  Wenn Sie in der neuen Installation von Exchange Server Öffentliche Ordner verwenden möchten, ändern Sie die entsprechende Einstellung in **Ja**.  
  
6.  Führen Sie die Schritte in der Checkliste zum Bereitstellen von Exchange Server.  
  
     Der Exchange Server-Bereitstellungs-Assistenten können Sie:  
  
    -   Drucken der Prüfliste an.  
  
    -   Senden Sie eine Kopie der Prüfliste an einen Empfänger per e-Mail.  
  
    -   Herunterladen der Prüfliste als PDF-Datei.  
  
> [!NOTE]
>  -   Sie müssen stets auch die Verwaltungstools auf dem Server installieren, auf denen Exchange Server ausgeführt wird. Die Verwaltungstools sind von der Exchange Server-Integrationsfeature unter Windows Server Essentials erforderlich.  
> -   Wenn Sie virtuelle Verzeichnisse konfigurieren müssen, sollten Sie auch festlegen, die **InternalUrl** Eigenschaften auf dieselbe URL wie die **ExternalUrl** Eigenschaft für jedes virtuelle Verzeichnis. Weitere Informationen finden Sie unter [Verwalten von Clients für virtuelle Verzeichnisse](https://go.microsoft.com/fwlink/p/?LinkId=251058) auf dem Exchange Server 2010-Onlinehilfe.  
> -   Wenn Sie Outlook Web Access (OWA) von innerhalb des Standorts Remote Web Access in Windows Server Essentials zugreifen möchten, müssen Sie die Externalurl-Eigenschaft für OWA festlegen.  
  
 Wenn Sie Exchange Server 2010 im eines vollständig neuen Setups installieren, auch können die folgenden Skripts Sie Exchange-Server einrichten.  
  
#### <a name="to-use-scripts-to-set-up-exchange-server"></a>Verwenden Sie Skripts zum Einrichten von Exchange Server  
  
1.  Öffnen Sie Editor, und fügen Sie das folgende Skript in eine neue Datei:  
  
     `Import-Module ServerManager`  
  
     `Add-WindowsFeature NET-Framework,RSAT-ADDS,Web-Server,Web-Basic-Auth,Web-Windows-Auth,Web-Metabase,Web-Net-Ext,Web-Lgcy-Mgmt-Console,WAS-Process-Model,RSAT-Web-Server,Web-ISAPI-Ext,Web-Digest-Auth,Web-Dyn-Compression,NET-HTTP-Activation,Web-Asp-Net,Web-Client-Auth,Web-Dir-Browsing,Web-Http-Errors,Web-Http-Logging,Web-Http-Redirect,Web-Http-Tracing,Web-ISAPI-Filter,Web-Request-Monitor,Web-Static-Content,Web-WMI,RPC-Over-HTTP-Proxy  �Restart`  
  
2.  Speichern Sie die Datei **installdependencies. ps1**.  
  
3.  Kopieren Sie das Exchange-SSL-Zertifikat an einen Speicherort auf dem Server.  
  
4.  Öffnen Sie eine neue Editordatei, und kopieren Sie den folgenden Text in die Datei:  
  
     `param (`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "The path to your Certificate file, must be a *.pfx format")]`  
  
     `$CertPath = "c:\certificates\ExchangeCertificate.pfx",`  
  
     `[Security.SecureString]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "The password of your cert")]`  
  
     `$CertPassword = $null,`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Domain Name, eg. contoso.com")]`  
  
     `$DomainName = "contoso.com",`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Server IP Address, eg. 192.168.0.1")]`  
  
     `$ServerIpAddress = "192.168.0.1",`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Internal Ip Range, eg. 192.168.0.0-192.168.0.255")]`  
  
     `$InternalIpRange = "192.168.0.0-192.168.0.255"`  
  
     `)`  
  
     `#Import Exchange Certificate, and Enable it for POP IIS IMAP SMTP services.`  
  
     `Import-ExchangeCertificate  �FileData ([Byte[]]$(Get-content -Path $CertPath  �Encoding byte  �ReadCount 0)) -Password:$CertPassword -Force | Enable-ExchangeCertificate -Services 'POP, IIS, IMAP, SMTP' -Force`  
  
     `#New AcceptedDomain and set it to default`  
  
     `New-AcceptedDomain  �Name "official name"  �DomainName $domainname`  
  
     `Set-AcceptedDomain  �Identity "official name"  �MakeDefault $true`  
  
     `#New EmailAddress Policy`  
  
     `$address = "%m@" + $DomainName`  
  
     `New-EmailAddressPolicy -Name "Windows Server Essentials Email Address Policy" -IncludedRecipients AllRecipients -EnabledPrimarySMTPAddressTemplate $address`  
  
     `#Set owa and ecp VirtualDirectory ExternalUrl`  
  
     `$hostname = "mail." + $DomainName`  
  
     `$owa = "https://" + $hostname + "/owa"`  
  
     `$ecp = "https://" + $hostname + "/ecp"`  
  
     `$activesync = "https://" + $hostname + "/Microsoft-Server-ActiveSync"`  
  
     `$oab = "https://" + $hostname + "/OAB"`  
  
     `$ews = "https://" + $hostname + "/EWS/Exchange.asmx"`  
  
     `Get-OwaVirtualDirectory | Set-OwaVirtualDirectory  �ExternalUrl $owa  �InternalUrl $owa`  
  
     `Get-EcpVirtualDirectory | Set-EcpVirtualDirectory  �ExternalUrl $ecp  �InternalUrl $ecp`  
  
     `Get-ActiveSyncVirtualDirectory | Set-ActiveSyncVirtualDirectory -ExternalUrl $activesync  �InternalUrl $activesync`  
  
     `Get-OABVirtualDirectory | Set-OABVirtualDirectory -ExternalUrl $oab -InternalUrl $oab -RequireSSL:$true`  
  
     `Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -ExternalUrl $ews -InternalUrl $ews -BasicAuthentication:$True -Force`  
  
     `#Enable outlook Anywhere`  
  
     `Enable-OutlookAnywhere  �ClientAuthenticationMethod:Basic  �ExternalHostname:$hostname  �SSLOffloading:$false`  
  
     `#new receive/send connector`  
  
     `$machinename = get-content env:computername`  
  
     `$bindingIpaddress = $ServerIpAddress + ":25"`  
  
     `$RecevieConnectorName = $machinename + "\Default " + $machinename`  
  
     `Set-ReceiveConnector $RecevieConnectorName -RemoteIPRanges $InternalIpRange`  
  
     `New-ReceiveConnector -Name "WSE Internet Receive Connector" -Usage "Internet" -Bindings $bindingIpaddress -Fqdn $hostname -Enabled $true -Server $machinename -AuthMechanism Tls,BasicAuth,BasicAuthRequireTLS,Integrated`  
  
     `New-SendConnector -Name "WSE Internet SendConnector" -Usage "Internet" -AddressSpaces 'SMTP:*;1' -IsScopedConnector $false -DNSRoutingEnabled $true -UseExternalDNSServersEnabled $true -SourceTransportServers $machinename`  
  
5.  Legen Sie die Parameter am Anfang des Skripts gemäß Ihrer Netzwerkumgebung.  
  
6.  Speichern Sie die Datei **configureexchange. ps1**.  
  
7.  Windows PowerShell als Administrator ausführen.  
  
8.  Geben Sie an der Windows PowerShell-Eingabeaufforderung **Set-ExecutionPolicy RemoteSigned**, und drücken Sie dann die EINGABETASTE.  
  
9. Führen Sie das Skript **installdependencies. ps1**.  
  
10. Starten Sie die Server, und führen Sie Windows PowerShell als Administrator.  
  
11. Führen Sie an der Windows PowerShell-Eingabeaufforderung das folgende Skript aus:  
  
     `E:\setup.com /mode:install /roles:mb,ht,ca /OrganizationName:"First Organization"`  
  
    > [!NOTE]
    >  Achten Sie darauf, dass den richtigen Pfad für das Exchange Server-Setupprogramm eingeben.  
  
12. Wenn Exchange Server-Setup abgeschlossen ist, werden die öffnen Sie Exchange-Verwaltungsshell als Administrator.  
  
13. Geben Sie an der Exchange-Verwaltungsshell-Eingabeaufforderung **Set-ExecutionPolicy RemoteSigned**, und drücken Sie dann die EINGABETASTE.  
  
14. Führen Sie das Skript **configureexchange. ps1**.  
  
15. Starten Sie den Server neu.  
  
> [!NOTE]
>  Wenn Sie anstelle eines selbst ausgegebenen Zertifikats ein öffentlich vertrauenswürdiges SSL-Zertifikat verwenden möchten, können Sie anhand der Anleitungen im Handbuch für das Erstellen einer zertifikatanforderung und zu der ausgewählten Zertifizierungsstelle gesendet wird. Ein Exchange PowerShell-Cmdlet können auch eine zertifikatanforderung erstellen. Ein Beispiel:  
>   
>  `New-ExchangeCertificate -GenerateRequest -SubjectName "C=US, S=Washington, L=Redmond, O=contoso, OU=contoso, CN=mail.contoso.com" -DomainName mail.contoso.com -PrivateKeyExportable $true | Set-Content -path "c:\Docs\MyCertRequest.req"`  
>   
>  Passen Sie die Skriptparameter gemäß Ihrer Netzwerkumgebung.  
  
## <a name="post-installation-tasks"></a>Aufgaben nach der Installation  
 Dieser Abschnitt beschreibt die Schritte der Serverkonfiguration möglicherweise müssen Sie die Aufgaben nach der Installation durchführen, die enthält spezielle Informationen zur Einrichtung eines lokalen Servers, auf dem Exchange-Server in einem Windows Server Essentials-Netzwerk ausgeführt wird.  
  
### <a name="add-the-public-email-domain-and-configure-the-email-address-policies"></a>Der öffentliche e-Mail-Domäne hinzufügen und Konfigurieren der e-Mail-Adressrichtlinien  
  
> [!NOTE]
>  Dies ist ein erforderlicher Schritt, wenn Sie einen vollständig neuen Setups durchführen. Überspringen Sie diesen Schritt, wenn Sie von Windows Small Business Server migrieren.  
  
 Sie müssen Ihre e-Mail-Domäne als akzeptierte Standarddomäne angeben und konfigurieren Sie e-Mail-Adresse.  
  
##### <a name="to-add-your-email-domain-as-the-default-accepted-domain"></a>Die e-Mail-Domäne als Standard hinzufügen akzeptierte Standarddomäne  
  
1.  Folgen Sie den Anweisungen im Exchange Server-Artikel [Erstellen einer akzeptierten Domäne](https://go.microsoft.com/fwlink/p/?LinkId=249174) um eine akzeptierte Domäne hinzuzufügen.  
  
2.  Melden Sie sich an den zweiten Server als Administrator, der Exchange-Verwaltungskonsole zu öffnen, und navigieren Sie zu den **Hub-Transport** auf der Registerkarte der **Organisationskonfiguration**.  
  
3.  Klicken Sie im Arbeitsbereich der Exchange-Verwaltungskonsole mit der rechten Maustaste in der neuen akzeptierten Domäne, und klicken Sie dann auf **als Standard festlegen**.  
  
4.  Folgen Sie den Anweisungen im Exchange Server-Artikel [Erstellen einer E-Mail-Adressrichtlinie](https://go.microsoft.com/fwlink/p/?LinkId=249179) um eine neue e-Mail-Adressrichtlinie zu erstellen. Sie können Sie alle Standardwerte mit Ausnahme der e-Mail-Adresse akzeptieren. Geben Sie für die e-Mail-Adresse Ihre öffentliche e-Mail-Domäne.  
  
### <a name="create-smtp-send-and-receive-connectors"></a>Erstellen von SMTP-Sende- und Empfangsconnectors  
  
> [!NOTE]
>  Dies ist ein erforderlicher Schritt.  
  
 Sie müssen einen SMTP-Sendeconnector und einen SMTP-Empfangsconnector für die ausgehende und eingehende Übertragung von e-Mail-Nachrichten konfigurieren.  
  
 Um einen SMTP-Sendeconnector zu erstellen, folgen Sie die Anweisungen im Exchange Server-Artikel [Erstellen eines SMTP-Sendeconnectors](https://technet.microsoft.com/library/aa997285.aspx).  
  
 Führen Sie zum Erstellen eines SMTP-Empfangsconnectors die Schritte im Exchange Server-Artikel [Erstellen eines SMTP-Empfangsconnectors](https://technet.microsoft.com/library/bb125159.aspx).  
  
 Optional können Sie beziehen sich auf das Skript weiter oben in diesem Dokument zum Erstellen von senden und Empfangsconnectors mithilfe von Exchange PowerShell-Cmdlets.  
  
### <a name="configure-the-network-router"></a>Konfigurieren des Netzwerkrouters  
  
> [!NOTE]
>  Dies ist ein erforderlicher Schritt, wenn Sie einen vollständig neuen Setups durchführen. Wenn Sie von Windows Small Business Server migrieren, finden Sie unter [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md) Anweisungen zum Konfigurieren des Netzwerks.  
  
 Zumindest müssen Sie die folgenden Porteinstellungen auf dem Router konfigurieren:  
  
|Router-port|Ziel-IP-|Zielport|Hinweis:|  
|-----------------|--------------------|----------------------|----------|  
|25 (SMTP)|Interne IP-Adresse des lokalen Servers, auf denen Exchange Server ausgeführt wird.|25||  
|80 (HTTP)|Interne IP-Adresse des Servers, auf denen Windows Server Essentials ausgeführt wird|80||  
|443 (HTTPS)|Interne IP-Adresse des Servers, auf denen Windows Server Essentials ausgeführt wird|443||  
  
 Wenn Sie den POP3- oder IMAP-messaging-Protokolle in Ihrem Netzwerk unterstützen, müssen Sie auch portweiterleitungen für diese Protokolle konfigurieren. Weitere Informationen finden Sie im Abschnitt **Clientzugriffsserver** im Thema [Exchange-Netzwerkportreferenz](https://go.microsoft.com/fwlink/p/?LinkId=250773) in der TechNet-Bibliothek für Exchange Server.  
  
> [!NOTE]
>  -   Wir empfehlen, konfigurieren Sie statische IP-Adressen für den Server, auf der Windows Server Essentials ausgeführt wird und für den zweiten Server mit Exchange Server ausgeführt wird. Informationen zum Konfigurieren einer statischen IP-Adresse auf einem Computer unter Windows Server 2003 oder Windows Server 2008 R2 finden Sie unter [Konfigurieren einer statischen IP-Adresse](https://technet.microsoft.com/library/cc754203\(v=ws.10\).aspx) in der TechNet-Bibliothek für Windows Server  
>   
>      **Hinweis:** die DNS-servereinstellung sollte immer zeigen Sie auf die IP-Adresse des Servers, auf denen Windows Server Essentials ausgeführt wird.  
> -   Auf dem Router sicher, dass die IP-Adressen der Server, auf der Windows Server Essentials ausgeführt wird und dem Server mit Exchange Server entweder reserviert sind oder außerhalb des DHCP IP-Adressbereichs liegen.  
> -   Die Routerkonfiguration in diesem Abschnitt wird davon ausgegangen, dass Sie nur eine öffentliche IP-Adresse von Ihrem Internetdienstanbieter (ISP) zugewiesen haben. Wenn Sie mehrere öffentliche IP-Adressen haben, können Sie eine andere IP-Adresse zuweisen, mit dem Server, auf der Windows Server Essentials ausgeführt wird und mit dem Server, auf der Exchange Server ausgeführt wird und dann basierte auf den öffentlichen IP-Adressen portweiterleitungen erstellen.  
  
### <a name="enable-on-premises-exchange-server-integration-on-windows-server-essentials"></a>Aktivieren der lokalen Exchange Server-Integration in Windows Server Essentials  
  
> [!NOTE]
>  Wenn Sie von einer Windows Small Business Server-Installation migrieren, wird empfohlen, dass Sie diesen Schritt jetzt überspringen und nach der Deinstallation der vorherigen Installations von Exchange Server auf dem Quellserver ausführen.  
  
 Nachdem Sie installieren und Konfigurieren eines Servers, auf denen Exchange Server ausgeführt wird, müssen Sie die lokale Exchange Server-Integration auf dem Server aktivieren, auf denen Windows Server Essentials ausgeführt wird.  
  
##### <a name="to-enable-on-premises-exchange-server-integration-from-the-dashboard"></a>So aktivieren Sie die lokale Exchange Server-Integration über das Dashboard  
  
1.  Melden Sie sich an den Server, auf der Windows Server Essentials als Administrator ausgeführt wird, und öffnen Sie das Dashboard.  
  
2.  Auf der **Home** auf **mit Meine E-Mail-Dienst verbinden**, und klicken Sie dann auf **integrieren Sie den Exchange-Server**.  
  
3.  Klicken Sie im Informationsbereich auf **Exchange Server-Integration einrichten**.  
  
4.  Folgen Sie den Anweisungen im Assistenten aus.  
  
### <a name="configure-a-reverse-proxy"></a>Konfigurieren eines Reverseproxys  
  
> [!NOTE]
>  Dies ist ein erforderlicher Schritt, wenn Sie nur eine Internetverbindung von Ihrem Internetdienstanbieter haben.  
  
 Windows Server Essentials und Exchange Server werden remotezugriffsszenarios für Netzwerkbenutzer unterstützt. Z. B. Wenn Sie "Zugriff überall" auf dem Server, auf denen Windows Server Essentials ausgeführt wird aktivieren, können Sie Remote auf die Remotewebzugriff-Website zugreifen oder mit virtuelles privates Netzwerk (VPN) eine Remoteverbindung mit dem Windows Server Essentials-Netzwerk herzustellen. Um den Remotezugriff auf die e-Mail-Nachrichten müssen Sie Outlook Anywhere, Outlook Web Access (OWA) oder ActiveSync verwenden.  
  
 Wenn Windows Server Essentials und dem Server mit Exchange Server jeweils mit demselben Router verbunden und nur eine eingehende Internetverbindung von Ihrem Internetdienstanbieter zum Router besteht, müssen Sie eine reverseproxylösung verwenden, um unterschiedliche Arten von Remotezugriffsanforderungen aus dem Internet basierend auf den Zielhostnamen weiterzuleiten. Wir empfehlen die Verwendung von Microsoft unterstützten IIS Application Request Routing (ARR) Erweiterung als reverseproxylösung. Weitere Informationen zum IIS Application Request Routing finden Sie auf der [Website zum Application Request Routing](https://go.microsoft.com/fwlink/p/?LinkId=249181).  
  
##### <a name="to-install-and-configure-application-request-routing"></a>So installieren und Konfigurieren von Application Request Routing  
  
1.  Melden Sie sich mit Windows Server Essentials als Administrator an.  
  
2.  Öffnen Sie den Internetbrowser, und navigieren Sie zu den [Website zum Application Request Routing](https://go.microsoft.com/fwlink/p/?LinkId=249181).  
  
3.  Klicken Sie auf der ARR-Website auf **installieren**, und folgen Sie dann die Anweisungen, um die Installation von arr aus  
  
    > [!NOTE]
    >  Sie müssen das URL-Rewrite-Modul während der ARR-Installation auswählen.  
    >   
    >  Sie erhalten möglicherweise eine Fehlermeldung am Ende der ARR-Installation, die KB 2589179 für ARR 2.5 nicht erfolgreich installiert wurde. Sie können diesen Fehler ignorieren.  
  
4.  Nach Abschluss der ARR-Installation neu starten der **Remotedesktopgateway** zu verarbeiten, wenn er nicht ausgeführt wird.  
  
    > [!NOTE]
    >  Nach der Installation von ARR, die **Remotedesktopgateway** Dienst wurde möglicherweise beendet. Um den Dienst manuell neu zu starten, öffnen Sie die **Dienste** Verwaltungstool, und starten Sie den **Remotedesktopgateway** Service.  
  
5.  [Laden Sie KB2732764 für ARR 2.5](https://go.microsoft.com/fwlink/?LinkID=258302), und klicken Sie dann das Update installieren, auf dem Server, auf denen Windows Server Essentials ausgeführt wird.  
  
6.  Kopieren Sie die SSL-Zertifikatdatei für Exchange Server, auf dem Server, auf der Windows Server Essentials ausgeführt wird. Die Zertifikatdatei muss den privaten Schlüssel enthalten, und es muss im PFX-Format sein.  
  
    > [!NOTE]
    >  Bei Verwendung ein selbst ausgegebenen Zertifikats, folgen Sie den Anweisungen im Exchange Server-Artikel [Exportieren eines Exchange-Zertifikats](https://technet.microsoft.com/library/dd351274.aspx) zum Exportieren des Zertifikats.  
  
7.  Je nachdem, welche Version von Windows Server Essentials Sie ausgeführt werden führen Sie eine der folgenden:  
  
    -   Für Windows Server Essentials: Öffnen Sie ein Befehlsfenster als Administrator, und öffnen Sie dann die %ProgramFiles%\Windows Server\Bin Verzeichnis  
  
    -   Für WindowsServer Essentials: Öffnen Sie ein Befehlsfenster als Administrator, und öffnen Sie dann das Verzeichnis %Windir%\System32\Essentials.  
  
8.  Basierend auf Ihrem Installationsszenario, führen Sie einen der folgenden Schritte zur Konfiguration von ARR aus:  
  
    -   Wenn Sie einen vollständig neuen Setups durchführen, führen Sie den folgenden Befehl aus:  
  
         ** ARRConfig Config Cert ** *Pfad zur Zertifikatdatei* ** Hostnamen ** *Hostnamen für Exchange Server* ****  
  
        > [!NOTE]
        >  Beispiel: ** ARRConfig Config Cert ***c:\temp\certificate.pfx*** Hostnamen ***mail.contoso.com***  
        >   
        >  Ersetzen Sie *mail.contoso.com* mit dem Namen Ihrer Domäne, die durch das Zertifikat geschützt ist.  
  
    -   In werden Sie die Migration von Windows Small Business Server, führen Sie den folgenden Befehl:  
  
         ** ARRConfig Config Cert ** *Pfad zur Zertifikatdatei* ** Hostnamen ** *Hostnamen für Exchange Server* ** Targetserver ** *Servername von Exchange Server* ****  
  
         Beispiel: ** ARRConfig Config Cert ***c:\temp\certificate.pfx*** Hostnamen ***mail.contoso.com*** Targetserver *** ExchangeSvr ***  
  
         Ersetzen Sie *mail.contoso.com* mit dem Namen Ihrer Domäne. Ersetzen Sie *ExchangeSvr* mit dem Namen des Servers, auf denen Exchange Server ausgeführt wird.  
  
9. Wenn Sie aufgefordert werden, geben Sie das Kennwort für das Zertifikat.  
  
> [!NOTE]
>  -   Die Hostnamen, die Sie bereitstellen müssen in das SSL-Zertifikat enthalten sein, die Sie für Exchange Server erworben haben.  
> -   Wenn Sie mehrere Hostnamen haben, verwenden Sie ein Komma (,) voneinander trennen.  
  
 Um sicherzustellen, dass die Konfiguration funktioniert, versuchen Sie die OWA-Website für den Server, auf die Exchange-Server (https://mail.) ausgeführt wird *IhrDomänenname*.com/Owa) von einem Computer, der nicht Mitglied der Domäne ist. Zur Behandlung von Verbindungsproblemen können Sie auch das Onlinetool [Microsoft-Remoteverbindungsuntersuchung](https://go.microsoft.com/fwlink/p/?LinkId=249455) Tool.  
  
### <a name="configure-split-dns-for-exchange-server"></a>Konfigurieren einer DNS-Aufteilung, für die Exchange-Server  
  
> [!NOTE]
>  Dies ist ein empfohlener Schritt.  
  
 DNS-Aufteilung können Sie verschiedene IP-Adressen in DNS konfigurieren, für den gleichen Hostnamen, je nachdem, wo die DNS-Anforderung stammt. Wenn der Clientcomputer im Intranet befindet, die DNS-Anforderung, die in eine Intranet-IP-Adresse aufgelöst werden. Wenn der Client im Internet befindet, löst die DNS-Anforderung an eine IP-Adresse. Dies ist für Benutzer transparent.  
  
 Es wird empfohlen, die Sie konfigurieren, dass die Split DNS in einer Weise, die Benutzern ermöglicht, immer den gleichen Hostnamen verwenden, um Zugriff auf Exchange Server-Dienste, unabhängig von ihrem Standort.  
  
##### <a name="to-configure-split-dns-for-exchange-server"></a>So konfigurieren Sie DNS-Aufteilung für Exchange Server  
  
1.  Melden Sie sich bei Windows Server Essentials als Administrator, und öffnen Sie den DNS-Manager.  
  
2.  In der DNS-Manager-Konsolenstruktur mit der rechten Maustaste in des Servers, und klicken Sie dann auf **neue Zone**. Die **Assistent zum Erstellen neuer Zonen** angezeigt wird.  
  
3.  Auf der **Zonentyp** Seite des Assistenten, akzeptieren Sie die Standardoption, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Active Directory-Zonenreplikationsbereich** Seite, akzeptieren Sie die Standardoption, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Forward- oder Reverse-Lookupzone** übernehmen bzw. wählen **Forward-Lookupzone**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Zonenname** Geben Sie den FQDN des Servers, auf dem Exchange-Server (z. B. ausgeführt wird *mail.contoso.com*), und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **dynamisches Update** Seite, akzeptieren Sie die Standardoption, klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen**.  
  
8.  Der DNS-Manager-Konsolenstruktur mit der Maustaste die forward-Lookupzone, und klicken Sie dann auf **neuer Host (A oder AAAA)**.  
  
9. Auf der **neuer Host** Seite, lassen Sie die **Namen** Feld leer, geben Sie die Intranet-IP-Adresse des Servers, auf denen Exchange Server ausgeführt wird, und klicken Sie dann auf **Host hinzufügen**.  
  
    > [!NOTE]
    >  Beim Verlassen der **Namen** vornehmen, der Server wird standardmäßig die Namen der übergeordneten Domäne verwendet.  
  
10. Auf der **neuer Host** auf **Fertig**.  
  
> [!NOTE]
>  Wenn Sie ActiveSync verwenden, jedoch nicht die e-Mail für einige Postfachkonten synchronisieren, zu bestimmen, ob diese Konten Mitglieder einer oder mehrerer geschützter Gruppen wie z. B. Domänen-Admins sind. Weitere Informationen, mit denen Sie dieses Problem zu beheben kann, finden Sie [Exchange ActiveSync zurückgegebenen Fehler HTTP 500](https://technet.microsoft.com/library/dd439375\(EXCHG.80\).aspx).  
  
## <a name="related-topics"></a>Verwandte Themen  
 Weitere Informationen zur Integration eines lokalen Exchange-Servers finden Sie unter den folgenden Abschnitten.  
  
### <a name="what-happens-if-i-disable-exchange-integration"></a>Was geschieht, wenn ich die Exchange-Integration deaktiviere?  
 Wenn Sie die Integration in einen lokalen Exchange-Server deaktivieren, sind Sie werden nicht mehr in der Windows Server Essentials-Dashboard anzeigen, erstellen oder Verwalten von Exchange Server-Postfächer verwenden können.  
  
### <a name="what-do-i-need-to-know-about-email-accounts"></a>Was muss ich über e-Mail-Konten wissen?  
 Eine gehostete e-Mail-Lösung wird auf dem Server konfiguriert. Eine Lösung vom Anbieter einer gehosteten e-Mail, z. B. Microsoft Office 365, kann einzelne e-Mail-Konten für Netzwerkbenutzer bereitstellen. Wenn Sie die Add a User Account Wizard in Windows Server Essentials zum Erstellen eines Benutzerkontos ausführen, versucht der Assistent das Benutzerkonto, das die verfügbaren gehosteten e-Mail-Lösung hinzu. Zur gleichen Zeit wird der Assistent weist einen e-Mail-Namen (Alias) für den Benutzer und legt die maximale Größe der Mailbox (Quote) fest. Die maximale Größe des Postfachs variiert je nach den e-Mail-Anbieter, den Sie verwenden. Nachdem das Benutzerkonto hinzugefügt haben, können Sie weiterhin die Postfachinformationen Alias- und Kontingent auf der Eigenschaftenseite für den Benutzer zu verwalten. Verwenden Sie für die vollständige Verwaltung von Benutzerkonten und des gehosteten e-Mail-Anbieter die Verwaltungskonsole des gehosteten Anbieters. Je nach Anbieter können Sie die Verwaltungskonsole über ein webbasiertes Portal oder über eine Registerkarte im serverdashboard zugreifen.  
  
 Der Alias, den Sie bereitstellen, wenn Sie dem Hinzufügen einer Benutzerkonten-Assistent ausgeführt wird als vorgeschlagener Name für den Benutzeralias an den gehosteten e-Mail-Anbieter gesendet. Wenn der Alias des Benutzers ist z. B. *FrankM*, die e-Mail-Adresse des Benutzers s möglicherweise * FrankM@Contoso.com *.  
  
 Darüber hinaus wird das Kennwort, das Sie für den Benutzer in der Add a User Account Wizard festlegen, das Kennwort des Benutzers in der gehosteten e-Mail-Lösung sein.  
  
 Schließlich, wenn Sie den Benutzer löschen, mit der Delete a User Account Wizard auf dem Server, sendet der Assistent auch eine Anforderung an gehosteten e-Mail-Anbieter auf dem System auch löschen. Der Anbieter löscht unter Umständen das Benutzerkonto s und die e-Mail, die dem Konto zugeordnet ist.  
  
 Benutzerinformationen zum Einrichten der erforderlichen e-Mail-Client-Software oder wie Sie ein e-Mail-Konto zugreifen finden Sie in der Hilfe von Ihrem gehosteten e-Mail-Anbieter bereitgestellt.  
  
### <a name="what-is-a-mailbox-quota"></a>Was ist ein Postfachkontingent?  
 Die Menge an Speicherplatz, der für einen Netzwerkbenutzer s Daten für Exchange-Postfach zugeordnet ist, wird als Postfachkontingent bezeichnet.  
  
 Beim Ausführen der **Exchange Server-Integration einrichten** Aufgabe auf dem Dashboard den Assistenten Konto hinzufügen, die Sie auswählen, ob Sie Postfachkontingente erzwingen und die Kontingentgröße angeben können, eine Seite hinzugefügt. Standardmäßig die **Postfachkontingente** aktiviert ist (ein), und Benutzerpostfächern werden 2 GB Speicherplatz zugewiesen. Exchange-Administratoren können den Postfach-Kontingentvorlage die Bedürfnisse ihres Unternehmens anpassen.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Systemanforderungen für Windows Server Essentials](../get-started/system-requirements.md)  
  
-   [Verwalten der Integration der E-Mail-Dienst](Manage-Email-Service-Integration-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
