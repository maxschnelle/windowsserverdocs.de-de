---
ms.assetid: 5f733510-c96e-4d3a-85d2-4407de95926e
title: Veröffentlichen von Anwendungen mit ADFS-Vorauthentifizierung
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server
ms.technology: web-app-proxy
ms.openlocfilehash: bd5c4c97e01942e7c5ab8ed1aba3fcf92030ac59
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404263"
---
# <a name="publishing-applications-using-ad-fs-preauthentication"></a>Veröffentlichen von Anwendungen mit ADFS-Vorauthentifizierung

>Gilt für: Windows Server 2016

**Diese Inhalte sind für die lokale Version des webanwendungsproxys relevant. Informationen zum Aktivieren des sicheren Zugriffs auf lokale Anwendungen über die Cloud finden Sie in den [Azure AD Anwendungs Proxy-Inhalt](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/).**  
  
In diesem Thema wird beschrieben, wie Sie Anwendungen über den webanwendungsproxy mithilfe der Vorauthentifizierung Active Directory-Verbunddienste (AD FS) (AD FS) veröffentlichen.  
  
Für alle Anwendungs Typen, die Sie mit AD FS-Vorauthentifizierung veröffentlichen können, müssen Sie der Verbunddienst eine AD FS Vertrauensstellung der vertrauenden Seite hinzufügen.  
  
Der allgemeine Ablauf der AD FS Vorauthentifizierung lautet wie folgt:  
  
> [!NOTE]  
> Dieser Authentifizierungs Ablauf gilt nicht für Clients, die Microsoft Store-Apps verwenden.  
  
1.  Das Client Gerät versucht, auf eine veröffentlichte Webanwendung unter einer bestimmten Ressourcen-URL zuzugreifen. beispielsweise https://app1.contoso.com/.  
  
    Die Ressourcen-URL ist eine öffentliche Adresse, an der webanwendungsproxy eingehende HTTPS-Anforderungen überwacht.  
  
    Wenn die Umleitung von http zu HTTPS aktiviert ist, lauscht der webanwendungsproxy auch auf eingehende HTTP-Anforderungen.  
  
2.  Der webanwendungsproxy leitet die HTTPS-Anforderung mit URL-codierten Parametern an den AD FS Server um, einschließlich der Ressourcen-URL und der apprealm (Bezeichner der vertrauenden Seite).  
  
    Der Benutzer authentifiziert sich mit der für den AD FS Server erforderlichen Authentifizierungsmethode. beispielsweise Benutzername und Kennwort, zweistufige Authentifizierung mit einem einmaligen Kennwort usw.  
  
3.  Nachdem der Benutzer authentifiziert wurde, gibt der AD FS Server ein Sicherheits Token (das edgetoken) mit den folgenden Informationen aus und leitet die HTTPS-Anforderung zurück an den webanwendungsproxy-Server:  
  
    -   Ressourcenbezeichner, auf den der Benutzer zuzugreifen versuchte  
  
    -   Die Identität des Benutzers als Benutzer Prinzipal Name (User Principal Name, UPN).  
  
    -   Ablaufdatum der Zugriffserteilungsgenehmigung (d. h. dem Benutzer wird für einen beschränkten Zeitraum, nach dem er sich erneut authentifizieren muss, Zugriff gewährt)  
  
    -   Signatur der Informationen im Edgetoken  
  
4.  Der webanwendungsproxy empfängt die umgeleitete HTTPS-Anforderung vom AD FS Server mit dem edgetoken und überprüft und verwendet das Token wie folgt:  
  
    -   Überprüft, ob die edgetokensignatur aus dem Verbund Dienst stammt, der in der Konfiguration des webanwendungsproxys konfiguriert ist.  
  
    -   Er überprüft, ob das Token für die richtige Anwendung ausgestellt wurde.  
  
    -   Er überprüft, ob das Token noch gültig ist.  
  
    -   Er verwendet bei Bedarf die Benutzeridentität für die Überprüfungen, z. B. zum Abrufen eines Kerberos-Tickets, wenn der Back-End-Server zur Verwendung der integrierten Windows-Authentifizierung konfiguriert ist.  
  
5.  Wenn das edgetoken gültig ist, leitet der webanwendungsproxy die HTTPS-Anforderung über HTTP oder HTTPS an die veröffentlichte Webanwendung weiter.  
  
6.  Der Client kann jetzt auf die veröffentlichte Webanwendung zugreifen, diese kann jedoch so konfiguriert sein, dass der Benutzer eine zusätzliche Authentifizierung durchführen muss. Wenn es sich bei der veröffentlichten Webanwendung z. B. um eine SharePoint-Website handelt und keine weitere Authentifizierung erforderlich ist, sieht der Benutzer die SharePoint-Website im Browser.  
  
