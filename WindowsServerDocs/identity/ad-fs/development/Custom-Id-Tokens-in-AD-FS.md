---
title: Anpassen von Ansprüchen ausgegebenen im ID-Token bei Verwendung von OpenID Connect oder OAuth mit AD FS 2016 oder höher sein.
description: Eine technische Übersicht über die benutzerdefinierte Id-token-Konzepte in AD FS 2016 oder höher
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: c4f9a2880aa91b7a600cdb40238bead7d565e6bc
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2019
ms.locfileid: "65977051"
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016-or-later"></a>Anpassen von Ansprüchen ausgegebenen im ID-Token bei Verwendung von OpenID Connect oder OAuth mit AD FS 2016 oder höher sein.

## <a name="overview"></a>Übersicht
Der Artikel [hier](native-client-with-ad-fs.md) wird gezeigt, wie Sie eine app erstellen, die AD FS verwendet wird, für die OpenID Connect, anmelden. Standardmäßig gibt es gibt jedoch nur einen festen Satz von Ansprüchen in ID-Token verfügbar. AD FS 2016 und späteren Versionen haben die Möglichkeit, die "id_token" in OpenID Connect-Szenarien anzupassen.

## <a name="when-are-custom-id-token-used"></a>Wenn benutzerdefinierte ID sind, das verwendet wird?
In bestimmten Szenarien ist es möglich, dass die Clientanwendung, die sie zugreifen möchten, ist eine Ressource nicht verfügt. Aus diesem Grund ist nicht wirklich ein Zugriffstoken erforderlich. In solchen Fällen benötigt die Clientanwendung im Wesentlichen nur einen ID-token aber einige zusätzliche Ansprüche aus, um die Funktionalität zu unterstützen.

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>Was sind die Einschränkungen für das Abrufen von benutzerdefinierter Ansprüchen in ID-token?

### <a name="scenario-1"></a>Szenario 1

![Einschränken](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  Response_mode wird als Form_post festgelegt.
2.  Nur öffentliche Clients können benutzerdefinierte Ansprüche in ID token abrufen
3.  Bezeichner vertrauenden Seite (Web-API-Bezeichner) muss als Client-ID übereinstimmen.

### <a name="scenario-2"></a>Szenario 2

![Einschränken](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

Mit [KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) auf Ihren AD FS-Servern installiert
1.  Response_mode wird als Form_post festgelegt.
2.  Sowohl öffentliche als auch vertrauliche Clients können benutzerdefinierte Ansprüche in ID token abrufen
3.  Weisen Sie Bereich Allatclaims an den Client – die RP-Paar ein.
Sie können den Bereich zuweisen, mit dem Cmdlet Grant-ADFSApplicationPermission, wie im folgenden Beispiel dargestellt:

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-and-configuring-an-oauth-application-to-handle-custom-claims-in-id-token"></a>Erstellen und Konfigurieren einer OAuth-Anwendung zur Handhabung von benutzerdefinierter Ansprüchen in ID-token
Die unten angegebenen Schritte zum Erstellen und die Anwendung für den Empfang von ID-Token mit benutzerdefinierter Ansprüche in AD FS konfigurieren.

### <a name="create-and-configure-an-application-group-in-ad-fs-2016-or-later"></a>Erstellen Sie und konfigurieren Sie eine Anwendungsgruppe in AD FS 2016 oder höher

1. In AD FS-Verwaltung mit der rechten Maustaste auf die Gruppen für Anwendungen, und wählen Sie **Anwendungsgruppe hinzufügen**.

2. Geben Sie auf den Assistenten-Anwendung, für den Namen **ADFSSSO** , und wählen Sie Client / Server-Anwendungen die **systemeigene Anwendung, die Zugriff auf eine Webanwendung** Vorlage. Klicken Sie auf **Weiter**.

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

3. Kopieren der **Clientbezeichner** Wert.  Es wird später als Wert für Ida: Client-ID in der web.config-Datei der Anwendung verwendet werden.

4. Geben Sie Folgendes für **Umleitungs-URI:**  -  **https://localhost:44320/** .  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

5. Auf der **Konfigurieren von Web-API-** Bildschirm, geben Sie Folgendes für **Bezeichner** -  **https://contoso.com/WebApp** .  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  Dieser Wert wird später verwendet werden, für die **Ida: ResourceID** in der web.config-Datei der Anwendung.

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

6. Auf der **Zugriffssteuerungsrichtlinien wählen** auf **alle zulassen** , und klicken Sie auf **Weiter**.

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

7. Auf der **Anwendungsberechtigungen konfigurieren** Bildschirm, stellen Sie sicher, dass **Openid** und **Allatclaims** ausgewählt sind, und klicken Sie auf **Weiter**.

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap5.png)

8. Auf der **Zusammenfassung** auf **Weiter**.  

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap6.png)

9. Auf der **abschließen** auf **schließen**.

10. AD FS-Verwaltung klicken Sie auf Gruppen für Anwendungen, die Liste der Gruppen für alle Anwendungen zu erhalten. Mit der rechten Maustaste auf **ADFSSSO** , und wählen Sie **Eigenschaften**. Wählen Sie **ADFSSSO - Web-API-** , und klicken Sie auf **bearbeiten...**

    ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap7.png)

