---
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: Erstellen Sie eine Webanwendung, die Verwendung von OpenID Connect mit AD FS 2016
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f8040b19576ac9de4ced43e6313cad69276a3d27
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016"></a>Erstellen Sie eine Webanwendung, die Verwendung von OpenID Connect mit AD FS 2016

>Gilt für: Windows Server 2016

AD FS 2016 die anfängliche Oauth-Unterstützung in AD FS unter Windows Server2012 R2 erstellen, wird die Unterstützung für die Anmeldung OpenId Connect mit eingeführt.  
  
## <a name="pre-requisites"></a>Voraussetzungen  
Im folgenden finden eine Liste der erforderlichen Komponenten, die vor Abschluss dieses Dokuments erforderlich sind. In diesem Dokument wird davon ausgegangen, dass AD FS installiert ist und eine AD FS-Farm erstellt wurde.  
  
-   Ein Azure AD-Abonnement (eine kostenlose Testversion ist in Ordnung)  
  
-   GitHub-Client-Tools  
  
-   AD FS in Windows Server2016 Technical Preview 4 oder höher  
  
-   Visual Studio2013 oder höher.  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>Erstellen Sie eine Anwendungsgruppe in AD FS 2016  
Im folgende Abschnittwird beschrieben, konfigurieren Sie die Anwendungsgruppe in AD FS 2016.  
  
#### <a name="create-application-group"></a>Anwendungsgruppe erstellen  
  
1.  In AD FS-Verwaltung mit der rechten Maustaste auf die Gruppen aus, und wählen Sie **Anwendungsgruppe hinzufügen**.  
  
2.  Geben Sie auf den App-Assistenten für den Namen **ADFSSSO** und wählen Sie unter **eigenständige Anwendungen**wählen Sie die **Server-Anwendung oder Website** Vorlage.  Klicken Sie auf **Weiter**.  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)  
  
3.  Kopieren der **Client-ID** Wert.  Es wird später als Wert für Ida: ClientId in die Web.config-Anwendungsdatei verwendet werden.  
  
4.  Geben Sie den folgenden für **Umleitungs-URI:** - **https://localhost:44320/**.  Klicken Sie auf **hinzufügen**. Klicken Sie auf **Weiter**.  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)  
  
5.  Auf der **Anwendungsanmeldeinformationen konfigurieren** Bildschirm, aktivieren Sie das Kontrollkästchen **generieren Sie einen gemeinsamen geheimen Schlüssel**, und kopieren Sie den geheimen Schlüssel. Klicken Sie auf **weiter**  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)  
  
6.  Auf der **Zusammenfassung** auf **Weiter**.  
  
7.  Auf der **Complete** auf **schließen**.  
  
8.  Nun auf die neue Anwendungsgruppe mit der rechten Maustaste und wählen Sie **Eigenschaften**.  
  
9. Auf der **ADFSSSO Eigenschaften** klicken Sie auf **Anwendung hinzufügen**.  
  
10. Auf der **Hinzufügen einer neuen Anwendung mit Beispielanwendung** wählen **Web-API-**, und klicken Sie auf **Weiter**.  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_4.PNG)  
  
11. Auf der **konfigurieren Sie Web-API-** Bildschirm, geben Sie Folgendes für **Bezeichner** - **https://contoso.com/WebApp**.  Klicken Sie auf **hinzufügen**. Klicken Sie auf **Weiter**.  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_7.PNG)  
  
12. Auf der **Zugriffssteuerungsrichtlinie wählen** wählen **zulassen "Jeder"**, und klicken Sie auf **Weiter**.  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. Auf der **Berechtigungen konfigurieren** Bildschirm, stellen Sie sicher, dass **Openid** ausgewählt ist, und klicken Sie auf **Weiter**.  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_7.PNG)  
  
14. Auf der **Zusammenfassung** auf **Weiter**.  
  
15. Auf der **Complete** auf **schließen**.  
  
16. Auf der **Beispiel für die Anwendungseigenschaften** klicken Sie auf **OK**.  
  
## <a name="download-and-modify-mvp-app-to-authenticate-via-openid-connect-and-ad-fs"></a>Laden und Ändern von MVP-App für die Authentifizierung über OpenId Connect und AD FS  
In diesem Abschnittwird erläutert, wie das Web-API-Beispiel herunterladen, und ändern sie in Visual Studio wird.   Wir verwenden das Azure AD-Beispiel, das ist [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect).  
  
Zum Herunterladen der Beispiel-Projekt verwenden Sie Git Bash, und geben Sie Folgendes ein:  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  
  
![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)  
  
#### <a name="to-modify-the-app"></a>So ändern Sie die App  
  
1.  Öffnen Sie das Beispiel mit Visual Studio.  
  
2.  Kompilieren Sie die App so, dass die fehlenden NuGets wiederhergestellt werden.  
  
3.  Öffnen Sie die Datei "Web.config".  Ändern Sie die folgenden Werte, damit das Erscheinungsbild wie folgt:  
  
    ```  
    <add key="ida:ClientId" value="8219ab4a-df10-4fbd-b95a-8b53c1d8669e" />  
    <add key="ida:ADFSDiscoveryDoc" value="https://adfs.contoso.com/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:ResourceID" value="https://contoso.com/WebApp"  
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="https://localhost:44320/" />  
    ```  
  
    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)  
  
4.  Öffnen Sie die Datei Startup.Auth.cs, und nehmen Sie die folgenden Änderungen:  
  
    -   Kommentieren Sie die folgenden:  
  
        ```  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
    -   Optimieren Sie die Middleware Initialisierungslogik OpenId Connect mit folgenden Änderungen:  
  
        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];  
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  
  
        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)  
  
    -   Weiter unten, die OpenId Connect Middleware-Optionen wie folgt ändern:  
  
        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                MetadataAddress = metadataAddress,  
                RedirectUri = postLogoutRedirectUri,  
                PostLogoutRedirectUri = postLogoutRedirectUri 
        ```  
  
        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)  
  
        Durch Ändern der oben genannten führen wir Folgendes:  
  
        -   Anstatt die Autorität für die Kommunikation von Daten zur Identifizierung des vertrauenswürdigen Ausstellers geben wir die Ermittlung dokumentenspeicherort direkt über MetadataAddress  
  
        -   Azure AD erzwingt das Vorhandensein einer Redirect_uri in der Anforderung nicht, aber ADFS unterstützt. Daher müssen wir es hier hinzufügen  
  
## <a name="verify-the-app-is-working"></a>Stellen Sie sicher, dass die App ausgeführt wird  
Nachdem Sie die oben genannten Änderungen vorgenommen wurden, drücken Sie F5.  Dadurch wird die Seite angezeigt.  Klicken Sie auf anmelden.  
  
![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)  
  
Um die AD FS-Anmeldeseite umgeleitet werden.  Fahren Sie fort, und melden Sie sich.  
  
![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)  
  
Wenn dies erfolgreich ist sollte angezeigt werden, dass Sie jetzt angemeldet sind.  
  
![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)  
  
## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  

