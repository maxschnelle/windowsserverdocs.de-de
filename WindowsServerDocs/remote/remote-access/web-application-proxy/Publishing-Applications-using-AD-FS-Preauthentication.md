---
ms.assetid: 5f733510-c96e-4d3a-85d2-4407de95926e
title: Veröffentlichen von Anwendungen mit ADFS-Vorauthentifizierung
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: ca4d8661f8f0252334bdecbde85603d8af5e2d2a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446811"
---
# <a name="publishing-applications-using-ad-fs-preauthentication"></a>Veröffentlichen von Anwendungen mit ADFS-Vorauthentifizierung

>Gilt für: Windows Server 2016

**Dieser Inhalt ist für die lokale Version des Webanwendungsproxys relevant. Zum Aktivieren des sicheren Zugriffs auf lokale Anwendungen über die Cloud finden Sie unter den [Azure AD-Anwendungsproxy-Inhalt](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/).**  
  
In diesem Thema wird beschrieben, wie Sie Anwendungen per Webanwendungsproxy mit Active Directory-Verbunddienste (AD FS)-Vorauthentifizierung veröffentlichen.  
  
Für alle Anwendungstypen, die Sie mit AD FS-Vorauthentifizierung veröffentlichen können, müssen Sie eine AD FS für den Verbunddienst Vertrauensstellung einer vertrauenden Seite hinzufügen.  
  
Der allgemeine Ablauf der AD FS-Vorauthentifizierung lautet wie folgt aus:  
  
> [!NOTE]  
> Dieser Authentifizierungsablauf gilt nicht für Clients, die Microsoft Store-apps verwenden.  
  
1.  Das Clientgerät versucht auf eine veröffentlichte Webanwendung auf einer bestimmten Ressourcen-URL zuzugreifen; z. B. https://app1.contoso.com/.  
  
    Die Ressourcen-URL ist eine öffentliche Adresse, die auf der Webanwendungsproxy eingehende HTTPS-Anforderungen lauscht.  
  
    Wenn Sie HTTP, HTTPS-Umleitung aktiviert ist, wird Web Application Proxy auch für eingehende HTTP-Anforderungen lauschen.  
  
2.  Webanwendungsproxy leitet die HTTPS-Anforderung an den AD FS-Server mit URL-codierte Parameter, einschließlich der Ressourcen-URL und die AppRealm (ein relying Party-Bezeichner).  
  
    Der Benutzer wird authentifiziert, mit der AD FS-Server erforderliche Authentifizierungsmethode; z. B. Benutzername und Kennwort, zweistufige Authentifizierung mit einem Einmalkennwort und So weiter.  
  
3.  Nachdem der Benutzer authentifiziert wurde, Token die AD FS-Server ein token, das "Edge", mit den folgenden Informationen aus und leitet die HTTPS-an den Webanwendungsproxy-Server Anforderung:  
  
    -   Ressourcenbezeichner, auf den der Benutzer zuzugreifen versuchte  
  
    -   Die Identität des Benutzers als einen Benutzerprinzipalnamen (UPN).  
  
    -   Ablaufdatum der Zugriffserteilungsgenehmigung (d. h. dem Benutzer wird für einen beschränkten Zeitraum, nach dem er sich erneut authentifizieren muss, Zugriff gewährt)  
  
    -   Signatur der Informationen im Edgetoken  
  
4.  Webanwendungsproxy empfängt die umgeleitete HTTPS-Anforderung von AD FS-Server mit dem edgetoken und überprüft und verwendet das Token wie folgt:  
  
    -   Überprüft, dass die Signatur über den Verbunddienst, der in der Konfiguration der Web Application Proxy konfiguriert ist.  
  
    -   Er überprüft, ob das Token für die richtige Anwendung ausgestellt wurde.  
  
    -   Er überprüft, ob das Token noch gültig ist.  
  
    -   Er verwendet bei Bedarf die Benutzeridentität für die Überprüfungen, z. B. zum Abrufen eines Kerberos-Tickets, wenn der Back-End-Server zur Verwendung der integrierten Windows-Authentifizierung konfiguriert ist.  
  
5.  Wenn das edgetoken gültig ist, leitet der Web Application Proxy die HTTPS-Anforderung an die veröffentlichte Webanwendung, die per HTTP oder HTTPS.  
  
6.  Der Client kann jetzt auf die veröffentlichte Webanwendung zugreifen, diese kann jedoch so konfiguriert sein, dass der Benutzer eine zusätzliche Authentifizierung durchführen muss. Wenn es sich bei der veröffentlichten Webanwendung z. B. um eine SharePoint-Website handelt und keine weitere Authentifizierung erforderlich ist, sieht der Benutzer die SharePoint-Website im Browser.  
  
7.  Web Application Proxy speichert ein Cookie auf dem Clientgerät. Das Cookie wird vom Webanwendungsproxy verwendet, um zu identifizieren, dass diese Sitzung bereits eine Vorauthentifizierung stattgefunden hat und keine weitere Präauthentifizierung erforderlich ist.  
  
