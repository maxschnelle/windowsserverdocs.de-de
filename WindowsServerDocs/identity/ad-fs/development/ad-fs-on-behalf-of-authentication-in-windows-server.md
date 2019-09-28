---
ms.assetid: 5052f13c-ff35-471d-bff5-00b5dd24f8aa
title: Erstellen einer Anwendung mit mehreren Stufen mithilfe von "on-Auftrag-of" (OBO) mithilfe von OAuth mit AD FS 2016 oder höher
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9c6c6e7d2c12b6b822989bba05370015f7cd1833
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407811"
---
# <a name="build-a-multi-tiered-application-using-on-behalf-of-obo-using-oauth-with-ad-fs-2016-or-later"></a>Erstellen einer Anwendung mit mehreren Stufen mithilfe von "on-Auftrag-of" (OBO) mithilfe von OAuth mit AD FS 2016 oder höher


Diese exemplarische Vorgehensweise enthält Anweisungen zum Implementieren einer "in-Auftrag-von"-Authentifizierung (OBO) mithilfe von AD FS in Windows Server 2016 TP5 oder höher. Weitere Informationen zur OBO-Authentifizierung finden Sie unter [AD FS OpenID Connect/OAuth-Flows und Anwendungs Szenarios](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md) .

>WARNUNG: Das Beispiel, das Sie hier erstellen können, dient nur zu Schulungszwecken. Diese Anweisungen gelten für die einfachste, kleinste Implementierung, die die erforderlichen Elemente des Modells verfügbar machen kann. Das Beispiel enthält möglicherweise nicht alle Aspekte der Fehlerbehandlung und weitere Funktionen, die sich nur auf die erfolgreiche OBO-Authentifizierung beziehen.

## <a name="overview"></a>Übersicht

In diesem Beispiel erstellen wir einen Authentifizierungs Fluss, bei dem ein Client auf einen Webdienst der mittleren Ebene zugreift, und der Webdienst wird dann im Namen des authentifizierten Clients ausgeführt, um ein Zugriffs Token zu erhalten.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO28.png)

Im folgenden finden Sie den Authentifizierungs Ablauf, den das Beispiel erreicht.
1. Client authentifiziert sich bei AD FS Autorisierungs Endpunkt und fordert einen Autorisierungs Code an
2. Der Autorisierungs Endpunkt gibt Authentifizierungscode an den Client zurück.
3. Der Client verwendet den Authentifizierungscode und präsentiert ihn dem AD FS Token-Endpunkt, um ein Zugriffs Token für den Webdienst der mittleren Ebene als WebAPI anzufordern.
4. AD FS gibt das Zugriffs Token für den Mid-Tier-Webdienst zurück. Für zusätzliche Funktionalität benötigt der Dienst der mittleren Ebene Zugriff auf die Back-End-WebAPI.
5. Der Client verwendet das Zugriffs Token für die Verwendung des Diensts der mittleren Ebene.
6. Der Dienst der mittleren Ebene stellt das Zugriffs Token für den Endpunkt des AD FS Tokens bereit und fordert im Auftrag des authentifizierten Benutzers ein Zugriffs Token für die Back-End-WebAPI an.
7. AD FS gibt das Zugriffs Token für die Back-End-WebAPI an die Dienst Aktivierung der mittleren Ebene als Client zurück
8. Der Dienst der mittleren Ebene verwendet das Zugriffs Token, das in Schritt 7 AD FS, um auf die Back-End-WebAPI als Client zuzugreifen und die erforderlichen Funktionen auszuführen.

## <a name="sample-structure"></a>Beispiel Struktur

Das Beispiel besteht aus drei Modulen.


Modul | Beschreibung
-------|------------
-Client | Native Client, mit dem der Benutzer interagiert
ToDoService | Web-API der mittleren Ebene, die als Client für die Back-End-WebAPI fungiert
Webapiobo | Back-End-Web-API, die von "dedoservice" zum Ausführen des erforderlichen Vorgangs verwendet wird, wenn der Benutzer ein ""




## <a name="setting-up-the-development-box"></a>Einrichten der Entwicklungs Box

