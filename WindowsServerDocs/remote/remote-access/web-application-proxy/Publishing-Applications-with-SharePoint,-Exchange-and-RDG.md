---
ms.assetid: 61ed00fd-51c7-4728-91fa-8501de9d8f28
title: Veröffentlichen von Anwendungen mit SharePoint, Exchange und RDG
description: ''
author: billmath
manager: mtillman
ms.author: billmath
ms.date: 04/30/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: 21ea6ecf717392027c1d00f818e230e2fe56a11d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826821"
---
# <a name="publishing-applications-with-sharepoint-exchange-and-rdg"></a>Veröffentlichen von Anwendungen mit SharePoint, Exchange und RDG

>Gilt für: Windows Server 2016

**Dieser Inhalt ist für die lokale Version des Webanwendungsproxys relevant. Zum Aktivieren des sicheren Zugriffs auf lokale Anwendungen über die Cloud finden Sie unter den [Azure AD-Anwendungsproxy-Inhalt](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/).**  
  
Dieses Thema beschreibt die erforderlichen Aufgaben zum Veröffentlichen von SharePoint-Server, Exchange Server oder Remote Desktop Gateway (RDP) über den Webanwendungsproxy.  

>[!NOTE]
>Diese Informationen dienen als-ist.  Remote Desktop Services unterstützt und empfiehlt die Verwendung von [Azure-App-Proxy Bereitstellen von sicherem Remotezugriff auf lokale Anwendungen](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).
  
## <a name="BKMK_6.1"></a>Veröffentlichen von SharePoint Server  
Sie können eine SharePoint-Website per Webanwendungsproxy veröffentlichen, wenn die SharePoint-Website für die anspruchsbasierte Authentifizierung oder integrierte Windows-Authentifizierung konfiguriert ist. Wenn Sie Active Directory Federation Services (AD FS) für die Vorauthentifizierung verwenden möchten, müssen Sie mithilfe eines Assistenten eine vertrauende konfigurieren.  
  
-   Wenn die SharePoint-Website die anspruchsbasierte Authentifizierung verwendet, müssen Sie den Assistenten zum Hinzufügen der Vertrauensstellung der vertrauenden Seite für die Anwendung verwenden.  
  