> [!IMPORTANT]  
> Achten Sie beim Konfigurieren der externen URL und der URL für den Back-End-Server darauf, dass Sie den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) und keine IP-Adresse einfügen.  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_1.1"></a>Veröffentlichen einer anspruchsbasierten Anwendung für Webbrowserclients  
Um eine Anwendung zu veröffentlichen, die Ansprüche für die Authentifizierung verwendet, müssen Sie dem Verbunddienst eine Vertrauensstellung der vertrauenden Seite für die Anwendung hinzufügen.  
  
Beim Veröffentlichen von anspruchsbasierten Anwendungen, auf die über einen Browser zugegriffen wird, ist der allgemeine Authentifizierungsablauf wie folgt:  
  
1.  Der Client versucht, die eine anspruchsbasierte Anwendung mit einem Webbrowser zugreifen; z. B. https://appserver.contoso.com/claimapp/.  
  
2.  Der Webbrowser sendet eine HTTPS-Anforderung an den Webanwendungsproxy-Server, der Anforderung an die AD FS-Server umgeleitet.  
  
3.  AD FS-Server authentifiziert den Benutzer und dem Gerät und leitet die Anforderung wieder an die Web Application Proxy. Die Anforderung enthält jetzt das Edgetoken. AD FS-Server hinzugefügt die Anforderung ein einmaliges Anmelden (SSO) Cookie, da der Benutzer bereits authentifiziert AD FS-Server durchgeführt hat.  
  
4.  Webanwendungsproxy überprüft das Token, fügt ein eigenes Cookie hinzu und leitet die Anforderung an den Back-End-Server weiter.  
  
5.  Der Back-End-Server leitet die Anforderung an die AD FS-Server, um das anwendungssicherheitstoken abzurufen.  
  
6.  Die Anforderung wird an den Back-End-Server von AD FS-Server umgeleitet. Die Anforderung enthält jetzt das Anwendungstoken und das SSO-Cookie. Dem Benutzer wird Zugriff auf die Anwendung gewährt, ohne einen Benutzernamen oder ein Kennwort eingeben zu müssen.  
  
In diesem Verfahren wird beschrieben, wie Sie eine anspruchsbasierte Anwendung veröffentlichen, z. B. eine SharePoint-Website, auf die von Webbrowserclients zugegriffen wird. Bevor Sie beginnen, sollten Sie sicherstellen, dass Sie Folgendes ausgeführt haben:  
  
-   Erstellt eine Vertrauensstellung der vertrauenden Seite für die Anwendung in der AD FS-Verwaltungskonsole.  
  
-   Überprüft, dass ein Zertifikat auf dem Webanwendungsproxy-Server für die Anwendung geeignet ist, die Sie veröffentlichen möchten.  
  

  
#### <a name="to-publish-a-claims-based-application"></a>So veröffentlichen Sie eine anspruchsbasierte Anwendung  
  
1.  Auf dem Webanwendungsproxy-Server, in der Remotezugriffs-Verwaltungskonsole in der **Navigation** Bereich klicken Sie auf **Web Application Proxy**, und klicken Sie dann in der **Aufgaben** Bereich klicken Sie auf **Veröffentlichen**.  
  
2.  Klicken Sie auf der Seite **Willkommen** des **Assistenten zum Veröffentlichen neuer Anwendungen** auf **Weiter**.  
  
3.  Auf der **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS)** , und klicken Sie dann auf **Weiter**.  
  
4.  Wählen Sie auf der Seite **Unterstützte Clients** die Option **Web und MSOFBA**aus, und klicken Sie dann auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Vertrauende Seite** in der Liste die vertrauende Seite für die zu veröffentlichende Anwendung aus, und klicken Sie dann auf **Weiter**.  
  
6.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie im Feld **Name** einen Anzeigenamen für die Anwendung ein.  
  
        Dieser Name wird nur in der Remotezugriffs-Verwaltungskonsole in der Liste der veröffentlichten Anwendungen verwendet.  
  
    -   Geben Sie im Feld **Externe URL** die externe URL für diese Anwendung ein, z. B. https://sp.contoso.com/app1/.  
  
    -   Wählen Sie in der Liste **Externes Zertifikat** ein Zertifikat aus, dessen Antragsteller die externe URL enthält.  
  
    -   Geben Sie im Feld **URL des Back-End-Servers** die URL des Back-End-Servers ein. Beachten Sie, dass dieser Wert automatisch eingegeben wird, wenn Sie die externe URL eingeben und sie ändern sollten nur, wenn die URL des Back-End-Servers unterscheidet. z. B. https://sp/app1/.  
  
        > [!NOTE]  
        > Webanwendungsproxy können Hostnamen in URLs übersetzt werden, jedoch keine Pfadnamen. Daher können Sie unterschiedliche Hostnamen eingeben, während der Pfadname gleich sein muss. Sie können z. B. einen externen URL eingeben https://apps.contoso.com/app1/ und Back-End-Server-URL des https://app-server/app1/. Allerdings kann nicht eingegebene externen URL %% https://apps.contoso.com/app1/ und Back-End-Server-URL des https://apps.contoso.com/internal-app1/.  
  
