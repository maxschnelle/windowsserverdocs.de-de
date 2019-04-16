---
title: Erstellen Sie eine einzelne Seite Web-Anwendung, die mithilfe von OAuth und ADAL.JS mit AD FS 2016
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: 7b3d48e1e38baffeb84b1f236efb43cfda5048c0
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-single-page-web-application-using-oauth-and-adaljs-with-ad-fs-2016"></a>Erstellen Sie eine einzelne Seite Web-Anwendung, die mithilfe von OAuth und ADAL.JS mit AD FS 2016

>Gilt für: Windows Server 2016

In dieser exemplarischen Vorgehensweise enthält Anweisungen für die Authentifizierung mit AD FS mit ADAL für JavaScript Sichern einer AngularJS einzelseitenanwendung mit einer ASP.NET Web-API-Back-End-implementiert.

>Warnung: Das Beispiel, das Sie hier erstellen können nur zu Lernzwecken ist. Diese Anweisungen gelten für die einfachste und die minimale Implementierung möglich, die erforderlichen Elemente des Modells verfügbar zu machen. Das Beispiel umfasst möglicherweise nicht alle Aspekte der Fehlerbehandlung und andere Funktionen beziehen.

>[!NOTE]
>In dieser exemplarischen Vorgehensweise gilt **nur** zu AD FS-Server2016 und höher 

## <a name="overview"></a>(Übersicht)
In diesem Beispiel werden wir eine Authentifizierungsablauf erstellen, in denen ein einzelne Seite Anwendungsclient bei AD FS zum Sichern des Zugriffs auf die WebAPI Ressourcen auf dem Back-End-authentifiziert werden wird. Im folgenden ist der allgemeine Authentifizierungsablauf


![AD FS-Autorisierung](media/Single-Page-Application-with-AD-FS/authenticationflow.PNG)

Wenn Sie eine einzelne Seite Anwendung verwenden, der Benutzer navigiert zu einer Ausgangsposition von wo Seite und eine Auflistung von JavaScript-Dateien ab, und HTML-Ansichten werden geladen. Sie müssen die Active Directory Authentifizierung Library (ADAL) um zu wissen, die wichtige Informationen zu Ihrer Anwendung, d.h. die AD FS-Instanz, Client-ID, so konfigurieren, dass sie die AD FS-Authentifizierung verweisen kann.

Wenn einen Trigger für die Authentifizierung von ADAL angezeigt wird, verwendet die Informationen, die von der Anwendung bereitgestellte und leitet die Authentifizierung Ihrer AD FS-STS.  Die Anwendung einzelne Seite, der als öffentliche in AD FS-Client registriert ist, wird für die implizite Zugriffserteilung automatisch konfiguriert. Die autorisierungsanforderung führt ein ID-Token, das über eine #fragment an die Anwendung zurückgegeben wird. Weitere Aufrufe an den Back-End-WebAPI wird dieses Token-ID als Bearer Token in der Kopfzeile für den Zugriff auf die WebAPI ausführen.

