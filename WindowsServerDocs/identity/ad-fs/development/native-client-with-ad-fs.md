---
title: Erstellen einer nativen Client Anwendung mit öffentlichen OAuth-Clients mit AD FS 2016 oder höher
description: Eine exemplarische Vorgehensweise, die Anweisungen zum Aufbauen einer systemeigenen Client Anwendung mit öffentlichen OAuth-Clients und AD FS 2016 oder höher bietet.
author: billmath
ms.author: billmath
ms.reviewer: anandy
manager: mtillman
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.openlocfilehash: 96659164a9eea1784cb529c47dd58be70d546f80
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75948735"
---
# <a name="build-a-native-client-application-using-oauth-public-clients-with-ad-fs-2016-or-later"></a>Erstellen einer nativen Client Anwendung mit öffentlichen OAuth-Clients mit AD FS 2016 oder höher

## <a name="overview"></a>Übersicht

In diesem Artikel wird gezeigt, wie Sie eine native Anwendung erstellen, die mit einer Web-API interagiert, die von AD FS 2016 oder höher geschützt wird.

1. Die .net todolistclient WPF-Anwendung verwendet die Active Directory-Authentifizierungsbibliothek (Adal), um ein JWT-Zugriffs Token von Azure Active Directory (Azure AD) über das OAuth 2,0-Protokoll abzurufen.
2. Das Zugriffs Token wird als bearertoken verwendet, um den Benutzer zu authentifizieren, wenn der/ToDoList-Endpunkt der Web-API TodoListService aufgerufen wird.
 Wir verwenden das Anwendungsbeispiel für die Azure Ad hier und ändern es dann für AD FS 2016 oder höher.

![Anwendungs überschreichung](media/native-client-with-ad-fs-2016/appoverview.png)

## <a name="pre-requisites"></a>Voraussetzungen
Im folgenden finden Sie eine Liste der Voraussetzungen, die vor der Fertigstellung dieses Dokuments erforderlich sind. In diesem Dokument wird davon ausgegangen, dass AD FS installiert und eine AD FS-Farm erstellt wurde.

* GitHub-Client Tools
* AD FS in Windows Server 2016 oder höher
* Visual Studio 2013 oder höher

## <a name="creating-the-sample-walkthrough"></a>Erstellen der exemplarischen Vorgehensweise

### <a name="create-the-application-group-in-ad-fs"></a>Erstellen Sie die Anwendungs Gruppe in AD FS

1. Klicken Sie in AD FS Verwaltung mit der rechten Maustaste auf **Anwendungs Gruppen** , und wählen Sie **Anwendungs Gruppe hinzufügen**aus.

2. Geben Sie im Anwendungs Gruppen-Assistenten für den Namen einen beliebigen Namen ein, z. b. nativedolistappgroup. Wählen Sie die **native Anwendung auf eine Web-API** -Vorlage aus. Klicken Sie auf **Weiter**.
 ![Anwendungs Gruppe hinzufügen](media/native-client-with-ad-fs-2016/addapplicationgroup1.png)

3. Notieren Sie sich auf der Seite **native Anwendung** den von AD FS generierten Bezeichner. Dies ist die ID, mit der AD FS die öffentliche Client-App erkennt. Kopieren Sie den Wert für den **Client Bezeichner** . Sie wird später als Wert für " **Ida: ClientID** " im Anwendungscode verwendet. Wenn Sie möchten, können Sie hier einen benutzerdefinierten Bezeichner eingeben. Der Umleitungs-URI ist ein beliebiger Wert, z. b. https://ToDoListClient ![ Native App](media/native-client-with-ad-fs-2016/addapplicationgroup2.png)

4. Legen Sie auf der Seite **Web-API konfigurieren** den Bezeichnerwert für die Web-API fest. In diesem Beispiel sollte dies der Wert der **SSL-URL** sein, auf der die Web-App ausgeführt werden soll. Sie erhalten diesen Wert, indem Sie auf die Eigenschaften des Projekts "Projekt in der Projekt Mappe" klicken. Diese wird später als **TODO: todolistresourceid-** Wert in der Datei " **app. config** " der systemeigenen Client Anwendung und auch als " **TODO: todolistbaseaddress**" verwendet.
![Web-API](media/native-client-with-ad-fs-2016/addapplicationgroup3.png)

