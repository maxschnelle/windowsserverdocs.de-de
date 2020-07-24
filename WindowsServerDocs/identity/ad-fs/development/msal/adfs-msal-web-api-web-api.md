---
title: AD FS msal-Web-API, die Web-API aufrufen (im Auftrag des Szenarios)
description: Erfahren Sie, wie Sie eine Web-API zum Aufrufen einer anderen Web-API erstellen.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a28132d87fe0b10ac5ab2969f94cdf8905d731fe
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966742"
---
# <a name="scenario-web-api-calling-web-api-on-behalf-of-scenario"></a>Szenario: Web-API-Aufruf der Web-API (im Auftrag des Szenarios) 
> Gilt für: AD FS 2019 und höher 
 
Erfahren Sie, wie Sie eine Web-API erstellen, die eine andere Web-API im Auftrag des Benutzers aufruft.  
 
Bevor Sie diesen Artikel lesen, sollten Sie sich mit den [AD FS Konzepten](../ad-fs-openid-connect-oauth-concepts.md) und dem [Behalf_Of Flow](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#on-behalf-of-flow) vertraut machen.

## <a name="overview"></a>Übersicht 


- Ein Client (Web-App), der im folgenden Diagramm nicht dargestellt wird: Ruft eine geschützte Web-API auf und stellt ein JWT-bearertoken im "Authorization"-http-Header bereit. 
- Die geschützte Web-API überprüft das Token und verwendet die msal [acquiretokenonbehalfof](/dotnet/api/microsoft.identitymodel.clients.activedirectory.authenticationcontext.acquiretokenasync?view=azure-dotnet#Microsoft_IdentityModel_Clients_ActiveDirectory_AuthenticationContext_AcquireTokenAsync_System_String_Microsoft_IdentityModel_Clients_ActiveDirectory_ClientCredential_Microsoft_IdentityModel_Clients_ActiveDirectory_UserAssertion_)-   Methode, um (von AD FS) ein anderes Token anzufordern, damit es selbst eine zweite Web-API (mit dem Namen "Downstream Web API") im Namen des Benutzers aufrufen kann. 
- Die geschützte Web-API verwendet dieses Token, um eine Downstream-API aufzurufen. Sie kann auch acquiretokensilentlater aufrufen, um Token für andere downstreamapis anzufordern (aber immer noch im Namen desselben Benutzers).Acquiretokensilent aktualisiert das Token bei Bedarf.  
 
     ![Übersicht](media/adfs-msal-web-api-web-api/webapi1.png)
 
Um besser zu verstehen, wie Sie im Namen des Authentifizierungs Szenarios in ADFS konfigurieren, verwenden wir ein Beispiel, das [hier](https://github.com/microsoft/adfs-sample-msal-dotnet-webapi-to-webapi-onbehalfof) verfügbar ist, und Exemplarische Vorgehensweise die Schritte für die APP-Registrierung und die Code Konfiguration.  
 
## <a name="pre-requisites"></a>Voraussetzungen 

- GitHub-Client Tools 
- AD FS 2019 oder höher konfiguriert und wird ausgeführt 
- Visual Studio 2013 oder höher 
 
## <a name="app-registration-in-ad-fs"></a>App-Registrierung in AD FS 

In diesem Abschnitt wird gezeigt, wie Sie die native App als öffentliche Client und Web-APIs als vertrauende Seiten (RP) in AD FS registrieren. 

  1. Klicken Sie in AD FS Verwaltung mit der rechten Maustaste auf **Anwendungs Gruppen** , und wählen Sie **Anwendungs Gruppe hinzufügen**aus.  
  
  2. Wählen Sie im Anwendungs Gruppen-Assistenten für **Name** den Namen **webapiin WebAPI** aus, und wählen Sie unter **Client-Server Anwendungen** die native Anwendung aus, die auf **eine Web-API-Vorlage zugreift** . Klicken Sie auf **Weiter**.

      ![App-Registrierung](media/adfs-msal-web-api-web-api/webapi2.png)

  3. Kopieren Sie den Wert für den **Client Bezeichner** . Sie wird später als Wert für **ClientID** in der **App.config** Datei der Anwendung verwendet. Geben Sie für **Umleitungs-URI Folgendes ein:**  -  https://ToDoListClient . Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**. 
  
      ![App-Registrierung](media/adfs-msal-web-api-web-api/webapi3.png)
  
  4. Geben Sie auf dem Bildschirm Web-API konfigurieren den **Bezeichner ein:** https://localhost:44321/ . Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**. Dieser Wert wird später in den **App.config** -und **Web.Config** Dateien der Anwendung verwendet.  
 
      ![App-Registrierung](media/adfs-msal-web-api-web-api/webapi4.png)

  5. Wählen Sie auf der Seite Access Control Richtlinie anwenden die Option **Alle zulassen** aus, und klicken Sie auf **weiter**. 
  
      ![App-Registrierung](media/adfs-msal-web-api-web-api/webapi5.png)  

  6. Wählen Sie auf dem Bildschirm Anwendungs Berechtigungen konfigurieren die Option **OpenID** und **user_impersonation**aus. Klicken Sie auf **Weiter**.  
  
      ![App-Registrierung](media/adfs-msal-web-api-web-api/webapi6.png)  

  7. Klicken Sie auf dem Bildschirm Zusammenfassung auf **weiter**. 

  8. Klicken Sie im Bildschirm Fertigstellen auf **Schließen**. 


  9. Klicken Sie in AD FS Verwaltung auf **Anwendungs Gruppen** , und wählen Sie **WebAPI-WebAPI** -Anwendungs Gruppe aus. Klicken Sie mit der rechten Maustaste, und wählen Sie **Eigenschaften** aus. 
  
      ![App-Registrierung](media/adfs-msal-web-api-web-api/webapi7.png)  

  10. Klicken Sie auf dem Bildschirm WebAPI-WebAPI-Eigenschaften auf **Anwendung hinzufügen...**. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi8.png)

  11. Wählen Sie unter eigenständige Anwendungen die Option **Server Anwendung**aus.  
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi9.png)

  12. Fügen Sie auf dem Bildschirm Server Anwendung https://localhost:44321/ als **Client Bezeichner** und **Umleitungs-URI**hinzu. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi10.png)

  13. Wählen Sie auf dem Bildschirm Anwendungs Anmelde Informationen konfigurieren die Option **gemeinsamen geheimen Schlüssel generieren**. Kopieren Sie den geheimen Schlüssel für die spätere Verwendung.
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi11.png)

  14. Klicken Sie auf dem Bildschirm Zusammenfassung auf **weiter**. 

  15. Klicken Sie im Bildschirm Fertigstellen auf **Schließen**. 

  16. Klicken Sie in AD FS Verwaltung auf **Anwendungs Gruppen** , und wählen Sie **WebAPI-WebAPI** -Anwendungs Gruppe aus. Klicken Sie mit der rechten Maustaste, und wählen Sie **Eigenschaften** aus. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi12.png)

  17. Klicken Sie auf dem Bildschirm WebAPI-WebAPI-Eigenschaften auf **Anwendung hinzufügen...**. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi13.png)

  18. Klicken Sie unter eigenständige Anwendungen auf **Web-API**. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi14.png)  

  19. Fügen Sie unter Web-API konfigurieren https://localhost:44300 als **Bezeichner**hinzu.  
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi15.png)

  20. Wählen Sie auf der Seite Access Control Richtlinie anwenden die Option **Alle zulassen** aus, und klicken Sie auf **weiter**. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi16.png)

  21. Klicken Sie auf dem Bildschirm Anwendungs Berechtigungen konfigurieren auf **weiter**. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi17.png)

  22. Klicken Sie auf dem Bildschirm Zusammenfassung auf **weiter**.

  23. Klicken Sie im Bildschirm Fertigstellen auf **Schließen**.  

  24. Klicken Sie auf der Seite webapiin WebAPI – Web-API 2-Eigenschaften auf OK.  

  25. Wählen Sie auf dem Bildschirm WebAPI-WebAPI-Eigenschaften die Option **webapiwebapi – Web-API** aus, und klicken Sie auf **Bearbeiten...**.  
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi18.png)

  26. Wählen Sie im Bildschirm webapitowebapi – Web-API-Eigenschaften die Registerkarte Ausstellungs **Transformationsregeln** aus, und klicken Sie auf **Regel hinzufügen.** 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi19.png)

  27. Wählen Sie im Assistenten zum Hinzufügen von Transformations Anspruchs Regeln die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden** aus, und klicken Sie auf **weiter**. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi20.png)

  28. Geben Sie **passallclaims** in **Name der Anspruchs Regel ein:** Feld und **x: [] => Issue (Claim = x);** Anspruchs Regel in benutzerdefinierter Regel: Feld, und klicken Sie auf Fertigstellen.  
   
      ![App-reg](media/adfs-msal-web-api-web-api/webapi21.png)

  29. Klicken Sie auf der Seite webapiin WebAPI – Web-API-Eigenschaften auf OK.

  30. Wählen Sie auf dem Bildschirm WebAPI-WebAPI-Eigenschaften die Option webapito WebAPI – Web-API 2 aus, und klicken Sie auf Bearbeiten...</br> 
  ![App-reg](media/adfs-msal-web-api-web-api/webapi22.png)

  31. Wählen Sie auf der Seite webapitowebapi – Web-API 2-Eigenschaften die Registerkarte Ausstellungs Transformationsregeln aus, und klicken Sie auf Regel hinzufügen. 

  32. Wählen Sie im Assistenten zum Hinzufügen von Transformations Anspruchs Regeln die Option Ansprüche mithilfe einer benutzerdefinierten Regel senden aus, und klicken Sie auf Next ![ App reg.](media/adfs-msal-web-api-web-api/webapi23.png)

  33. Geben Sie passallclaims in Name der Anspruchs Regel ein: Feld und **x: [] => Issue (Claim = x);** Anspruchs Regel in **benutzerdefinierter Regel:** Feld, und klicken Sie auf **Fertig**stellen.  
   
      ![App-reg](media/adfs-msal-web-api-web-api/webapi24.png)

  34.  Klicken Sie auf der Seite webapito WebAPI – Web-API 2-Eigenschaften auf OK und dann auf dem Bildschirm WebAPI-WebAPI-Eigenschaften.  
 

