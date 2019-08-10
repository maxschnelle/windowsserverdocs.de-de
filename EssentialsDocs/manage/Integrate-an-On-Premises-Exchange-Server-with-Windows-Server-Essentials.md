---
title: Integration eines lokalen Exchange-Servers mit Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
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
ms.openlocfilehash: 142ae8514a6a480f8181ce193c2f437e2f286e2d
ms.sourcegitcommit: 0e3c2473a54f915d35687d30d1b4b1ac2bae4068
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68914607"
---
# <a name="integrate-an-on-premises-exchange-server-with-windows-server-essentials"></a>Integration eines lokalen Exchange-Servers mit Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Diese Anleitung enthält Informationen und grundlegende Anweisungen zur Einrichtung und Integration eines lokalen Servers, auf dem Exchange Server ausgeführt wird, und eines Servers, auf dem Windows Server Essentials ausgeführt wird.  

 Lesen Sie diese Anleitung vor dem Bereitstellen eines lokalen Servers, auf dem Exchange Server in einem Windows Server Essentials-Netzwerk ausgeführt wird.  

> [!NOTE]
>  Für Exchange Server 2010 wird die Installation nicht auf Computern unterstützt, auf denen Windows Server 2012 ausgeführt wird.  

## <a name="prerequisites"></a>Vorraussetzungen  
 Stellen Sie vor dem Installieren von Exchange Server in einem Windows Server Essentials-Netzwerk sicher, dass Sie die in diesem Abschnitt beschriebenen Aufgaben ausführen.  

-   [Einrichten eines Servers, auf dem Windows Server Essentials ausgeführt wird](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SetUpSBS8)  

-   [Vorbereiten eines zweiten Servers, auf dem Exchange Server installiert werden soll](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SecondServer)  

-   [Konfigurieren des Internet Domänen Namens](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_DomainNames)  

###  <a name="BKMK_SetUpSBS8"></a>Einrichten eines Servers, auf dem Windows Server Essentials ausgeführt wird  
 Es muss bereits ein Server eingerichtet worden sein, auf dem Windows Server Essentials ausgeführt wird. Dies ist der Domänencontroller für den Server, auf dem Exchange Server ausgeführt wird. Weitere Informationen zum Einrichten von Windows Server Essentials finden Sie unter [Install Windows Server Essentials](../install/Install-Windows-Server-Essentials.md).  

###  <a name="BKMK_SecondServer"></a>Vorbereiten eines zweiten Servers, auf dem Exchange Server installiert werden soll  
 Sie müssen Exchange Server auf einem zweiten Server mit einer Version des Windows Server-Betriebssystems installieren, von dem die Ausführung von Exchange Server 2010 oder Exchange Server 2013 offiziell unterstützt wird. Anschließend müssen Sie für den zweiten Server den Beitritt zur Windows Server Essentials-Domäne durchführen.  

 Informationen dazu, wie Sie einen zweiten Server der Windows Server Essentials-Domäne hinzufügen, finden Sie unter Verbinden eines zweiten Servers mit dem Netzwerk in " [Verbindung](../use/Get-Connected-in-Windows-Server-Essentials.md)herstellen".  

> [!NOTE]
>  Von Microsoft wird das Installieren von Exchange Server auf einem Server, auf dem Windows Server Essentials ausgeführt wird, nicht unterstützt.  

###  <a name="BKMK_DomainNames"></a>Konfigurieren des Internet Domänen Namens  
 Zum Integrieren eines lokalen Servers, auf dem Exchange Server mit Windows Server Essentials ausgeführt wird, müssen Sie für Ihr Unternehmen bereits einen gültigen Internetdomänennamen (z. B. *contoso.com*) registriert haben. Außerdem müssen Sie in Zusammenarbeit mit Ihrem Domänennamenanbieter die DNS-Ressourceneinträge erstellen, die für Exchange Server erforderlich sind.  

 Wenn der Internetdomänenname Ihres Unternehmens z. B. %%amp;quot;contoso.com%%amp;quot; lautet und Sie den vollqualifizierten Domänennamen (FQDN) *mail.contoso.com* zum Verweisen auf den lokalen Server mit Exchange Server verwenden möchten, sollten Sie sich wegen der Erstellung der in der folgenden Tabelle aufgeführten DNS-Ressourceneinträge an Ihren Domänennamenanbieter wenden.  


