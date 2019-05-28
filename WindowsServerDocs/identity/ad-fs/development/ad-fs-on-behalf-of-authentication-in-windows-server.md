---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: Erstellen einer Multi-Tier-Anwendung, die mit der im-Auftrag (OBO) mithilfe von OAuth mit AD FS 2016 oder höher
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f98141745cb5bc8355d1ad3c37e72b4710eb4fc9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190618"
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016-or-later"></a>Erstellen einer Multi-Tier-Anwendung, die mit der im-Auftrag (OBO) mithilfe von OAuth mit AD FS 2016 oder höher


Diese exemplarische Vorgehensweise enthält Anweisungen für die Implementierung einer im-Auftrag-von (OBO) Authentifizierung mithilfe von AD FS in Windows Server 2016 TP5 oder höher. Weitere Informationen zum OBO-Authentifizierung finden Sie [AD FS-Szenarien für Entwickler](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)

>WARNUNG: Das Beispiel, das Sie erstellen können, ist nur zu Lernzwecken. Diese Anweisungen gelten für die einfachste und minimale Implementierung, die Möglichkeit, um die erforderlichen Elemente des Modells verfügbar zu machen. Im Beispiel enthalten möglicherweise nicht alle Aspekte der Fehlerbehandlung und andere Funktionen beziehen und konzentriert sich nur auf eine erfolgreiche Authentifizierung für die OBO abrufen.

## <a name="overview"></a>Übersicht

In diesem Beispiel werden wir erstellen eine Authentifizierungsablauf, in dem ein Client wird auf einen Webdienst der mittleren Ebene zugreifen werden, und klicken Sie dann der Webdienst für den authentifizierten Client zum Abrufen eines Zugriffstokens angewendet wird.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.png)

Im folgenden finden Sie der Authentifizierungsablauf, den im Beispiel erreicht wird
1. Client mit AD FS-Autorisierung-Endpunkt authentifiziert und fordert einen Autorisierungscode
2. Autorisierungsendpunkt gibt Code für die Authentifizierung an Client zurück.
3. Client verwendet der Code für die Authentifizierung und präsentiert es den AD FS-token-Endpunkt auf Anforderung von Zugriffstoken für den Webdienst der mittleren Ebene als Web-API
4. AD FS gibt das Zugriffstoken an Mid-Tier-Webdienst zurück. Zusätzliche Funktionen benötigt der Dienst der mittleren Ebene Zugriff auf die Backend-WebAPI
5. Client verwendet das Zugriffstoken für den Dienst der mittleren Ebene verwendet.
6. Dienst der mittleren Ebene stellt das Zugriffstoken an den Endpunkt der AD FS-token und Anforderungen Zugriffstoken für Backend-WebAPI im-Auftrag-von des authentifizierten Benutzers
7. AD FS gibt Zugriffstoken für die Back-End-Web-API zum Dienst der mittleren Ebene Actiing zurück, als client
8. Dienst der mittleren Ebene verwendet das Zugriffstoken, das von AD FS in Schritt 7 bereitgestellt, um Zugriff auf das Back-End-Web-API als Client, und führen Sie die erforderlichen Funktionen

## <a name="sample-structure"></a>Beispielstruktur

Beispiel werden drei Modulen besteht.


Modul | Beschreibung
-------|------------
ToDoClient | Native Client, mit denen der Benutzer interagiert
ToDoService | Middle-Tier-Web-API fungiert als Client für das Back-End-Web-API
WebAPIOBO | Back-End-web-api, die von ToDoService verwendet wird, um den erforderlichen Vorgang auszuführen, wenn Benutzer ein ToDoItem hinzugefügt




## <a name="setting-up-the-development-box"></a>Das Feld für die Entwicklung einrichten

