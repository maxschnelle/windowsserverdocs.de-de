---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: Erstellen Sie eine Anwendung mit mehreren Ebenen mit On-Behalf-Of (OBO) mit OAuth mit AD FS 2016
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8940cde2b78ce3ead499263e6fba0fbe28aae695
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016"></a>Erstellen Sie eine Anwendung mit mehreren Ebenen mit On-Behalf-Of (OBO) mit OAuth mit AD FS 2016

>Gilt für: Windows Server 2016

Diese exemplarische Vorgehensweise enthält Anweisungen für die Implementierung einer im Auftrag von (OBO) Authentifizierung mit AD FS in Windows Server2016 TP5.  O erfahren Sie mehr über OBO Authentifizierung lesen [AD FS-Szenarien für Entwickler](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)

>Warnung: Das Beispiel, das Sie hier erstellen können nur zu Lernzwecken ist. Diese Anweisungen gelten für die einfachste und die minimale Implementierung möglich, die erforderlichen Elemente des Modells verfügbar zu machen. Das Beispiel umfasst möglicherweise nicht alle Aspekte der Fehlerbehandlung und andere Funktionen beziehen und konzentriert sich nur auf eine erfolgreiche Authentifizierung der OBO abrufen.

## <a name="overview"></a>(Übersicht)

In diesem Beispiel werden wir erstellen ein Authentifizierungsablauf, in dem ein Client einen Webdienst mittlerer Ebene greifen und der Webdienst dann für den authentifizierten Client zum erhalten eines Zugriffstokens fungiert.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.PNG)

Im folgenden ist der Authentifizierungsablauf, die im Beispiel erreicht wird
1. Client authentifiziert AD FS-Autorisierung-Endpunkt und ein Autorisierungscode angefordert
2. Autorisierungsendpunkt wird Code für die Authentifizierung an Client zurückgegeben.
3. Client-Code für die Authentifizierung verwendet und zeigt sie an den AD FS-Token-Endpunkt Anforderung Zugriffstoken für mittlere Ebene Webdienst als WebAPI
4. AD FS wird das Zugriffstoken auf mittlerer Ebene Webdienst zurückgegeben. Zusätzliche Funktionen muss mittlere Ebenen-Dienst den Zugriff auf die Backend WebAPI
5. Client verwendet das Zugriffstoken, um mittlere Ebene Dienst zu verwenden.
6. Mittlere Ebenen-Dienst bietet das Zugriffstoken an den Endpunkt der AD FS-Token und Anforderungen Zugriffstoken für Backend WebAPI im Auftrag von den authentifizierten Benutzer
7. AD FS gibt Zugriffstoken für Back-End-WebAPI auf mittlere Ebenen-Dienst Actiing als Client
8. Mittlere Ebenen-Dienst verwendet das Zugriffstoken von AD FS in Schritt7 bereitgestellt, um Zugriff auf die Back-End-WebAPI als Client und Ausführen der erforderlichen Funktionen

## <a name="sample-structure"></a>Beispielstruktur für

Beispiel umfasst drei Modulen


Modul | Beschreibung
-------|------------
ToDoClient | Native Client mit dem der Benutzer interagiert.
ToDoService | Mittlerer Ebene Web-API die fungiert als Client für die Back-End-WebAPI
WebAPIOBO | Back-End-Web-API, die von ToDoService verwendet wird, zu den erforderlichen Vorgang durchführen, wenn Benutzer a ToDoItem hinzufügt.




## <a name="setting-up-the-development-box"></a>Das Feld für die Entwicklung einrichten