7.  Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen, und klicken Sie dann auf **Veröffentlichen**. Sie können den PowerShell-Befehl kopieren, um weitere veröffentlichte Anwendungen einzurichten.  
  
8.  Überprüfen Sie auf der Seite **Ergebnisse**, ob die Anwendung veröffentlicht wurde, und klicken Sie dann auf **Schließen**.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)***<em>Gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerURL 'https://sp.contoso.com/app1/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://sp.contoso.com/app1/'  
    -Name 'SP'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'SP_Relying_Party'  
```  
  
## <a name="BKMK_1.2"></a>Veröffentlichen Sie eine integrierte Windows-Authentifizierung basierenden Anwendung für Webbrowserclients  
Webanwendungsproxy kann verwendet werden, zum Veröffentlichen von Anwendungen, die integrierte Windows-Authentifizierung verwendet wird. d. h. kann Web Application Proxy führt dabei die Präauthentifizierung wie erforderlich, und anschließend SSO bei der veröffentlichten Anwendung, die integrierte Windows-Authentifizierung verwendet. Um eine Anwendung zu veröffentlichen, die die integrierte Windows-Authentifizierung verwendet, müssen Sie dem Verbunddienst eine Ansprüche nicht unterstützende Vertrauensstellung der vertrauenden Seite für die Anwendung hinzufügen.  
  
Um Web Application Proxy, einmaliges Anmelden (SSO) durchzuführen und führen Sie die Delegierung von Anmeldeinformationen mithilfe von Kerberos zu ermöglichen die eingeschränkte Delegierung der Webanwendungsproxy-Server zu einer Domäne angehören muss. Finden Sie unter [Planen von Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD).  
  
Damit die Benutzer den Zugriff auf Anwendungen, die integrierte Windows-Authentifizierung verwenden, muss der Webanwendungsproxy-Server für die veröffentlichte Anwendung Delegierung für Benutzer bereitstellen können. Diese Konfiguration kann auf dem Domänencontroller für jede Anwendung vorgenommen werden. Sie können hierzu auch auf dem Back-End-Server, wenn es auf Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Weitere Informationen finden Sie unter [What's New in Kerberos Authentication](https://technet.microsoft.com/library/hh831747.aspx).  
  
Eine exemplarische Vorgehensweise zum Konfigurieren von Web Application Proxy zum Veröffentlichen einer Anwendung mithilfe der integrierten Windows-Authentifizierung finden Sie in [Konfigurieren einer Site-Verwendung der integrierten Windows-Authentifizierung](https://technet.microsoft.com/library/dn280943.aspx#BKMK_3).  
  
Bei Verwendung der integrierten Windows-Authentifizierung für Back-End-Server die Authentifizierung zwischen Webanwendungsproxy und die veröffentlichte Anwendung nicht Claims-basierte, sondern verwendet stattdessen die eingeschränkte Kerberos-Delegierung zur Authentifizierung von Endbenutzern für die Anwendung. Der allgemeine Ablauf wird im Folgenden beschrieben:  
  
1.  Der Client versucht, die eine nicht anspruchsbasierte Anwendung mit einem Webbrowser zugreifen; z. B. https://appserver.contoso.com/nonclaimapp/.  
  
2.  Der Webbrowser sendet eine HTTPS-Anforderung an den Webanwendungsproxy-Server, der Anforderung an die AD FS-Server umgeleitet.  
  
3.  AD FS-Server authentifiziert den Benutzer und leitet die Anforderung wieder an die Web Application Proxy. Die Anforderung enthält jetzt das Edgetoken.  
  
4.  Webanwendungsproxy überprüft das Token.  
  
5.  Wenn das Token gültig ist, ruft ein Kerberos-Ticket vom Domänencontroller mit Web Application Proxy für den Benutzer ab.  
  
6.  Webanwendungsproxy fügt das Kerberos-Ticket der Anforderung als Teil des Simple and Protected GSS-API Negotiation Mechanismus (SPNEGO)-Tokens hinzu und leitet die Anforderung an den Back-End-Server weiter. Da die Anforderung das Kerberos-Ticket enthält, wird dem Benutzer der Zugriff auf die Anwendung gewährt, ohne sich zusätzlich authentifizieren zu müssen.  
  
In diesem Verfahren wird beschrieben, wie Sie eine Anwendung mit integrierter Windows-Authentifizierung, z. B. eine Outlook Web App, veröffentlichen, auf die von Webbrowserclients zugegriffen wird. Bevor Sie beginnen, sollten Sie sicherstellen, dass Sie Folgendes ausgeführt haben:  
  
-   Non-Claims-aware Anspruchsanbieter-Vertrauensstellung für die Anwendung erstellt in der AD FS-Verwaltungskonsole.  
  
-   Konfigurieren des Back-End-Servers zum Unterstützen der eingeschränkten Kerberos-Delegierung auf dem Domänencontroller oder mithilfe des Set-ADUser-Cmdlets mit dem Parameter %%amp;quot;-PrincipalsAllowedToDelegateToAccount%%amp;quot;. Beachten Sie, wenn der Back-End-Server unter Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, können Sie diesen PowerShell-Befehl auf dem Back-End-Server auch ausführen.  
  
-   Wird dafür gesorgt, dass die Webanwendungsproxy-Server für die Delegierung auf die Dienstprinzipalnamen der Back-End-Server konfiguriert sind.  
  
-   Überprüft, dass ein Zertifikat auf dem Webanwendungsproxy-Server für die Anwendung geeignet ist, die Sie veröffentlichen möchten.  
  
 
  
#### <a name="to-publish-a-non-claims-based-application"></a>So veröffentlichen Sie eine nicht anspruchsbasierte Anwendung  
  
1.  Auf dem Webanwendungsproxy-Server, in der Remotezugriffs-Verwaltungskonsole in der **Navigation** Bereich klicken Sie auf **Web Application Proxy**, und klicken Sie dann in der **Aufgaben** Bereich klicken Sie auf **Veröffentlichen**.  
  
2.  Klicken Sie auf der Seite **Willkommen** des **Assistenten zum Veröffentlichen neuer Anwendungen** auf **Weiter**.  
  
3.  Auf der **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS)** , und klicken Sie dann auf **Weiter**.  
  
4.  Wählen Sie auf der Seite **Unterstützte Clients** die Option **Web und MSOFBA**aus, und klicken Sie dann auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Vertrauende Seite** in der Liste die vertrauende Seite für die zu veröffentlichende Anwendung aus, und klicken Sie dann auf **Weiter**.  
  
6.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie im Feld **Name** einen Anzeigenamen für die Anwendung ein.  
  
        Dieser Name wird nur in der Remotezugriffs-Verwaltungskonsole in der Liste der veröffentlichten Anwendungen verwendet.  
  
    -   Geben Sie im Feld **Externe URL** die externe URL für diese Anwendung ein, z. B. https://owa.contoso.com/.  
  
    -   Wählen Sie in der Liste **Externes Zertifikat** ein Zertifikat aus, dessen Antragsteller die externe URL enthält.  
  
    -   Geben Sie im Feld **URL des Back-End-Servers** die URL des Back-End-Servers ein. Beachten Sie, dass dieser Wert automatisch eingegeben wird, wenn Sie die externe URL eingeben und sie ändern sollten nur, wenn die URL des Back-End-Servers unterscheidet. z. B. https://owa/.  
  
        > [!NOTE]  
        > Webanwendungsproxy können Hostnamen in URLs übersetzt werden, jedoch keine Pfadnamen. Daher können Sie unterschiedliche Hostnamen eingeben, während der Pfadname gleich sein muss. Sie können z. B. einen externen URL eingeben https://apps.contoso.com/app1/ und Back-End-Server-URL des https://app-server/app1/. Allerdings kann nicht eingegebene externen URL %% https://apps.contoso.com/app1/ und Back-End-Server-URL des https://apps.contoso.com/internal-app1/.  
  
    -   Geben Sie im Feld **Dienstprinzipalname des Back-End-Servers** den Dienstprinzipalnamen für den Back-End-Server ein, %%amp;quot;z. B. HTTP/owa.contoso.com%%amp;quot;.  
  
7.  Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen, und klicken Sie dann auf **Veröffentlichen**. Sie können den PowerShell-Befehl kopieren, um weitere veröffentlichte Anwendungen einzurichten.  
  
8.  Überprüfen Sie auf der Seite **Ergebnisse**, ob die Anwendung veröffentlicht wurde, und klicken Sie dann auf **Schließen**.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)***<em>Gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerAuthenticationSpn 'HTTP/owa.contoso.com'  
    -BackendServerURL 'https://owa.contoso.com/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://owa.contoso.com/'  
    -Name 'OWA'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'Non-Claims_Relying_Party'  
```  
  
