---
title: AD FS Native msal-APP, die Web-API aufrufen
description: erfahren Sie, wie Sie eine systemeigene App-Anmeldung erstellen, die durch AD FS 2019 authentifiziert wird, und Token mithilfe der msal-Bibliothek zum Abrufen von Web-APIs abrufen.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8b27097ac64f981343c1d455c826fa1b9004133e
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949586"
---
# <a name="scenario-native-app-calling-web-api"></a>Szenario: Native APP, die Web-API aufrufen 
>Gilt für: AD FS 2019 und höher 
 
Erfahren Sie, wie Sie eine systemeigene App-Anmeldung erstellen, die durch AD FS 2019 authentifiziert wird, und Token mithilfe der [msal-Bibliothek](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki) zum Abrufen von Web-APIs abrufen.  
 
Bevor Sie diesen Artikel lesen, sollten Sie sich mit den [AD FS Konzepten](../ad-fs-openid-connect-oauth-concepts.md) und dem [Flow zum Erteilen von Autorisierungscodes](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md#authorization-code-grant-flow) vertraut machen.
 
## <a name="overview"></a>Übersicht 
 
 ![Übersicht](media/adfs-msal-native-app-web-api/native1.png)

In diesem Flow fügen Sie Ihrer nativen app (öffentlicher Client) eine Authentifizierung hinzu, wodurch sich Benutzer anmelden und eine Web-API aufrufen können. Um eine Web-API aus einer nativen App aufzurufen, die Benutzer anmeldet, können Sie die [acquiretokeninteractive-tokenerwerbs](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.ipublicclientapplication.acquiretokeninteractive?view=azure-dotnet#Microsoft_Identity_Client_IPublicClientApplication_AcquireTokenInteractive_System_Collections_Generic_IEnumerable_System_String__) -Methode von msal verwenden. MSAL nutzt einen Webbrowser, um diese Interaktion zu aktivieren. 

 
Um besser zu verstehen, wie Sie eine native app in AD FS konfigurieren, um das Zugriffs Token interaktiv abzurufen, verwenden wir ein Beispiel, das [hier](https://github.com/microsoft/adfs-sample-msal-dotnet-native-to-webapi) verfügbar ist, und Exemplarische Vorgehensweise die Schritte zur APP-Registrierung und Code Konfiguration.  
 

## <a name="pre-requisites"></a>Voraussetzungen 


- GitHub-Client Tools 
- AD FS 2019 oder höher konfiguriert und wird ausgeführt 
- Visual Studio 2013 oder höher 
 

## <a name="app-registration-in-ad-fs"></a>App-Registrierung in AD FS 
In diesem Abschnitt wird gezeigt, wie Sie die native App als einen öffentlichen Client und eine Web-API als vertrauende Seite (RP) in AD FS registrieren. 

  1. Klicken Sie in **AD FS Verwaltung**mit der rechten Maustaste auf **Anwendungs Gruppen** , und wählen Sie **Anwendungs Gruppe hinzufügen**aus.   
  
  2. Geben Sie im Anwendungs Gruppen-Assistenten für den Namen **nativeapptwebapi** ein, und wählen Sie unter **Client-Server Anwendungen** die native Anwendung aus, die auf **eine Web-API-Vorlage zugreift** . Klicken Sie auf **Weiter**.  
  
      ![App-reg](media/adfs-msal-native-app-web-api/native2.png)  

  3. Kopieren Sie den Wert für den **Client Bezeichner** . Sie wird später als Wert für **ClientID** in der **app. config** -Datei der Anwendung verwendet. Geben Sie Folgendes für den **Umleitungs-URI ein:** https://ToDoListClient. Klicken Sie auf **Add**. Klicken Sie auf **Weiter**.  
 
     ![App-reg](media/adfs-msal-native-app-web-api/native3.png) 

  4. Geben Sie auf dem Bildschirm Web-API konfigurieren den **Bezeichner:** https://localhost:44321/ ein. Klicken Sie auf **Add**. Klicken Sie auf **Weiter**. Dieser Wert wird später in den Dateien " **app. config** " und " **Web. config** " der Anwendung verwendet.
 
     ![App-reg](media/adfs-msal-native-app-web-api/native4.png)   
  
  5. Wählen Sie auf der Seite Access Control Richtlinie anwenden die Option **Alle zulassen** aus, und klicken Sie auf **weiter**. 
  
     ![App-reg](media/adfs-msal-native-app-web-api/native5.png)   
  
  6. Vergewissern Sie sich auf dem Bildschirm Anwendungs Berechtigungen konfigurieren, dass **OpenID** ausgewählt ist, und klicken Sie auf **weiter**.  
     
     ![App-reg](media/adfs-msal-native-app-web-api/native6.png) 

  7. Klicken Sie auf dem Bildschirm Zusammenfassung auf **weiter**.
  
  8. Klicken Sie im Bildschirm Fertigstellen auf **Schließen**. 
  
  9. Klicken Sie in AD FS Verwaltung auf **Anwendungs Gruppen** , und wählen Sie dann **nativeappswebapi** -Anwendungs Gruppe aus. Klicken Sie mit der rechten Maustaste, und wählen Sie **Eigenschaften**aus.
  
      ![App-reg](media/adfs-msal-native-app-web-api/native7.png)

  10. Wählen Sie auf dem Bildschirm Eigenschaften von nativeapptewebapi die Option **nativeappto WebAPI – Web-API** unter **Web-API** aus, und klicken Sie auf **Bearbeiten.** 
  
      ![App-reg](media/adfs-msal-native-app-web-api/native8.png) 

  11. Wählen Sie auf der Seite nativeapptowebapi – Web-API-Eigenschaften die Registerkarte Ausstellungs **Transformationsregeln** aus, und klicken Sie auf **Regel hinzufügen.** 
  
      ![App-reg](media/adfs-msal-native-app-web-api/native9.png) 

  12. Wählen Sie im Assistenten zum Hinzufügen von Transformations Anspruchs Regeln die **Option eingehenden Anspruch** in der **Anspruchs Regel Vorlage transformieren:** Dropdown aus, und klicken Sie auf **weiter**.  
  
      ![App-reg](media/adfs-msal-native-app-web-api/native10.png) 

  13. Geben Sie im Feld **Anspruchs Regel Name: den Namen** **NameID** ein. Wählen Sie **Name** für **Typ des eingehenden Anspruchs aus:** , Name- **ID** für **ausgehenden Anspruchstyp:** und allgemeiner **Name** für das **Format der ausgehenden namens-ID:** Klicken Sie auf **Fertig stellen**.
  
      ![App-reg](media/adfs-msal-native-app-web-api/native11.png) 

  14. Klicken Sie auf der Seite nativeappto WebAPI – Web API Properties auf OK und anschließend auf dem Bildschirm nativeapptewebapi-Eigenschaften.  
 
## <a name="code-configuration"></a>Code Konfiguration 
In diesem Abschnitt wird gezeigt, wie Sie eine native App für den Anmelde Benutzer konfigurieren und Token zum Aufrufen der Web-API abrufen. 

1. Das Beispiel [hier](https://github.com/microsoft/adfs-sample-msal-dotnet-native-to-webapi) herunterladen 

2. Öffnen Sie das Beispiel mithilfe von Visual Studio. 

3. Öffnen Sie die Datei App.config. Ändern Sie Folgendes: 
   - Ida: Authority-Enter https://[Your AD FS Hostname]/ADFS
   - Ida: ClientID: Geben Sie den Wert für den **Client Bezeichner** aus #3 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
   - Ida: redirecturi: Geben Sie den **Umleitungs-URI** -Wert aus #3 in der APP-Registrierung in AD FS obigen Abschnitt ein.
   - TODO: todolistresourceid – geben Sie den **Bezeichnerwert** aus #4 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
   - Ida: TODO: todolistbaseaddress: Geben Sie den **Bezeichnerwert** aus #4 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
 
     ![Code Konfiguration](media/adfs-msal-native-app-web-api/native12.png)

 4. Öffnen Sie die Datei  Web.config. Ändern Sie Folgendes: 
    - Ida: Audience: Geben Sie den **Bezeichnerwert** aus #4 in der APP-Registrierung in AD FS obigen Abschnitt ein. 
    - Ida: AdfsMetadataEndpoint-Enter https://[Your AD FS Hostname]/FederationMetadata/2007-06/FederationMetadata.XML 
    
      ![Code Konfiguration](media/adfs-msal-native-app-web-api/native13.png)
 
  
## <a name="test-the-sample"></a>Testen des Beispiels 
In diesem Abschnitt wird gezeigt, wie das oben konfigurierte Beispiel getestet wird. 

  1. Nachdem die Codeänderungen vorgenommen wurden, erstellen Sie die Projekt Mappe neu. 
 
  2. Klicken Sie in Visual Studio mit der rechten Maustaste auf Projekt Mappe, und wählen Sie **Start Projekte festlegen...**  
 
     ![App-Test](media/adfs-msal-native-app-web-api/native14.png)

  3. Stellen Sie auf den Eigenschaften Seiten sicher, dass die **Aktion** für jedes Projekt auf **Start** festgelegt ist. 
      
     ![App-Test](media/adfs-msal-native-app-web-api/native15.png)

  4. Klicken Sie oben in Visual Studio auf den grünen Pfeil.  
 
     ![App-Test](media/adfs-msal-native-app-web-api/native16.png)

  5. Klicken Sie auf dem Hauptbildschirm der nativen App auf **Anmelden**.  
  
     ![App-Test](media/adfs-msal-native-app-web-api/native17.png)

    Wenn der Bildschirm für die native APP nicht angezeigt wird, suchen Sie in dem Ordner, in dem das projektrepository auf Ihrem System gespeichert ist, die Datei * msalcache. bin. 

  6. Sie werden auf die AD FS Anmeldeseite umgeleitet. Melden Sie sich bei Azure an. 
  
      ![App-Test](media/adfs-msal-native-app-web-api/native18.png)

  7. Wenn Sie sich angemeldet haben, geben Sie im Feld **Create a to do einen**Text **Build Native app to Web API** ein. Klicken Sie auf **Element hinzufügen**.  Dadurch wird der **to Do List Service (Web-API)** aufgerufen und das Element im Cache hinzugefügt. 
    
       ![App-Test](media/adfs-msal-native-app-web-api/native19.png)
 
## <a name="next-steps"></a>Nächste Schritte
[AD FS OpenID Connect-/OAuth-Flows und Anwendungsszenarien](../../overview/ad-fs-openid-connect-oauth-flows-scenarios.md)
 