Diese exemplarische Vorgehensweise verwendet Visual Studio2015. Das Projekt verwendet stark Active Directory Authentifizierung Library (ADAL). Bitte lesen Sie ADAL Informationen [Active Directory-Authentifizierung Bibliothek .NET](https://msdn.microsoft.com/library/azure/mt417579.aspx)

Im Beispiel wird auch SQL LocalDB 11.0 verwendet. Installieren Sie die SQL LocalDB vor auf dem Beispiel funktioniert.

## <a name="setting-up-the-environment"></a>Einrichten der Umgebung
Wir arbeiten mit einer einfachen Installation von:

1. **DC**: Domänencontroller für die Domäne, in der AD FS gehostet werden,
2. **AD FS-Server**: der AD FS-Server für die Domäne
3. **Entwicklungscomputer**: Computer, in denen wir Visual Studio installiert haben und wird unser Beispiel entwickeln,

Sie können, wenn Sie möchten, nur zwei Computer verwenden. Eine für DC/ADFS und die andere für die Entwicklung des Beispiels.

Zum Einrichten der Domänencontroller und die AD FS ist nicht Gegenstand dieses Artikels. Weitere Informationen finden Sie unter:

- [AD DS-Bereitstellung](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS-Bereitstellung](../AD-FS-Deployment.md)

Im Beispiel ist, basierend auf dem vorhandenen OBO-Beispiel für Azure erstellt Vittorio Bertocci und [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof). Führen Sie die Anweisungen zum Klonen des Projekts auf dem Entwicklungscomputer, und erstellen Sie eine Kopie des Beispiels zum Beginnen der Arbeit mit.

## <a name="clone-or-download-this-repository"></a>Klonen oder dieses Repository herunterladen

Über die Shell oder die Befehlszeile:

    git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git

## <a name="modifying-the-sample"></a>Ändern das Beispiel

Sobald Sie die Projektmappe WebAPI-OnBehalfOf-DotNet.sln öffnen, sehen Sie sich, dass stehen Ihnen zwei Projekte in der Projektmappe-

* **ToDoListClient**: Dies dient als die der Benutzer interagiert OpenID Client
* **ToDoListService**: Dadurch werden die mittlerer Ebene WebServer App / Dienst, interagieren mit einer anderen Back-End-WebAPI OBO den authentifizierten Benutzer

Wie Sie sehen können, müssen wir später einem anderen Projekt hinzufügen, die als die Ressource fungiert, die von der ToDoListService mittlerer Ebene zugegriffen wird.

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>Konfigurieren von AD FS für den Client und WebServer-App

In der aktuellen Form des Beispiels ist die Authentifizierung mit Azure AD erfolgen konfiguriert. Wir den Authentifizierungsmechanismus ändern möchten, und direkte er zur AD FS lokalen bereitgestellt. Zu diesem Zweck müssen wir Konfigurieren von AD FS, den Client zu erkennen und WebServer-App wir haben im Beispiel.

**Erstellen eine Anwendungsgruppe**

Öffnen Sie die AD FS-MMC, und fügen Sie eine neue Anwendung hinzu. Native-Anwendung-WebAPI Vorlage auswählen.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

Klicken Sie auf Weiter, und es wird die Seite für die Angabe von Informationen zu Client-App angezeigt werden. Geben Sie einen passenden Namen für dem Client-App in AD FS. Kopieren Sie die Client-ID ein, und speichern Sie sie an einem Ort, den Sie später, wie dies in der Konfiguration der Anwendung in visual Studio erforderlich sind, zugreifen können.

>Hinweis: Umleitungs-URI kann beliebige URIS werden wie bei einem einheitlichen Clients wirklich nicht verwendet wird

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

Klicken Sie auf Weiter, und es wird die Seite für die Angabe von Informationen zu WebAPI angezeigt werden. Geben Sie einen geeigneten Namen für den AD FS-Eintrag für die WebAPI, und geben Sie die umleitungs-URI als den URI, die Sie in Visual Studio für die ToDoListService finden Sie unter

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

Klicken Sie auf Weiter, und die wählen Sie den Zugriff der Richtlinienseite angezeigt. Stellen Sie sicher, dass Sie finden Sie unter "alle Benutzer im Abschnittzu Richtlinien zulassen".

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

Klicken Sie auf Weiter, und es wird mit der Seite der App-Berechtigungen konfigurieren angezeigt werden. Wählen Sie auf dieser Seite die zulässigen Bereiche wie Openid (standardmäßig aktiviert) und User_impersonation. Der Bereich "User_impersonation" ist erforderlich, die erfolgreich im Auftrag von Zugriffstoken von AD FS anfordern können.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

Klicken Sie auf wird der Seite "Zusammenfassung" als Nächstes angezeigt werden. Der Rest des Assistenten durchlaufen Sie, und beenden Sie die Konfiguration.

Um im Auftrag von Authentifizierung zu aktivieren, müssen wir sicherstellen, dass AD FS ein Zugriffstoken mit Bereich User_impersonation an den Client zurückgegeben. Ändern Sie die Ausstellung Ansprüche für ToDoListServiceWebApi die folgenden drei benutzerdefinierte Regeln enthalten:

    @RuleName = "All claims"
    c:[]
    => issue(claim = c);

    @RuleName = "Issue open id scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "openid");

    @RuleName = "Issue user_impersonation scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**Hinzufügen von ToDoListService als Client in der Anwendungsgruppe**

In dieser Phase müssen wir einen zusätzlichen Eintrag in AD FS für die WebServer-App als Client und nicht nur als Ressource fungiert. Öffnen Sie die Anwendungsgruppe, die Sie gerade erstellt haben, und klicken Sie auf die Anwendung hinzufügen.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

Es wird die Seite "Eine neue Anwendung zum MySampleGroup hinzufügen" angezeigt werden. Wählen Sie auf der Seite "Server-Anwendung oder Website" als eigenständige Anwendung

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

Klicken Sie auf Weiter, und es wird mit der Seite, um die Anwendung Informationen angezeigt werden. Geben Sie einen geeigneten Namen für den Konfigurationseintrag "im AbschnittName. Stellen Sie sicher, dass die Client-ID als Bezeichner für die ToDoListServiceWebAPI übereinstimmt

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

Klicken Sie auf Weiter, und es wird die Seite so konfigurieren Sie die Anwendungsanmeldeinformationen angezeigt werden. Klicken Sie auf "einen gemeinsamen geheimen Schlüssel generieren". Es wird mit einem geheimen Schlüssel angezeigt werden, die automatisch generiert wird. Kopieren Sie den geheimen Schlüssel auf eine bestimmte Position, wie dies erforderlich sein wird, während wir die ToDoListService in visual Studio konfigurieren.


![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

Klicken Sie auf Weiter, und schließen Sie den Assistenten ab.

### <a name="modifying-the-todolistclient-code"></a>Ändern des Codes ToDoListClient

#### <a name="modify-the-application-config"></a>Ändern Sie die Anwendung Config

Rufen Sie Sie können das Projekt ToDoListClient WebAPI-OnBehalfOf-DotNet-Lösung. Öffnen Sie die App, und stellen Sie die folgenden Änderungen

* Kommentieren Sie den Schlüssel Ida: Mandanten-Eintrag
* Für die Ida: "redirecturi" Geben Sie den beliebigen URI, den Sie beim Konfigurieren der MySampleGroup_ClientApplication in AD FS bereitgestellt.
* Geben Sie für den Schlüssel Ida: ClientID die ID-Bezeichner, den AD FS beim Konfigurieren der MySampleGroup_ClientApplication gegeben haben.
* Die Ida: ToDoListResourceID bietet, die Ressourcen-ID konnten Sie beim Konfigurieren der ToDoListServiceWebApi in AD FS
* Kommentieren Sie die wichtigsten Ida: AADInstance
* Geben Sie die Ressourcen-ID der ToDoListServiceWebApi, für die Ida: ToDoListBaseAddress. Dies wird beim Aufrufen der ToDoList WebAPI verwendet werden.
* Hinzufügen einer Tasten Ida: Certification Authority, und geben Sie den Wert als den URI für AD FS.

Ihre **AppSettings** in App.Config sieht etwa wie folgt:

    <appSettings>
    <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />-->
    <add key="ida:ClientId" value="c7f7b85c-497c-4589-877f-b17a0bd13398" />
    <add key="ida:RedirectUri" value="https://arbitraryuri.com/" />
    <add key="ida:TodoListResourceId" value="https://localhost:44321/" />
    <!--<add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
    <add key="ida:TodoListBaseAddress" value="https://localhost:44321" />
    <add key="ida:Authority" value="https://fs.anandmsft.com/adfs/"/>
    </appSettings>

#### <a name="modifying-the-code"></a>Ändern des Codes

**MainWindow.xaml.cs**

Kommentieren Sie die Zeile, lesen die Mandanteninformationen aus der Konfiguration der Anwendung

    //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];

Ändern Sie den Wert der Zeichenfolge Behörde zu

    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

Ändern Sie den Code, um die richtigen Werte der ToDoListResourceId und ToDoListBaseAddress lesen

    private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
    private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];

Ändern Sie in der Funktion MainWindow() die Initialisierung Authcontext als:

    authContext = new AuthenticationContext(authority, false);

### <a name="adding-the-backend-resource"></a>Hinzufügen der Back-End-Ressource

Um den Fluss im Auftrag von abzuschließen, müssen Sie erstellen eine Back-End-Ressource, die die ToDoListService zugreifen im Auftrag von der authentifizierte Benutzer. Die Wahl der Back-End-Ressource kann entsprechend der Anforderung variieren, aber für dieses Beispiel können Sie eine grundlegende WebAPI erstellen.

* Klicken Sie mit der rechten Maustaste auf Lösung "WebAPI OnBehalfOf DotNet" im Projektmappen-Explorer, und wählen Sie hinzufügen -> Neues Projekt
* Wählen Sie die Vorlage "Webanwendung" ASP.NET

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* Klicken Sie auf der nächsten Aufforderung auf "Änderung Authentication"
* Wählen Sie "Arbeit und Schulkonten", und wählen Sie auf der richtigen Dropdownliste "Lokal"
* Geben Sie den federationmetadata.xml-Pfad für die AD FS-Bereitstellung, und geben Sie eine App-URI (Geben Sie alle URI für den Moment, und Sie später ändern), und klicken Sie auf Ok, um das Projekt der Projektmappe hinzuzufügen.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* Klicken Sie mit der rechten Maustaste auf Domänencontroller, im Projektmappen-Explorer unter dem neuen Projekt erstellt. Wählen Sie hinzufügen -> Domänencontroller
* Wählen Sie in der Vorlagenauswahl 'Web-API-2-Controller - Empty', und klicken Sie auf Ok.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* Benennen Sie entsprechende Controller

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* Fügen Sie folgenden Code im Controller


        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;
        namespace WebAPIOBO.Controllers
        {
            public class WebAPIOBOController : ApiController
            {
                public IHttpActionResult Get()
                {
                    return Ok("WebAPI via OBO");
                }
            }
        }

Dieser Code wird einfach die Zeichenfolge zurück, wenn jeder Benutzer eine Get-Anforderung für die WebAPI WebAPIOBO versetzt

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>Hinzufügen von neuen Back-End WebAPI zu AD FS

Öffnen Sie die Anwendungsgruppe MySampleGroup. Klicken Sie auf die Anwendung hinzufügen und Web-API-Vorlage auswählen, und klicken Sie auf Weiter.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

Geben Sie auf der Seite konfigurieren Sie Web-API einen entsprechenden Namen für den Eintrag WebAPI und den Bezeichner. Der Bezeichner sollte der Wert SSL-URL von WebAPIOBO-Projekt in visual Studio (ähnlich wie für BackendWebAPIAdfsAdd zuvor).

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

Führen Sie den Rest des Assistenten gleich als wenn wir die ToDoListService WebAPI konfiguriert. Am Ende sollte Ihre Anwendungsgruppe wie unten dargestellt aussehen:

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)