In dieser exemplarischen Vorgehensweise wird Visual Studio 2015 verwendet. Das Projekt verwendet stark Active Directory-Authentifizierungsbibliothek (Adal). Weitere Informationen zu Adal finden Sie unter [Active Directory-Authentifizierungsbibliothek .net](https://msdn.microsoft.com/library/azure/mt417579.aspx)

Das Beispiel verwendet auch SQL localdb v 11.0. Installieren Sie die SQL localdb, bevor Sie mit dem Beispiel arbeiten.

## <a name="setting-up-the-environment"></a>Einrichten der Umgebung
Wir arbeiten mit einer grundlegenden Einrichtung von:

1. **DC**: Domänen Controller für die Domäne, in der AD FS gehostet werden.
2. **AD FS Server**: Der AD FS Server für die Domäne
3. **Entwicklungs Computer**: Computer, auf dem Visual Studio installiert ist und das Beispiel entwickelt wird

Wenn Sie möchten, können Sie nur zwei Computer verwenden. Eine für DC/ADFS und die andere für die Entwicklung des Beispiels.

Das Einrichten des Domänen Controllers und AD FS würde den Rahmen dieses Artikels sprengen. Weitere Informationen zur Bereitstellung finden Sie unter:

- [AD DS-Bereitstellung](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS-Bereitstellung](../AD-FS-Deployment.md)

Das Beispiel basiert auf dem vorhandenen OBO-Beispiel für Azure, das von Vittorio Bertocci erstellt und [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof)verfügbar ist. Befolgen Sie die Anweisungen, um das Projekt auf dem Entwicklungs Computer zu klonen, und erstellen Sie eine Kopie des Beispiels, um mit der Arbeit mit zu beginnen.

## <a name="clone-or-download-this-repository"></a>Dieses Repository Klonen oder herunterladen

Über Ihre Shell oder Befehlszeile:

    git clone https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof.git

## <a name="modifying-the-sample"></a>Ändern des Beispiels

Sobald Sie die Projekt Mappe WebAPI-OnBehalfOf-dotnet. sln öffnen, werden Sie feststellen, dass Sie über zwei Projekte in der Projekt Mappe verfügen.

* ""- **Listclient**: Dies dient als OpenID-Client, mit dem der Benutzer interagieren wird.
* " **Dedolistservice**": Dabei handelt es sich um die Webserver-App/den Dienst der mittleren Ebene, die mit einem anderen Back-End-WebAPI-Dienst (authentifizierter Benutzer) interagieren

Wie Sie sehen können, müssen Sie später ein weiteres Projekt hinzufügen, das als Ressource fungiert, auf die der Dienst der mittleren Ebene "" zugreifen kann.

### <a name="configuring-ad-fs-for-the-client-and-webserver-app"></a>Konfigurieren von AD FS für die Client-und die Webserver-App

In der aktuellen Form des Beispiels ist die Authentifizierung so konfiguriert, dass Sie mit Azure AD ausgeführt wird. Wir möchten den Authentifizierungsmechanismus ändern und ihn an AD FS lokal bereitgestellten Bereitstellung weiterleiten. Um dies zu tun, müssen wir AD FS konfigurieren, um die Client-und die Webserver-APP zu erkennen, die im Beispiel vorhanden ist.

**Erstellen einer Anwendungs Gruppe**

Öffnen Sie die MMC für die AD FS Verwaltung, und fügen Sie eine neue Anwendungs Gruppe hinzu. Wählen Sie Native-Application-WebAPI-Vorlage aus.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO2.PNG)

Klicken Sie auf Weiter, um die Seite mit Informationen zur Client-App bereitzustellen. Benennen Sie die Client-app in AD FS entsprechend. Kopieren Sie die Client-ID, und speichern Sie Sie an einem beliebigen Ort, auf den Sie später zugreifen können. Dies ist in der Anwendungskonfiguration in Visual Studio erforderlich.

>Hinweis: Der Umleitungs-URI kann ein beliebiger URI sein, da er bei nativen Clients wirklich nicht verwendet wird.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO11.PNG)

Klicken Sie auf Weiter, um die Seite mit Informationen zu WebAPI bereitzustellen. Geben Sie einen passenden Namen für den AD FS Eintrag für die WebAPI an, und geben Sie den Umleitungs-URI als URI ein, den Sie in Visual Studio für den Dienst "" "" ""

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO16.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO18.PNG)

Wenn Sie auf Weiter klicken, wird die Seite Access Control Richtlinie auswählen angezeigt. Stellen Sie sicher, dass im Abschnitt Richtlinie "Alle zulassen" angezeigt wird.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO1.PNG)