7.  Der webanwendungsproxy speichert ein Cookie auf dem Client Gerät. Das Cookie wird vom webanwendungsproxy verwendet, um zu ermitteln, dass diese Sitzung bereits vorauthentifiziert wurde und keine weitere Vorauthentifizierung erforderlich ist.  
  
> [!IMPORTANT]  
> Achten Sie beim Konfigurieren der externen URL und der URL für den Back-End-Server darauf, dass Sie den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) und keine IP-Adresse einfügen.  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_1.1"></a>Veröffentlichen einer Anspruchs basierten Anwendung für Webbrowser Clients  
Um eine Anwendung zu veröffentlichen, die Ansprüche für die Authentifizierung verwendet, müssen Sie dem Verbunddienst eine Vertrauensstellung der vertrauenden Seite für die Anwendung hinzufügen.  
  
Beim Veröffentlichen von anspruchsbasierten Anwendungen, auf die über einen Browser zugegriffen wird, ist der allgemeine Authentifizierungsablauf wie folgt:  
  
1.  Der Client versucht, mithilfe eines Webbrowsers auf eine Anspruchs basierte Anwendung zuzugreifen. beispielsweise https://appserver.contoso.com/claimapp/.  
  
2.  Der Webbrowser sendet eine HTTPS-Anforderung an den webanwendungsproxy-Server, der die Anforderung an den AD FS-Server umleitet.  
  
3.  Der AD FS Server authentifiziert den Benutzer und das Gerät und leitet die Anforderung zurück an den webanwendungsproxy. Die Anforderung enthält jetzt das Edgetoken. Der AD FS Server fügt der Anforderung ein Single Sign-on-Cookie (SSO) hinzu, da der Benutzer bereits eine Authentifizierung für den AD FS Server durchgeführt hat.  
  
4.  Der webanwendungsproxy überprüft das Token, fügt ein eigenes Cookie hinzu und leitet die Anforderung an den Back-End-Server weiter.  
  
5.  Der Back-End-Server leitet die Anforderung an den AD FS-Server um, um das Anwendungs Sicherheits Token zu erhalten.  
  
6.  Die Anforderung wird vom AD FS Server an den Back-End-Server umgeleitet. Die Anforderung enthält jetzt das Anwendungstoken und das SSO-Cookie. Dem Benutzer wird Zugriff auf die Anwendung gewährt, ohne einen Benutzernamen oder ein Kennwort eingeben zu müssen.  
  
In diesem Verfahren wird beschrieben, wie Sie eine anspruchsbasierte Anwendung veröffentlichen, z. B. eine SharePoint-Website, auf die von Webbrowserclients zugegriffen wird. Bevor Sie beginnen, sollten Sie sicherstellen, dass Sie Folgendes ausgeführt haben:  
  
-   Es wurde eine Vertrauensstellung der vertrauenden Seite für die Anwendung in der AD FS Management Console erstellt.  
  
-   Es wurde überprüft, ob ein Zertifikat auf dem webanwendungsproxy-Server für die zu veröffentlichende Anwendung geeignet ist.  
  

  
#### <a name="to-publish-a-claims-based-application"></a>So veröffentlichen Sie eine anspruchsbasierte Anwendung  
  
1.  Klicken Sie auf dem webanwendungsproxy-Server in der Remote Zugriffs-Verwaltungskonsole im **Navigations** Bereich auf **webanwendungsproxy**, und klicken Sie dann im Bereich **Tasks** auf **veröffentlichen**.  
  
2.  Klicken Sie auf der Seite **Willkommen** des **Assistenten zum Veröffentlichen neuer Anwendungen** auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS) (AD FS)** , und klicken Sie dann auf **weiter**.  
  
4.  Wählen Sie auf der Seite **Unterstützte Clients** die Option **Web und MSOFBA**aus, und klicken Sie dann auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Vertrauende Seite** in der Liste die vertrauende Seite für die zu veröffentlichende Anwendung aus, und klicken Sie dann auf **Weiter**.  
  
6.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie im Feld **Name** einen Anzeigenamen für die Anwendung ein.  
  
        Dieser Name wird nur in der Remotezugriffs-Verwaltungskonsole in der Liste der veröffentlichten Anwendungen verwendet.  
  
    -   Geben Sie im Feld **Externe URL** die externe URL für diese Anwendung ein, z. B. https://sp.contoso.com/app1/.  
  
    -   Wählen Sie in der Liste **Externes Zertifikat** ein Zertifikat aus, dessen Antragsteller die externe URL enthält.  
  
    -   Geben Sie im Feld **URL des Back-End-Servers** die URL des Back-End-Servers ein. Beachten Sie, dass dieser Wert automatisch eingegeben wird, wenn Sie die externe URL eingeben. Sie sollten Sie nur ändern, wenn sich die URL des Back-End-Servers unterscheidet. beispielsweise https://sp/app1/.  
  
        > [!NOTE]  
        > Der webanwendungsproxy kann Hostnamen in URLs übersetzen, aber keine Pfadnamen übersetzen. Daher können Sie unterschiedliche Hostnamen eingeben, während der Pfadname gleich sein muss. Beispielsweise können Sie eine externe URL https://apps.contoso.com/app1/ und eine Back-End-Server-URL https://app-server/app1/eingeben. Es ist jedoch nicht möglich, eine externe URL https://apps.contoso.com/app1/ und eine Back-End-Server-URL https://apps.contoso.com/internal-app1/einzugeben.  
  