In dieser exemplarischen Vorgehensweise wird Visual Studio 2015 verwendet. Das Projekt verwendet häufig Active Directory Authentication Library (ADAL). Informationen finden Sie ADAL [Active Directory Authentication Library .NET](https://msdn.microsoft.com/library/azure/mt417579.aspx)

Das Beispiel verwendet auch SQL LocalDB V11. 0. Installieren Sie SQL LocalDB vor auf dem Beispiel.

## <a name="setting-up-the-environment"></a>Einrichten der Umgebung
Wir werden eine grundlegende Einteilung des arbeiten:

1. **DC**: Domänencontroller für die Domäne, die in der AD FS gehostet wird
2. **AD FS-Server**: Die AD FS-Server für die Domäne
3. **Entwicklungscomputer**: Computer, auf der Visual Studio installiert haben und wird in diesem Beispiel entwickeln

Sie können, wenn Sie möchten, nur zwei Computer verwenden. Eine für DC/AD FS und der andere für die Entwicklung des Beispiels.

Einrichten der Domänencontroller und AD FS sprengen den Rahmen dieses Artikels aus. Zusätzliche bereitstellungs-Informationen finden Sie unter:

- [AD DS-Bereitstellung](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS-Bereitstellung](../AD-FS-Deployment.md)

Im Beispiel wird basierend auf dem vorhandenen OBO-Beispiel für Azure, die von Vittorio Bertocci erstellt wurden und verfügbar [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof). Führen Sie die Anweisungen zum Klonen des Projekts auf dem Entwicklungscomputer, und erstellen ein Exemplar des Beispiels zum Arbeiten mit ein.

## <a name="clone-or-download-this-repository"></a>Klonen oder Herunterladen von diesem repository

Der Shell oder über die Befehlszeile:

    git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git

## <a name="modifying-the-sample"></a>Ändern das Beispiel

Sobald Sie die Web-API-OnBehalfOf-DotNet.sln Projektmappe öffnen, werden Sie feststellen, dass Sie in der Projektmappe zwei Projekte verfügen

* **ToDoListClient**: Dies wird wie der OpenID-Client dienen, der der Benutzer interagieren
* **ToDoListService**: Dadurch werden die Anwendung der mittleren Ebene WebServer / Dienst, wird sein Interaktion mit einem anderen Back-End-WebAPI OBO den authentifizierten Benutzer

Wie Sie sehen können, müssen wir später ein anderes Projekt hinzufügen, die als Ressource fungiert, die von der mittleren Ebene "todolistservice" zugegriffen wird.

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>Konfigurieren von AD FS für den Client und WebServer-App

In der derzeitigen Form des Beispiels ist die Authentifizierung bei Azure AD durchgeführt werden konfiguriert. Wir den Authentifizierungsmechanismus ändern möchten, und direkte es für AD FS lokal bereitgestellt. Zu diesem Zweck müssen wir Konfigurieren von AD FS für die der Client erkennen und die WebServer-App, die wir im Beispiel.

**Erstellen eine Anwendungsgruppe**

Öffnen Sie die AD FS-Verwaltungs-MMC, und fügen Sie eine neue Anwendung hinzu. Native-Anwendung-Web-API-Vorlage auswählen.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

Klicken Sie auf Weiter, und es wird mit der Seite für die Bereitstellung von Informationen zu Client-App angezeigt werden. Geben Sie einen passenden Namen, an dem Client-App in AD FS. Kopieren Sie den Client-ID, und speichern Sie sie an einer Stelle dich später, wie dies in der Konfigurationsdatei der Anwendung in visual Studio erforderlich ist.

>Hinweis: Der Umleitungs-URI kann jeder beliebigen URI sein, da es nicht wirklich bei nativen Clients verwendet wird

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

Klicken Sie auf Weiter, und es wird mit der Seite für die Bereitstellung von Informationen zu Web-API angezeigt werden. Geben Sie einen geeigneten Namen für den AD FS-Eintrag für die Web-API, und geben Sie den umleitungs-URI als den URI, die Sie für "todolistservice" in Visual Studio angezeigt

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

Klicken Sie auf Weiter, und Sie sehen, wählen Sie Access Control Seite mit der Richtlinie. Stellen Sie sicher, dass Sie finden Sie unter "alle Benutzer in dem Richtlinienabschnitt zulassen".

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

Klicken Sie auf Weiter, und es wird mit der Konfigurationsseite der Anwendungsberechtigungen angezeigt werden. Wählen Sie auf dieser Seite die zulässigen Bereiche als Openid (standardmäßig ausgewählt) und "user_impersonation" ein. Der Bereich "User_impersonation" ist erforderlich, die erfolgreich ein im-Auftrag-von Zugriffstoken von AD FS anfordern können.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

Klicken Sie auf wird der Seite "Zusammenfassung" als Nächstes angezeigt werden. Durchlaufen Sie den Assistenten, und schließen Sie die Konfiguration.

Um eine im-Auftrag-von Authentifizierung zu ermöglichen, müssen wir sicherstellen, dass AD FS ein Zugriffstoken mit Bereich "user_impersonation" an den Client zurückgibt. Ändern Sie die Ausstellung von Ansprüchen für ToDoListServiceWebApi auf die folgenden drei benutzerdefinierte Regeln enthalten:

    @RuleName = "All claims"
    c:[]
    => issue(claim = c);

    @RuleName = "Issue user_impersonation scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**Hinzufügen von "todolistservice" als Client in der Anwendungsgruppe**

In dieser Phase müssen wir einen weiteren Eintrag in AD FS für die WebServer-App, die als Client und nicht nur als Ressource fungiert vornehmen. Öffnen Sie die Anwendungsgruppe, die Sie gerade erstellt haben, und klicken Sie auf die Anwendung hinzufügen.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

Es wird die Seite "Hinzufügen eine neue Anwendung in MySampleGroup" angezeigt werden. Wählen Sie auf dieser Seite "Server-Anwendung oder Website" als eigenständige Anwendung

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

Klicken Sie auf Weiter und wird mit der Seite zu Details zur Anwendung angezeigt. Geben Sie einen geeigneten Namen für den Konfigurationseintrag in den "Antragsteller". Stellen Sie sicher, dass die Client-ID als Bezeichner für die ToDoListServiceWebAPI identisch ist

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

Klicken Sie auf Weiter, und Sie werden die Seite so konfigurieren Sie die Anmeldeinformationen der Anwendung angezeigt werden. Klicken Sie auf "einen gemeinsamen geheimen Schlüssel generieren". Es wird mit einem geheimen Schlüssel angezeigt werden, die automatisch generiert wird. Kopieren Sie den geheimen Schlüssel auf einen Speicherort aus, da dies erforderlich werden, während wir den "todolistservice" in visual Studio konfigurieren.


![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

Klicken Sie auf Weiter, und schließen Sie den Assistenten.

### <a name="modifying-the-todolistclient-code"></a>Ändern des Codes "todolistclient"

#### <a name="modify-the-application-config"></a>Ändern der Anwendungskonfiguration

Wechseln Sie zu der Sie können das Projekt "todolistclient" in Web-API-OnBehalfOf-DotNet-Lösung. Öffnen Sie die Datei "App.config", und nehmen die folgenden Änderungen vor

* Kommentieren Sie den Schlüssel Ida: Mandanten-Eintrag
* Die Ida: umleitungs-URI eingeben, die beliebigen URI, die Sie beim Konfigurieren der MySampleGroup_ClientApplication in AD FS bereitgestellt.
* Geben Sie für den Schlüssel "Ida: ClientID" den Client-ID-Bezeichner, den AD FS, die beim Konfigurieren der MySampleGroup_ClientApplication gegeben haben.
* Für die Ida: ToDoListResourceID bieten die Ressourcen-ID konnten Sie beim Konfigurieren der ToDoListServiceWebApi in AD FS
* Kommentieren Sie die wichtigsten Ida: AADInstance
* Geben Sie für die Ida: ToDoListBaseAddress der Ressourcen-ID der ToDoListServiceWebApi aus. Diese wird beim Aufrufen der ToDoList WebAPI verwendet werden.
* Fügen Sie eine wichtige Ida: Autorität aus, und geben Sie den Wert als URI für AD FS.

Ihre **"appSettings"** in "App.config" sieht in etwa wie folgt:

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

Kommentieren Sie die Zeile, die Informationen des Mandanten aus der Konfigurationsdatei der Anwendung lesen

    //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];

Ändern Sie den Wert der Zeichenfolge-Autorität auf

    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

Ändern Sie den Code, um die richtigen Werte ToDoListResourceId und ToDoListBaseAddress lesen

    private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
    private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];

Ändern Sie in der Funktion MainWindow() die Authcontext Initialisierung als:

    authContext = new AuthenticationContext(authority, false);

### <a name="adding-the-backend-resource"></a>Hinzufügen der Back-End-Ressource

Um den im-Auftrag-von-Fluss abzuschließen, müssen Sie eine Back-End-Ressource, die auf ToDoListService zugreifen im-Auftrag-von Erstellen des authentifizierten Benutzers. Die Wahl der Back-End-Ressource kann nach Bedarf variieren, aber im Rahmen dieses Beispiels können Sie eine einfache Web-API erstellen.

* Klicken Sie mit der rechten Maustaste auf Lösung "WebAPI"onbehalfof "DotNet" im Projektmappen-Explorer, und wählen Sie Add -> Neues Projekt
* ASP.NET Web Application-Vorlage auswählen

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* Klicken Sie auf der nächsten Aufforderung auf "Authentifizierung ändern"
* Wählen Sie "Geschäfts- und Schulkonten", und wählen Sie auf der rechten Dropdownliste "Lokal"
* Geben Sie den Pfad "FederationMetadata.xml" für Ihre AD FS-Bereitstellung und App-URI (Geben Sie einen beliebigen URI jetzt, und Sie später ändern), und klicken Sie auf Ok, um das Projekt zur Projektmappe hinzuzufügen.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* Klicken Sie mit der rechten Maustaste auf Controller, im Projektmappen-Explorer unter das neue Projekt erstellt wurde. Wählen Sie -> Controller hinzufügen
* Wählen Sie in der Vorlagenauswahl "Web API 2-Controller - leer", und klicken Sie auf Ok.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* Benennen Sie geeigneten controller

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* Fügen Sie den folgenden Code im controller


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

Dieser Code wird einfach die Zeichenfolge zurück, wenn jemand eine Get-Anforderung für die WebAPI WebAPIOBO versetzt

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>Hinzufügen der neuen Back-Ends-Web-API mit AD FS

Öffnen Sie die MySampleGroup Anwendungsgruppe. Klicken Sie auf die Anwendung hinzufügen und die Web-API-Vorlage auswählen, und klicken Sie auf Weiter.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

Geben Sie einen geeigneten Namen für den Eintrag für die Web-API und die ID, auf der Seite "Konfigurieren von Web-API". Der Bezeichner muss der Wert sein SSL-URL aus WebAPIOBO-Projekt in visual Studio (ähnlich wie für für BackendWebAPIAdfsAdd).

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

Weiterhin über den Assistenten identisch, wenn wir die ToDoListService WebAPI konfiguriert. Am Ende sollten Ihre Anwendungsgruppe wie folgt aussehen:

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)