### <a name="modifying-the-todolistservice-code"></a>Ändern des Codes ToDoListService

#### <a name="modifying-the-application-config"></a>Ändern die Anwendung config

* Öffnen Sie die Datei "Web.config"
* Ändern Sie die folgenden Schlüssel

| Schlüssel | Wert |
|:-----|:-------|
|IDA: Zielgruppe| ID der ToDoListService als AD FS beim Konfigurieren der ToDoListService WebAPI https://localhost:44321/|
|IDA: ClientID| ID der ToDoListService als AD FS beim Konfigurieren der ToDoListService WebAPI https://localhost:44321/ </br>**Es ist sehr wichtig, dass die Ida: Zielgruppe und Ida: ClientID überein**|
|IDA: ClientSecret| Dies ist der geheime Schlüssel, den AD FS generiert, wenn Sie den Client ToDoListService in AD FS konfigurieren wurden|
|IDA: ADFSMetadata| Dies ist die URL zu Ihrer AD FS-Metadaten für z.B. https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml|
|IDA: OBOWebAPIBase| Dies ist die Basis-Adresse, mit denen wir das Back-End-API, z.B. https://localhost:44300 aufrufen|
|IDA: Authority| Dies ist die URL für Ihre AD FS-Dienst wird https://fs.anandmsft.com/adfs/|