7.  Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen, und klicken Sie dann auf **Veröffentlichen**. Sie können den PowerShell-Befehl kopieren, um weitere veröffentlichte Anwendungen einzurichten.  
  
8.  Überprüfen Sie auf der Seite **Ergebnisse**, ob die Anwendung veröffentlicht wurde, und klicken Sie dann auf **Schließen**.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)von  ***<em>entsprechenden Windows PowerShell-Befehlen</em>***  
  
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
  
## <a name="BKMK_1.2"></a>Veröffentlichen einer integrierten Windows Authenticated-basierten Anwendung für Webbrowser Clients  
Webanwendungsproxy kann zum Veröffentlichen von Anwendungen verwendet werden, die die integrierte Windows-Authentifizierung verwenden. Das heißt, der webanwendungsproxy führt die Vorauthentifizierung nach Bedarf durch und kann dann SSO für die veröffentlichte Anwendung durchführen, die die integrierte Windows-Authentifizierung verwendet. Um eine Anwendung zu veröffentlichen, die die integrierte Windows-Authentifizierung verwendet, müssen Sie dem Verbunddienst eine Ansprüche nicht unterstützende Vertrauensstellung der vertrauenden Seite für die Anwendung hinzufügen.  
  
Damit der webanwendungsproxy Single Sign-on (SSO) ausführen und die Delegierung von Anmelde Informationen mithilfe der eingeschränkten Kerberos-Delegierung durchführen kann, muss der webanwendungsproxy-Server einer Domäne beitreten Siehe [Plan Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD).  
  