### <a name="modifying-the-todolistservice-code"></a>Ändern den Code für "todolistservice"

#### <a name="modifying-the-application-config"></a>Ändern der Anwendungskonfiguration

* Öffnen Sie die Datei "Web.config"
* Ändern Sie die folgenden Schlüssel

| Key | Wert |
|:-----|:-------|
|ida:Audience| Die ID des wie AD FS beim Konfigurieren des ToDoListService WebAPI, z. B. "todolistservice", https://localhost:44321/|
|ida:ClientID| Die ID des wie AD FS beim Konfigurieren des ToDoListService WebAPI, z. B. "todolistservice", https://localhost:44321/ </br>**Es ist sehr wichtig, dass die Ida: Zielgruppe und die Ida: Client-ID übereinstimmen**|
|ida:ClientSecret| Dies ist der geheime Schlüssel, den AD FS generiert, wenn Sie den Client "todolistservice" in AD FS konfigurieren wurden|
|ida:AdfsMetadataEndpoint| Dies ist die URL für Ihre AD FS-Metadaten für z. B. https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml|
|ida:OBOWebAPIBase| Dies ist die Basisadresse, die wir verwenden das Back-End-API, z. B. aufrufen https://localhost:44300|
|ida:Authority| Dies ist die URL für Ihren AD FS-Dienst, Beispiel https://fs.anandmsft.com/adfs/|