## <a name="BKMK_1.3"></a>Veröffentlichen einer Anwendung, die MS-OFBA verwendet.  
Webanwendungsproxy unterstützt den Zugriff von Microsoft Office-Clients wie Microsoft Word, greifen Sie auf Dokumente und Daten auf Back-End-Servern. Der einzige Unterschied zwischen diesen Anwendungen und einem Standardbrowser besteht darin, dass die Umleitung zum Sicherheitstokendienst nicht durch eine reguläre HTTP-Umleitung erfolgt, sondern mit speziellen MS-OFBA-Headern gemäß: [ https://msdn.microsoft.com/library/dd773463(v=office.12).aspx ](https://msdn.microsoft.com/library/dd773463(v=office.12).aspx). Die Back-End-Anwendung kann die anspruchsbasierte Authentifizierung oder die integrierte Windows-Authentifizierung verwenden.   
Zum Veröffentlichen einer Anwendung für Clients, die MS-OFBA verwenden, müssen Sie eine Vertrauensstellung der vertrauenden Seite für die Anwendung für den Verbunddienst hinzufügen. Je nach Anwendung können Sie die anspruchsbasierte Authentifizierung oder die integrierte Windows-Authentifizierung verwenden. Daher muss die entsprechende Vertrauensstellung der vertrauenden Seite für die Anwendung hinzugefügt werden.  
  
Um Web Application Proxy, einmaliges Anmelden (SSO) durchzuführen und führen Sie die Delegierung von Anmeldeinformationen mithilfe von Kerberos zu ermöglichen die eingeschränkte Delegierung der Webanwendungsproxy-Server zu einer Domäne angehören muss. Finden Sie unter [Planen von Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD).  
  
Wenn die Anwendung die anspruchsbasierte Authentifizierung verwendet, sind keine weiteren Planungsschritte erforderlich. Wenn die Anwendung die integrierte Windows-Authentifizierung verwendet, finden Sie unter [veröffentlichen Sie eine integrierte Windows-Authentifizierung basierenden Anwendung für Webbrowserclients](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2).  
  
Der Authentifizierungsablauf für Clients, die MS-OFBA-Protokoll mit anspruchsbasierter Authentifizierung verwenden, wird unten beschrieben. Bei der Authentifizierung für dieses Szenario kann das Anwendungstoken in der URL oder im Textkörper verwendet werden.  
  
1.  Der Benutzer arbeitet in einem Office-Programm und öffnet über die Liste **Zuletzt verwendete Dokumente** eine Datei auf einer SharePoint-Website.  
  
2.  Das Office-Programm zeigt ein Fenster mit einem Browsersteuerelement an, in dem der Benutzer Anmeldeinformationen eingeben muss.  
  
    > [!NOTE]  
    > In manchen Fällen wird das Fenster möglicherweise nicht angezeigt, weil der Client bereits authentifiziert ist.  
  
3.  Web Application Proxy leitet die Anforderung an die AD FS-Server, der die Authentifizierung durchführt.  
  
4.  AD FS-Server leitet die Anforderung an die Web Application Proxy. Die Anforderung enthält jetzt das Edgetoken.  
  
5.  AD FS-Server hinzugefügt die Anforderung ein einmaliges Anmelden (SSO) Cookie, da der Benutzer bereits authentifiziert AD FS-Server durchgeführt hat.  
  
6.  Webanwendungsproxy überprüft das Token und leitet die Anforderung an den Back-End-Server weiter.  
  
7.  Der Back-End-Server leitet die Anforderung an die AD FS-Server, um das anwendungssicherheitstoken abzurufen.  
  
8.  Die Anforderung wird an den Back-End-Server umgeleitet. Die Anforderung enthält jetzt das Anwendungstoken und das SSO-Cookie. Dem Benutzer wird Zugriff auf die SharePoint-Website gewährt, ohne zum Anzeigen der Datei einen Benutzernamen oder ein Kennwort eingeben zu müssen.  
  
Die Schritte zum Veröffentlichen einer Anwendung, die MS-OFBA verwendet sind identisch mit den Schritten für eine anspruchsbasierte Anwendung oder eine nicht anspruchsbasierte Anwendung. Anspruchsbasierte Anwendungen finden Sie unter [veröffentlichen eine anspruchsbasierten Anwendung für Webbrowserclients](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.1), nicht anspruchsbasierte Anwendungen finden Sie unter [veröffentlichen Sie eine integrierte Windows-Authentifizierung basierenden Anwendung für Web Browser-Clients](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2). Webanwendungsproxy erkennt den Client automatisch und authentifiziert den Benutzer bei Bedarf.  
  
## <a name="publish-an-application-that-uses-http-basic"></a>Veröffentlichen einer Anwendung, die HTTP-Standardauthentifizierung verwendet.  

HTTP-Standardauthentifizierung ist die Authorization-Protokoll von viele Protokolle zum Verbinden von rich-Clients, einschließlich Smartphones mit Ihrem Exchange-Postfach verwendet. Weitere Informationen zu HTTP-Standardauthentifizierung, finden Sie unter [RFC 2617](https://www.ietf.org/rfc/rfc2617.txt). Webanwendungsproxy an, die normalerweise mit AD FS mithilfe von umleitungen interagiert; Die meisten rich Clients unterstützen keine Cookies oder State Management. Auf diese Weise kann die Web Application Proxy die HTTP-app erhalten eine Ansprüche nicht Vertrauensstellung der vertrauenden für die Anwendung für den Verbunddienst. Finden Sie unter [Planen von Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD).  
  
Der Authentifizierungsablauf für Clients, die HTTP-Standardauthentifizierung zu verwenden, wird die nachfolgend und in diesem Diagramm beschrieben:  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/WebApplicationProxy_httpBasicflow.png)  
  
1.  Der Benutzer versucht, eine veröffentlichte Webanwendung eine Telefon-Client zugreifen.  
  
2.  Die app sendet eine HTTPS-Anforderung an die URL, die von Web Application Proxy veröffentlicht.  
  
3.  Wenn die Anforderung keine Anmeldeinformationen enthält, gibt eine HTTP 401-Antwort an die app, die mit der URL des authentifizierenden AD FS-Server von Web Application Proxy zurück.  
  
4.  Der Benutzer sendet die HTTPS-Anforderung an die app erneut mit Autorisierung, legen Sie auf Basic und den Benutzernamen und BASE64 verschlüsselte Kennwort des Benutzers in den Www-Authentifizierungsheader der Anforderung.  
  
5.  Da das Gerät kann nicht mit AD FS umgeleitet werden, sendet der Web Application Proxy einer Authentifizierungsanforderung mit AD FS mit den Anmeldeinformationen, einschließlich Benutzername und Kennwort aufweist. Das Token ist im Auftrag des Geräts abgerufen.  
  
6.  Um die Anzahl der Anforderungen an die AD FS gesendet zu minimieren, Überprüfung Web Application Proxy, von nachfolgenden Clientanforderungen zwischengespeicherte Token für verwenden, solange das Token gültig ist. Webanwendungsproxy wird in regelmäßigen Abständen den Cache bereinigt. Sie können die Größe des Caches mit den Leistungsindikator "" anzeigen.  
  
7.  Wenn das Token gültig ist, Web Application Proxy leitet die Anforderung an den Back-End-Server und dem Benutzer wird Zugriff auf die veröffentlichte Webanwendung gewährt.  
  
Das folgende Verfahren wird erläutert, wie grundlegende HTTP-Anwendungen zu veröffentlichen.  
  
#### <a name="to-publish-an-http-basic-application"></a>Veröffentlichen eine Anwendung für die HTTP-Standardauthentifizierung  
  
1.  Auf dem Webanwendungsproxy-Server, in der Remotezugriffs-Verwaltungskonsole in der **Navigation** Bereich klicken Sie auf **Web Application Proxy**, und klicken Sie dann in der **Aufgaben** Bereich klicken Sie auf **Veröffentlichen**.  
  
2.  Klicken Sie auf der Seite **Willkommen** des **Assistenten zum Veröffentlichen neuer Anwendungen** auf **Weiter**.  
  
3.  Auf der **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS)** , und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **unterstützte Clients** Seite **HTTP-Standardauthentifizierung** , und klicken Sie dann auf **Weiter**.  
  
    Wenn Sie den Zugriff auf Exchange nur von Workplace Join-Geräten zu aktivieren möchten, wählen Sie die **Aktivieren des Zugriffs nur für den Arbeitsplatz eingebundenen Geräten** Feld. Weitere Informationen finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose Second Factor Authentication Across Company Applications](https://technet.microsoft.com/library/dn280945.aspx).  
  
5.  Wählen Sie auf der Seite **Vertrauende Seite** in der Liste die vertrauende Seite für die zu veröffentlichende Anwendung aus, und klicken Sie dann auf **Weiter**. Beachten Sie, die diese Liste nur enthält auf anspruchsbasierten vertrauende Seiten.  
  
6.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie im Feld **Name** einen Anzeigenamen für die Anwendung ein.  
  
        Dieser Name wird nur in der Remotezugriffs-Verwaltungskonsole in der Liste der veröffentlichten Anwendungen verwendet.  
  
    -   In der **Externalurl** Geben Sie die externe URL für diese Anwendung ein, z. B. "Mail.contoso.com"  
  
    -   Wählen Sie in der Liste **Externes Zertifikat** ein Zertifikat aus, dessen Antragsteller die externe URL enthält.  
  
    -   Geben Sie im Feld **URL des Back-End-Servers** die URL des Back-End-Servers ein. Beachten Sie, dass dieser Wert automatisch eingegeben wird, wenn Sie die externe URL eingeben und sie ändern sollten nur, wenn die URL des Back-End-Servers unterscheidet. z. B. "Mail.contoso.com".  
  
7.  Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen, und klicken Sie dann auf **Veröffentlichen**. Sie können den PowerShell-Befehl kopieren, um weitere veröffentlichte Anwendungen einzurichten.  
  
8.  Überprüfen Sie auf der Seite **Ergebnisse**, ob die Anwendung veröffentlicht wurde, und klicken Sie dann auf **Schließen**.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)***<em>Gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
Dieses Windows PowerShell-Skript kann Vorauthentifizierung für alle Geräte, nicht nur die Geräte dem Arbeitsplatz beigetreten.  
  
