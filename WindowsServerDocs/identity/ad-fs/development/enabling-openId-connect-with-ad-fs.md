---
ms.assetid: d282bb4e-38a0-4c7c-83d8-f6ea89278057
title: Erstellen einer Web-Anwendung mithilfe von OpenID Connect mit AD FS 2016 und höher
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dbd42941f8952fc7f649636d2f3645f941240d49
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190425"
---
# <a name="build-a-web-application-using-openid-connect-with-ad-fs-2016-and-later"></a>Erstellen einer Web-Anwendung mithilfe von OpenID Connect mit AD FS 2016 und höher

## <a name="pre-requisites"></a>Voraussetzungen  
Folgendes ist eine Liste der Voraussetzungen, die vor dem Abschluss dieses Dokuments erforderlich sind. In diesem Dokument wird davon ausgegangen, dass AD FS installiert wurde und eine AD FS-Farm erstellt wurde.  

-   GitHub-Clienttools  

-   AD FS in Windows Server 2016 TP4 oder höher  

-   Visual Studio 2013 oder höher.  

## <a name="create-an-application-group-in-ad-fs-2016-and-later"></a>Erstellen Sie eine Anwendungsgruppe in AD FS 2016 und höher
Im folgende Abschnitt wird beschrieben, wie die Anwendung, die Gruppe in AD FS 2016 und höher konfiguriert wird.  

#### <a name="create-application-group"></a>Anwendungsgruppe erstellen  

1.  In AD FS-Verwaltung mit der rechten Maustaste auf die Gruppen für Anwendungen, und wählen Sie **Anwendungsgruppe hinzufügen**.  

2.  Geben Sie auf den Assistenten-Anwendung, für den Namen **ADFSSSO** und wählen Sie unter **Client-/ serveranwendungen** wählen Sie die **Webbrowser den Zugriff auf eine Webanwendung** Vorlage.  Klicken Sie auf **Weiter**.

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_1.PNG)  

3.  Kopieren der **Clientbezeichner** Wert.  Es wird später als Wert für Ida: Client-ID in der web.config-Datei der Anwendung verwendet werden.  

4.  Geben Sie Folgendes für **Umleitungs-URI:**  -  **https://localhost:44320/** .  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_2.PNG)  

5.  Auf der **Zusammenfassung** auf **Weiter**.  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_3.PNG)

6.  Auf der **abschließen** auf **schließen**.  

## <a name="download-and-modify-sample-application-to-authenticate-via-openid-connect-and-ad-fs"></a>Herunterladen Sie und ändern Sie die beispielanwendung zur Authentifizierung über OpenID Connect und AD FS  
In diesem Abschnitt wird erläutert, wie Sie das Beispiel-Web-APP herunterladen und ändern Sie sie in Visual Studio.   Wir verwenden das Azure AD-Beispiel, das ist [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect).  

Um das Beispielprojekt herunterzuladen, verwenden Sie Git Bash, und geben Sie Folgendes:  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_8.PNG)  

#### <a name="to-modify-the-app"></a>So ändern Sie die app  

1.  Öffnen Sie das Beispiel mithilfe von Visual Studio.  

2.  Erstellen Sie die app neu, damit alle die fehlende NuGet-Pakete wiederhergestellt werden.  

3.  Öffnen Sie die Datei "Web.config".  Ändern Sie die folgenden Werte an, damit das Aussehen wie folgt aus:  

    ```  
    <add key="ida:ClientId" value="[Replace this Client Id from #3 in above section]" />  
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with Redirect URI from #4 in the above section]" />  
    ```  

    ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_9.PNG)  

4.  Öffnen Sie die Datei "Startup.Auth.cs", und nehmen Sie die folgenden Änderungen:  

    -   Kommentieren Sie die folgenden:  

        ```  
        //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  

    -   Optimieren Sie die OpenId Connect-Middleware Initialisierungslogik mit den folgenden Änderungen:  

        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];  
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  

        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_10.PNG)  

    -   Ändern Sie weiter nach unten, die OpenId Connect-Middleware-Optionen wie im folgenden dargestellt:  

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

        ![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_11.PNG)  

        Ändern Sie den oben genannten machen wir Folgendes:  

        -   Anstatt die Autorität für die Kommunikation von Daten zu den vertrauenswürdigen Aussteller zu verwenden, geben wir den Speicherort des Discovery-Dokument direkt über MetadataAddress  

        -   Azure AD erzwingt das Vorhandensein eines umleitungs-URI in der Anforderung nicht, aber ADFS erreicht. Daher müssen wir sie hier hinzufügen  

## <a name="verify-the-app-is-working"></a>Stellen Sie sicher, dass die app ausgeführt wird  
Nachdem die oben genannten Änderungen vorgenommen wurden, drücken Sie F5.  Die Beispielseite wird angezeigt.  Klicken Sie auf diese Option, bei der Anmeldung.  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_12.PNG)  

Sie werden an die AD FS-Anmeldeseite umgeleitet.  Fahren Sie fort, und melden Sie sich.  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_13.PNG)  

Wenn dies erfolgreich war, sollten Sie sehen, dass Sie jetzt angemeldet sind.  

![AD FS OpenID](media/Enabling-OpenId-Connect-with-AD-FS-2016/AD_FS_OpenID_14.PNG)  

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