5. Durchlaufen Sie die **Richtlinie Apply Access Control** , und konfigurieren Sie die **Anwendungs Berechtigungen** mit den Standardwerten. Die Seite "Zusammenfassung" sollte wie folgt aussehen.
![Zusammenfassung](media/native-client-with-ad-fs-2016/addapplicationgroupsummary.png)

Klicken Sie auf Weiter, und schließen Sie den Assistenten ab.

### <a name="add-the-nameidentifier-claim-to-the-list-of-claims-issued"></a>Hinzufügen des NameIdentifier-Anspruchs zur Liste der ausgestellten Ansprüche
Die Demoanwendung verwendet den Wert im NameIdentifier-Anspruch an verschiedenen Stellen. Im Gegensatz zu Azure AD gibt AD FS standardmäßig keinen NameIdentifier-Anspruch aus. Daher müssen wir eine Anspruchs Regel hinzufügen, um den NameIdentifier-Anspruch auszugeben, damit die Anwendung den korrekten Wert verwenden kann. In diesem Beispiel wird der Vorname des Benutzers als NameIdentifier-Wert für den Benutzer im Token ausgegeben.
Öffnen Sie zum Konfigurieren der Anspruchs Regel die soeben erstellte Anwendungs Gruppe, und doppelklicken Sie auf die Web-API. Wählen Sie auf der Registerkarte Ausstellungs Transformationsregeln die Option Regel hinzufügen aus. Wählen Sie in der Regel Typ der Anspruchs Regel benutzerdefinierte Anspruchs Regel aus, und fügen Sie dann wie unten gezeigt die Anspruchs Regel hinzu.

```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier"), query = ";givenName;{0}", param = c.Value);
```

![NameIdentifier-Anspruchs Regel](media/native-client-with-ad-fs-2016/addnameidentifierclaimrule.png)

### <a name="modify-the-application-code"></a>Ändern des Anwendungscodes

In diesem Abschnitt wird erläutert, wie Sie die Beispiel-Web-API herunterladen und in Visual Studio ändern.   Wir verwenden das [hier](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop)Azure AD Beispiel.  

Verwenden Sie zum Herunterladen des Beispielprojekts git bash, und geben Sie Folgendes ein:  

```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-native-desktop  
```  

#### <a name="modify-todolistclient"></a>Ändern von "" in "".

Dieses Projekt in der Projekt Mappe stellt die Native Client Anwendung dar. Wir müssen sicherstellen, dass die Client Anwendung Folgendes kennt:

1. Wo soll der Benutzer bei Bedarf authentifiziert werden?
2. Welche ID muss der Client für die authentifizier Ende Zertifizierungsstelle (AD FS) bereitstellen?
3. Wie lautet die ID der Ressource, für die wir das Zugriffs Token anfordern?
4. Was ist die Basisadresse der Web-API?

Die folgenden Codeänderungen sind erforderlich, um die obigen Informationen in die Native Client-Anwendung zu übernehmen.

**"App. config"**

* Fügen Sie den Schlüssel " **Ida: Authority** " mit dem Wert hinzu, der den AD FS Dienst darstellt. Beispiel: https://fs.contoso.com/adfs/.
* Ändern Sie den Schlüssel " **Ida: ClientID** " mit dem Wert aus der **Client** -ID auf der Seite " **native Anwendung** " während der Erstellung der Anwendungs Gruppe in AD FS. Z. b. 3f 07368b-6efd-4e50a330-d93853f 4c855
* Ändern Sie **TODO: TODO: todolistresourceid** mit dem Wert aus **Bezeichner** auf der Seite **Web-API konfigurieren** während der Erstellung der Anwendungs Gruppe in AD FS. Beispiel: https://localhost:44321/.
* Ändern Sie **TODO: todolistbaseaddress** bei der Erstellung der Anwendungs **Gruppe in AD FS auf der** Seite Web- **API konfigurieren** . Beispiel: https://localhost:44321/.
* Legen Sie den Wert von **Ida: redirecturi** während der Erstellung der Anwendungs Gruppe in AD FS auf der Seite für die systemeigene **Anwendung** auf den **Umleitungs-URI** fest. Beispiel: https://ToDoListClient.
* Um das Lesen zu vereinfachen, können Sie den Schlüssel für " **Ida: Tenant** " und " **Ida: aadinstance**" entfernen/kommentieren.

  ![Anwendungskonfiguration](media/native-client-with-ad-fs-2016/app_configfile.PNG)