-   Wenn die SharePoint-Website die integrierte Windows-Authentifizierung verwendet, müssen Sie den nicht anspruchsbasierten Assistenten zum Hinzufügen der Vertrauensstellung der vertrauenden Seite für die Anwendung verwenden. IWA kann mit einer anspruchsbasierten Webanwendung genutzt werden, sofern KDC entsprechend konfiguriert ist.  
  
    Um Benutzern die Authentifizierung mithilfe der integrierten Windows-Authentifizierung zu ermöglichen, muss der Webanwendungsproxy-Server zu einer Domäne angehören.  
  
    Sie müssen die Anwendung zur Unterstützung der eingeschränkten Kerberos-Delegierung konfigurieren. Diese Konfiguration kann auf dem Domänencontroller für jede Anwendung vorgenommen werden. Sie können auch die Anwendung direkt auf dem Back-End-Server konfigurieren, wenn es auf Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Weitere Informationen finden Sie unter [What's New in Kerberos Authentication](https://technet.microsoft.com/library/hh831747.aspx). Sie müssen auch sicherstellen, dass die Webanwendungsproxy-Server für die Delegierung auf die Dienstprinzipalnamen der Back-End-Server konfiguriert sind. Eine exemplarische Vorgehensweise zum Konfigurieren von Web Application Proxy zum Veröffentlichen einer Anwendung mithilfe der integrierten Windows-Authentifizierung finden Sie in [Konfigurieren einer Site-Verwendung der integrierten Windows-Authentifizierung](assetId:///b0788958-627f-450f-877c-209b1bd0db52).  
  
Wenn die SharePoint-Website mithilfe alternativer Zugriffszuordnungen (AAM) oder hostbenannter Websitesammlungen konfiguriert ist, können Sie jeweils verschiedene URLs der externen und Back-End-Server zur Veröffentlichung Ihrer Anwendung verwenden. Wenn die SharePoint-Website jedoch nicht mithilfe von AAM oder hostbenannten Websitesammlungen konfiguriert ist, müssen Sie jeweils die gleichen externen und Back-End-Server-URLs verwenden.  
  
## <a name="BKMK_6.2"></a>Veröffentlichen von Exchange Server  
Die folgende Tabelle beschreibt die Exchange-Dienste, die Sie mithilfe des Webanwendungsproxys und die unterstützte Vorauthentifizierung für diese Dienste veröffentlichen können:  
  
|Exchange-Dienst|Vorauthentifizierung|Hinweise|  
|--------------------|-----------------------|---------|  
|Outlook Web App|-AD FS mit nicht anspruchsbasierter Authentifizierung<br />-Pass-Through<br />-AD FS mit anspruchsbasierter Authentifizierung für lokales Exchange 2013 Service Pack 1 (SP1)|Weitere Informationen finden Sie unter: [Verwenden Claims-basierte Authentifizierung von AD FS mit Outlook Web App und EAC](https://go.microsoft.com/fwlink/?LinkId=393723)|  
|Exchange-Systemsteuerung|Pass-Through||  
|Outlook Anywhere|Pass-Through|Zur ordnungsgemäßen Funktion müssen drei URLs für Outlook Anywhere veröffentlicht werden:<br /><br />-Die URL für _autodiscover<br />– Der externe Hostname des Exchange-Servers; d. h. die URL, die für Clients für die Verbindung konfiguriert ist.<br />– Der interne FQDN des Exchange-Servers.|  
|Exchange ActiveSync|Pass-Through<br/> AD FS mithilfe von HTTP-Standardauthentifizierung Authorization-Protokoll|| Weitere Informationen finden Sie unter: https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/publishing-applications-using-ad-fs-preauthentication 
  
Um Outlook Web App mithilfe der integrierten Windows-Authentifizierung zu veröffentlichen, müssen Sie den nicht anspruchsbasierten Assistenten zum Hinzufügen der Vertrauensstellung der vertrauenden Seite für die Anwendung verwenden.  
  
Damit Benutzer für die Authentifizierung mit Kerberos die eingeschränkte Delegierung, die die Webanwendungsproxy-Server zu einer Domäne verknüpft werden, muss aus.  
  
Sie müssen die Anwendung zur Unterstützung der Kerberos-Authentifizierung konfigurieren. Außerdem müssen Sie eine dem Dienstprinzipalnamen (SPN) registrieren für das Konto, unter der Webdienst ausgeführt wird. Dies ist auf dem Domänencontroller oder auf dem Back-End-Servern möglich. Bei einem Auslastungstest mit Lastenausgleich in diesem Fall erforderlich, mit dem alternativen Konto der Dienst, Exchange-Umgebung finden Sie unter [Konfigurieren der Kerberos-Authentifizierung für den Lastenausgleich der Clientzugriffsserver](https://technet.microsoft.com/library/ff808312(v=exchg.150).aspx)  
  
Sie können auch die Anwendung direkt auf dem Back-End-Server konfigurieren, wenn es auf Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Weitere Informationen finden Sie unter [What's New in Kerberos Authentication](https://technet.microsoft.com/library/hh831747.aspx). Sie müssen auch sicherstellen, dass die Webanwendungsproxy-Server für die Delegierung auf die Dienstprinzipalnamen der Back-End-Server konfiguriert sind.  
  
## <a name="publishing-remote-desktop-gateway-through-web-application-proxy"></a>Veröffentlichen von Remotedesktopgateway per Webanwendungsproxy  
Wenn Sie beschränken des Zugriffs auf Ihre Remote-Access-Gateway und Vorauthentifizierung für den Remotezugriff hinzufügen möchten, können sie per Webanwendungsproxy Rollout. Dies ist eine wirklich gute Möglichkeit, stellen Sie sicher, dass Sie umfassende Vorauthentifizierung für RDG einschließlich MFA verfügen. Veröffentlichen, ohne eine Vorauthentifizierung ist ebenfalls eine Option, und bietet eine zentrale des Eintrags in Ihren Systemen.  
  
#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-pass-through-authentication"></a>Gewusst wie: Veröffentlichen einer Anwendung in RDG mithilfe des Webanwendungsproxys Pass-Through-Authentifizierung  
  
1.  Installation unterscheiden sich je nachdem, ob Ihre Web Access für Remotedesktop (/ Rdweb) und RD-Gateway (Rpc)-Rollen sind, auf dem gleichen Server oder auf verschiedenen Servern.  
  
2.  Wenn die Web Access für Remotedesktop und RD-Gateway-Rollen auf dem gleichen RDG-Server gehostet werden, können Sie einfach veröffentlichen den Stamm-FQDN im Webanwendungsproxy z. B. https://rdg.contoso.com/.  
  
    Sie können auch veröffentlichen die beiden virtuellen Verzeichnisse einzeln z. B. https://rdg.contoso.com/rdweb/ und https://rdg.contoso.com/rpc/.  
  
3.  Wenn die Web Access für Remotedesktop und dem RD-Gateway auf separaten RDG-Servern gehostet werden, müssen Sie die beiden virtuellen Verzeichnisse einzeln veröffentlichen. Sie können des gleichen oder einem anderen externen FQDNs des z. B. https://rdweb.contoso.com/rdweb/ und https://gateway.contoso.com/rpc/.  
  
4.  Wenn die externen und internen FQDN unterschiedlich sind, sollten Sie nicht Anforderung headerübersetzung auf den RDWeb-Veröffentlichungsregel deaktivieren. Dies ist möglich durch das folgende PowerShell-Skript auf dem Webanwendungsproxy-Server ausgeführt, aber standardmäßig aktiviert sein.
  
    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false  
    ```  
  
    > [!NOTE]  
    > Bei Bedarf zur Unterstützung von rich Clients wie RemoteApp und Desktop-Verbindungen oder iOS herstellen von Remotedesktopverbindungen, unterstützen diese keine Vorauthentifizierung, daher Sie RDG mit Pass-Through-Authentifizierung zu veröffentlichen müssen.  
  
#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-with-pre-authentication"></a>Gewusst wie: Veröffentlichen einer Anwendung in mithilfe des Webanwendungsproxys, mit der Vorauthentifizierung RDG  
  
1.  Web Application Proxy-Vorauthentifizierung mit RDG funktioniert durch Übergeben der Vorauthentifizierung Cookies abgerufen, die von Internet Explorer, die an den Client Remotedesktopverbindung (mstsc.exe) übergeben wird. Dies wird durch den Client Remotedesktopverbindung (mstsc.exe) verwendet. Dies wird dann als Nachweis der Authentifizierung von Client Remotedesktopverbindung verwendet.  
  
    Im folgenden Abschnitt wird die Verwaltungsgruppe die erforderlichen benutzerdefinierten RDP-Eigenschaften in den Remote-App-RDP-Dateien einschließen, die an Clients gesendet werden. Diese Teilen der Client das Vorauthentifizierung erforderlich ist, und übergeben Sie die Cookies für die Vorauthentifizierung Serveradresse zum Client Remotedesktopverbindung (mstsc.exe). In Verbindung mit "HttpOnly" für die Web Application Proxy-Anwendung deaktivieren ermöglicht dies den Client Remotedesktopverbindung (mstsc.exe), das Web Application Proxy-Cookie erhalten über den Browser zu verwenden.  
  
    Authentifizierung beim Server Web Access für Remotedesktop wird weiterhin die Web Access für Remotedesktop-Formular-Anmeldung verwendet. Dies bietet die geringste Anzahl der Benutzer aufgefordert werden, da das Anmeldeformular von Web Access für Remotedesktop einen Client-Side-Anmeldeinformationsspeicher erstellt, die vom Client Remotedesktopverbindung (mstsc.exe) für alle nachfolgenden Remote-App-Start verwendet werden kann.  
  
2.  Erstellen Sie zunächst eine manuelle der vertrauenden Seite Vertrauensstellung bei AD FS auf, als ob Sie eine Ansprüche unterstützende app veröffentlicht wurden. Dies bedeutet, dass Sie ein Dummy, die die Vorauthentifizierung zu erzwingen, damit Sie die Vorauthentifizierung ohne eingeschränkte Kerberos-Delegierung zum veröffentlichten Server erhalten Vertrauensstellung einer vertrauenden Seite zu erstellen. Sobald ein Benutzer authentifiziert wurde, wird alles übergeben.  
  
    > [!WARNING]  
    > Es scheint, dass mithilfe der Delegierung empfiehlt sich aber Mstsc SSO-Anforderungen nicht vollständig gelöst und Probleme vorliegen, wenn in das Verzeichnis/RPC zu delegieren, da der Client erwartet, dass die RD-Gateway-Authentifizierung zu verarbeiten.  
  
3.  Führen Sie die Schritte in der AD FS-Verwaltungskonsole, um eine manuelle der vertrauenden Seite Vertrauensstellung zu erstellen:  
  
    1.  Verwenden der **Partei Vertrauensstellung der vertrauenden Seite hinzufügen** Assistenten  
  
    2.  Wählen Sie **Daten über die vertrauende Seite manuell eingeben**.  
  
    3.  Übernehmen Sie alle Standardeinstellungen.  
  
    4.  Für den Bezeichner der vertrauenden Seite Geben Sie in der externe FQDN, Sie für den RDG-Zugriff, z. B. verwenden https://rdg.contoso.com/.  
  
        Dies ist die Vertrauensstellung der vertrauenden, die Sie verwenden, wenn die app in Web Application Proxy zu veröffentlichen.  
  
4.  Veröffentlichen Sie den Stamm des Standorts (z. B. https://rdg.contoso.com/ ) im Webanwendungsproxy. Legen Sie die Vorauthentifizierung für AD FS und verwenden Sie die Vertrauensstellung der vertrauenden, die, der Sie soeben erstellt haben. Dadurch werden /rdweb "und" / RPC, um das gleiche Cookie der Web Application Proxy-Authentifizierung verwenden.  
  
    Es ist möglich, /rdweb "und" / RPC als separate Anwendungen veröffentlichen und sogar anderen veröffentlichten Server verwenden. Sie müssen nur sicherstellen, dass Sie veröffentlichen, sowohl mithilfe der gleichen der vertrauenden Seite Vertrauensstellung, wie das Web Application Proxy-Token, für die vertrauenden Seite Vertrauensstellung ausgegeben wird und daher für Anwendungen, die mit der gleichen der vertrauenden Seite Vertrauensstellung veröffentlicht gilt.  
  
5.  Wenn die externen und internen FQDN unterschiedlich sind, sollten Sie nicht Anforderung headerübersetzung auf den RDWeb-Veröffentlichungsregel deaktivieren. Dies ist möglich durch das folgende PowerShell-Skript auf dem Webanwendungsproxy-Server ausgeführt, aber standardmäßig aktiviert sein:
  
    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false 
    ```  
  
6.  Deaktivieren Sie die "HttpOnly"-Cookie-Eigenschaft in der Web Application Proxy auf dem RDG einer veröffentlichten Anwendung. Um den RDG-ActiveX-Steuern des Zugriffs auf das Authentifizierungscookie Web Application Proxy zu ermöglichen, müssen Sie die Eigenschaft "HttpOnly" für das Web Application Proxy-Cookie zu deaktivieren.  
  
    Dies erfordert, dass Folgendes installiert sein [Web Application Proxy Hotfix](https://support.microsoft.com/en-gb/kb/3000850) oder [ https://support.microsoft.com/en-gb/kb/3000850 ](https://support.microsoft.com/en-gb/kb/3000850).  
  
    Führen Sie das folgende PowerShell-Skript nach der Installation des Hotfixes auf dem Webanwendungsproxy-Server, die Namen der entsprechenden Anwendung angeben:  
  
    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableHttpOnlyCookieProtection:$true  
    ```  
  
    Deaktivieren "HttpOnly" ermöglicht dem RDG-ActiveX-Steuern des Zugriffs auf das Authentifizierungscookie Web Application Proxy.  
  
7.  Konfigurieren Sie die relevanten RDG-Auflistung, auf dem Server "Auflistung" können Sie die Remotedesktopverbindung (mstsc.exe)-Client wissen, dass die erforderliche Authentifizierung in der Rdp-Datei erforderlich ist.  
  
    -   In Windows Server 2012 und Windows Server 2012 R2 kann dies mit dem folgenden PowerShell-Cmdlet auf dem RDG-Collection-Server erreicht werden:  
  
        ```
        Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s: <https://externalfqdn/rdweb/>`nrequire pre-authentication:i:1"
        ```
  
        Stellen Sie sicher, dass Sie entfernen die < und > Klammern ein, wenn Sie z. B. durch Ihre eigenen Werte ersetzen:
        
        ```
        Set-RDSessionCollectionConfiguration -CollectionName "MyAppCollection" -CustomRdpProperty "pre-authentication server address:s: https://rdg.contoso.com/rdweb/`nrequire pre-authentication:i:1"
        ```
  
    -   Unter Windows Server 2008 R2:  
  
        1.  Melden Sie sich die Terminal-Server mit einem Konto, das über Administratorrechte verfügt.  
  
        2.  Wechseln Sie zu **starten** >**Verwaltung** > **Terminaldienste** > **TS RemoteApp-Manager.**  
  
        3.  In der **Übersicht** Bereich des Terminaldienste-RemoteApp-Managers, neben den RDP-Einstellungen, klicken Sie auf **Änderung**.  
  
        4.  Auf der **benutzerdefinierte RDP-Einstellungen** Registerkarte, und geben Sie die folgenden RDP-Einstellungen in das Feld der benutzerdefinierten RDP-Einstellungen:  
  
            `pre-authentication server address: s: https://externalfqdn/rdweb/`  
  
            `require pre-authentication:i:1`  
  
        5.  Wenn Sie fertig sind, klicken Sie auf **übernehmen**.  
  
            Dies weist die Auflistung-Server mit benutzerdefinierten RDP-Eigenschaften in den RDP-Dateien, die an Clients gesendet werden. Diese Teilen der Client das Vorauthentifizierung erforderlich ist, und übergeben Sie die Cookies für die Vorauthentifizierung Serveradresse für den Client Remotedesktopverbindung (mstsc.exe). Dies ermöglicht in Verbindung mit der Deaktivierung von "HttpOnly" für die Web Application Proxy-Anwendung, den Client Remotedesktopverbindung (mstsc.exe), das Web Application Proxy-Authentifizierungscookie abgerufen, die über den Browser zu verwenden.  
  
            Weitere Informationen zu RDP finden Sie unter [zum Konfigurieren des TS-Gateway-OTP-Szenarios](https://technet.microsoft.com/library/cc731249(v=ws.10).aspx).  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Planen der Anwendungsveröffentlichung per Webanwendungsproxy](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11))  
  
-   [Problembehandlung des Webanwendungsproxys](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))  
  
-   [Web Application Proxy-Handbuch mit exemplarischer Vorgehensweise](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280944(v=ws.11))  