11. Auf **ADFSSSO - Web-API-Eigenschaften** auf **Ausstellungstransformationsregeln** Registerkarte, und klicken Sie auf **Regel hinzufügen...**

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap8.png)

12. Auf **transformieren Anspruch Assistenten zum Hinzufügen von** auf **Ansprüche mit benutzerdefinierter Regel senden** aus der Dropdownliste aus, und klicken Sie auf **weiter**

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap9.png)

13. Auf **transformieren Anspruch Assistenten zum Hinzufügen von** Bildschirm, geben Sie **ForCustomIDToken** in **anspruchsregelname** und die folgende Anspruchsregel in **benutzerdefinierte Regel**. Klicken Sie auf **Fertig stellen**

  ```  
  x:[]
  => issue(claim=x);  
  ```

  ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap10.png)

```

>[!NOTE]
>You can also use PowerShell to assign the allatclaims and openid scopes
>``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "[Client ID from #3 above]" -ServerRoleIdentifier "[Identifier from #5 above]" -ScopeNames "allatclaims","openid"
```

### <a name="download-and-modify-the-sample-application-to-emit-custom-claims-in-idtoken"></a>Herunterladen Sie und ändern Sie die beispielanwendung zum Ausgeben von benutzerdefinierter Ansprüchen in ID-Token

In diesem Abschnitt wird erläutert, wie Sie das Beispiel-Web-APP herunterladen und ändern Sie sie in Visual Studio.   Wir verwenden das Azure AD-Beispiel, das ist [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect).  

Um das Beispielprojekt herunterzuladen, verwenden Sie Git Bash, und geben Sie Folgendes:  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect  
```  

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_1.PNG)

#### <a name="to-modify-the-app"></a>So ändern Sie die app

1.  Öffnen Sie das Beispiel mithilfe von Visual Studio.  

2.  Erstellen Sie die app neu, damit alle die fehlende NuGet-Pakete wiederhergestellt werden.  

3.  Öffnen Sie die Datei "Web.config".  Ändern Sie die folgenden Werte an, damit das Aussehen wie folgt aus:  

    ```  
    <add key="ida:ClientId" value="[Replace this Client Id from #3 above under section Create and configure an Application Group in AD FS 2016 or later]" />  
    <add key="ida:ResourceID" value="[Replace this with the Web API Identifier from #5 above]"  />
    <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />  
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />      
    <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->  
    <add key="ida:PostLogoutRedirectUri" value="[Replace this with the Redirect URI from #4 above]" />  
    ```  

    ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_2.PNG)  

4.  Öffnen Sie die Datei "Startup.Auth.cs", und nehmen Sie die folgenden Änderungen:  

    -   Optimieren Sie die OpenId Connect-Middleware Initialisierungslogik mit den folgenden Änderungen:  

        ```  
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];
        private static string resourceId = ConfigurationManager.AppSettings["ida:ResourceID"];
        private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];  
        ```  

    -   Kommentieren Sie die folgenden:  

            ```  
            //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
            ```

          ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_3.PNG)

    -   Ändern Sie weiter nach unten, die OpenId Connect-Middleware-Optionen wie im folgenden dargestellt:  

        ```  
        app.UseOpenIdConnectAuthentication(  
            new OpenIdConnectAuthenticationOptions  
            {  
                ClientId = clientId,  
                //Authority = authority,  
                Resource = resourceId,
                MetadataAddress = metadataAddress,  
                PostLogoutRedirectUri = postLogoutRedirectUri,
                RedirectUri = postLogoutRedirectUri
        ```  

        ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_4.PNG)

5.  Öffnen Sie die Datei "HomeController.cs", und nehmen Sie die folgenden Änderungen:  

    -   Führen Sie dann die folgende Aktion aus:  

            ```  
            using System.Security.Claims;  
            ```

    -   Aktualisieren Sie die About()-Methode, wie unten dargestellt:  

        ```  
        [Authorize]
        public ActionResult About()
        {
            ClaimsPrincipal cp = ClaimsPrincipal.Current;
            string userName = cp.FindFirst(ClaimTypes.WindowsAccountName).Value;
            ViewBag.Message = String.Format("Hello {0}!", userName);
            return View();
        }
        ```  

        ![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_5.PNG)

### <a name="test-the-custom-claims-in-id-token"></a>Testen Sie die benutzerdefinierten Ansprüche im ID-token

Nachdem die oben genannten Änderungen vorgenommen wurden, drücken Sie F5. Die Beispielseite wird angezeigt. Klicken Sie auf diese Option, bei der Anmeldung.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_6.PNG)

Sie werden an die AD FS-Anmeldeseite umgeleitet. Fahren Sie fort, und melden Sie sich.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_7.PNG)

Wenn dies erfolgreich war, sollten Sie sehen, dass Sie jetzt angemeldet sind.

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_8.PNG)

Klicken Sie auf diese Option, über den Link. Hallo [Benutzername] sehen Sie die von den Anspruch "Benutzername" im ID-Token abgerufen wird

![AD FS OpenID](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_9.PNG)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
