---
title: AD FS msal-Web-App (Server-APP) Aufrufen von Web-APIs
description: Erfahren Sie, wie Sie eine Web-App-Anmelde Benutzer erstellen, die durch AD FS 2019 authentifiziert werden.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d2ac36180992d44f837ce74ace40cf95533309c9
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69983428"
---
# <a name="scenario-web-app-server-app-calling-web-api"></a>Szenario: Web-App (Server-APP) Aufrufen der Web-API 
>Gilt für: AD FS 2019 und höher 
 
Erfahren Sie, wie Sie eine Web-App-Anmelde Benutzer, die durch AD FS 2019 authentifiziert werden, erstellen und Token mithilfe der [msal-Bibliothek](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki) zum Abrufen von Web-APIs abrufen.  
 
Bevor Sie diesen Artikel lesen, sollten Sie sich mit den [AD FS Konzepten](../ad-fs-openid-connect-oauth-concepts.md) und dem [Flow zum Erteilen von Autorisierungscodes](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#authorization-code-grant-flow) vertraut machen.
 
## <a name="overview"></a>Übersicht 
 
![Übersicht über Web-Apps, die Web-API aufrufen](media/adfs-msal-web-app-web-api/webapp1.png)

In diesem Flow fügen Sie der Web-App (Server-APP) eine Authentifizierung hinzu, die daher Benutzer anmelden und eine Web-API aufrufen kann. Verwenden Sie in der Web-App zum Aufrufen der Web-API die [acquiretokenbyauthorizationcode](https://docs.microsoft.com/en-us/dotnet/api/microsoft.identity.client.acquiretokenbyauthorizationcodeparameterbuilder?view=azure-dotnet) -tokenerwerbs-Methode von msal. Sie verwenden den Autorisierungs Code Fluss, der das erworbene Token im Tokencache speichert. Der Controller erhält bei Bedarf automatisch Token aus dem Cache. Msal aktualisiert das Token bei Bedarf. 

Web-Apps, die Web-APIs aufrufen: 


- handelt es sich um vertrauliche Client Anwendungen. 
- Daher haben Sie ein Geheimnis (gemeinsames Anwendungs Geheimnis, Zertifikat oder AD-Konto) mit AD FS registriert. Dieser geheime Schlüssel wird während des Aufrufes AD FS zum Abrufen eines Tokens übergebenen.  

Um besser zu verstehen, wie Sie eine Web-App in AD FS registrieren und zum Abrufen von Token zum Abrufen einer Web-API konfigurieren, verwenden wir ein Beispiel, das [hier](https://github.com/microsoft/adfs-sample-msal-dotnet-webapp-to-webapi) verfügbar ist, und Exemplarische Vorgehensweise die Schritte für die APP-Registrierung und die Code Konfiguration.  

 
## <a name="pre-requisites"></a>Voraussetzungen 

- GitHub-Client Tools 
- AD FS 2019 oder höher konfiguriert und wird ausgeführt 
- Visual Studio 2013 oder höher 
 
## <a name="app-registration-in-ad-fs"></a>App-Registrierung in AD FS 
In diesem Abschnitt wird gezeigt, wie Sie die Web-App als vertrauende Seite und Web-API als vertrauende Seite (RP) in AD FS registrieren. 

  1. Klicken Sie in AD FS Verwaltung mit der rechten Maustaste auf **Anwendungs Gruppen** , und wählen Sie **Anwendungs Gruppe hinzufügen**aus.  
  2. Wählen Sie im Anwendungs Gruppen-Assistenten für den Namen **webappto WebAPI** aus, und wählen Sie unter **Client-Server Anwendungen** die Server Anwendung aus, die auf **eine Web-API** -Vorlage zugreift. Klicken Sie auf **Weiter**.  
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp2.png)
  
  3. Kopieren Sie den Wert für den **Client Bezeichner** . Sie wird später als Wert für " **Ida: ClientID** " in der Datei " **Web. config** " der Anwendung verwendet. Geben Sie für **Umleitungs-URI** - Folgendes ein: https://localhost:44326. Klicken Sie auf „Hinzufügen“. Klicken Sie auf **Weiter**. 
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp3.png)
  
  4. Aktivieren Sie auf dem Bildschirm Anwendungs Anmelde Informationen konfigurieren die Option **einen gemeinsamen geheimen Schlüssel generieren** , und kopieren Sie den geheimen Schlüssel. Diese wird später als Wert für " **Ida: clientsecret** " in der Datei " **Web. config** " der Anwendung verwendet. Klicken Sie auf **Weiter**.  
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp4.png)
  
  5. Geben Sie auf dem Bildschirm Web-API konfigurieren den Bezeichner ein **:** https://webapi. Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**. Dieser Wert wird später für " **Ida: graphresourceid** " in der Datei " **Web. config** " der Anwendung verwendet. 
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp5.png)
  
  6. Wählen Sie auf der Seite Access Control Richtlinie anwenden die Option Alle **zulassen** aus, und klicken Sie auf **weiter**. 
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp6.png)
  
  7. Vergewissern Sie sich, dass auf dem Bildschirm Anwendungs Berechtigungen konfigurieren die Option **OpenID** und **user_impersonation** ausgewählt sind, und klicken Sie auf **weiter**. 
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp7.png)
  
  8. Klicken Sie auf dem Bildschirm Zusammenfassung auf **weiter**. 
  
  9. Klicken Sie im Bildschirm Fertigstellen auf **Schließen**.