Wenn Sie auf Weiter klicken, wird die Seite Anwendungs Berechtigungen konfigurieren angezeigt. Wählen Sie auf dieser Seite die zulässigen Bereiche als OpenID (standardmäßig ausgewählt) und user_impersonation aus. Der Bereich "user_impersonation" ist erforderlich, um erfolgreich ein Zugriffs Token aus AD FS anfordern zu können.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO12.PNG)

Klicken Sie auf Weiter, um die Seite Zusammenfassung anzuzeigen. Durchlaufen Sie den Rest des Assistenten, und schließen Sie die Konfiguration ab.

Um die Authentifizierung im Auftrag der Authentifizierung zu aktivieren, müssen Sie sicherstellen, dass AD FS ein Zugriffs Token mit dem Bereich user_impersonation an den Client zurückgibt. Ändern Sie die Anspruchs Ausstellung für todolistservicewebapi so, dass Sie die folgenden drei benutzerdefinierten Regeln enthält:

    @RuleName = "All claims"
    c:[]
    => issue(claim = c);

    @RuleName = "Issue user_impersonation scope"
    => issue(Type = "https://schemas.microsoft.com/identity/claims/scope", Value = "user_impersonation");

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO10.PNG)

**Hinzufügen von "dedolistservice" als Client in der Anwendungs Gruppe**

In dieser Phase müssen Sie einen zusätzlichen Eintrag in AD FS erstellen, damit die Webserver-App als Client und nicht nur als Ressource fungiert. Öffnen Sie die soeben erstellte Anwendungs Gruppe, und klicken Sie auf Anwendung hinzufügen.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO15.PNG)

Die Seite "neue Anwendung zu mysamplegroup hinzufügen" wird angezeigt. Wählen Sie auf dieser Seite die Option "Server Anwendung oder Website" als eigenständige Anwendung aus.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO19.PNG)

Wenn Sie auf Weiter klicken, wird die Seite angezeigt, auf der Sie die Details der Anwendung angeben können. Geben Sie einen geeigneten Namen für den Konfigurationseintrag im Abschnitt Name an. Stellen Sie sicher, dass der Client Bezeichner mit dem Bezeichner für die "" "" "" "" ""

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO20.PNG)

Wenn Sie auf Weiter klicken, wird die Seite angezeigt, auf der Sie die Anmelde Informationen für die Anwendung konfigurieren können. Klicken Sie auf "freigegebenen geheimen Schlüssel generieren". Ihnen wird ein geheimer Schlüssel angezeigt, der automatisch generiert wird. Kopieren Sie den geheimen Schlüssel an einem Speicherort, da dies erforderlich ist, während wir den "dedolistservice" in Visual Studio konfigurieren.


![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO17.PNG)

Klicken Sie auf Weiter, und schließen Sie den Assistenten ab.

### <a name="modifying-the-todolistclient-code"></a>Ändern des "dedolistclient"-Codes

#### <a name="modify-the-application-config"></a>Ändern der Anwendungskonfiguration

Wechseln Sie zu Ihrem todolistclient-Projekt in der Projekt Mappe WebAPI-onbehalfof-dotnet. Öffnen Sie die Datei app. config, und nehmen Sie die folgenden Änderungen vor:

* Kommentieren Sie den Eintrag "Ida: Tenant Key".
* Für "Ida: redirecturi" geben Sie den beliebigen URI ein, den Sie beim Konfigurieren des MySampleGroup_ClientApplication in AD FS angegeben haben.
* Geben Sie für den Schlüssel "Ida: ClientID" den Client-ID-Bezeichner an, den AD FS beim Konfigurieren des MySampleGroup_ClientApplication gegeben hat.
* Geben Sie für die Datei "Ida: todolistresourceid" die Ressourcen-ID an, die Sie beim Konfigurieren von "todolistservicewebapi" in AD FS
* Kommentieren Sie den Schlüssel "Ida: aadinstance".
* Geben Sie für "Ida: todolistbaseaddress" die Ressourcen-ID von todolistservicewebapi ein. Diese wird verwendet, wenn die ToDoList-WebAPI aufgerufen wird.
* Fügen Sie einen Schlüssel "Ida: Authority" hinzu, und geben Sie den Wert als URI für AD FS an.

Ihre **appSettings** in app. config sollten in etwa wie folgt aussehen:

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