Alle anderen Ida: XXXXXXX-Schlüsseln in der **"appSettings"** Knoten auskommentiert oder gelöscht werden kann

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>Ändern Sie die Authentifizierung von Azure AD und AD FS

* Öffnen Sie die Datei Startup.Auth.cs
* Entfernen Sie den folgenden Code.

        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
                TokenValidationParameters = new TokenValidationParameters{ SaveSigninToken = true }
            });

durch

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

#### <a name="modifying-the-todolistcontroller"></a>Ändern die ToDoListController

Fügen Sie der Verweis auf System.Web.Extensions hinzu. Ändern Sie die Klassenmember, indem Sie den folgenden Code ersetzen

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

durch

    //
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    // The client secret is the credentials for the WebServer Client

    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

    // Base address of the WebAPI
    private static string OBOWebAPIBase = ConfigurationManager.AppSettings["ida:OBOWebAPIBase"];

**Ändern Sie den Anspruch für Namen verwendet**

Von AD FS werden wir den Nmae Anspruch ausstellen, aber wir NameIdentifier-Anspruch nicht ausgeben. Das Beispiel verwendet die NameIdentifier eindeutig Schlüssel in der ToDo-Elemente. Der Einfachheit halber können Sie problemlos den NameIdentifier mit Name-Anspruch im Code entfernen. Suchen Sie und Ersetzen Sie alle Vorkommen von NameIdentifier mit dem Namen.