Alle anderen Ida: XXXXXXX-Schlüssel der **Appsettings** Knoten auskommentiert oder gelöscht werden kann

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>Ändern Sie die Authentifizierung von Azure AD zu AD FS

* Öffnen Sie die Datei Startup.Auth.cs
* Entfernen Sie den folgenden Code

        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
                TokenValidationParameters = new TokenValidationParameters{ SaveSigninToken = true }
            });

mit

        app.UseActiveDirectoryFederationServicesBearerAuthentication(
            new ActiveDirectoryFederationServicesBearerAuthenticationOptions
            {
                MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
                TokenValidationParameters = new TokenValidationParameters()
                {
                    SaveSigninToken = true,
                    ValidAudience = ConfigurationManager.AppSettings["ida:Audience"]
                }
            });

#### <a name="modifying-the-todolistcontroller"></a>Ändern der ToDoListController

Verweis auf System.Web hinzufügen. Erweiterungen. Ändern Sie die Member der Klasse, indem der folgende Code ersetzen

    //
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    // The App Key is a credential used by the application to authenticate to Azure AD.
    // The Tenant is the name of the Azure AD tenant in which this application is registered.
    // The AAD Instance is the instance of Azure, for example public Azure or Azure China.
    // The Authority is the sign-in URL of the tenant.
    //
    private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string appKey = ConfigurationManager.AppSettings["ida:AppKey"];

    //
    // To authenticate to the Graph API, the app needs to know the Grah API's App ID URI.
    // To contact the Me endpoint on the Graph API we need the URL as well.
    //
    private static string graphResourceId = ConfigurationManager.AppSettings["ida:GraphResourceId"];
    private static string graphUserUrl = ConfigurationManager.AppSettings["ida:GraphUserUrl"];
    private const string TenantIdClaimType = "https://schemas.microsoft.com/identity/claims/tenantid";