Kommentieren Sie die Zeile aus, die die Mandanten Informationen aus der Anwendungskonfiguration liest.

    //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
    //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];

Ändern Sie den Wert der Zeichen folgen Autorität in.

    private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

Ändern Sie den Code, um die korrekten Werte von "dedolistresourceid" und "dedolistbaseaddress" zu lesen

    private static string todoListResourceId = ConfigurationManager.AppSettings["ida:TodoListResourceId"];
    private static string todoListBaseAddress = ConfigurationManager.AppSettings["ida:TodoListBaseAddress"];

Ändern Sie in der Funktion MainWindow () die authcontext-Initialisierung wie folgt:

    authContext = new AuthenticationContext(authority, false);

### <a name="adding-the-backend-resource"></a>Hinzufügen der Backend-Ressource

Um den "im Auftrag von"-Ablauf abzuschließen, müssen Sie eine Back-End-Ressource erstellen, auf die der TodoListService im Auftrag des authentifizierten Benutzers zugreift. Die Auswahl der Back-End-Ressource kann je nach Anforderung variieren. für dieses Beispiel können Sie jedoch eine einfache WebAPI erstellen.

* Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Projekt Mappe "WebAPI-onbehalfof-dotnet", und wählen Sie Add-> Neues Projekt
* ASP.NET-Webanwendungs Vorlage auswählen

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO4.PNG)

* Klicken Sie bei der nächsten Eingabeaufforderung auf "Authentifizierung ändern".
* Wählen Sie "Geschäfts-, Schul-und unikonten" aus, und wählen Sie in der rechten Dropdown Liste "lokal" aus.
* Geben Sie den Pfad "FederationMetadata. xml" für Ihre AD FS-Bereitstellung ein, und geben Sie einen app-URI an (geben Sie einen beliebigen URI für den Moment an, und ändern Sie ihn später), und klicken Sie auf OK, um das Projekt

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO9.PNG)

* Klicken Sie im Projektmappen-Explorer unter dem neu erstellten Projekt mit der rechten Maustaste auf Controller. Wählen Sie Add-> Controller aus.
* Wählen Sie in der Vorlagen Auswahl "Web-API 2 Controller-Empty" aus, und klicken Sie auf OK.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO3.PNG)

* Entsprechenden Controller Namen vergeben

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO13.PNG)

* Fügen Sie den folgenden Code im Controller hinzu.


~~~
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
~~~

Mit diesem Code wird einfach die Zeichenfolge zurückgegeben, wenn jemand eine GET-Anforderung für die WebAPI webapiobo einfügt.

### <a name="adding-the-new-backend-webapi-to-ad-fs"></a>Hinzufügen der neuen Back-End-WebAPI zu AD FS

Öffnen Sie die Anwendungs Gruppe mysamplegroup. Klicken Sie auf Anwendung hinzufügen, und wählen Sie Web-API-Vorlage und dann weiter aus.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO6.PNG)

Geben Sie auf der Seite Web-API konfigurieren einen passenden Namen für den WebAPI-Eintrag und den Bezeichner an. Der Bezeichner sollte der Wert SSL-URL aus dem webapiobo-Projekt in Visual Studio sein (ähnlich wie bei backendwebapiadfsadd).

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO8.PNG)

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO7.PNG)

Fahren Sie mit dem Assistenten fort, wie bei der Konfiguration der WebAPI "dedolistservice". Am Ende sollte die Anwendungs Gruppe wie folgt aussehen:

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO5.PNG)


### <a name="modifying-the-todolistservice-code"></a>Ändern des "dedolistservice"-Codes

#### <a name="modifying-the-application-config"></a>Ändern der Anwendungskonfiguration

* Öffnen Sie die Datei "Web. config".
* Ändern Sie die folgenden Schlüssel.