```  
Add-WebApplicationProxyApplication  
     -BackendServerUrl 'https://mail.contoso.com'   
     -ExternalCertificateThumbprint '697F4FF0B9947BB8203A96ED05A3021830638E50'   
     -ExternalUrl 'https://mail.contoso.com'   
     -Name 'Exchange'   
     -ExternalPreAuthentication ADFSforRichClients  
     -ADFSRelyingPartyName 'EAS_Relying_Party'  
```  
  
Die folgenden führt die Vorauthentifizierung nur Arbeitsplatz eingebundenen Hybridgeräten:  
  
```  
Add-WebApplicationProxyApplication  
     -BackendServerUrl 'https://mail.contoso.com'   
     -ExternalCertificateThumbprint '697F4FF0B9947BB8203A96ED05A3021830638E50'   
     -EnableHTTPRedirect:$true   
     -ExternalUrl 'https://mail.contoso.com'   
     -Name 'Exchange'   
     -ExternalPreAuthentication ADFSforRichClients  
     -ADFSRelyingPartyName 'EAS_Relying_Party'  
```  
  
## <a name="BKMK_1.4"></a>Veröffentlichen einer Anwendung, die "oauth2", z. B. eine Microsoft Store-App verwendet.  
Um eine Anwendung für Microsoft Store-apps zu veröffentlichen, müssen Sie eine Vertrauensstellung der vertrauenden Seite für die Anwendung für den Verbunddienst hinzufügen.  
  