mit

    //
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    // The client secret is the credentials for the WebServer Client

    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

    // Base address of the WebAPI
    private static string OBOWebAPIBase = ConfigurationManager.AppSettings["ida:OBOWebAPIBase"];

**Ändern Sie den Anspruch für verwendet**

Von AD FS werden wir den Nmae Anspruch ausstellen, aber wir sind nicht NameIdentifier Anspruch ausstellen. Im Beispiel verwendet NameIdentifier eindeutig Schlüssel in die ToDo-Elemente. Der Einfachheit halber können Sie problemlos die NameIdentifier mit Namensanspruch in den Code entfernen. Suchen Sie und Ersetzen Sie alle Vorkommnisse des NameIdentifier mit Namen.

**Post-Routine und CallGraphAPIOnBehalfOfUser() ändern**

Kopieren Sie und fügen Sie den folgenden Code in ToDoListController.cs ersetzen Sie den Code für die Post und CallGraphAPIOnBehalfOfUser

    // POST api/todolist
    public async Task Post(TodoItem todo)
    {
        if (!ClaimsPrincipal.Current.FindFirst("https://schemas.microsoft.com/identity/claims/scope").Value.Contains("user_impersonation"))
        {
            throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found" });
        }

        //
        // Call the WebAPIOBO On Behalf Of the user who called the To Do list web API.
        //
        string augmentedTitle = null;
        string custommessage = await CallGraphAPIOnBehalfOfUser();
        if (custommessage != null)
        {
            augmentedTitle = String.Format("{0}, Message: {1}", todo.Title, custommessage);
        }
        else
        {
            augmentedTitle = todo.Title;
        }

        if (null != todo && !string.IsNullOrWhiteSpace(todo.Title))
        {
            db.TodoItems.Add(new TodoItem { Title = augmentedTitle, Owner = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value });
            db.SaveChanges();
        }
    }

    public static async Task<string> CallGraphAPIOnBehalfOfUser()
    {
        string accessToken = null;
        AuthenticationResult result = null;
        AuthenticationContext authContext = null;
        HttpClient httpClient = new HttpClient();
        string custommessage = "";

        //
        // Use ADAL to get a token On Behalf Of the current user.  To do this we will need:
        //      The Resource ID of the service we want to call.
        //      The current user's access token, from the current request's authorization header.
        //      The credentials of this application.
        //      The username (UPN or email) of the user calling the API
        //
        ClientCredential clientCred = new ClientCredential(clientId, clientSecret);
        var bootstrapContext = ClaimsPrincipal.Current.Identities.First().BootstrapContext as System.IdentityModel.Tokens.BootstrapContext;
        string userName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn) != null ? ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value : ClaimsPrincipal.Current.FindFirst(ClaimTypes.Email).Value;
        string userAccessToken = bootstrapContext.Token;
        UserAssertion userAssertion = new UserAssertion(bootstrapContext.Token, "urn:ietf:params:oauth:grant-type:jwt-bearer", userName);

        string userId = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
        authContext = new AuthenticationContext(authority, false);

        // In the case of a transient error, retry once after 1 second, then abandon.
        // Retrying is optional.  It may be better, for your application, to return an error immediately to the user and have the user initiate the retry.
        bool retry = false;
        int retryCount = 0;

        do
        {
            retry = false;
            try
            {
                result = authContext.AcquireToken(OBOWebAPIBase, clientCred, userAssertion);
                accessToken = result.AccessToken;
            }
            catch (AdalException ex)
            {
                if (ex.ErrorCode == "temporarily_unavailable")
                {
                    // Transient error, OK to retry.
                    retry = true;
                    retryCount++;
                    Thread.Sleep(1000);
                }
            }
        } while ((retry == true) && (retryCount < 1));

        if (accessToken == null)
        {
            // An unexpected error occurred.
            return (null);
        }

        // Once the token has been returned by ADAL, add it to the http authorization header, before making the call to access the To Do list service.
        httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

        // Call the WebAPIOBO.
        HttpResponseMessage response = await httpClient.GetAsync(OBOWebAPIBase + "/api/WebAPIOBO");


        if (response.IsSuccessStatusCode)
        {
            // Read the response and databind to the GridView to display To Do items.
            string s = await response.Content.ReadAsStringAsync();
            JavaScriptSerializer serializer = new JavaScriptSerializer();
            custommessage = serializer.Deserialize<string>(s);
            return custommessage;
        }
        else
        {
            custommessage = "Unsuccessful OBO operation : " + response.ReasonPhrase;
        }
        // An unexpected error occurred calling the Graph API.  Return a null profile.
        return (null);
    }