Um Benutzern den Zugriff auf Anwendungen zu ermöglichen, die die integrierte Windows-Authentifizierung verwenden, muss der webanwendungsproxy-Server in der Lage sein, Benutzern die Delegierung für die veröffentlichte Anwendung Diese Konfiguration kann auf dem Domänencontroller für jede Anwendung vorgenommen werden. Dies können Sie auch auf dem Back-End-Server tun, wenn er unter Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Weitere Informationen finden Sie unter [What's New in Kerberos Authentication](https://technet.microsoft.com/library/hh831747.aspx).  
  
Eine exemplarische Vorgehensweise zum Konfigurieren des webanwendungsproxys zum Veröffentlichen einer Anwendung mithilfe der integrierten Windows-Authentifizierung finden Sie unter [Konfigurieren eines Standorts für die Verwendung der integrierten Windows](https://technet.microsoft.com/library/dn280943.aspx#BKMK_3)-Authentifizierung.  
  
Bei der Verwendung der integrierten Windows-Authentifizierung für Back-End-Server ist die Authentifizierung zwischen webanwendungsproxy und der veröffentlichten Anwendung nicht Anspruchs basiert, sondern verwendet die eingeschränkte Kerberos-Delegierung, um Endbenutzer bei der Anwendung zu authentifizieren. Der allgemeine Ablauf wird im Folgenden beschrieben:  
  
1.  Der Client versucht, mithilfe eines Webbrowsers auf eine nicht Anspruchs basierte Anwendung zuzugreifen. beispielsweise https://appserver.contoso.com/nonclaimapp/.  
  
2.  Der Webbrowser sendet eine HTTPS-Anforderung an den webanwendungsproxy-Server, der die Anforderung an den AD FS-Server umleitet.  
  
3.  Der AD FS Server authentifiziert den Benutzer und leitet die Anforderung zurück an den webanwendungsproxy. Die Anforderung enthält jetzt das Edgetoken.  
  
4.  Der webanwendungsproxy überprüft das Token.  
  
5.  Wenn das Token gültig ist, ruft der webanwendungsproxy im Auftrag des Benutzers ein Kerberos-Ticket vom Domänen Controller ab.  
  
6.  Der webanwendungsproxy fügt das Kerberos-Ticket der Anforderung als Teil des Simple und Protected spschgo (GSS-API-Aushandlungs Mechanismus)-Tokens hinzu und leitet die Anforderung an den Back-End-Server weiter. Da die Anforderung das Kerberos-Ticket enthält, wird dem Benutzer der Zugriff auf die Anwendung gewährt, ohne sich zusätzlich authentifizieren zu müssen.  
  
In diesem Verfahren wird beschrieben, wie Sie eine Anwendung mit integrierter Windows-Authentifizierung, z. B. eine Outlook Web App, veröffentlichen, auf die von Webbrowserclients zugegriffen wird. Bevor Sie beginnen, sollten Sie sicherstellen, dass Sie Folgendes ausgeführt haben:  
  
-   Es wurde eine nicht Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite für die Anwendung in der AD FS Management Console erstellt.  
  
-   Konfigurieren des Back-End-Servers zum Unterstützen der eingeschränkten Kerberos-Delegierung auf dem Domänencontroller oder mithilfe des Set-ADUser-Cmdlets mit dem Parameter %%amp;quot;-PrincipalsAllowedToDelegateToAccount%%amp;quot;. Beachten Sie Folgendes: Wenn der Back-End-Server unter Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, können Sie diesen PowerShell-Befehl auch auf dem Back-End-Server ausführen.  
  
-   Stellen Sie sicher, dass die webanwendungsproxy-Server für die Delegierung an die Dienst Prinzipal Namen der Back-End-Server  
  
-   Es wurde überprüft, ob ein Zertifikat auf dem webanwendungsproxy-Server für die zu veröffentlichende Anwendung geeignet ist.  
  
 
  
#### <a name="to-publish-a-non-claims-based-application"></a>So veröffentlichen Sie eine nicht anspruchsbasierte Anwendung  
  
1.  Klicken Sie auf dem webanwendungsproxy-Server in der Remote Zugriffs-Verwaltungskonsole im **Navigations** Bereich auf **webanwendungsproxy**, und klicken Sie dann im Bereich **Tasks** auf **veröffentlichen**.  
  
2.  Klicken Sie auf der Seite **Willkommen** des **Assistenten zum Veröffentlichen neuer Anwendungen** auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS) (AD FS)** , und klicken Sie dann auf **weiter**.  
  
4.  Wählen Sie auf der Seite **Unterstützte Clients** die Option **Web und MSOFBA**aus, und klicken Sie dann auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Vertrauende Seite** in der Liste die vertrauende Seite für die zu veröffentlichende Anwendung aus, und klicken Sie dann auf **Weiter**.  
  
6.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie im Feld **Name** einen Anzeigenamen für die Anwendung ein.  
  
        Dieser Name wird nur in der Remotezugriffs-Verwaltungskonsole in der Liste der veröffentlichten Anwendungen verwendet.  
  
    -   Geben Sie im Feld **Externe URL** die externe URL für diese Anwendung ein, z. B. https://owa.contoso.com/.  
  
    -   Wählen Sie in der Liste **Externes Zertifikat** ein Zertifikat aus, dessen Antragsteller die externe URL enthält.  
  
    -   Geben Sie im Feld **URL des Back-End-Servers** die URL des Back-End-Servers ein. Beachten Sie, dass dieser Wert automatisch eingegeben wird, wenn Sie die externe URL eingeben. Sie sollten Sie nur ändern, wenn sich die URL des Back-End-Servers unterscheidet. beispielsweise https://owa/.  
  
        > [!NOTE]  
        > Der webanwendungsproxy kann Hostnamen in URLs übersetzen, aber keine Pfadnamen übersetzen. Daher können Sie unterschiedliche Hostnamen eingeben, während der Pfadname gleich sein muss. Beispielsweise können Sie eine externe URL https://apps.contoso.com/app1/ und eine Back-End-Server-URL https://app-server/app1/eingeben. Es ist jedoch nicht möglich, eine externe URL https://apps.contoso.com/app1/ und eine Back-End-Server-URL https://apps.contoso.com/internal-app1/einzugeben.  
  
    -   Geben Sie im Feld **Dienstprinzipalname des Back-End-Servers** den Dienstprinzipalnamen für den Back-End-Server ein, %%amp;quot;z. B. HTTP/owa.contoso.com%%amp;quot;.  
  
7.  Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen, und klicken Sie dann auf **Veröffentlichen**. Sie können den PowerShell-Befehl kopieren, um weitere veröffentlichte Anwendungen einzurichten.  
  
8.  Überprüfen Sie auf der Seite **Ergebnisse**, ob die Anwendung veröffentlicht wurde, und klicken Sie dann auf **Schließen**.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)von  ***<em>entsprechenden Windows PowerShell-Befehlen</em>***  
  
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
  