| Name des Ressourceneintrags |     Typ des Eintrags     |                                                                         Einstellung des Eintrags                                                                          |                                                                                                                                                                                                                                                              Beschreibung                                                                                                                                                                                                                                                              |
|----------------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         mail         |      Host (A)       |                                                        Address=*Vom Anbieter (ISP) zugewiesene öffentliche IP-Adresse*                                                         |                                                                                                                                                                                                   An %%amp;quot;mail.contoso.com%%amp;quot; adressierte E-Mails werden von Exchange Server empfangen.<br /><br /> Sie können auch einen anderen Namen wählen.                                                                                                                                                                                                    |
|          MX          | Mail-Exchanger (MX) |                                            Hostname=@<br /><br /> Address=mail.contoso.com<br /><br /> Preference=0                                             |                                                                                                                                                                                                      Ermöglicht das Senden von e email@contoso.com -Mail-Nachrichten für Ihren lokalen Server, auf dem Exchange Server ausgeführt wird.                                                                                                                                                                                                       |
|         SPF          |     Text (TXT)      |                                                                        v=spf1 a mx ~all                                                                         |                                                                                                                                                                                                                      Ressourceneintrag, mit dem verhindert wird, dass von Ihrem Server gesendete E-Mail-Nachrichten als Spam identifiziert werden.                                                                                                                                                                                                                      |
|  autodiscover._tcp   |    Dienst (SRV)    | Service: _autodiscover<br /><br /> Protocol: _tcp<br /><br /> Priorität: 0<br /><br /> Gewichtung: 0<br /><br /> Port: 443<br /><br /> Target host: mail.contoso.com | Ermöglicht Microsoft Office Outlook und mobilen Geräten die automatische Ermittlung Ihres lokalen Servers, auf dem Exchange Server ausgeführt wird.<br /><br /> **Hinweis**: Sie können auch einen Ressourcen Daten Satz für den automatische Erkennung-Host (A) konfigurieren und den Datensatz auf die öffentliche IP-Adresse Ihres lokalen Servers verweisen, auf dem Exchange Server ausgeführt wird. Wenn Sie diese Option implementieren, müssen Sie auch ein SSL-Zertifikat vom Typ %%amp;quot;alternativer Antragstellername%%amp;quot; bereitstellen, das sowohl den Domänennamen %%amp;quot;mail.contoso.com%%amp;quot; als auch %%amp;quot;autodiscover.contoso.com%%amp;quot; unterstützt. |

> [!NOTE]
>  -   Ersetzen Sie die Instanzen von *contoso.com* in diesem Beispiel durch den Internetdomänennamen, den Sie registriert haben.  

 Sie müssen für den lokalen Server mit Exchange Server einen anderen FQDN als jenen FQDN wählen, den Sie für den Server mit Windows Server Essentials verwenden. Beispielsweise können Sie *remote.contoso.com* als FQDN wählen, mit dem Computer über das Internet auf den Server zugreifen, auf dem Windows Server Essentials ausgeführt wird. Sie können *mail.contoso.com* als FQDN zum Weiterleiten von E-Mail-Nachrichten auf Ihren lokalen Server mit Exchange Server verwenden.  

## <a name="install-exchange-server"></a>Installieren von Exchange Server  
 Vom Exchange Server-Integrationsfeature werden unter Windows Server Essentials die folgenden Versionen von Exchange Server unterstützt:  

- Exchange Server 2013  

- Exchange Server 2010 mit Service Pack 1 (SP1)  

  Bevor Sie Exchange Server auf dem zweiten Server installieren, müssen Sie zuerst das aktuelle Administratorkonto der Gruppe **Enterprise Admins** hinzufügen.  

#### <a name="to-add-the-current-administrator-account-to-the-enterprise-admins-group"></a>So fügen Sie das aktuelle Administratorkonto der Gruppe %%amp;quot;Organisations-Admins%%amp;quot; hinzu  

1.  Melden Sie sich bei Windows Server Essentials als Administrator an.  

2.  Führen Sie Windows PowerShell als Administrator aus.  

3.  Geben Sie an der Windows PowerShell-Eingabeaufforderung **Add-adgroupmember "Enterprise Admins" $ENV: username**ein, und drücken Sie dann die EINGABETASTE.  

#### <a name="to-install-exchange-server"></a>So installieren Sie Exchange Server  

1.  Melden Sie sich am zweiten Server als Administrator an.  