| Key                      | Wert                                                                                                                                                                                                                   |
|:-------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ida: Audience             | ID des TodoListService, wie AD FS beim Konfigurieren der WebAPI TodoListService angegeben wird, z. b. https://localhost:44321/                                                                                         |
| Ida: ClientID             | ID des TodoListService, wie AD FS beim Konfigurieren der WebAPI TodoListService angegeben wird, z. b. <https://localhost:44321/> </br>**Es ist sehr wichtig, dass die "Ida: Audience" und "Ida: ClientID" einander entsprechen.** |
| Ida: clientsecret         | Dies ist der geheime Schlüssel, der beim Konfigurieren des Clients "dedolistservice" in generiert AD FS AD FS                                                                                                                   |
| Ida: AdfsMetadataEndpoint | Dies ist die URL zu ihren AD FS Metadaten, z. b. https://fs.anandmsft.com/federationmetadata/2007-06/federationmetadata.xml                                                                                             |
| Ida: obowebapibase        | Dies ist die Basisadresse, die wir verwenden, um die Back-End-API aufzurufen, z. b. https://localhost:44300                                                                                                                     |
| Ida: Authority            | Dies ist die URL für den AD FS Dienst, z. b. https://fs.anandmsft.com/adfs/                                                                                                                                          |

Alle anderen Ida: XXXXXXX-Schlüssel im Knoten " **appSettings** " können auskommentiert oder gelöscht werden.

#### <a name="change-authentication-from-azure-ad-to-ad-fs"></a>Ändern Sie die Authentifizierung von Azure AD in AD FS

* Öffnen Sie die Datei Startup.auth.cs.
* Entfernen Sie den folgenden Code:

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

#### <a name="modifying-the-todolistcontroller"></a>Ändern von "" "-listcontroller"

Fügen Sie einen Verweis auf System. Web. Extensions hinzu. Ändern Sie die Klassenmember, indem Sie den folgenden Code ersetzen.

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

**Ändern des für den Namen verwendeten Anspruchs**

Von AD FS wir den nmae-Anspruch ausgeben, aber wir geben keinen NameIdentifier-Anspruch aus. Im Beispiel wird NameIdentifier zum eindeutigen Schlüssel in den TODO-Elementen verwendet. Der Einfachheit halber können Sie den NameIdentifier mit dem namens Anspruch im Code sicher entfernen. Suchen und ersetzen Sie alle Vorkommen von NameIdentifier durch den Namen.

**Beitrags Routine ändern und callgraphapionbehalfofuser ()**

Kopieren Sie den unten stehenden Code, und fügen Sie ihn in ToDoListController.cs ein, und ersetzen Sie den Code für Post und callgraphapionbehalfofuser.

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


Visual Studio ist standardmäßig so konfiguriert, dass ein Projekt ausgeführt wird, wenn Sie das Debuggen zum Ausführen erreichen.

* Klicken Sie mit der rechten Maustaste auf die Lösung, und wählen Sie Eigenschaften
* Wählen Sie auf der Seite Eigenschaften mehrere Start Projekte aus, und ändern Sie die Aktion für alle drei Einträge in Start.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO14.PNG)

Drücken Sie F5, und führen Sie die Lösung aus

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO24.PNG)

Klicken Sie auf die Schaltfläche anmelden. Sie werden aufgefordert, sich mit AD FS anzumelden.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO25.PNG)

Fügen Sie nach der Anmeldung ein TODO-Element in die Liste ein. Im Hintergrund führen wir einen Post-Vorgang an den "" "" "" "" "" "" "" "" "" "" ".

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO26.PNG)

Bei einem erfolgreichen Vorgang sehen Sie, dass das Element der Liste mit der zusätzlichen Meldung von der Back-End-Web-API hinzugefügt wurde, auf die mithilfe von OBO auth-Flow zugegriffen wurde.

![AD FS OBO](media/AD-FS-On-behalf-of-Authentication-in-Windows-Server-2016/ADFS_OBO27.PNG)

Sie können auch die detaillierten Ablauf Verfolgungen für "fddler" sehen. Starten Sie "fddler" und aktivieren Sie die HTTPS-Entschlüsselung. Sie können sehen, dass wir zwei Anforderungen an den/ADFS/oautincludes-Endpunkt senden.
In der ersten Interaktion präsentieren wir den Zugriffs Code für den tokenendpunkt und erhalten ein Zugriffs Token für https://localhost:44321/ ![ AD FS OBO @ no__t-2

In der zweiten Interaktion mit dem tokenendpunkt sehen Sie, dass **requested_token_use** als **on_behalf_of** festgelegt ist und wir das Zugriffs Token verwenden, das für den Webdienst der mittleren Ebene abgerufen wurde, d. h. https://localhost:44321/ als die-Assertion zum Abrufen der "im Auftrag von"-Token.
![AD FS OBO @ NO__T-1

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