## <a name="BKMK_1.3"></a>Veröffentlichen einer Anwendung, die MS-ofba verwendet  
Webanwendungsproxy unterstützt den Zugriff von Microsoft Office Clients wie Microsoft Word, die auf Dokumente und Daten auf Back-End-Servern zugreifen Der einzige Unterschied zwischen diesen Anwendungen und einem Standardbrowser besteht darin, dass die Umleitung zum Sicherheitstokendienst nicht über eine reguläre HTTP-Umleitung erfolgt, sondern mit speziellen MS-ofba-Headern, wie in: [https://msdn.microsoft.com/library/dd773463(v=office.12).aspx](https://msdn.microsoft.com/library/dd773463(v=office.12).aspx)angegeben. Die Back-End-Anwendung kann die anspruchsbasierte Authentifizierung oder die integrierte Windows-Authentifizierung verwenden.   
Zum Veröffentlichen einer Anwendung für Clients, die MS-ofba verwenden, müssen Sie der Verbunddienst eine Vertrauensstellung der vertrauenden Seite für die Anwendung hinzufügen. Je nach Anwendung können Sie die anspruchsbasierte Authentifizierung oder die integrierte Windows-Authentifizierung verwenden. Daher muss die entsprechende Vertrauensstellung der vertrauenden Seite für die Anwendung hinzugefügt werden.  
  
Damit der webanwendungsproxy Single Sign-on (SSO) ausführen und die Delegierung von Anmelde Informationen mithilfe der eingeschränkten Kerberos-Delegierung durchführen kann, muss der webanwendungsproxy-Server einer Domäne beitreten Siehe [Plan Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD).  
  
Wenn die Anwendung die anspruchsbasierte Authentifizierung verwendet, sind keine weiteren Planungsschritte erforderlich. Wenn die Anwendung die integrierte Windows-Authentifizierung verwendet hat, finden Sie weitere Informationen unter [Veröffentlichen einer integrierten Windows Authenticated-basierten Anwendung für Webbrowser Clients](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2).  
  
Der Authentifizierungs Ablauf für Clients, die das MS-ofba-Protokoll mithilfe der Anspruchs basierten Authentifizierung verwenden, wird im folgenden beschrieben. Bei der Authentifizierung für dieses Szenario kann das Anwendungstoken in der URL oder im Textkörper verwendet werden.  
  
1.  Der Benutzer arbeitet in einem Office-Programm und öffnet über die Liste **Zuletzt verwendete Dokumente** eine Datei auf einer SharePoint-Website.  
  
2.  Das Office-Programm zeigt ein Fenster mit einem Browsersteuerelement an, in dem der Benutzer Anmeldeinformationen eingeben muss.  
  
    > [!NOTE]  
    > In manchen Fällen wird das Fenster möglicherweise nicht angezeigt, weil der Client bereits authentifiziert ist.  
  
3.  Der webanwendungsproxy leitet die Anforderung an den AD FS-Server um, der die Authentifizierung ausführt.  
  
4.  Der AD FS Server leitet die Anforderung zurück an den webanwendungsproxy. Die Anforderung enthält jetzt das Edgetoken.  
  
5.  Der AD FS Server fügt der Anforderung ein Single Sign-on-Cookie (SSO) hinzu, da der Benutzer bereits eine Authentifizierung für den AD FS Server durchgeführt hat.  
  
6.  Der webanwendungsproxy überprüft das Token und leitet die Anforderung an den Back-End-Server weiter.  
  
7.  Der Back-End-Server leitet die Anforderung an den AD FS-Server um, um das Anwendungs Sicherheits Token zu erhalten.  
  
8.  Die Anforderung wird an den Back-End-Server umgeleitet. Die Anforderung enthält jetzt das Anwendungstoken und das SSO-Cookie. Dem Benutzer wird Zugriff auf die SharePoint-Website gewährt, ohne zum Anzeigen der Datei einen Benutzernamen oder ein Kennwort eingeben zu müssen.  
  
Die Schritte zum Veröffentlichen einer Anwendung, die MS-ofba verwendet, sind identisch mit den Schritten für eine Anspruchs basierte Anwendung oder eine nicht Anspruchs basierte Anwendung. Informationen zu Anspruchs basierten Anwendungen finden Sie unter Veröffentlichen [einer Anspruchs basierten Anwendung für Webbrowser Clients](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.1)für nicht Anspruchs basierte Anwendungen. Weitere Informationen finden Sie unter [Veröffentlichen einer integrierten Windows Authenticated-basierten Anwendung für Webbrowser Clients](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md#BKMK_1.2). Der webanwendungsproxy erkennt den Client automatisch und authentifiziert den Benutzer bei Bedarf.  
  
## <a name="publish-an-application-that-uses-http-basic"></a>Veröffentlichen einer Anwendung, die HTTP Basic verwendet  

HTTP Basic ist das Autorisierungs Protokoll, das von vielen Protokollen verwendet wird, um Rich-Clients, einschließlich Smartphones, mit Ihrem Exchange-Postfach zu verbinden. Weitere Informationen zu HTTP Basic finden Sie unter [RFC 2617](https://www.ietf.org/rfc/rfc2617.txt). Der webanwendungsproxy interagiert traditionell mit AD FS mithilfe von Umleitungen. die meisten Rich-Clients unterstützen keine Cookies oder Zustands Verwaltung. Auf diese Weise ermöglicht der webanwendungsproxy der http-APP, eine nicht anspruchsvolle Vertrauensstellung der vertrauenden Seite für die Anwendung für die Verbunddienst zu empfangen. Siehe [Plan Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD).  
  
Der Authentifizierungs Ablauf für Clients, die HTTP Basic verwenden, wird im folgenden und in diesem Diagramm beschrieben:  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/WebApplicationProxy_httpBasicflow.png)  
  
1.  Der Benutzer versucht, auf eine veröffentlichte Webanwendung einen Telefon Client zuzugreifen.  
  
2.  Die APP sendet eine HTTPS-Anforderung an die vom webanwendungsproxy veröffentlichte URL.  
  
3.  Wenn die Anforderung keine Anmelde Informationen enthält, gibt der webanwendungsproxy eine HTTP 401-Antwort an die APP zurück, die die URL des authentifizier enden AD FS Servers enthält.  
  
4.  Der Benutzer sendet die HTTPS-Anforderung erneut an die APP, wobei die Autorisierung im HTTPS-Authenticate-Anforderungs Header auf Basic und Benutzername und auf Basis 64 verschlüsseltes Kennwort des Benutzers festgelegt ist.  
  
5.  Da das Gerät nicht an AD FS umgeleitet werden kann, sendet der webanwendungsproxy eine Authentifizierungsanforderung an AD FS mit den Anmelde Informationen, einschließlich Benutzername und Kennwort. Das Token wird im Namen des Geräts abgerufen.  
  
6.  Um die Anzahl der an den AD FS gesendeten Anforderungen, den webanwendungsproxy, zu minimieren, überprüft nachfolgende Client Anforderungen mithilfe zwischen gespeicherter Token, solange das Token gültig ist. Der webanwendungsproxy bereinigt den Cache regelmäßig. Sie können die Größe des Caches mithilfe des Leistungs Zählers anzeigen.  
  
7.  Wenn das Token gültig ist, leitet der webanwendungsproxy die Anforderung an den Back-End-Server weiter, und dem Benutzer wird Zugriff auf die veröffentlichte Webanwendung gewährt.  
  
Im folgenden Verfahren wird erläutert, wie http-Basisanwendungen veröffentlicht werden.  
  
#### <a name="to-publish-an-http-basic-application"></a>So veröffentlichen Sie eine HTTP-Basisanwendung  
  
1.  Klicken Sie auf dem webanwendungsproxy-Server in der Remote Zugriffs-Verwaltungskonsole im **Navigations** Bereich auf **webanwendungsproxy**, und klicken Sie dann im Bereich **Tasks** auf **veröffentlichen**.  
  
2.  Klicken Sie auf der Seite **Willkommen** des **Assistenten zum Veröffentlichen neuer Anwendungen** auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS) (AD FS)** , und klicken Sie dann auf **weiter**.  
  
4.  Wählen Sie auf der Seite **Unterstützte Clients** die Option **HTTP Basic** aus, und klicken Sie auf **weiter**.  
  
    Wenn Sie den Zugriff auf Exchange nur über mit dem Arbeitsplatz verbundene Geräte aktivieren möchten, aktivieren Sie das **Kontrollkästchen Zugriff nur für mit dem Arbeitsplatz verbundene Geräte aktivieren** . Weitere Informationen finden [Sie unter Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](https://technet.microsoft.com/library/dn280945.aspx).  
  
5.  Wählen Sie auf der Seite **Vertrauende Seite** in der Liste die vertrauende Seite für die zu veröffentlichende Anwendung aus, und klicken Sie dann auf **Weiter**. Beachten Sie, dass diese Liste nur auf Ansprüche abhängige Seiten enthält.  
  
6.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie im Feld **Name** einen Anzeigenamen für die Anwendung ein.  
  
        Dieser Name wird nur in der Remotezugriffs-Verwaltungskonsole in der Liste der veröffentlichten Anwendungen verwendet.  
  
    -   Geben Sie im Feld **externe URL** die externe URL für diese Anwendung ein. Beispiel: Mail.contoso.com  
  
    -   Wählen Sie in der Liste **Externes Zertifikat** ein Zertifikat aus, dessen Antragsteller die externe URL enthält.  
  
    -   Geben Sie im Feld **URL des Back-End-Servers** die URL des Back-End-Servers ein. Beachten Sie, dass dieser Wert automatisch eingegeben wird, wenn Sie die externe URL eingeben. Sie sollten Sie nur ändern, wenn sich die URL des Back-End-Servers unterscheidet. beispielsweise Mail.contoso.com.  
  
7.  Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen, und klicken Sie dann auf **Veröffentlichen**. Sie können den PowerShell-Befehl kopieren, um weitere veröffentlichte Anwendungen einzurichten.  
  
8.  Überprüfen Sie auf der Seite **Ergebnisse**, ob die Anwendung veröffentlicht wurde, und klicken Sie dann auf **Schließen**.  
  
![](../../media/Publishing-Applications-using-AD-FS-Preauthentication/PowerShellLogoSmall.gif)von  ***<em>entsprechenden Windows PowerShell-Befehlen</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
Dieses Windows PowerShell-Skript ermöglicht die Vorauthentifizierung für alle Geräte, nicht nur für Arbeitsplatz verbundene Geräte.  
  
```  
Add-WebApplicationProxyApplication  
     -BackendServerUrl 'https://mail.contoso.com'   
     -ExternalCertificateThumbprint '697F4FF0B9947BB8203A96ED05A3021830638E50'   
     -ExternalUrl 'https://mail.contoso.com'   
     -Name 'Exchange'   
     -ExternalPreAuthentication ADFSforRichClients  
     -ADFSRelyingPartyName 'EAS_Relying_Party'  
```  
  
Im folgenden werden nur mit dem Arbeitsplatz verbundene Geräte vorab authentifiziert:  
  
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
  
## <a name="BKMK_1.4"></a>Veröffentlichen einer Anwendung, die OAuth2 verwendet, z. b. eine Microsoft Store-App  
Zum Veröffentlichen einer Anwendung für Microsoft Store-Apps müssen Sie der Verbunddienst eine Vertrauensstellung der vertrauenden Seite für die Anwendung hinzufügen.  
  
Damit der webanwendungsproxy Single Sign-on (SSO) ausführen und die Delegierung von Anmelde Informationen mithilfe der eingeschränkten Kerberos-Delegierung durchführen kann, muss der webanwendungsproxy-Server einer Domäne beitreten Siehe [Plan Active Directory](https://technet.microsoft.com/library/dn383648.aspx#BKMK_AD).  
  
> [!NOTE]  
> Webanwendungsproxy unterstützt die Veröffentlichung nur für Microsoft Store-Apps, die das OAuth 2,0-Protokoll verwenden  
  
In der AD FS-Verwaltungskonsole müssen Sie sicherstellen, dass der OAuth-Endpunkt Proxy aktiviert ist. Öffnen Sie dazu die AD FS-Verwaltungskonsole, erweitern Sie den Knoten **Dienst**, klicken Sie auf **Endpunkte**, suchen Sie in der Liste **Endpunkte** nach dem OAuth-Endpunkt, und vergewissern Sie sich, dass in der Spalte **Proxy aktiviert** der Wert **Ja**angezeigt wird.  
  
Der Authentifizierungs Ablauf für Clients, die Microsoft Store-Apps verwenden, wird im folgenden beschrieben:  
  
> [!NOTE]  
> Der webanwendungsproxy leitet zur Authentifizierung an den AD FS-Server weiter. Da Microsoft Store-Apps Umleitungen nicht unterstützen, ist es erforderlich, die URL des AD FS Servers mithilfe des Cmdlets Set-webapplicationproxyconfiguration und des oauthauthenticationurl-Parameters festzulegen, wenn Sie Microsoft Store-Apps verwenden.  
>   
> Microsoft Store-Apps können nur mithilfe von Windows PowerShell veröffentlicht werden.  
  
1.  Der Client versucht, mithilfe einer Microsoft Store-App auf eine veröffentlichte Webanwendung zuzugreifen.  
  
2.  Die APP sendet eine HTTPS-Anforderung an die vom webanwendungsproxy veröffentlichte URL.  
  
3.  Der webanwendungsproxy gibt eine HTTP 401-Antwort an die APP zurück, die die URL des authentifizier enden AD FS Servers enthält. Dieser Prozess wird als "Ermittlung" bezeichnet.  
  
    > [!NOTE]  
    > Wenn die APP die URL des authentifizier enden AD FS Servers kennt und bereits über ein Kombinations Token verfügt, das das OAuth-Token und das edgetoken enthält, werden die Schritte 2 und 3 in diesem Authentifizierungs Ablauf übersprungen.  
  
4.  Die APP sendet eine HTTPS-Anforderung an den AD FS-Server.  
  
5.  Die APP generiert mithilfe des Webauthentifizierungs Brokers ein Dialogfeld, in dem der Benutzer Anmelde Informationen für die Authentifizierung beim AD FS Server eingibt. Informationen zum Webauthentifizierungsbroker finden Sie unter [Webauthentifizierungsbroker](https://msdn.microsoft.com/library/windows/apps/hh750287.aspx).  
  
6.  Nach erfolgreicher Authentifizierung erstellt der AD FS-Server ein Kombinations Token, das das OAuth-Token und das edgetoken enthält, und sendet das Token an die app.  
  
7.  Die APP sendet eine HTTPS-Anforderung mit dem Kombinations Token an die vom webanwendungsproxy veröffentlichte URL.  
  
8.  Der webanwendungsproxy teilt das Kombinations Token in seine zwei Teile auf und überprüft das edgetoken.  
  
9. Wenn das edgetoken gültig ist, leitet der webanwendungsproxy die Anforderung nur mit dem OAuth-Token an den Back-End-Server. Dem Benutzer wird der Zugriff auf die veröffentlichte Webanwendung gewährt.  
  
Hier wird beschrieben, wie Sie eine Anwendung für OAuth2 veröffentlichen. Diese Art von Anwendung kann nur mithilfe von Windows PowerShell veröffentlicht werden. Bevor Sie beginnen, sollten Sie sicherstellen, dass Sie Folgendes ausgeführt haben:  
  
-   Es wurde eine Vertrauensstellung der vertrauenden Seite für die Anwendung in der AD FS Management Console erstellt.  
  
-   Stellen Sie sicher, dass der OAuth-Endpunkt in der AD FS-Verwaltungskonsole Proxy aktiviert ist, und notieren Sie sich den URL-Pfad.  
  
-   Es wurde überprüft, ob ein Zertifikat auf dem webanwendungsproxy-Server für die zu veröffentlichende Anwendung geeignet ist.  
  
#### <a name="to-publish-an-oauth2-app"></a>So veröffentlichen Sie eine OAuth2-App  
  
1.  Klicken Sie auf dem webanwendungsproxy-Server in der Remote Zugriffs-Verwaltungskonsole im **Navigations** Bereich auf **webanwendungsproxy**, und klicken Sie dann im Bereich **Tasks** auf **veröffentlichen**.  
  
2.  Klicken Sie auf der Seite **Willkommen** des **Assistenten zum Veröffentlichen neuer Anwendungen** auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **Vorauthentifizierung** auf **Active Directory-Verbunddienste (AD FS) (AD FS)** , und klicken Sie dann auf **weiter**.  
  
4.  Wählen Sie auf der Seite **Unterstützte Clients** **OAuth2** aus, und klicken Sie dann auf **weiter**.  
  
5.  Wählen Sie auf der Seite **Vertrauende Seite** in der Liste die vertrauende Seite für die zu veröffentlichende Anwendung aus, und klicken Sie dann auf **Weiter**.  
  
6.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie im Feld **Name** einen Anzeigenamen für die Anwendung ein.  
  
        Dieser Name wird nur in der Remotezugriffs-Verwaltungskonsole in der Liste der veröffentlichten Anwendungen verwendet.  
  
    -   Geben Sie im Feld **Externe URL** die externe URL für diese Anwendung ein, z. B. https://server1.contoso.com/app1/.  
  
    -   Wählen Sie in der Liste **Externes Zertifikat** ein Zertifikat aus, dessen Antragsteller die externe URL enthält.  
  
        Um sicherzustellen, dass Ihre Benutzer auf Ihre App zugreifen können, aktivieren Sie das Kontrollkästchen **http-zu-HTTPS-Umleitung aktivieren** , auch wenn Sie in der URL nicht den Typ HTTPS eingeben.  
  
    -   Geben Sie im Feld **URL des Back-End-Servers** die URL des Back-End-Servers ein. Beachten Sie, dass dieser Wert automatisch eingegeben wird, wenn Sie die externe URL eingeben. Sie sollten Sie nur ändern, wenn sich die URL des Back-End-Servers unterscheidet. beispielsweise https://sp/app1/.  
  
        > [!NOTE]  
        > Der webanwendungsproxy kann Hostnamen in URLs übersetzen, aber keine Pfadnamen übersetzen. Daher können Sie unterschiedliche Hostnamen eingeben, während der Pfadname gleich sein muss. Beispielsweise können Sie eine externe URL https://apps.contoso.com/app1/ und eine Back-End-Server-URL https://app-server/app1/eingeben. Es ist jedoch nicht möglich, eine externe URL https://apps.contoso.com/app1/ und eine Back-End-Server-URL https://apps.contoso.com/internal-app1/einzugeben.  
  
7.  Überprüfen Sie auf der Seite **Bestätigung** die Einstellungen, und klicken Sie dann auf **Veröffentlichen**. Sie können den PowerShell-Befehl kopieren, um weitere veröffentlichte Anwendungen einzurichten.  
  
8.  Überprüfen Sie auf der Seite **Ergebnisse**, ob die Anwendung veröffentlicht wurde, und klicken Sie dann auf **Schließen**.  
  
Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
So legen Sie die URL für die OAuth-Authentifizierung für eine Verbund Server Adresse von FS.contoso.com und den URL-Pfad/ADFS/oauth2/fest:  
  
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
  
-   [Anwendungen über den webanwendungsproxy veröffentlichen](https://technet.microsoft.com/library/dn383659.aspx)  
  
-   [Planen der Veröffentlichung von Anwendungen mit webanwendungsproxy](https://technet.microsoft.com/library/dn383650.aspx)  
  
-   [Leitfaden für webanwendungsproxy](https://technet.microsoft.com/library/dn280944.aspx)  
  
-   [Webanwendungsproxy-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/dn283404.aspx)  
  
-   [Add-webapplicationproxyapplication](https://technet.microsoft.com/library/dn283409.aspx)  
  
-   [Set-webapplicationproxyconfiguration](https://technet.microsoft.com/library/dn283406.aspx)  
  


