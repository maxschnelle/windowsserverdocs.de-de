---
title: Erstellen Sie einen nativen Client-Anwendung mithilfe von öffentlichen OAuth-Clients mit AD FS 2016 oder höher
description: Eine exemplarische Vorgehensweise bietet Anweisungen, die einen nativen Client-Anwendung mithilfe von öffentlichen OAuth-Clients und AD FS 2016 oder höher erstellen
author: billmath
ms.author: billmath
ms.reviewer: anandy
manager: mtillman
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.openlocfilehash: 15bb6f1e39f64ff19ebb5515188ee944e277d3b7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445478"
---
# <a name="build-a-native-client-application-using-oauth-public-clients-with-ad-fs-2016-or-later"></a>Erstellen Sie einen nativen Client-Anwendung mithilfe von öffentlichen OAuth-Clients mit AD FS 2016 oder höher

## <a name="overview"></a>Übersicht

In diesem Artikel zeigt, wie eine systemeigene Anwendung zu erstellen, die mit einer Web-API geschützte von AD FS 2016 oder höher interagiert wird.

1. .Net TodoListClient-WPF-Anwendung verwendet die Active Directory Authentication Library (ADAL), um ein JWT-Zugriffstoken aus Azure Active Directory (Azure AD) über das OAuth 2.0-Protokoll zu erhalten.
2. Das Zugriffstoken dient als ein trägertoken, das zum Authentifizieren des Benutzers, beim Aufrufen des Endpunkts /todolist den "todolistservice"-Web-API.
 Wir werden im Beispiel hier Azure AD verwenden und anschließend für AD FS 2016 oder höher ändern.

![Anwendung Übersicht zu](media/native-client-with-ad-fs-2016/appoverview.png)

## <a name="pre-requisites"></a>Voraussetzungen
Folgendes ist eine Liste der Voraussetzungen, die vor dem Abschluss dieses Dokuments erforderlich sind. In diesem Dokument wird davon ausgegangen, dass AD FS installiert wurde und eine AD FS-Farm erstellt wurde.

* GitHub-Clienttools
* AD FS in Windows Server 2016 oder höher
* Visual Studio 2013 oder höher

## <a name="creating-the-sample-walkthrough"></a>Erstellen die exemplarische Vorgehensweise

### <a name="create-the-application-group-in-ad-fs"></a>Erstellen Sie die Anwendungsgruppe in AD FS

1. AD FS-Verwaltung mit der Maustaste auf **Anwendungsgruppen** , und wählen Sie **Anwendungsgruppe hinzufügen**.

2. Geben Sie auf den Assistenten-Anwendung für den Namen einen beliebigen Namen, die, den Sie bevorzugen, den z. b. NativeToDoListAppGroup aus. Wählen Sie die **systemeigene Anwendung, die Zugriff auf eine Web-API** Vorlage. Klicken Sie auf **Weiter**.
 ![Anwendungsgruppe hinzufügen](media/native-client-with-ad-fs-2016/addapplicationgroup1.png)

3. Auf der **systemeigene Anwendung** Seite, den von AD FS generierte Bezeichner beachten. Dies ist die Id, die mit der AD FS die öffentlichen Client-app erkannt wird. Kopieren der **Clientbezeichner** Wert. Sie werden später verwendet als Wert für **Ida: "ClientID"** im Anwendungscode. Wenn Sie möchten, erhalten Sie hier einen beliebigen benutzerdefinierten Bezeichner. Der umleitungs-URI ist, jeden beliebigen Wert ein, beispielsweise put https://ToDoListClient ![Native app](media/native-client-with-ad-fs-2016/addapplicationgroup2.png)

4. Auf der **Konfigurieren von Web-API-** Seite, legen Sie den ID-Wert, für die Web-API. In diesem Beispiel muss dies der Wert des der **SSL-URL** , in dem die Web-App ausgeführt werden sollte. Sie können diesen Wert durch Klicken auf die Eigenschaften des Projekts TooListServer in der Lösung zu erhalten. Dies wird später verwendet als die **Todo:TodoListResourceId** Wert in **"App.config"** Datei, die systemeigene Clientanwendung und auch als die **Todo:TodoListBaseAddress**.
![Web-API](media/native-client-with-ad-fs-2016/addapplicationgroup3.png)

