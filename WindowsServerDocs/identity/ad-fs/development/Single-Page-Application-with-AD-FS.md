---
title: Erstellen Sie eine Webanwendung mit einer einzelnen Seite mithilfe von OAuth und Adal. JS mit AD FS 2016 oder höher
description: Eine exemplarische Vorgehensweise, die Anweisungen zum Authentifizieren für AD FS mithilfe von Adal für JavaScript bietet, das eine angularjs-basierte Single-Page-Anwendung sichert
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/13/2018
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.openlocfilehash: f62b6ad288e2733083d535260f0b3f5ffb5b50bf
ms.sourcegitcommit: f829a48b9b0c7b9ed6e181b37be828230c80fb8a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/27/2020
ms.locfileid: "82173623"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016-or-later"></a>Erstellen Sie eine Webanwendung mit einer einzelnen Seite mithilfe von OAuth und Adal. JS mit AD FS 2016 oder höher

Diese exemplarische Vorgehensweise enthält Anweisungen zum Authentifizieren für AD FS mithilfe von Adal für JavaScript, das eine angularjs-basierte Single-Page-Anwendung sichert, die mit einem ASP.net-Web-API Back-End implementiert wird

In diesem Szenario verwendet das JavaScript-Front-End bei der Benutzeranmeldung die [Active Directory Authentication Library für JavaScript (ADAL.JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js) und die implizite Gewährung der Autorisierung, um ein ID-Token (id_token) von Azure AD zu erhalten. Das Token wird zwischengespeichert und der Anforderung als Bearertoken angefügt, wenn der Client Aufrufe an das durch die OWIN-Middleware gesicherte Web-API-Back-End sendet.

>[!IMPORTANT]
>Das Beispiel, das Sie hier erstellen können, dient nur zu Schulungszwecken. Diese Anweisungen gelten für die einfachste, kleinste Implementierung, die die erforderlichen Elemente des Modells verfügbar machen kann. Das Beispiel enthält möglicherweise nicht alle Aspekte der Fehlerbehandlung und andere Funktionen zum verknüpfen.

>[!NOTE]
>Diese exemplarische Vorgehensweise gilt **nur** für AD FS Server 2016 und höher. 

## <a name="overview"></a>Übersicht
In diesem Beispiel erstellen wir einen Authentifizierungs Fluss, bei dem ein Single-Page-Anwendungs Client für AD FS authentifiziert wird, um den Zugriff auf die WebAPI-Ressourcen auf dem Back-End zu sichern. Unten ist der allgemeine Authentifizierungs Ablauf angegeben.


![AD FS Autorisierung](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

Wenn eine Einzelseiten Anwendung verwendet wird, navigiert der Benutzer zu einem Start Speicherort, von dem aus die Startseite und eine Sammlung von JavaScript-Dateien und HTML-Ansichten geladen werden. Sie müssen die Active Directory-Authentifizierungsbibliothek (Adal) so konfigurieren, dass Sie die wichtigen Informationen zu Ihrer Anwendung, d. h. die AD FS Instanz, Client-ID, kennen, damit Sie die Authentifizierung an Ihren AD FS weiterleiten kann.

Wenn die Adal einen Authentifizierungs-und Authentifizierungs-und Authentifizierungsdienst erhält, verwendet Sie die von der Anwendung bereitgestellten Informationen und leitet die Authentifizierung an Ihren AD FS STS weiter.  Die Single-Page-Anwendung, die in AD FS als öffentlicher Client registriert ist, wird automatisch für den impliziten Zuweisungs Fluss konfiguriert. Die Autorisierungs Anforderung führt zu einem ID-Token, das über einen #Fragment an die Anwendung zurückgegeben wird. Weitere Aufrufe der Back-End-WebAPI tragen dieses ID-Token als bearertoken in der Kopfzeile ein, um Zugriff auf die WebAPI zu erhalten.

## <a name="setting-up-the-development-box"></a>Einrichten der Entwicklungs Box
In dieser exemplarischen Vorgehensweise wird Visual Studio 2015 verwendet. Das Projekt verwendet die Adal-js-Bibliothek. Weitere Informationen zu Adal finden Sie unter [Active Directory-Authentifizierungsbibliothek .net.](https://msdn.microsoft.com/library/azure/mt417579.aspx)

## <a name="setting-up-the-environment"></a>Einrichten der Umgebung
In dieser exemplarischen Vorgehensweise verwenden wir eine grundlegende Einrichtung von:

1.    DC: Domänen Controller für die Domäne, in der AD FS gehostet werden.
2.    AD FS Server: der AD FS Server für die Domäne
3.    Entwicklungs Computer: der Computer, auf dem Visual Studio installiert ist, und wird unser Beispiel entwickeln

Wenn Sie möchten, können Sie nur zwei Computer verwenden. Eine für DC/AD FS und die andere für die Entwicklung des Beispiels.

Das Einrichten des Domänen Controllers und AD FS würde den Rahmen dieses Artikels sprengen. Weitere Informationen zur Bereitstellung finden Sie unter:

- [AD DS-Bereitstellung](../../ad-ds/deploy/AD-DS-Deployment.md)
- [AD FS-Bereitstellung](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>Klonen oder Herunterladen des Repositorys
Wir verwenden die Beispielanwendung, die für die Integration von Azure AD in eine einseitige angularjs-App erstellt wurde, und ändern Sie, um die Back-End-Ressource mithilfe AD FS zu sichern.

Verwenden Sie in Ihrer Shell oder Befehlszeile Folgendes:

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>Informationen über den Code
Die Schlüsseldateien, die die Authentifizierungs Logik enthalten, lauten wie folgt:

**App. js** : fügt die Adal-Modul Abhängigkeit ein, stellt die APP-Konfigurationswerte bereit, die von Adal für die Verwendung von Protokoll Interaktionen mit Aad verwendet werden, und gibt an, auf welche Routen ohne vorherige Authentifizierung nicht zugegriffen werden soll.

" **Index. html** " enthält einen Verweis auf "Adal. js".

**HomeController. js**: zeigt, wie die Login ()-Methode und die Logout ()-Methode in Adal genutzt werden.

**Userdatacontroller. js** : zeigt, wie Benutzerinformationen aus dem zwischengespeicherten id_token extrahiert werden.

**Startup.auth.cs** : enthält die Konfiguration für die WebAPI, um Active Directory Verbunddienst für die Träger Authentifizierung zu verwenden.

## <a name="registering-the-public-client-in-ad-fs"></a>Der öffentliche Client wird in AD FS registriert.
Im Beispiel ist die WebAPI für das Abhören von https://localhost:44326/konfiguriert. Der Anwendungs Gruppen-Webbrowser, der auf **eine Webanwendung zugreift** , kann zum Konfigurieren der impliziten Grant Flow-Anwendung verwendet werden.

1. Öffnen Sie die AD FS-Verwaltungskonsole, und klicken Sie auf **Anwendungs Gruppe hinzufügen**. Geben Sie im **Assistenten zum Hinzufügen von Anwendungs Gruppen** den Namen der Anwendung und die Beschreibung ein, und wählen Sie den Webbrowser, der auf **eine Webanwendungsvorlage zugreift** , im Abschnitt **Client/Server-Anwendungen** aus.

    ![Neue Anwendungs Gruppe erstellen](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. Geben Sie auf der nächsten Seite **native Anwendung**den Anwendungs Client Bezeichner und den Umleitungs-URI wie unten dargestellt an.

    ![Neue Anwendungs Gruppe erstellen](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. Übernehmen Sie auf der nächsten Seite **Access Control Richtlinie anwenden** die Berechtigungen für *Alle zulassen* .

4. Die Zusammenfassungs Seite sollte in etwa wie folgt aussehen.

    ![Neue Anwendungs Gruppe erstellen](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. Klicken Sie **auf Weiter, um** das Hinzufügen der Anwendungs Gruppe abzuschließen und den Assistenten zu schließen.

## <a name="modifying-the-sample"></a>Ändern des Beispiels
Konfigurieren von Adal js

Öffnen Sie die Datei " **app. js** ", und ändern Sie die Definition " **adalprovider. init** " in:

    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
    );

|Konfiguration|BESCHREIBUNG|
|--------|--------|
|instance|Ihre STS-URL, z. b.https://fs.contoso.com/|
|tenant|Als "ADFS" beibehalten|
|clientID|Dies ist die Client-ID, die Sie beim Konfigurieren des öffentlichen Clients für Ihre Single-Page-Anwendung angegeben haben.|

## <a name="configure-webapi-to-use-ad-fs"></a>Konfigurieren von WebAPI für die Verwendung von AD FS
Öffnen Sie die Datei **Startup.auth.cs** im Beispiel, und fügen Sie am Anfang Folgendes hinzu:

    using System.IdentityModel.Tokens;

aufgeh

    app.UseWindowsAzureActiveDirectoryBearerAuthentication(
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions
        {
            Audience = ConfigurationManager.AppSettings["ida:Audience"],
            Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
        }
    );

und hinzufügen:

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
|Validauer|Hiermit wird der Wert von "Audience" konfiguriert, der im Token gegen überprüft wird.|
|Validierer|Hiermit wird der Wert "Aussteller" konfiguriert, der im Token überprüft wird.|
|MetadataEndpoint|Dies verweist auf die Metadateninformationen Ihres STS.|

## <a name="add-application-configuration-for-ad-fs"></a>Anwendungskonfiguration für AD FS hinzufügen
Ändern Sie die AppSettings wie folgt:
```xml
    <appSettings>
        <add key="ida:Audience" value="https://localhost:44326/" />
        <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
        <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
    </appSettings>
    ```

## Running the solution
Clean the solution, rebuild the solution and run it. If you want to see detailed traces, launch Fiddler and enable HTTPS decryption.

The browser (use Chrome browser) will load the SPA and you will be presented with the following screen:

![Register the client](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

Click on Login.  The ToDo List will trigger the authentication flow and ADAL JS will direct the authentication to AD FS

![Login](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

In Fiddler you can see the token being returned as part of the URL in the # fragment.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

You will be able to now call the backend API to add ToDo List items for the logged-in user:

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## Next Steps
[AD FS Development](../../ad-fs/AD-FS-Development.md)  