**MainWindow.xaml.cs**

* Kommentieren Sie die Zeile für aadinstance wie unten beschrieben.

        // private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];

* Fügen Sie den Wert für Authority wie unten beschrieben hinzu.

        private static string authority = ConfigurationManager.AppSettings["ida:Authority"];

* Löschen Sie die Zeile zum Erstellen des **Autoritäts** Werts aus aadinstance und Tenant.

        private static string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);

* Ändern Sie im **MainWindow**-Funktions Fenster die authcontext-Instanziierung in.

        authContext = new AuthenticationContext(authority,false);

    Adal unterstützt das Validieren von AD FS als Autorität nicht. Daher muss ein false-Wert-Flag für den validateauthority-Parameter übergeben werden.

  ![Hauptfenster](media/native-client-with-ad-fs-2016/mainwindow.PNG)

#### <a name="modify-todolistservice"></a>Ändern von "dedolistservice"
In diesem Projekt müssen zwei Dateien geändert werden – "Web. config" und "Startup.auth.cs". Web. config-Änderungen sind erforderlich, um die korrekten Werte der Parameter zu erhalten. Startup.auth.cs Änderungen sind erforderlich, um die WebAPI für die Authentifizierung mit AD FS anstatt Azure AD festzulegen.

**Web.config**

* Kommentieren Sie den Schlüssel **Ida: Tenant** , da wir ihn nicht benötigen.
* Fügen Sie den Schlüssel für **Ida: Authority** mit dem Wert hinzu, der den voll qualifizierten Namen des Verbund Dienstanbieter angibt, z. b. https://fs.contoso.com/adfs/
* Ändern Sie Key **Ida: Audience** mit dem Wert des Web-API-Bezeichners, den Sie auf der Seite **Web-API konfigurieren** beim Hinzufügen einer Anwendungs Gruppe in AD FS angegeben haben.
* Fügen Sie Key **Ida: AdfsMetadataEndpoint** mit einem Wert hinzu, der der Verbund Metadaten-URL des AD FS Dienstanbieter entspricht, für Ex: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

![Web-Konfiguration](media/native-client-with-ad-fs-2016/webconfig.PNG)


**Startup.Auth.cs**

Ändern Sie die Funktion "Konfiguration" wie unten beschrieben.

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

Im wesentlichen konfigurieren wir die Authentifizierung für die Verwendung AD FS und geben weitere Informationen über die AD FS Metadaten an. um das Token zu validieren, sollte der Anspruch der Zielgruppe der Wert sein, der von der Web-API erwartet wird.
Ausführen der Anwendung

1. Klicken Sie in der Projekt Mappe nativeClient-dotnet mit der rechten Maustaste, und wechseln Sie zu Eigenschaften. Ändern Sie das Startprojekt wie unten dargestellt in mehrere Start Projekte, und legen Sie für "Start" sowohl "dedolistclient" als auch "dedolistservice"
![Projektmappeneigenschaften](media/native-client-with-ad-fs-2016/solutionproperties.png)

2.  Drücken Sie die Taste F5, oder wählen Sie Debuggen > in der Menüleiste fortfahren Dadurch werden sowohl die native Anwendung als auch die WebAPI gestartet. Klicken Sie in der systemeigenen Anwendung auf die Schaltfläche "Anmelden", und es wird eine interaktive Anmeldung von AD Al angezeigt, und Sie können eine Umleitung an den AD FS Dienst durchführt. Geben Sie die Anmelde Informationen eines gültigen Benutzers ein.
![Anmelden](media/native-client-with-ad-fs-2016/sign-in.png)

In diesem Schritt wird die native Anwendung an AD FS umgeleitet und ein ID-Token und ein Zugriffs Token für die Web-API erhalten.

3. Geben Sie in das Textfeld ein Element ein, und klicken Sie auf Element hinzufügen. In diesem Schritt erreicht die Anwendung die Web-API, um das Aufgaben Element hinzuzufügen, und stellt zu diesem Zweck das Zugriffs Token für die WebAPI dar, die aus AD FS abgerufen wurde. Die Web-API entspricht dem Audience-Wert, um sicherzustellen, dass das Token für Sie bestimmt ist, und überprüft die Tokensignatur anhand der Informationen aus den Verbund Metadaten.

![Anmelden](media/native-client-with-ad-fs-2016/clienttodoadd.png)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