5. Sehen Sie sich die **Access-Control-Richtlinie anwenden** und **Anwendungsberechtigungen konfigurieren** mit den Standardwerten eingerichtet. Die Seite "Zusammenfassung" sollte wie folgt aussehen.
![Zusammenfassung](media/native-client-with-ad-fs-2016/addapplicationgroupsummary.png)

Klicken Sie auf Weiter, und schließen Sie den Assistenten.

### <a name="add-the-nameidentifier-claim-to-the-list-of-claims-issued"></a>Fügen Sie den NameIdentifier Anspruch auf die Liste der ausgestellten Ansprüche hinzu.
Die demoanwendung verwendet den Wert im NameIdentifier-Anspruch an verschiedenen Stellen. Im Gegensatz zu Azure AD wird der AD FS einen NameIdentifier-Anspruch nicht standardmäßig ausgegeben. Aus diesem Grund müssen wir fügen eine Anspruchsregel aus, um den NameIdentifier-Anspruch ausstellen, sodass die Anwendung der richtige Wert verwendet werden kann. In diesem Beispiel wird der Vorname des Benutzers als den NameIdentifier-Wert für den Benutzer in das Token ausgegeben.
Um die Anspruchsregel konfigurieren zu können, öffnen Sie die Anwendungsgruppe, die gerade erstellt haben, und klicken Sie mit der Doppelklicken auf die Web-API. Wählen Sie die Registerkarte "Ausstellungstransformationsregeln", und klicken Sie dann auf die Schaltfläche "Regel hinzufügen" auf. Wählen Sie in den Typ von anspruchsregelvorlagen die benutzerdefinierte Anspruchsregel aus, und klicken Sie dann fügen Sie die Anspruchsregel wie folgt hinzu.

```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier"), query = ";givenName;{0}", param = c.Value);
```

![Regel für NameIdentifier-Anspruch](media/native-client-with-ad-fs-2016/addnameidentifierclaimrule.png)

### <a name="modify-the-application-code"></a>Ändern des Anwendungscodes

In diesem Abschnitt wird erläutert, wie Sie Web-API-Beispiel herunterladen und ändern Sie sie in Visual Studio.   Wir verwenden das Azure AD-Beispiel, das ist [hier](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop).  