## <a name="running-the-solution"></a>Ausführen der Projektmappe


Standardmäßig ist visual Studio so konfiguriert, dass ein Projekt ausgeführt, wenn Sie auf die Wiedergabeschaltfläche Debug ausgeführt wird.

* Klicken Sie mit der rechten Maustaste auf die Projektmappe und wählen Sie Eigenschaften.
* Die Seite "Eigenschaften" Wählen Sie Start mehrere Projekte und ändern Sie die Aktion, die für alle drei Einträge zu starten.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

Drücken Sie F5, und führen Sie die Lösung

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

Klicken Sie auf die Schaltfläche "Anmelden". Sie werden aufgefordert, melden Sie sich mit AD FS

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

Nach dem anmelden, ein ToDo-Element in der Liste hinzufügen. Hinter den Kulissen werden wir einen Post-Vorgang auf den ToDoListService möchten eine POST-Anforderung an die WebAPIOBO Web-API weiter ausgeführt wird.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

Für den reibungslosen Betrieb sehen Sie sich, dass das Element der Liste mit den zusätzlichen Meldung vom Back-End-Web-API hinzugefügt wurden, auf die zugegriffen wurde mit OBO Auth-Fluss.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

Sie können auch die detaillierten Spuren auf Fiddler angezeigt. Starten Sie Fiddler, und aktivieren Sie die HTTPS-Entschlüsselung. Sie sehen, dass wir zwei Anforderungen an den Endpunkt /adfs/oautincludes vornehmen.
In der ersten Interaktion, wir stellen die Zugangscode an den Token-Endpunkt, und erhalten eines Zugriffstokens für https://localhost:44321/ ![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO22.PNG)

In der zweiten Interaktion mit dem Token Endpunkt, Sie können sehen, dass wir **Requested_Token_use** als **on_behalf_of**, und wir verwenden das Zugriffstoken für den Webdienst von mittlerer Ebene, d.h. https://localhost:44321/ als der Assertion zum Abrufen der im Auftrag von Token abgerufen.
![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO23.PNG)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