## <a name="code-configuration"></a>Code Konfiguration 

In diesem Abschnitt wird gezeigt, wie eine ASP.net-Web-App für den Anmelde Benutzer konfiguriert und das Token zum Aufrufen der Web-API abgerufen wird. 

  1. Das Beispiel [hier](https://github.com/microsoft/adfs-sample-msal-dotnet-webapp-to-webapi) herunterladen   
  
  2. Öffnen Sie das Beispiel mithilfe von Visual Studio. 
  
  3. Öffnen Sie die Datei "Web. config". Ändern Sie Folgendes: 
       - Ida: ClientID: Geben Sie den Wert für den **Client Bezeichner** aus #3 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - Ida: clientsecret: Geben Sie den **geheimen** Wert aus #4 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - Ida: redirecturi: Geben Sie den **Umleitungs-URI** -Wert aus #3 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - Ida: Authority-Enter https://[Your AD FS Hostname]/ADFS. Z. b. https://adfs.contoso.com/adfs 
       - Ida: Resource: Geben Sie den Bezeichnerwert aus #5 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
      
          ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp8.png)
 
 
### <a name="test-the-sample"></a>Testen des Beispiels 
In diesem Abschnitt wird gezeigt, wie das oben konfigurierte Beispiel getestet wird. 

  1. Nachdem die Codeänderungen vorgenommen wurden, erstellen Sie die Projekt Mappe neu. 
  
  2. Stellen Sie oben in Visual Studio sicher, dass Internet Explorer ausgewählt ist, und klicken Sie auf den grünen Pfeil. 
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp9.png)

  3. Klicken Sie auf der Startseite auf anmelden. 
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp10.png)

  4. Sie werden auf die AD FS Anmeldeseite umgeleitet. Fahren Sie fort, und melden Sie sich an. 
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp11.png)

  5. Nachdem Sie sich angemeldet haben, klicken Sie auf Zugriffs Token.  
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp12.png)

  6. Wenn Sie auf das Zugriffs Token klicken, werden die Informationen zum Zugriffs Token durch Aufrufen der Web-API angezeigt. 
  
      ![Anwendungs Gruppe hinzufügen](media/adfs-msal-web-app-web-api/webapp13.png)
 
 ## <a name="next-steps"></a>Nächste Schritte
[AD FS OpenID Connect/OAuth-Flows und Anwendungsszenarien](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 