Um Web Application Proxy, einmaliges Anmelden (SSO) durchzuführen und führen Sie die Delegierung von Anmeldeinformationen mithilfe von Kerberos zu ermöglichen die eingeschränkte Delegierung der Webanwendungsproxy-Server zu einer Domäne angehören muss. Finden Sie unter [Planen von Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD).  
  
> [!NOTE]  
> Webanwendungsproxy unterstützt die Veröffentlichung nur für Microsoft Store-apps, die das OAuth 2.0-Protokoll verwenden.  
  
In der AD FS-Verwaltungskonsole müssen Sie sicherstellen, dass der Proxy die OAuth-Endpunkt aktiviert ist. Öffnen Sie dazu die AD FS-Verwaltungskonsole, erweitern Sie den Knoten **Dienst**, klicken Sie auf **Endpunkte**, suchen Sie in der Liste **Endpunkte** nach dem OAuth-Endpunkt, und vergewissern Sie sich, dass in der Spalte **Proxy aktiviert** der Wert **Ja**angezeigt wird.  
  
Der Authentifizierungsablauf für Clients, die Microsoft Store-apps verwenden, lautet wie folgt:  
  
> [!NOTE]  
> Die Web Application Proxy leitet an die AD FS-Server für die Authentifizierung. Da es sich bei Microsoft Store-apps umleitungen nicht unterstützen, werden bei Verwendung von Microsoft Store-apps, ist es erforderlich, um die URL des AD FS-Server mit dem Cmdlet Set-WebApplicationProxyConfiguration und dem OAuthAuthenticationURL-Parameter festzulegen.  
>   
> Microsoft Store-apps können nur mithilfe von Windows PowerShell veröffentlicht werden.  
  