Um das Beispielprojekt herunterzuladen, verwenden Sie Git Bash, und geben Sie Folgendes:  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-native-desktop  
```  

#### <a name="modify-todolistclient"></a>Ändern Sie "todolistclient"

Dieses Projekt in der Lösung stellt die systemeigene Clientanwendung dar. Wir müssen sicherstellen, dass die Clientanwendung erkennt:

1. Wo der Benutzer authentifiziert, wenn erforderlich?
2. Was ist, dass die dem Client-ID muss der Authentifizierungsstelle (AD FS) bereitstellen?
3. Was ist die ID der Ressource, der das Zugriffstoken für aufgefordert?
4. Was ist die Basisadresse des Web-API?

Die folgenden codeänderungen sind erforderlich, um die oben angegebenen Informationen für die native Client-Anwendung zu erhalten.

**App.config**

* Fügen Sie den Schlüssel **Ida: Autorität** mit dem Wert, der mit AD FS-Diensts. beispielsweise https://fs.contoso.com/adfs/
* Ändern Sie **Ida: "ClientID"** Schlüssel mit dem Wert aus **Client-ID** in die **systemeigene Anwendung** Seite während der Erstellung der Anwendungsgruppe in AD FS. Z. B. 3f07368b-6efd-4f50-a330-d93853f4c855
* Ändern der **Todo:todo:TodoListResourceId** mit dem Wert von **Bezeichner** in die **Konfigurieren von Web-API-** Seite während der Erstellung der Anwendungsgruppe in AD FS. beispielsweise https://localhost:44321/
* Ändern der **Todo:TodoListBaseAddress** mit dem Wert von **Bezeichner** in die **Konfigurieren von Web-API-** Seite während der Erstellung der Anwendungsgruppe in AD FS. beispielsweise https://localhost:44321/
* Legen Sie den Wert der **Ida: RedirectUri** mit dem Wert von **Umleitungs-URI** in die **systemeigene Anwendung** Seite während der Erstellung der Anwendungsgruppe in AD FS. beispielsweise https://ToDoListClient
* Zur Erleichterung des Lesens können Sie entfernen / kommentieren Sie den Schlüssel für **Ida: Mandanten** und **Ida: AADInstance**.

  ![App-Konfiguration](media/native-client-with-ad-fs-2016/app_configfile.PNG)


**MainWindow.xaml.cs**

* Kommentieren Sie die Zeile für AadInstance als folgende

        // private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];

* Fügen Sie den Wert für die Autorität, wie unten gezeigt

        private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

* Löschen Sie die Zeile für die Erstellung der **Autorität** Wert AadInstance und Mandanten

        private static string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);

* In der Funktion **MainWindow**, AuthContext Instanziierung ändern

        authContext = new AuthenticationContext(authority,false);

    ADAL unterstützt nicht die AD FS als Autorität für die Überprüfung und aus diesem Grund müssen wir ein false-Wert-Flag für ValidateAuthority-Parameter übergeben.

  ![Klicken Sie im Hauptfenster](media/native-client-with-ad-fs-2016/mainwindow.PNG)

#### <a name="modify-todolistservice"></a>Ändern Sie "todolistservice"
Zwei Dateien benötigen, Änderungen in diesem Projekt – "Web.config" und Startup.Auth.cs. Änderungen der Datei "Web.config" sind erforderlich, um die richtigen Werte der Parameter zu erhalten. Startup.Auth.cs Änderungen sind erforderlich, die Web-API zum Authentifizieren von AD FS anstelle von Azure AD festgelegt.

**Web.config**

* Kommentieren Sie den Schlüssel **Ida: Mandanten** wie wir ihn nicht benötigen
* Fügen Sie den Schlüssel für **Ida: Autorität** mit dem Wert, der angibt, des FQDN des Verbunds-Dienst, Beispiel https://fs.contoso.com/adfs/
* Schlüssel bearbeiten **Ida: Zielgruppe** mit dem Wert von der Web-API-Bezeichner, der Sie angegeben haben, in der **Konfigurieren von Web-API-** Seite während der Anwendungsgruppe in AD FS hinzufügen.
* Fügen Sie Schlüssel **Ida: AdfsMetadataEndpoint** mit dem Wert für die Verbundmetadaten-URL des AD FS Dienst, zum Beispiel: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

![Webkonfiguration](media/native-client-with-ad-fs-2016/webconfig.PNG)


**Startup.Auth.cs**

Ändern Sie wie unten gezeigt die ConfigureAuth-Funktion

    public void ConfigureAuth(IAppBuilder app)
    {
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
    }

Im Wesentlichen muss konfigurieren wir die Authentifizierung verwenden von AD FS, und geben Sie weitere Informationen über die AD FS-Metadaten und zum Überprüfen des Tokens, die "Audience"-Anspruch der Wert, der von der Web-API erwartet wird.
Ausführen der Anwendung

1. Klicken Sie mit der rechten Maustaste auf, und wechseln Sie zu Eigenschaften, auf die Projektmappe NativeClient-DotNet. Ändern Sie das Startprojekt wie unten dargestellt in mehrere Startprojekte aus, und legen Sie "todolistclient" und "todolistservice" auf Start.
![Projektmappeneigenschaften](media/native-client-with-ad-fs-2016/solutionproperties.png)

2.  Drücken Sie F5-Taste oder die Option Debuggen > Weiter in der Menüleiste. Hierdurch wird die systemeigene Anwendung und die Web-API. Klicken Sie auf die Schaltfläche "Anmelden" für die systemeigene Anwendung und wird Popupfenster eine interaktive Anmeldung über AD AL und Umleiten an Ihrem AD FS-Dienst. Geben Sie die Anmeldeinformationen eines gültigen Benutzers ein.
![Anmeldung](media/native-client-with-ad-fs-2016/sign-in.png)

In diesem Schritt die systemeigene Anwendung mit AD FS umgeleitet werden soll, und haben Sie ein ID-Token und Zugriffstoken für die Web-API

3. Geben Sie ein Element in das Textfeld ein und klicken auf das Element hinzufügen. In diesem Schritt wendet die Anwendung sich an die Web-API hinzufügen das Element, und klicken Sie hierfür, übergibt das Zugriffstoken, um die Web-API von AD FS abgerufen. Die Web-API entspricht den Audience-Wert, um sicherzustellen, dass das Token ist dafür vorgesehen, und überprüft die Signatur des Tokens anhand der Informationen aus den Metadaten des Verbunds.

![Anmelden](media/native-client-with-ad-fs-2016/clienttodoadd.png)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