2.  Öffnen Sie den Internetbrowser, und navigieren Sie zur Website mit dem [Bereitstellungs-Assistenten für Exchange Server](https://go.microsoft.com/fwlink/p/?LinkID=249163) .  

3.  Klicken Sie auf **On-Premises Only**.  

4.  Klicken Sie auf die Option zur Neuinstallation für die Version von Exchange Server, die Sie installieren möchten.  

    > [!NOTE]
    >  Wenn Sie eine Migration von einer Windows Small Business Server-Installation durchführen, wählen Sie die entsprechende Upgradeoption mit den Migrationsschritten aus.  

5.  Übernehmen Sie auf der nächsten Seite die Standardeinstellungen, und klicken Sie auf **Weiter**.  

    > [!NOTE]
    >  Falls Sie für die Neuinstallation von Exchange Server öffentliche Ordner verwenden möchten, ändern Sie die entsprechende Einstellung in **Ja**.  

6.  Befolgen Sie die Schritt-für-Schritt-Anleitung der Prüfliste, um Exchange Server bereitzustellen.  

     Mit dem Bereitstellungs-Assistenten für Exchange Server haben Sie außerdem folgende Möglichkeiten:  

    -   Drucken der Prüfliste  

    -   Senden der Prüfliste an einen Empfänger per E-Mail  

    -   Herunterladen der Prüfliste als PDF-Datei  

> [!NOTE]
> - Auf dem Server, auf dem Exchange Server ausgeführt wird, müssen Sie immer die Installation der Verwaltungstools auswählen. Die Verwaltungstools sind für das Exchange Server-Integrationsfeature unter Windows Server Essentials erforderlich.  
>   -   Falls Sie virtuelle Verzeichnisse konfigurieren müssen, wird empfohlen, die **InternalUrl** -Eigenschaft für jedes virtuelle Verzeichnis zusätzlich auf dieselbe URL wie die **ExternalUrl** -Eigenschaft festzulegen. Weitere Informationen finden Sie unter [Verwaltung für virtuelle Verzeichnisse](https://go.microsoft.com/fwlink/p/?LinkId=251058) in der Onlinehilfe zu Exchange Server 2010.  
>   -   Wenn Sie in Windows Server Essentials über die Website für den Remotewebzugriff auf Outlook Web Access (OWA) zugreifen möchten, müssen Sie die ExternalUrl-Eigenschaft für OWA festlegen.  

 Falls Sie Exchange Server 2010 im Rahmen eines vollständig neuen Setups installieren, können Sie zum Einrichten von Exchange Server auch die unten angegebenen Skripts verwenden.  

#### <a name="to-use-scripts-to-set-up-exchange-server"></a>So verwenden Sie Skripts zum Einrichten von Exchange Server  

1.  Öffnen Sie den Editor, und fügen Sie das folgende Skript in eine neue Datei ein:  

```powershell
Import-Module ServerManager

Add-WindowsFeature NET-Framework,RSAT-ADDS,Web-Server,Web-Basic-Auth,Web-Windows-Auth,Web-Metabase,Web-Net-Ext,Web-Lgcy-Mgmt-Console,WAS-Process-Model,RSAT-Web-Server,Web-ISAPI-Ext,Web-Digest-Auth,Web-Dyn-Compression,NET-HTTP-Activation,Web-Asp-Net,Web-Client-Auth,Web-Dir-Browsing,Web-Http-Errors,Web-Http-Logging,Web-Http-Redirect,Web-Http-Tracing,Web-ISAPI-Filter,Web-Request-Monitor,Web-Static-Content,Web-WMI,RPC-Over-HTTP-Proxy  Restart
```

2. Speichern Sie die Datei unter dem Namen **InstallDependencies.ps1**.  

3. Kopieren Sie das Exchange-SSL-Zertifikat an einen Speicherort auf dem Server.  

4. Öffnen Sie im Editor eine neue Datei, und kopieren Sie den folgenden Text in die Datei:  

```powershell
param (
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "The path to your Certificate file, must be a *.pfx format")]
    $CertPath = "c:\certificates\ExchangeCertificate.pfx",
    [Security.SecureString]
    [Parameter(Mandatory=$true, HelpMessage = "The password of your cert")]
    $CertPassword = $null,
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Domain Name, eg. contoso.com")]
    $DomainName = "contoso.com",
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Server IP Address, eg. 192.168.0.1")]
    $ServerIpAddress = "192.168.0.1",
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Internal Ip Range, eg. 192.168.0.0-192.168.0.255")]
    $InternalIpRange = "192.168.0.0-192.168.0.255"
)

#Import Exchange Certificate, and Enable it for POP IIS IMAP SMTP services.

Import-ExchangeCertificate  -FileData ([Byte[]]$(Get-content -Path $CertPath  -Encoding byte  -ReadCount 0)) -Password:$CertPassword -Force | Enable-ExchangeCertificate -Services 'POP, IIS, IMAP, SMTP' -Force

#New AcceptedDomain and set it to default

New-AcceptedDomain  -Name "official name"  -DomainName $domainname

Set-AcceptedDomain  -Identity "official name"  -MakeDefault $true

#New EmailAddress Policy

$address = "%m@" + $DomainName

New-EmailAddressPolicy -Name "Windows Server Essentials Email Address Policy" -IncludedRecipients AllRecipients -EnabledPrimarySMTPAddressTemplate $address

#Set owa and ecp VirtualDirectory ExternalUrl

$hostname = "mail." + $DomainName

$owa = "https://" + $hostname + "/owa"

$ecp = "https://" + $hostname + "/ecp"

$activesync = "https://" + $hostname + "/Microsoft-Server-ActiveSync"

$oab = "https://" + $hostname + "/OAB"

$ews = "https://" + $hostname + "/EWS/Exchange.asmx"

Get-OwaVirtualDirectory | Set-OwaVirtualDirectory  -ExternalUrl $owa  -InternalUrl $owa

Get-EcpVirtualDirectory | Set-EcpVirtualDirectory  -ExternalUrl $ecp  -InternalUrl $ecp

Get-ActiveSyncVirtualDirectory | Set-ActiveSyncVirtualDirectory -ExternalUrl $activesync  -InternalUrl $activesync

Get-OABVirtualDirectory | Set-OABVirtualDirectory -ExternalUrl $oab -InternalUrl $oab -RequireSSL:$true

Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -ExternalUrl $ews -InternalUrl $ews -BasicAuthentication:$True -Force

#Enable outlook Anywhere

Enable-OutlookAnywhere  -ClientAuthenticationMethod:Basic  -ExternalHostname:$hostname  -SSLOffloading:$false

#new receive/send connector

$machinename = get-content env:computername

$bindingIpaddress = $ServerIpAddress + ":25"

$ReceiveConnectorName = $machinename + "\Default " + $machinename

Set-ReceiveConnector $ReceiveConnectorName -RemoteIPRanges $InternalIpRange

New-ReceiveConnector -Name "WSE Internet Receive Connector" -Usage "Internet" -Bindings $bindingIpaddress -Fqdn $hostname -Enabled $true -Server $machinename -AuthMechanism Tls,BasicAuth,BasicAuthRequireTLS,Integrated

New-SendConnector -Name "WSE Internet SendConnector" -Usage "Internet" -AddressSpaces 'SMTP:*;1' -IsScopedConnector $false -DNSRoutingEnabled $true -UseExternalDNSServersEnabled $true -SourceTransportServers $machinename
```

5. Legen Sie die Parameter am Anfang des Skripts gemäß Ihrer Netzwerkumgebung fest.  

6. Speichern Sie die Datei unter dem Namen **ConfigureExchange.ps1**.  

7. Führen Sie Windows PowerShell als Administrator aus.  

8. Geben Sie an der Windows PowerShell-Eingabeaufforderung **Set-ExecutionPolicy RemoteSigned**ein, und drücken Sie die EINGABETASTE.  

9. Führen Sie das Skript **InstallDependencies.ps1**aus.  

10. Starten Sie den Server neu, und führen Sie dann Windows PowerShell als Administrator aus.  

11. Führen Sie an der Windows PowerShell-Eingabeaufforderung das folgende Skript aus:  

    `E:\setup.com /mode:install /roles:mb,ht,ca /OrganizationName:"First Organization"`  

   > [!NOTE]
   >  Achten Sie darauf, dass Sie den richtigen Pfad zum Exchange Server-Setupprogramm eingeben.  

12. Öffnen Sie nach Abschluss des Exchange Server-Setups die Exchange-Verwaltungsshell als Administrator.  

13. Geben Sie an der Exchange-Verwaltungsshell-Eingabeaufforderung **Set-ExecutionPolicy RemoteSigned** ein, und drücken Sie die EINGABETASTE.  

14. Führen Sie das Skript **ConfigureExchange.ps1**aus.  

15. Starten Sie den Server neu.  

> [!NOTE]
>  Wenn Sie anstelle eines selbst ausgegebenen Zertifikats ein öffentlich vertrauenswürdiges SSL-Zertifikat verwenden möchten, können Sie die Anweisungen im Installationshandbuch befolgen, um eine Zertifikat Anforderung zu erstellen und an die ausgewählte Zertifizierungsstelle zu senden. Sie können auch ein Exchange PowerShell-Cmdlet verwenden, um eine Zertifikatanforderung zu erstellen. Unten ist ein Beispiel angegeben.  
>   
>  `New-ExchangeCertificate -GenerateRequest -SubjectName "C=US, S=Washington, L=Redmond, O=contoso, OU=contoso, CN=mail.contoso.com" -DomainName mail.contoso.com -PrivateKeyExportable $true | Set-Content -path "c:\Docs\MyCertRequest.req"`  
>   
>  Passen Sie die Skriptparameter gemäß Ihrer Netzwerkumgebung an.  

## <a name="post-installation-tasks"></a>Nach der Installation durchzuführende Schritte  
 In diesem Abschnitt werden Schritte der Serverkonfiguration beschrieben, die Sie nach der Installation möglicherweise durchführen müssen. Er enthält spezielle Informationen zur Einrichtung eines lokalen Servers, auf dem Exchange Server in einem Windows Server Essentials-Netzwerk ausgeführt wird.  

### <a name="add-the-public-email-domain-and-configure-the-email-address-policies"></a>Hinzufügen der öffentlichen E-Mail-Domäne und Konfigurieren der E-Mail-Adressrichtlinien  

> [!NOTE]
>  Wenn Sie ein vollständig neues Setup durchführen, ist dies ein erforderlicher Schritt. Sie können diesen Schritt überspringen, wenn Sie die Migration von Windows Small Business Server durchführen.  

 Sie müssen die E-Mail-Domäne als akzeptierte Standarddomäne angeben und dann die E-Mail-Adressrichtlinie konfigurieren.  

##### <a name="to-add-your-email-domain-as-the-default-accepted-domain"></a>So fügen Sie die E-Mail-Domäne als akzeptierte Standarddomäne hinzu  

1.  Führen Sie die Schritte im Exchange Server-Artikel [Erstellen einer akzeptierten Domäne](https://go.microsoft.com/fwlink/p/?LinkId=249174) aus, um eine akzeptierte Domäne hinzuzufügen.  

2.  Melden Sie sich am zweiten Server als Administrator an, öffnen Sie die Exchange-Verwaltungskonsole, und navigieren Sie unter **Organisationskonfiguration** zur Registerkarte **Hub-Transport**.  

3.  Klicken Sie im Arbeitsbereich der Exchange-Verwaltungskonsole mit der rechten Maustaste auf die neue akzeptierte Domäne, und klicken Sie dann auf **Als Standard festlegen**.  

4.  Führen Sie die Schritte im Exchange Server-Artikel [Erstellen einer E-Mail-Adressrichtlinie](https://go.microsoft.com/fwlink/p/?LinkId=249179) aus, um eine neue E-Mail-Adressrichtlinie zu erstellen. Mit Ausnahme der E-Mail-Adresse können Sie alle Standardwerte akzeptieren. Geben Sie als E-Mail-Adresse Ihre öffentliche E-Mail-Domäne an.  

### <a name="create-smtp-send-and-receive-connectors"></a>Erstellen von SMTP-Sende- und -Empfangsconnectors  

> [!NOTE]
>  Dies ist eine erforderliche Aufgabe.  

 Sie müssen einen SMTP-Sendeconnector und einen SMTP-Empfangsconnector für die ausgehende und eingehende Übertragung von E-Mail-Nachrichten konfigurieren.  

 Führen Sie zum Erstellen eines SMTP-Sendeconnectors die Schritte im Exchange Server-Artikel [Erstellen eines SMTP-Sendeconnectors](https://technet.microsoft.com/library/aa997285.aspx)aus.  

 Führen Sie zum Erstellen eines SMTP-Empfangsconnectors die Schritte im Exchange Server-Artikel [Erstellen eines SMTP-Empfangsconnectors](https://technet.microsoft.com/library/bb125159.aspx)aus.  

 Sie können auch auf das Skript weiter oben in diesem Dokument zurückgreifen, um die Sende- und Empfangsconnectors mithilfe von Exchange PowerShell-Cmdlets zu erstellen.  

### <a name="configure-the-network-router"></a>Konfigurieren des Netzwerkrouters  

> [!NOTE]
>  Wenn Sie ein vollständig neues Setup durchführen, ist dies ein erforderlicher Schritt. Wenn Sie von Windows Small Business Server migrieren, finden Sie unter [Migrate Server Data to Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md) Anweisungen zum Konfigurieren des Netzwerks.  

 Auf dem Router müssen mindestens die folgenden Porteinstellungen konfiguriert sein:  

|Routerport|Ziel-IP|Zielport|Hinweis|  
|-----------------|--------------------|----------------------|----------|  
|25 (SMTP)|Interne IP-Adresse des lokalen Servers, auf dem Exchange Server ausgeführt wird.|25||  
|80 (HTTP)|Interne IP-Adresse des Servers, auf dem Windows Server Essentials ausgeführt wird|80||  
|443 (HTTPS)|Interne IP-Adresse des Servers, auf dem Windows Server Essentials ausgeführt wird|443||  

 Wenn in Ihrem Netzwerk die Messaging-Protokolle POP3 oder IMAP unterstützt werden, müssen Sie auch Portweiterleitungen für diese Protokolle konfigurieren. Weitere Informationen hierzu finden Sie in der technischen Bibliothek zu Exchange Server im Thema **Exchange-Netzwerkportreferenz** unter [Clientzugriffsserver](https://go.microsoft.com/fwlink/p/?LinkId=250773) .  

> [!NOTE]
> - Wir empfehlen Ihnen die Konfiguration statischer IP-Adressen für den Server, auf dem Windows Server Essentials ausgeführt wird, und für den zweiten Server, auf dem Exchange Server ausgeführt wird. Eine Anleitung zur Konfiguration einer statischen IP-Adresse auf einem Computer mit Windows Server 2003 oder Windows Server 2008 R2 finden Sie in der technischen Bibliothek zu Windows Server unter [Konfigurieren einer statischen IP-Adresse](https://technet.microsoft.com/library/cc754203\(v=ws.10\).aspx) .  
> 
>   **Hinweis**: Für die DNS-Servereinstellung sollte immer auf die IP-Adresse des Servers verwiesen werden, auf dem Windows Server Essentials ausgeführt wird.  
>   -   Stellen Sie auf dem Router sicher, dass die IP-Adressen auf dem Server mit Windows Server Essentials und dem Server mit Exchange Server entweder reserviert sind oder außerhalb des DHCP-IP-Adressbereichs liegen.  
>   -   Für die Routerkonfiguration in diesem Abschnitt wird vorausgesetzt, dass Ihnen von Ihrem Internetdienstanbieter (Internet Service Provider, ISP) nur eine öffentliche IP-Adresse zugewiesen wurde. Falls Sie über mehrere öffentliche IP-Adressen verfügen, können Sie dem Server mit Windows Server Essentials und dem Server mit Exchange Server jeweils eine andere IP-Adresse zuweisen und dann basierend auf den öffentlichen IP-Adressen Portweiterleitungen erstellen.  

### <a name="enable-on-premises-exchange-server-integration-on-windows-server-essentials"></a>Aktivieren der lokalen Exchange Server-Integration in Windows Server Essentials  

> [!NOTE]
>  Wenn Sie eine Migration von einer Windows Small Business Server-Installation durchführen, empfehlen wir Ihnen das Überspringen dieses Schritts an dieser Stelle. Führen Sie ihn später aus, nachdem Sie die vorherige Installation von Exchange Server auf dem Quellserver deinstalliert haben.  

 Nach dem Installieren und Konfigurieren eines Servers, auf dem Exchange Server ausgeführt wird, müssen Sie die lokale Exchange Server-Integration auf dem Server aktivieren, auf dem Windows Server Essentials ausgeführt wird.  

##### <a name="to-enable-on-premises-exchange-server-integration-from-the-dashboard"></a>So aktivieren Sie die lokale Exchange Server-Integration über das Dashboard  

1.  Melden Sie sich an dem Server, auf dem Windows Server Essentials ausgeführt wird, als Administrator an, und öffnen Sie das Dashboard.  

2.  Klicken Sie auf der Seite **Home** auf **Connect to My Email Service** (Mit meinem E-Mail-Dienst verbinden) und dann auf **Integrate your Exchange Server** (Exchange Server integrieren).  

3.  Klicken Sie im Informationsbereich auf **Set up Exchange Server Integration**(Exchange Server-Integration einrichten).  

4.  Befolgen Sie die Anweisungen im Assistenten.  

### <a name="configure-a-reverse-proxy"></a>Konfigurieren eines Reverseproxys  

> [!NOTE]
>  Dies ist ein erforderlicher Schritt, wenn Sie nur über eine einzelne Internetverbindung Ihres Internetdienstanbieters verfügen.  

 Sowohl von Windows Server Essentials als auch von Exchange Server werden Remotezugriffsszenarios für Netzwerkbenutzer unterstützt. Wenn Sie beispielsweise "Zugriff überall" auf dem Server aktivieren, auf dem Windows Server Essentials ausgeführt wird, können Sie die Remotewebzugriff-Website per Remotezugriff erreichen oder VPN (virtuelles privates Netzwerk) nutzen, um eine Remoteverbindung mit dem Windows Server Essentials-Netzwerk herzustellen. Für den Remotezugriff auf E-Mail-Nachrichten müssen Sie Outlook Anywhere, Outlook Web Access (OWA) oder ActiveSync verwenden.  

 Falls Windows Server Essentials und der Server mit Exchange Server jeweils mit demselben Router verbunden sind und nur eine eingehende Internetverbindung von Ihrem Internetdienstanbieter zum Router besteht, müssen Sie eine Reverseproxylösung einsetzen, um unterschiedliche Arten von Remotezugriffsanforderungen aus dem Internet basierend auf den Zielhostnamen weiterzuleiten. Wir empfehlen Ihnen als Reverseproxylösung die Verwendung der von Microsoft unterstützten IIS-Erweiterung für das Routing von Anwendungsanforderungen (Application Request Routing, ARR). Weitere Informationen zum IIS Application Request Routing finden Sie auf der [Website zum Application Request Routing](https://go.microsoft.com/fwlink/p/?LinkId=249181).  

##### <a name="to-install-and-configure-application-request-routing"></a>So installieren und konfigurieren Sie das Routing von Anwendungsanforderungen (Application Request Routing)  

1. Melden Sie sich bei Windows Server Essentials als Administrator an.  

2. Öffnen Sie den Internetbrowser, und navigieren Sie zur [Website zum Application Request Routing](https://go.microsoft.com/fwlink/p/?LinkId=249181).  

3. Klicken Sie auf der ARR-Website auf die Schaltfläche **Install**(Installieren), und führen Sie die Schritte zur Installation von ARR aus.  

   > [!NOTE]
   >  Während der ARR-Installation müssen Sie das URL-Rewrite-Module auswählen.  
   >   
   >  Möglicherweise wird am Ende der ARR-Installation der Fehler angezeigt, dass %%amp;quot;KB 2589179 für ARR 2.5 nicht installiert werden konnte%%amp;quot;. Sie können diesen Fehler ignorieren.  

4. Starten Sie den Dienst **Remotedesktopgateway** nach Abschluss der ARR-Installation neu, wenn er nicht ausgeführt wird.  

   > [!NOTE]
   >  Nach der Installation von ARR befindet sich der Dienst **Remotedesktopgateway** möglicherweise im beendeten Zustand. Öffnen Sie zum manuellen Neustarten des Diensts das Verwaltungstool **Dienste**, und starten Sie den Dienst **Remotedesktopgateway** neu.  

5. [Laden Sie KB2732764 für ARR 2.5 herunter](https://go.microsoft.com/fwlink/?LinkID=258302), und installieren Sie dann das Update auf dem Server, auf dem Windows Server Essentials ausgeführt wird.  

6. Kopieren Sie die SSL-Zertifikatdatei für Exchange Server auf den Server, auf dem Windows Server Essentials ausgeführt wird. Die Zertifikatdatei muss den privaten Schlüssel enthalten und im PFX-Dateiformat vorliegen.  

   > [!NOTE]
   >  Führen Sie bei Verwendung eines selbst ausgegebenen Zertifikats die Anweisungen zum Exportieren des Zertifikats im Exchange Server-Artikel [Exportieren eines Exchange-Zertifikats](https://technet.microsoft.com/library/dd351274.aspx) aus.  

7. Führen Sie je nach Version von Windows Server Essentials, die Sie ausführen, die folgenden Schritte aus:  

   -   Unter Windows Server Essentials: Öffnen Sie ein Befehlsfenster mit Administratorrechten, und öffnen Sie dann das Verzeichnis "%ProgramFiles%\Windows Server\Bin".  

   -   Unter Windows Server Essentials: Öffnen Sie ein Befehlsfenster mit Administratorrechten, und öffnen Sie dann das Verzeichnis "%Windir%\System32\Essentials".  

8. Führen Sie basierend auf Ihrem Installationsszenario einen der folgenden Schritte zur Konfiguration von ARR aus:  

   - Führen Sie bei einem vollständig neuen Setup den folgenden Befehl aus:  

      **Arrconfig-Konfiguration-CERT** _Pfad zur Zertifikat Datei_ **-hostnames** _Hostnamen für Exchange Server_  

     > [!NOTE]
     >  Beispiel: **Arrconfig-Konfiguration-CERT** _c:\temp\certificate.pfx_ **-hostnames** _Mail.contoso.com_  
     > 
     >  Ersetzen Sie *mail.contoso.com* durch den Namen Ihrer Domäne, die durch das Zertifikat geschützt ist.  

   - Führen Sie den folgenden Befehl bei einer Migration von Windows Small Business Server aus:  

      **Arrconfig-Konfiguration-CERT** _Pfad zur Zertifikat Datei_ **-hostnames** _Hostnamen für Exchange Server_ **-TargetServer** _Servername von Exchange Server_  

      Beispiel: **Arrconfig-Konfiguration-CERT** _c:\temp\certificate.pfx_ **-hostnames** _Mail.contoso.com_ * *-TargetServer * * _ExchangeSvr_  

      Ersetzen Sie *mail.contoso.com* durch den Namen Ihrer Domäne. Ersetzen Sie *ExchangeSvr* durch den Namen des Servers, auf dem Exchange Server ausgeführt wird.  

9. Geben Sie das Kennwort für das Zertifikat ein, wenn Sie dazu aufgefordert werden.  

> [!NOTE]
> - Die von Ihnen angegebenen Hostnamen müssen in dem SSL-Zertifikat enthalten sein, das Sie für Exchange Server erworben haben.  
>   -   Fügen Sie bei Verwendung mehrerer Hostnamen als Trennzeichen jeweils ein Komma (,) ein.  

 Um zu überprüfen, ob die Konfiguration funktioniert, versuchen Sie, auf die OWA-Website für Ihren Server zuzugreifen https://mail, auf dem Exchange Server ausgeführt wird (. *Name_Ihrer_Domäne*.com/owa) von einem Computer aus zuzugreifen, der nicht Mitglied der Domäne ist. Zur Behandlung von Verbindungsproblemen können Sie auch das Onlinetool [Microsoft-Remoteverbindungsuntersuchung](https://go.microsoft.com/fwlink/p/?LinkId=249455) verwenden.  

### <a name="configure-split-dns-for-exchange-server"></a>Konfigurieren einer DNS-Aufteilung für Exchange Server  

> [!NOTE]
>  Dies ist ein empfohlener Schritt.  

 Mithilfe der DNS-Aufteilung (Split DNS) können Sie für einen Hostnamen im DNS unterschiedliche IP-Adressen konfigurieren, die in Abhängigkeit davon verwendet werden, woher die DNS-Anforderung stammt. Wenn sich der Clientcomputer im Intranet befindet, wird die DNS-Anforderung zu einer Intranet-IP-Adresse aufgelöst. Wenn sich der Clientcomputer im Internet befindet, wird die DNS-Anforderung zu einer Internet-IP-Adresse aufgelöst. Dies ist für Benutzer transparent.  

 Wir empfehlen Ihnen eine Konfiguration der DNS-Aufteilung, bei der Benutzer unabhängig vom Standort immer den gleichen Hostnamen verwenden können, um auf Exchange Server zuzugreifen.  

##### <a name="to-configure-split-dns-for-exchange-server"></a>So konfigurieren Sie die DNS-Aufteilung für Exchange Server  

1.  Melden Sie sich an Windows Server Essentials als Administrator an, und öffnen Sie den DNS-Manager.  

2.  Klicken Sie im DNS-Manager in der Konsolenstruktur mit der rechten Maustaste auf Ihren Server, und klicken Sie dann auf **Neue Zone**. Der **Assistent zum Erstellen neuer Zonen** wird angezeigt.  

3.  Übernehmen Sie auf der Seite **Zonentyp** des Assistenten die Standardoption, und klicken Sie auf **Weiter**.  

4.  Übernehmen Sie auf der Seite **Active Directory-Zonenreplikationsbereich** die Standardoption, und klicken Sie auf **Weiter**.  

5.  Übernehmen bzw. wählen Sie auf der Seite **Forward- oder Reverse-Lookupzone** die Option **Forward-Lookupzone**, und klicken Sie auf **Weiter**.  

6.  Geben Sie auf der Seite **Zonenname** den FQDN Ihres Servers ein, auf dem Exchange Server ausgeführt wird (z. B. *mail.contoso.com*), und klicken Sie auf **Weiter**.  

7.  Übernehmen Sie auf der Seite **Dynamisches Update** die Standardoption, und klicken Sie dann auf **Weiter** und **Fertig stellen**.  

8.  Klicken Sie im DNS-Manager in der Konsolenstruktur mit der rechten Maustaste auf die neue Forward-Lookupzone, und klicken Sie dann auf **Neuer Host (A oder AAAA)** .  

9. Lassen Sie auf der Seite **Neuer Host** das Feld **Name** leer, geben Sie die Intranet-IP-Adresse des Servers ein, auf dem Exchange Server ausgeführt wird, und klicken Sie dann auf **Host hinzufügen**.  

    > [!NOTE]
    >  Wenn Sie das Feld **Name** leer lassen, wird vom Server standardmäßig der Name der übergeordneten Domäne verwendet.  

10. Klicken Sie auf der Seite **Neuer Host** auf **Fertig**.  

> [!NOTE]
>  Gehen Sie wie folgt vor, wenn Sie ActiveSync verwenden, die E-Mail-Nachrichten für einige Postfachkonten jedoch nicht synchronisieren können: Ermitteln Sie, ob die Konten Mitglieder einer oder mehrerer geschützter Gruppen sind, z. B. der Gruppe %%amp;quot;Domänen-Admins%%amp;quot;. Weitere Informationen, die für die Behebung dieses Problems hilfreich sind, finden Sie unter [Exchange ActiveSync hat den Fehler HTTP 500 zurückgegeben](https://technet.microsoft.com/library/dd439375\(EXCHG.80\).aspx).  

## <a name="related-topics"></a>Verwandte Themen  
 Weitere Informationen zur Integration eines lokalen Exchange-Servers finden Sie in den folgenden Abschnitten.  

### <a name="what-happens-if-i-disable-exchange-integration"></a>Was geschieht, wenn ich die Exchange-Integration deaktiviere?  
 Wenn Sie die Integration in einen lokalen Exchange-Server deaktivieren, können Sie das Windows Server Essentials-Dashboard nicht länger verwenden, um die Exchange Server-Postfächer anzuzeigen, zu erstellen oder zu verwalten.  

### <a name="what-do-i-need-to-know-about-email-accounts"></a>Was muss ich über E-Mail-Konten wissen?  
 Eine gehostete E-Mail-Lösung wird auf dem Server konfiguriert. Eine Lösung von einem gehosteten e-Mail-Anbieter wie Microsoft Office 365 kann einzelne e-Mail-Konten für Netzwerk Benutzer bereitstellen. Wenn Sie den Assistenten zum Hinzufügen eines Benutzerkontos in Windows Server Essentials ausführen, um ein Benutzerkonto zu erstellen, versucht der Assistent das Benutzerkonto zu der verfügbaren gehosteten E-Mail-Lösung hinzuzufügen. Zur gleichen Zeit weist der Assistent dem Benutzer einen E-Mail-Namen (Alias) zu und legt die maximale Größe der Mailbox (Quote) fest. Die maximale Größe des Postfachs variiert je nach E-Mail-Anbieter, den Sie nutzen. Nachdem das Benutzerkonto hinzugefügt wurde, können Sie die Mailbox-Alias- und Kontingent-Informationen auf der Eigenschaftenseite für den Benutzer weiterhin verwalten. Verwenden Sie für eine umfassende Verwaltung der Benutzerkonten und des gehosteten E-Mail-Anbieters die Verwaltungskonsole des gehosteten Anbieters. Je nach Anbieter können Sie auf die Verwaltungskonsole über ein webbasiertes Portal oder über eine Registerkarte im Serverdashboard zugreifen.  

 Der Alias, den Sie beim Ausführen des Assistenten zum Hinzufügen eines Benutzerkontos bereitstellen, wird als vorgeschlagener Name für den Benutzeralias an den gehosteten E-Mail-Anbieter gesendet. Wenn der Benutzeralias beispielsweise *FrankM*ist, kann die e-Mail-Adresse <em>FrankM@Contoso.com</em>des Benutzers lauten.  

 Darüber hinaus wird das Kennwort, das Sie für den Benutzer im Assistenten zum Hinzufügen eines Benutzerkontos festlegen, zum Initialkennwort des Benutzers in der gehosteten E-Mail-Lösung.  

 Wenn Sie den Benutzer löschen, indem Sie den Assistenten zum Löschen eines Benutzerkontos auf dem Server verwenden, sendet der Assistent auch eine Anforderung an den gehosteten E-Mail-Anbieter, um den Benutzer auch aus dessen System zu löschen. Der Anbieter kann sowohl das Konto des Benutzers als auch die e-Mail, die dem Konto zugeordnet ist, löschen.  

 Benutzerinformationen zum Einrichten der erforderlichen E-Mail-Client-Software oder zum Zugriff auf ein E-Mail-Konto finden Sie in der Hilfe-Dokumentation, die von Ihrem gehosteten E-Mail-Anbieter bereitgestellt wird.  

### <a name="what-is-a-mailbox-quota"></a>Was ist ein Postfachkontingent?  
 Der Speicherplatz, der für die Exchange-Post Fach Daten eines Netzwerk Benutzers zugeordnet wird, wird als Post Fach Kontingent bezeichnet.  

 Beim Ausführen der Aufgabe **Einrichten der Exchange Server-Integration** auf dem Dashboard fügt der Assistent eine Seite zum Assistenten zum Hinzufügen von Benutzerkonten hinzu. Damit können Sie wählen, ob Sie Postfachkontingente erzwingen möchten, und die Kontingentgröße angeben. Standardmäßig ist die Option **Postfachkontingente erzwingen** aktiviert, und Benutzerpostfächern werden 2 GB an Speicherplatz zugewiesen. Exchange-Administratoren können die Mailbox-Kontingenteinstellungen anpassen, um sie auf die Anforderungen ihres Unternehmens abzustimmen.  

## <a name="see-also"></a>Siehe auch  

-   [Systemanforderungen für Windows Server Essentials](../get-started/system-requirements.md)  

-   [E-Mail-Dienst Integration verwalten](Manage-Email-Service-Integration-in-Windows-Server-Essentials.md)  

-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
