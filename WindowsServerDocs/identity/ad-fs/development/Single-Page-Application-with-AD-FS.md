---
title: Erstellen einer Single-Page-Webanwendung mithilfe von OAuth und ADAL.JS mit AD FS 2016 oder höher
description: Eine exemplarische Vorgehensweise, die Anweisungen zum Authentifizieren für AD FS mithilfe von Adal für JavaScript bietet, das eine angularjs-basierte Single-Page-Anwendung sichert
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/13/2018
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.openlocfilehash: 934ef170f6cbd5a2bd4031d336907d6b925cff06
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519899"
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016-or-later"></a>Erstellen einer Single-Page-Webanwendung mithilfe von OAuth und ADAL.JS mit AD FS 2016 oder höher

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
In dieser exemplarischen Vorgehensweise wird Visual Studio 2015 verwendet. Das Projekt verwendet die Adal-js-Bibliothek. Weitere Informationen zu Adal finden Sie unter [Active Directory-Authentifizierungsbibliothek .net.](/dotnet/api/microsoft.identitymodel.clients.activedirectory?view=azure-dotnet)

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

```
git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git
```

## <a name="about-the-code"></a>Informationen über den Code
Die Schlüsseldateien, die die Authentifizierungs Logik enthalten, lauten wie folgt:

**App.js** fügt die Adal-Modul Abhängigkeit ein, stellt die von Adal verwendeten App-Konfigurationswerte für das Verwenden von Protokoll Interaktionen mit Aad bereit und gibt an, auf welche Routen ohne vorherige Authentifizierung nicht zugegriffen werden soll.

**index.html** -enthält einen Verweis auf adal.js

**HomeController.js**: zeigt, wie die Login ()-Methode und die Logout ()-Methode in Adal genutzt werden.

**UserDataController.js** : zeigt, wie Benutzerinformationen aus dem zwischengespeicherten id_token extrahiert werden.

**Startup.auth.cs** : enthält die Konfiguration für die WebAPI, um Active Directory Verbunddienst für die Träger Authentifizierung zu verwenden.

## <a name="registering-the-public-client-in-ad-fs"></a>Der öffentliche Client wird in AD FS registriert.
Im Beispiel ist die WebAPI für das Abhören von konfiguriert https://localhost:44326/ . Der Anwendungs Gruppen-Webbrowser, der auf **eine Webanwendung zugreift** , kann zum Konfigurieren der impliziten Grant Flow-Anwendung verwendet werden.

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

Öffnen Sie die Datei **app.js** , und ändern Sie die Definition des **adalProvider.init** in:

```
    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
    );
```

|Konfiguration|BESCHREIBUNG|
|--------|--------|
|instance|Ihre STS-URL, z. b.https://fs.contoso.com/|
|tenant|Als "ADFS" beibehalten|
|clientID|Dies ist die Client-ID, die Sie beim Konfigurieren des öffentlichen Clients für Ihre Single-Page-Anwendung angegeben haben.|

## <a name="configure-webapi-to-use-ad-fs"></a>Konfigurieren von WebAPI für die Verwendung von AD FS
Öffnen Sie die Datei **Startup.auth.cs** im Beispiel, und fügen Sie am Anfang Folgendes hinzu:

```
    using System.IdentityModel.Tokens;

remove:

    app.UseWindowsAzureActiveDirectoryBearerAuthentication(
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions
        {
            Audience = ConfigurationManager.AppSettings["ida:Audience"],
            Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
        }
    );

and add:

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
```

|Parameter|BESCHREIBUNG|
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

## <a name="running-the-solution"></a>Ausführen der Lösung
Bereinigen Sie die Lösung, erstellen Sie Sie neu, und führen Sie Sie aus Wenn Sie ausführliche Ablauf Verfolgungen anzeigen möchten, starten Sie die Datei "fddler" und aktivieren die HTTPS-Entschlüsselung.

Der Browser (Chrome-Browser verwenden) lädt die Spa, und Ihnen wird der folgende Bildschirm angezeigt:

![Registrieren des Clients](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

Klicken Sie auf anmelden.  Die TODO-Liste löst den Authentifizierungs Fluss aus, und Adal js leitet die Authentifizierung an AD FS

![Anmelden](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

In "fddler" können Sie sehen, dass das Token als Teil der URL im #-Fragment zurückgegeben wird.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

Nun können Sie die Back-End-API zum Hinzufügen von TODO-Listenelementen für den angemeldeten Benutzer abrufen:

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)