## <a name="setting-up-the-development-box"></a>Das Feld für die Entwicklung einrichten
Diese exemplarische Vorgehensweise verwendet Visual Studio2015. Das Projekt verwendet ADAL JS-Bibliothek. Bitte lesen Sie ADAL Informationen [Active Directory-Authentifizierung Bibliothek .NET.](https://msdn.microsoft.com/library/azure/mt417579.aspx)

## <a name="setting-up-the-environment"></a>Einrichten der Umgebung
In dieser exemplarischen Vorgehensweise verwenden wir ein grundlegendes Setup von:

1.  DC: Domänencontroller für die Domäne, in der AD FS gehostet wird
2.  AD FS-Server: Der AD FS-Server für die Domäne
3.  : Entwicklung Computer, in denen wir Visual Studio installiert haben und wird unser Beispiel entwickeln

Sie können, wenn Sie möchten, nur zwei Computer verwenden. Eine für DC/AD FS und die andere für die Entwicklung des Beispiels.

Zum Einrichten der Domänencontroller und die AD FS ist nicht Gegenstand dieses Artikels. Weitere Informationen finden Sie unter:

- [AD DS-Bereitstellung](../../ad-ds/deploy/AD-DS-Deployment.md) 
- [AD FS-Bereitstellung](../AD-FS-Deployment.md)



## <a name="clone-or-download-this-repository"></a>Klonen oder dieses Repository herunterladen
Wir werden die Beispiel-App erstellt, für die Integration von Azure AD in einer einzelnen Seite-App AngularJS und ändern sie verwenden stattdessen die Back-End-Ressource mit AD FS sichern.

Über die Shell oder die Befehlszeile:

    git clone https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp.git

## <a name="about-the-code"></a>Über den Code
Die wichtigsten Dateien, die mit Authentifizierungslogik sind die folgenden:

**App.js** – fügt die Abhängigkeit ADAL Modul, stellt die App-Konfigurationswerte von ADAL für die Fahrt Protokoll Interaktionen mit AAD verwendet und gibt an, welche Routen nicht ohne vorherige Authentifizierung zugegriffen werden soll.

**"Index.HTML"** -enthält einen Verweis auf adal.js

**HomeController.js**-zeigt, wie Sie die Methoden login() und logOut() ADAL nutzen.

**UserDataController.js** -zeigt, wie Sie Benutzerinformationen aus dem zwischengespeicherten ID_Token zu extrahieren.

**Startup.Auth.cs** -Konfiguration für die WebAPI Bearer Authentifizierung mit Active Directory-Verbunddienste enthält.

## <a name="registering-the-public-client-in-ad-fs"></a>Registrieren den öffentlichen Client in AD FS
In diesem Beispiel ist die WebAPI am https://localhost:44326/ hören konfiguriert. Die Anwendungsgruppe **Webbrowser, die Zugriff auf eine Anwendung** implicit Grant Flow Anwendung konfigurieren, verwendet werden können.

1. Öffnen Sie die AD FS-Verwaltungskonsole, und klicken Sie auf **Anwendungsgruppe hinzufügen**. In der **Assistenten zum Hinzufügen einer Anwendung** Geben Sie den Namen der Anwendung, Beschreibung und wählen Sie die **Webbrowser, die Zugriff auf eine Anwendung** Vorlage aus der **Client / Server-Anwendungen** Abschnittwie folgt
    <br>![Erstellen einer neuen Anwendungsgruppe](media/Single-Page-Application-with-AD-FS/appgroup_step1.png)

2. Auf der nächsten Seite **systemeigene Anwendung**, Client-ID der Anwendung bereitzustellen und zu URI umleiten, wie unten dargestellt
    <br>![Erstellen einer neuen Anwendungsgruppe](media/Single-Page-Application-with-AD-FS/appgroup_step2.png)

3. Auf der nächsten Seite **Zugriffssteuerungsrichtlinie gelten** behalten Sie die Berechtigungen als *alle Benutzer zulassen*

4. Die Seite "Zusammenfassung" sollte wie im folgenden aussehen.
    <br>![Erstellen einer neuen Anwendungsgruppe](media/Single-Page-Application-with-AD-FS/appgroup_step3.png)

5. Klicken Sie auf **Weiter** vervollständigen Sie die der Anwendungsgruppe und den Assistenten zu schließen.

## <a name="modifying-the-sample"></a>Ändern das Beispiel
Konfigurieren von ADAL JS

Öffnen der **App.js** Datei, und ändern Sie die **adalProvider.init** Definition:

    adalProvider.init(
        {
            instance: 'https://fs.contoso.com/', // your STS URL
            tenant: 'adfs',                      // this should be adfs
            clientId: 'https://localhost:44326/', // your client ID of the
            //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
        },
        $httpProvider
        );

|Konfiguration|Beschreibung
|--------|--------
|Instanz|Der STS-URL, z.B. https://fs.contoso.com/
|Mandanten|Halten Sie es als "AD FS"
|clientID|Dies ist die Client-ID, die Sie beim Konfigurieren des öffentlichen Clients für eine einzelne Seite Anwendung angegeben haben

## <a name="configure-webapi-to-use-ad-fs"></a>Konfigurieren von WebAPI Verwendung von AD FS
Öffnen der **Startup.Auth.cs** Datei im Beispiel, und fügen Sie die folgenden am Anfang: 

    using System.IdentityModel.Tokens;

Entfernen:

                app.UseWindowsAzureActiveDirectoryBearerAuthentication(
    new WindowsAzureActiveDirectoryBearerAuthenticationOptions
    {
    Audience = ConfigurationManager.AppSettings["ida:Audience"],
    Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
    });

Und hinzufügen:

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

|Parameter|Beschreibung
|--------|--------
|ValidAudience|Dadurch wird den Wert der "Audience" konfiguriert werden, die im Token verglichen werden
|ValidIssuer|Wird konfiguriert, um den Wert der ' Aussteller, mit der das Token verglichen werden,
|Kann der MetadataEndpoint|Dies verweist auf die Metadaten-Informationen von Ihrem STS

## <a name="add-application-configuration-for-ad-fs"></a>Fügen Sie die Konfiguration für AD FS
Ändern Sie die Appsettings wie folgt:

    <appSettings>
    <add key="ida:Audience" value="https://localhost:44326/" />
    <add key="ida:AdfsMetadataEndpoint" value="https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml" />
    <add key="ida:Issuer" value="https://fs.contoso.com/adfs" />
      </appSettings>

## <a name="running-the-solution"></a>Ausführen der Projektmappe
Reinigen Sie die Lösung, erstellen Sie die Projektmappe neu und ausführen. Wenn Sie detaillierte Spuren anzeigen möchten, starten Sie Fiddler, und aktivieren Sie HTTPS-Entschlüsselung.

Der Browser lädt die SPA und wird mit dem folgenden Bildschirm angezeigt werden:

![Registrieren des Clients](media/Single-Page-Application-with-AD-FS/singleapp3.PNG)

Klicken Sie bei der Anmeldung.  Die Aufgabenliste löst der Authentifizierungsablauf und ADAL JS gelangt der AD FS-Authentifizierung

![Melden Sie sich](media/Single-Page-Application-with-AD-FS/singleapp4a.PNG)

In Fiddler sehen Sie das Token, die als Teil der URL im Fragment # zurückgegeben wird.

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp5a.PNG)

Sie werden jetzt rufen Sie die Back-End-API, um Elemente der Aufgabenliste für den angemeldeten Benutzer hinzufügen können:

![Fiddler](media/Single-Page-Application-with-AD-FS/singleapp6.PNG)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