**Ändern der Post-Routine und CallGraphAPIOnBehalfOfUser()**

Kopieren Sie und fügen Sie den folgenden Code in ToDoListController.cs aus, und Ersetzen Sie den Code für Post- und CallGraphAPIOnBehalfOfUser

    // POST api/todolist
    public async Task Post(TodoItem todo)
    {
      if (!ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value.Contains("user_impersonation"))
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
        // The Resource ID of the service we want to call.
        // The current user's access token, from the current request's authorization header.
        // The credentials of this application.
        // The username (UPN or email) of the user calling the API
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
                    result = await authContext.AcquireTokenAsync(OBOWebAPIBase, clientCred, userAssertion);
                    //result = await authContext.AcquireTokenAsync(...);
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

## <a name="running-the-solution"></a>Ausführen der Lösung


Standardmäßig ist visual Studio konfiguriert, um ein Projekt ausgeführt, wenn Sie Debuggen, ausführen erreichen.

* Klicken Sie mit der rechten Maustaste auf die Projektmappe, und wählen Sie die Eigenschaften.
* Die Seite "Eigenschaften" Wählen Sie mehrere Startprojekte und ändern Sie die Aktion, die für alle drei Einträge zu starten.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

Drücken Sie F5, und führen Sie die Lösung

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

Klicken Sie auf die Schaltfläche "Anmelden". Sie werden aufgefordert, melden Sie sich mithilfe von AD FS

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

Nach der Anmeldung, ToDo-Element in der Liste hinzufügen. Hinter den Kulissen werden wir einen Post-Vorgang um "todolistservice" ausführen, wodurch die weiteren einen POST-Aufruf die WebAPIOBO-Web-API ausgeführt werden.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

Für die erfolgreiche Ausführung sehen Sie sich, dass das Element der Liste mit der zusätzlichen Meldung aus dem Back-End-Web-API hinzugefügt wurde, auf die zugegriffen wurde mit OBO-authentifizierungsfluss.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

Sie können auch die ausführlichen ablaufverfolgungen auf Fiddler sehen. Starten Sie Fiddler, und aktivieren Sie der Entschlüsselung von HTTPS. Sie können sehen, dass wir zwei Anforderungen an den Endpunkt /adfs/oautincludes vornehmen.
In der ersten Interaktion, wir der Access-Code an den tokenendpunkt vorhanden, und Abrufen eines Zugriffstokens für https://localhost:44321/ ![OBO für AD FS](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO22.PNG)

Im zweiten Interaktion mit den token-Endpunkt, sehen Sie, dass wir haben **Requested_token_use** als **on_behalf_of** und verwenden wir das Zugriffstoken für den Webdienst der mittleren Ebene, d. h. https://localhost:44321/ als die Assertion, die im-Auftrag-von-Token zu erhalten.
![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO23.PNG)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