1.  Der Client versucht, eine veröffentlichte Webanwendung, die mit einer Microsoft Store-app zugreifen.  
  
2.  Die app sendet eine HTTPS-Anforderung an die URL, die von Web Application Proxy veröffentlicht.  
  
3.  Webanwendungsproxy gibt eine HTTP 401-Antwort an die app, die mit der URL des authentifizierenden AD FS-Server zurück. Dieser Prozess wird als "Ermittlung" bezeichnet.  
  
    > [!NOTE]  
    > Wenn die app die URL des authentifizierenden AD FS-Server kann und bereits ein kombinationstoken, das OAuth-Token und das edgetoken enthält, werden die Schritte 2 und 3 in diesem Authentifizierungsablauf übersprungen.  
  
4.  Die app sendet eine HTTPS-Anforderung an die AD FS-Server.  
  
5.  Die app verwendet Web Authentication Broker, um ein Dialogfeld zu generieren, in dem der Benutzer die Anmeldeinformationen für die Authentifizierung auf dem AD FS-Server gibt. Informationen zum Webauthentifizierungsbroker finden Sie unter [Webauthentifizierungsbroker](https://msdn.microsoft.com/library/windows/apps/hh750287.aspx).  
  
6.  Nach erfolgreicher Authentifizierung erstellt der AD FS-Server ein kombinationstoken, das das OAuth-Token und das edgetoken enthält, und sendet das Token an die app.  
  
7.  Die app sendet eine HTTPS-Anforderung mit dem kombinationstoken an die URL, die von Web Application Proxy veröffentlicht wird.  
  
8.  Webanwendungsproxy teilt das kombinationstoken in zwei Teile auf und überprüft das edgetoken.  
  
9. Wenn das edgetoken gültig ist, leitet die Anforderung an den Back-End-Server mit dem OAuth-Token von Web Application Proxy weiter. Dem Benutzer wird der Zugriff auf die veröffentlichte Webanwendung gewährt.  
  
Hier wird beschrieben, wie Sie eine Anwendung für OAuth2 veröffentlichen. Diese Art von Anwendung kann nur mithilfe von Windows PowerShell veröffentlicht werden. Bevor Sie beginnen, sollten Sie sicherstellen, dass Sie Folgendes ausgeführt haben:  
  
-   Erstellt eine Vertrauensstellung der vertrauenden Seite für die Anwendung in der AD FS-Verwaltungskonsole.  
  
-   Wird dafür gesorgt, dass der OAuth-Endpunkt Proxy in der AD FS-Verwaltungskonsole aktiviert ist, und notieren des URL-Pfads.  
  
-   Überprüft, dass ein Zertifikat auf dem Webanwendungsproxy-Server für die Anwendung geeignet ist, die Sie veröffentlichen möchten.  
  
#### <a name="to-publish-an-oauth2-app"></a>Veröffentlichen eine OAuth2-app  
  
1.  Auf dem Webanwendungsproxy-Server, in der Remotezugriffs-Verwaltungskonsole in der **Navigation** Bereich klicken Sie auf **Web Application Proxy**, und klicken Sie dann in der **Aufgaben** Bereich klicken Sie auf **Veröffentlichen**.  
  
2.  Klicken Sie auf der Seite **Willkommen** des **Assistenten zum Veröffentlichen neuer Anwendungen** auf **Weiter**.  
  
3.  Auf der **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS)** , und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **unterstützte Clients** Seite **OAuth2** , und klicken Sie dann auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Vertrauende Seite** in der Liste die vertrauende Seite für die zu veröffentlichende Anwendung aus, und klicken Sie dann auf **Weiter**.  
  
