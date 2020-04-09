---
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: Erstellen einer Webanwendung mit OpenID Connect mit AD FS 2016 und höher
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 49d952a49cf474708f57a0ae2a7760d2470af607
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857493"
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016-and-later"></a>Erstellen einer Webanwendung mit OpenID Connect mit AD FS 2016 und höher

## <a name="pre-requisites"></a>Voraussetzungen  
Im folgenden finden Sie eine Liste der Voraussetzungen, die vor der Fertigstellung dieses Dokuments erforderlich sind. In diesem Dokument wird davon ausgegangen, dass AD FS installiert und eine AD FS-Farm erstellt wurde.  

-   GitHub-Client Tools  

-   AD FS in Windows Server 2016 TP4 oder höher  

-   Visual Studio 2013 oder höher.  

## <a name="create-an-application-group-in-ad-fs-2016-and-later"></a>Erstellen einer Anwendungs Gruppe in AD FS 2016 und höher
Im folgenden Abschnitt wird beschrieben, wie Sie die Anwendungs Gruppe in AD FS 2016 und höher konfigurieren.  

#### <a name="create-application-group"></a>Anwendungs Gruppe erstellen  

1.  Klicken Sie in AD FS Verwaltung mit der rechten Maustaste auf Anwendungs Gruppen, und wählen Sie **Anwendungs Gruppe hinzufügen**aus.  

2.  Geben Sie im Anwendungs Gruppen-Assistenten für den Namen **ADF-so** ein, und wählen Sie unter **Client-Server Anwendungen** den Webbrowser aus, der auf **eine Webanwendungsvorlage zugreift** .  Klicken Sie auf **Weiter**.

    ![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)  

3.  Kopieren Sie den Wert für den **Client Bezeichner** .  Sie wird später als Wert für "Ida: ClientID" in der Datei "Web. config" der Anwendung verwendet.  

4.  Geben Sie Folgendes für den **Umleitungs-URI ein:**  -  **https://localhost:44320/** .  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  

    ![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)  

5.  Klicken Sie auf dem Bildschirm **Zusammenfassung** auf **weiter**.  

    ![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)

6.  Klicken Sie im Bildschirm **Fertig** stellen auf **Schließen**.  

## <a name="download-and-modify-sample-application-to-authenticate-via-openid-connect-and-ad-fs"></a>Herunterladen und Ändern der Beispielanwendung für die Authentifizierung über OpenID Connect und AD FS  
In diesem Abschnitt wird erläutert, wie Sie die Beispiel-Web-App herunterladen und in Visual Studio ändern.   Wir verwenden das [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)Azure AD Beispiel.  

Verwenden Sie zum Herunterladen des Beispielprojekts git bash, und geben Sie Folgendes ein:  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)  

#### <a name="to-modify-the-app"></a>So ändern Sie die APP  

1.  Öffnen Sie das Beispiel mithilfe von Visual Studio.  

2.  Erstellen Sie die APP neu, sodass alle fehlenden nugets wieder hergestellt werden.  

3.  Öffnen Sie die Datei "Web. config".  Ändern Sie die folgenden Werte so, dass Sie wie folgt aussehen:  

    ```  
    <add key="ida:ClientId" value="[Replace this Client Id from #3 in above section]" />  
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with Redirect URI from #4 in the above section]" />  
    ```  

    ![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)  

4.  Öffnen Sie die Datei Startup.auth.cs, und nehmen Sie die folgenden Änderungen vor:  

    -   Kommentieren Sie Folgendes aus:  

        ```  
        //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  

    -   Optimieren Sie die Initialisierungs Logik der OpenID Connect-Middleware mit den folgenden Änderungen:  

        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];  
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  

        ![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)  

    -   Ändern Sie die Optionen für die OpenID Connect-Middleware wie folgt:  

        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                MetadataAddress = metadataAddress,  
                PostLogoutRedirectUri = postLogoutRedirectUri,
                RedirectUri = postLogoutRedirectUri
        ```  

        ![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)  

        Durch Ändern der oben genannten Aktionen gehen wir wie folgt vor:  

        -   Anstatt die Berechtigung zum Kommunizieren von Daten über den vertrauenswürdigen Aussteller zu verwenden, geben wir den Speicherort des Discovery doc direkt über MetadataAddress an.  

        -   Azure AD erzwingt nicht das vorhanden sein einer redirect_uri in der Anforderung, ADFS jedoch. Wir müssen ihn hier hinzufügen.  

## <a name="verify-the-app-is-working"></a>Überprüfen, ob die APP funktioniert  
Nachdem die obigen Änderungen vorgenommen wurden, drücken Sie F5.  Dadurch wird die Beispielseite angezeigt.  Klicken Sie auf anmelden.  

![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)  

Sie werden auf die AD FS Anmeldeseite umgeleitet.  Fahren Sie fort, und melden Sie sich an.  

![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)  

Wenn dies erfolgreich ist, sollten Sie sehen, dass Sie jetzt angemeldet sind.  

![OpenID AD FS](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)  

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