## <a name="code-configuration"></a>Code Konfiguration 

In diesem Abschnitt erfahren Sie, wie Sie eine Web-API zum Abrufen einer anderen Web-API konfigurieren 

  1. Das Beispiel [hier](https://github.com/microsoft/adfs-sample-msal-dotnet-webapi-to-webapi-onbehalfof) herunterladen  
  
  2. Öffnen Sie das Beispiel mithilfe von Visual Studio. 
  
  3. Öffnen Sie die Datei App.config. Ändern Sie Folgendes: 
       - Ida: Authority-Enter https://[Your AD FS Hostname]/ADFS/
       - Ida: ClientID: Geben Sie den Wert aus #3 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - Ida: redirecturi: Geben Sie den Wert aus #3 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - TODO: todolistresourceid – geben Sie den Bezeichnerwert aus #4 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - Ida: TODO: todolistbaseaddress: Geben Sie den Bezeichnerwert aus #4 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
      
            ![App-reg](media/adfs-msal-web-api-web-api/webapi25.png)

  4. Öffnen Sie die Datei Web.config unter TodoListService. Ändern Sie Folgendes: 
       - Ida: Audience: Geben Sie den Wert für den Client Bezeichner aus #12 in App-Registrierung in AD FS obigen Abschnitt ein.
       - Ida: ClientID: Geben Sie den Wert für den Client Bezeichner aus #12 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - Ida: clientsecret: Geben Sie den gemeinsamen geheimen Schlüssel ein, der aus #13 in App-Registrierung in AD FS obigen Abschnitt kopiert wurde.
       - Ida: redirecturi: Geben Sie den redirecturi-Wert aus #12 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - Ida: AdfsMetadataEndpoint-geben Sie https://[Your AD FS Hostname]/FederationMetadata/2007-06/federationmetadata.xml 
       - Ida: obowebapibase: Geben Sie den Bezeichnerwert aus #19 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
       - Ida: Authority-Enter https://[Your AD FS Hostname]/ADFS 
  
          ![App-reg](media/adfs-msal-web-api-web-api/webapi26.png) 

 5. Öffnen Sie die Datei Web.config unter webapiobo. Ändern Sie Folgendes: 
       - Ida: AdfsMetadataEndpoint-geben Sie https://[Your AD FS Hostname]/FederationMetadata/2007-06/federationmetadata.xml 
       - Ida: Audience: Geben Sie den Wert für den Client Bezeichner aus #12 in App-Registrierung in AD FS obigen Abschnitt ein. 
 
          ![App-reg](media/adfs-msal-web-api-web-api/webapi27.png)
 
## <a name="test-the-sample"></a>Testen des Beispiels 

In diesem Abschnitt wird gezeigt, wie das oben konfigurierte Beispiel getestet wird. 

Nachdem die Codeänderungen vorgenommen wurden, erstellen Sie die Projekt Mappe neu. 
 
  1. Klicken Sie in Visual Studio mit der rechten Maustaste auf Projekt Mappe, und wählen Sie **Start Projekte festlegen...** 
      
      ![App-reg](media/adfs-msal-web-api-web-api/webapi28.png)

  2. Stellen Sie auf den Eigenschaften Seiten sicher, dass die **Aktion** für jedes Projekt mit Ausnahme von "dedolistspa" auf **Start** festgelegt ist.  
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi29.png)
  
  3. Klicken Sie oben in Visual Studio auf den grünen Pfeil.  
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi30.png)

  4. Klicken Sie auf dem Hauptbildschirm der nativen App auf **Anmelden**. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi31.png)

     Wenn der Bildschirm für die native APP nicht angezeigt wird, suchen Sie in dem Ordner, in dem das projektrepository auf Ihrem System gespeichert ist, die Datei * msalcache. bin. 
  
  5. Sie werden auf die AD FS Anmeldeseite umgeleitet. Melden Sie sich bei Azure an. 
  
      ![App-reg](media/adfs-msal-web-api-web-api/webapi32.png)

  6. Wenn Sie sich angemeldet haben, geben Sie in das **Element Create a to do**den Text Web API to Web API-Aufrufe ein. Klicken Sie auf **Element hinzufügen**.  Dadurch wird die Web-API (to Do List Service) aufgerufen, die dann Web-API 2 (webapiobo) aufruft und das Element im Cache hinzufügt.  
 
      ![App-reg](media/adfs-msal-web-api-web-api/webapi33.png)
 
 ## <a name="next-steps"></a>Nächste Schritte
[AD FS OpenID Connect-/OAuth-Flows und Anwendungsszenarien](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 
 