6.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie im Feld **Name** einen Anzeigenamen für die Anwendung ein.  
  
        Dieser Name wird nur in der Remotezugriffs-Verwaltungskonsole in der Liste der veröffentlichten Anwendungen verwendet.  
  
    -   Geben Sie im Feld **Externe URL** die externe URL für diese Anwendung ein, z. B. https://server1.contoso.com/app1/.  
  
    -   Wählen Sie in der Liste **Externes Zertifikat** ein Zertifikat aus, dessen Antragsteller die externe URL enthält.  
  
        Um sicherzustellen, dass Ihre Benutzer können Ihre app zugreifen, selbst wenn sie nicht in der URL HTTPS eingeben, wählen Sie die **HTTP auf HTTPS-Umleitung aktivieren** Feld.  
  
    -   Geben Sie im Feld **URL des Back-End-Servers** die URL des Back-End-Servers ein. Beachten Sie, dass dieser Wert automatisch eingegeben wird, wenn Sie die externe URL eingeben und sie ändern sollten nur, wenn die URL des Back-End-Servers unterscheidet. z. B. https://sp/app1/.  
  
        > [!NOTE]  
        > Webanwendungsproxy können Hostnamen in URLs übersetzt werden, jedoch keine Pfadnamen. Daher können Sie unterschiedliche Hostnamen eingeben, während der Pfadname gleich sein muss. Sie können z. B. einen externen URL eingeben https://apps.contoso.com/app1/ und Back-End-Server-URL des https://app-server/app1/. Allerdings kann nicht eingegebene externen URL %% https://apps.contoso.com/app1/ und Back-End-Server-URL des https://apps.contoso.com/internal-app1/.  
  
7.  Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen, und klicken Sie dann auf **Veröffentlichen**. Sie können den PowerShell-Befehl kopieren, um weitere veröffentlichte Anwendungen einzurichten.  
  
8.  Überprüfen Sie auf der Seite **Ergebnisse**, ob die Anwendung veröffentlicht wurde, und klicken Sie dann auf **Schließen**.  
  
Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
So legen Sie die URL der OAuth-Authentifizierung für einen Verbundserver Adresse "FS.contoso.com" und ein URL-Pfad des /adfs/oauth2/fest  
  
```  
Set-WebApplicationProxyConfiguration -OAuthAuthenticationURL 'https://fs.contoso.com/adfs/oauth2/'  
```  
  
So veröffentlichen Sie die Anwendung  
  
```  
Add-WebApplicationProxyApplication  
    -BackendServerURL 'https://storeapp.contoso.com/'  
    -ExternalCertificateThumbprint '1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b'  
    -ExternalURL 'https://storeapp.contoso.com/'  
    -Name 'Microsoft Store app Server'  
    -ExternalPreAuthentication ADFS  
    -ADFSRelyingPartyName 'Store_app_Relying_Party'  
    -UseOAuthAuthentication  
```  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Problembehandlung: Webanwendungsproxy](https://technet.microsoft.com/library/dn770156.aspx)  
  
-   [Veröffentlichen von Anwendungen per Webanwendungsproxy](https://technet.microsoft.com/library/dn383659.aspx)  
  
-   [Planen der Anwendungsveröffentlichung per Webanwendungsproxy](https://technet.microsoft.com/library/dn383650.aspx)  
  
-   [Web Application Proxy-Handbuch mit exemplarischer Vorgehensweise](https://technet.microsoft.com/library/dn280944.aspx)  
  
-   [Webanwendungsproxy-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/dn283404.aspx)  
  
-   [Add-WebApplicationProxyApplication](https://technet.microsoft.com/library/dn283409.aspx)  
  
-   [Set-WebApplicationProxyConfiguration](https://technet.microsoft.com/library/dn283406.aspx)  
  


