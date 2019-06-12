---
title: Erstellen einer einseitigen Web-App mithilfe von OAuth und ADAL. Node.js mit AD FS 2016 oder höher
description: Eine exemplarische Vorgehensweise bietet Anleitungen für die Authentifizierung bei AD FS mit ADAL für JavaScript Sichern einer AngularJS-basierten einseitigen Anwendung
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/13/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: f8a8d6b81f63a691954eecf02dba4e33215a462a
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811750"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016-or-later"></a>Erstellen einer einseitigen Web-App mithilfe von OAuth und ADAL. Node.js mit AD FS 2016 oder höher

Diese exemplarische Vorgehensweise enthält Anweisungen für die Authentifizierung bei AD FS mithilfe von ADAL für JavaScript Sichern einer AngularJS-basierten einseitige Anwendung, die mit einer ASP.NET Web-API-Back-End implementiert.

In diesem Szenario beim Anmelden des Benutzers, der JavaScript-Front-End verwendet [Active Directory-Authentifizierungsbibliothek für JavaScript (ADAL. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js) und impliziten Gewährung der Autorisierung ein ID-Token (Id_token) von Azure AD abgerufen. Das Token wird zwischengespeichert, und der Client fügt es der Anforderung als trägertoken Wenn Aufrufe an die Web-API-back-End, das durch die OWIN-Middleware abgesichert.

>[!IMPORTANT]
>Das Beispiel, das Sie erstellen können, ist nur zu Lernzwecken. Diese Anweisungen gelten für die einfachste und minimale Implementierung, die Möglichkeit, um die erforderlichen Elemente des Modells verfügbar zu machen. Im Beispiel umfassen möglicherweise nicht alle Aspekte der Fehlerbehandlung und andere Funktionen beziehen.

>[!NOTE]
>In dieser exemplarischen Vorgehensweise gilt **nur** mit AD FS-Server 2016 und höher 

## <a name="overview"></a>Übersicht
In diesem Beispiel werden wir einen authentifizierungsdatenfluss erstellen, in denen eine einseitige Anwendung für AD FS zum Schützen des Zugriffs auf die Web-API-Ressourcen im Back-End Clientauthentifizierung werden wird. Im folgenden finden Sie der allgemeinen Authentifizierungsablauf


![AD FS-Autorisierung](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

Wenn Sie eine einseitige Anwendung verwenden zu können, der Benutzer navigiert, einen Startort anzugeben, wo Seite und eine Sammlung von JavaScript-Dateien ab, und HTML-Ansichten werden geladen. Sie müssen die Active Directory Authentication Library (ADAL) um zu erfahren, die wichtige Informationen zu Ihrer Anwendung, d. h. den AD FS-Instanz, Client-ID und so konfigurieren, dass sie die Authentifizierung bei AD FS weiterleiten kann.

Wenn ADAL über einen Trigger für die Authentifizierung wird, verwendet die Informationen, die von der Anwendung bereitgestellt und die Authentifizierung Ihrer AD FS-STS leitet.  Die einseitige Anwendung, die als öffentlicher Client bei AD FS registriert ist, wird automatisch für die implizite Gewährung konfiguriert. Die autorisierungsanforderung führt zu einem ID-Token, die an die Anwendung über eine #fragment zurückgegeben wird. Weitere Aufrufe an die Back-End-Web-API wird dieses ID-Token als bearertoken im Header für den Zugriff auf die Web-API ausführen.

## <a name="setting-up-the-development-box"></a>Das Feld für die Entwicklung einrichten
In dieser exemplarischen Vorgehensweise wird Visual Studio 2015 verwendet. Das Projekt verwendet die ADAL-JS-Bibliothek. Informationen finden Sie ADAL [Active Directory Authentication Library .NET.](https://msdn.microsoft.com/library/azure/mt417579.aspx)

## <a name="setting-up-the-environment"></a>Einrichten der Umgebung
In dieser exemplarischen Vorgehensweise wird eine grundlegende Einteilung des verwenden:

1.  DC: Domänencontroller für die Domäne, die in der AD FS gehostet wird
2.  AD FS-Server: Die AD FS-Server für die Domäne
3.  Entwicklungscomputer: Computer, auf der Visual Studio installiert haben und wird in diesem Beispiel entwickeln

Sie können, wenn Sie möchten, nur zwei Computer verwenden. Eine für DC/AD FS und der andere für die Entwicklung des Beispiels.

Einrichten der Domänencontroller und AD FS sprengen den Rahmen dieses Artikels aus. Zusätzliche bereitstellungs-Informationen finden Sie unter:

- [AD DS-Bereitstellung](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS-Bereitstellung](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>Klonen oder Herunterladen von diesem repository
Wir werden die beispielanwendung erstellt für das Integrieren von Azure AD in einer einseitigen AngularJS-app, und ändern ihn verwenden, um die Back-End-Ressource stattdessen zu sichern, indem Sie mithilfe von AD FS.

Der Shell oder über die Befehlszeile:

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>Zum Code
Wichtigsten Dateien, die Authentifizierungslogik lauten wie folgt:

**"App.js"** : Fügt die ADAL-Modul-Abhängigkeit, bietet die app-Konfigurationswerte, die von ADAL zum Steuern von protokollinteraktionen mit AAD verwendet und gibt an, welche Routen ohne vorherige Authentifizierung nicht zugegriffen werden soll.

**"Index.HTML"** -enthält einen Verweis auf "adal.js"

**HomeController.js**-zeigt, wie die Methoden bei login() und logOut() ADAL nutzen.

**UserDataController.js** -zeigt, wie Benutzerinformationen aus der zwischengespeicherten "id_token" extrahieren.

**Startup.Auth.cs** -enthält die Konfiguration für die Web-API zur Active Directory Federation Service bearerauthentifizierung verwenden.

## <a name="registering-the-public-client-in-ad-fs"></a>Registrieren den öffentlichen Client in AD FS
Im Beispiel wird die Web-API ist so konfiguriert, dass Lauschen am https://localhost:44326/. Die Anwendungsgruppe **Webbrowser den Zugriff auf eine Webanwendung** implizite Gewährung Flow Anwendung konfigurieren, verwendet werden können.

1. Öffnen Sie die AD FS-Verwaltungskonsole, und klicken Sie auf **Anwendungsgruppe hinzufügen**. In der **Assistenten zum Hinzufügen einer Anwendung** Geben Sie den Namen der Anwendung, Beschreibung und wählen Sie die **Webbrowser den Zugriff auf eine Webanwendung** Vorlage aus der **Client / Server Anwendungen** Abschnitt wie folgt

    ![Neue Anwendungsgruppe erstellen](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. Auf der nächsten Seite **systemeigene Anwendung**, geben Sie die Anwendungs-Client-ID und umleitungs-URI wie unten dargestellt.

    ![Neue Anwendungsgruppe erstellen](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. Auf der nächsten Seite **Access-Control-Richtlinie anwenden** lassen Sie die Berechtigungen wie *alle zulassen*

4. Die Seite "Zusammenfassung" sollte sieht etwa folgendermaßen aussehen.

    ![Neue Anwendungsgruppe erstellen](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. Klicken Sie auf **Weiter** , schließen Sie das Hinzufügen der Anwendungsgruppe und den Assistenten zu schließen.

## <a name="modifying-the-sample"></a>Ändern das Beispiel
Konfigurieren der ADAL-JS

Öffnen der **"App.js"** und Ändern der **adalProvider.init** Definition auf:

    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
        );

|Konfiguration|Beschreibung|
|--------|--------|
|Instanz|Die STS-URL, z. B. https://fs.contoso.com/|
|Mandanten|Behalten Sie ihn als "Adfs"|
|"ClientID"|Dies ist die Client-ID, die Sie beim Konfigurieren des öffentlichen Clients für die einzelseitenanwendung angegeben|

## <a name="configure-webapi-to-use-ad-fs"></a>Konfigurieren von Web-API zur Verwendung von AD FS
Öffnen der **Startup.Auth.cs** Datei, in dem Beispiel, und fügen Sie Folgendes am Anfang:

    using System.IdentityModel.Tokens;

Entfernen:

                app.UseWindowsAzureActiveDirectoryBearerAuthentication(
    new WindowsAzureActiveDirectoryBearerAuthenticationOptions
    {
    Audience = ConfigurationManager.AppSettings["ida:Audience"],
    Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
    });

ein, und fügen Sie hinzu:

    app.UseActiveDirectoryFederationServicesBearerAuthentication(
    new ActiveDirectoryFederationServicesBearerAuthenticationOptions
    {
    MetadataEndpoint = ConfigurationManager.AppSettings["ida:AdfsMetadataEndpoint"],
    TokenValidationParameters = new TokenValidationParameters()
    {
    ValidAudience = ConfigurationManager.AppSettings["ida:Audience"],
    ValidIssuer = ConfigurationManager.AppSettings["ida:Issuer"]
    }
    }
    );

|Parameter|Beschreibung|
|--------|--------|
|ValidAudience|Dadurch wird den Wert des "Audience" konfiguriert werden, die im Token verglichen werden|
|ValidIssuer|Dadurch wird den Wert des konfiguriert "Aussteller, der im Token überprüft wird|
|MetadataEndpoint|Dies verweist auf die Metadateninformationen der Ihr STS|

## <a name="add-application-configuration-for-ad-fs"></a>Fügen Sie die Konfiguration von Anwendungen für AD FS
Ändern Sie die App-Einstellungen wie folgt:

    <appSettings>
    <add key="ida:Audience" value="https://localhost:44326/" />
    <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
    <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
      </appSettings>

## <a name="running-the-solution"></a>Ausführen der Lösung
Löschen Sie die Lösung, erstellen Sie die Projektmappe neu, und führen Sie ihn aus. Wenn ausführliche ablaufverfolgungen angezeigt werden sollen, starten Sie Fiddler, und aktivieren Sie der Entschlüsselung von HTTPS.

Browser (verwenden Sie Chrome-Browser) wird die SPA geladen, und es wird der folgende Bildschirm angezeigt werden:

![Registrieren des client](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

Klicken Sie auf diese Option, bei der Anmeldung.  Der ToDo-Liste wird der Ablauf der Authentifizierung ausgelöst, und ADAL-JS leitet die Authentifizierung bei AD FS

![Login](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

Fiddler sehen Sie das Token, die als Teil der URL in das #-Fragment zurückgegeben wird.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

Sie werden können nun das Back-End-API zum Hinzufügen von Elementen der ToDo-Liste für den angemeldeten Benutzer aufgerufen:

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
