---
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: Erstellen Sie eine AD FS 2016 vertraulicher OAuth-Clients mit serverseitigen Anwendung
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 175c683f9097aeba4c1f06e8671183476c98aa3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869581"
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016"></a>Erstellen Sie eine AD FS 2016 vertraulicher OAuth-Clients mit serverseitigen Anwendung

>Gilt für: Windows Server 2016

Baut auf der anfänglichen Oauth-Unterstützung in AD FS unter Windows Server 2012 R2 auf und führt die AD FS 2016-Unterstützung für Clients verwalten ihre eigenen geheimen Schlüssel ein, z. B. eine app oder ein Dienst, der auf einem Webserver ausgeführt.  Diese Clients werden als vertrauliche Clients bezeichnet.    
Im folgenden finden Sie eine schematische Darstellung einer Webanwendung auf einem Webserver ausgeführt und dient als ein vertraulicher Client bei AD FS:  
  
## <a name="pre-requisites"></a>Voraussetzungen  
Folgendes ist eine Liste der Voraussetzungen, die vor dem Abschluss dieses Dokuments erforderlich sind. In diesem Dokument wird davon ausgegangen, dass AD FS installiert wurde und eine AD FS-Farm erstellt wurde.  
  
-   Ein Azure AD-Abonnement (eine kostenlose Testversion ist in Ordnung)  
  
-   GitHub-Clienttools  
  
-   AD FS in Windows Server 2016 TP4 oder höher  
  
-   Visual Studio 2013 oder höher.  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>Erstellen Sie eine Anwendungsgruppe in AD FS 2016  
Der folgende Abschnitt beschreibt, wie Sie die Anwendungsgruppe in AD FS 2016 zu konfigurieren.  
  
#### <a name="create-the-application-group"></a>Die Anwendungsgruppe erstellen  
  
1.  In AD FS-Verwaltung mit der rechten Maustaste auf die Gruppen für Anwendungen, und wählen Sie **Anwendungsgruppe hinzufügen**.  
  
2.  Geben Sie auf den Assistenten-Anwendung, für den Namen **ADFSOAUTHCC** und wählen Sie unter **eigenständigen Anwendungen** wählen Sie die **Server-Anwendung oder Website** Vorlage.  Klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)  
  
3.  Kopieren der **Clientbezeichner** Wert.  Sie werden später verwendet als Wert für **Ida: "ClientID"** in der web.config-Datei der Anwendung.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)  
  
4.  Geben Sie Folgendes für **Umleitungs-URI:** - **https://localhost:44323**.  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  
  
5.  Auf der **Anwendungsanmeldeinformationen konfigurieren** Bildschirm, aktivieren Sie das Kontrollkästchen **generieren Sie einen gemeinsamen geheimen Schlüssel**, und kopieren Sie den geheimen Schlüssel.  Dies wird später als Wert für verwendet **Ida: AppKey** in der web.config-Datei der Anwendung.  Klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)  
  
6.  Auf der **Zusammenfassung** auf **Weiter**.  
  
7.  Auf der **abschließen** auf **schließen**.  
  
8.  Auf die Anwendungsgruppe mit der rechten Maustaste und wählen Sie **Eigenschaften**.  
  
9. Auf **ADFSOAUTHCC Eigenschaften** klicken Sie auf **Anwendung hinzufügen**.  
  
10. Auf der **hinzufügen eine neue Anwendung in der Beispielanwendung** wählen **Web-API-**, und klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)  
  
11. Auf der **Konfigurieren von Web-API-** Bildschirm, geben Sie Folgendes für **Bezeichner** - **https://contoso.com/WebApp**.  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  Dieser Wert wird später verwendet werden, für die **Ida: GraphResourceId** in der web.config-Datei der Anwendung.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)  
  
12. Auf der **Zugriffssteuerungsrichtlinien wählen** auf **alle zulassen** , und klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. Auf der **Anwendungsberechtigungen konfigurieren** Bildschirm, stellen Sie sicher, dass **"user_impersonation"** ausgewählt ist, und klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)  
  
14. Auf der **Zusammenfassung** auf **Weiter**.  
  
15. Auf der **abschließen** auf **schließen**.  
  
16. Auf der **ADFSOAUTHCC Eigenschaften** klicken Sie auf **OK**.  
  
## <a name="upgrade-the-database"></a>Aktualisieren Sie die Datenbank  
Visual Studio 2015 wurde verwendet, in dieser exemplarischen Vorgehensweise erstellen.   Um das Beispiel, das Arbeiten mit Visual Studio 2015 zu erhalten, müssen Sie die Datenbankdatei aktualisieren.  Führen Sie dazu die nachfolgend aufgeführten Schritte aus.  
  
In diesem Abschnitt wird erläutert, wie Sie das Beispiel-Web-API herunterzuladen, und aktualisieren Sie die Datenbank in Visual Studio 2015.   Wir verwenden das Azure AD-Beispiel, das ist [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity).  
  
Um das Beispielprojekt herunterzuladen, verwenden Sie Git Bash, und geben Sie Folgendes:  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git  
```  
  
![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)  
  
#### <a name="to-upgrade-the-database-file"></a>So aktualisieren die Datenbankdatei  
  
1.  Öffnen das Projekt in Visual Studio, wird ein Popup mit der Sie informiert, dass der app mit SQL Server 2102 Express erforderlich sind, oder Sie müssen die Datenbank zu aktualisieren.  Klicken Sie auf Ok.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)  
  
2.  Nächsten Kompilierung der Anwendung durch Auswahl von Build -> Projektmappe erstellen oben.  Dadurch werden alle NuGet-Pakete wiederhergestellt.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)  
  
3.  Wählen Sie im oberen Bereich jetzt **Ansicht** -> **Server-Explorer**.  Sobald die, die unter geöffnet wird, **Datenverbindungen**, mit der rechten Maustaste **DefaultConnection** , und wählen Sie **Verbindung ändern**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)  
  
4.  Auf **Verbindung ändern**Option **erweitert**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)  
  
5.  Klicken Sie auf die erweiterten Eigenschaften-Datenquelle, und verwenden Sie so ändern Sie sie aus der Dropdown- **(localdb\v11. 0)** zu **(LoaclDB) MSSQLLocalDB**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)  
  
6.  Klicken Sie auf Ok. Klicken Sie auf Ok.  Klicken Sie auf "Ja", um die Datenbank zu aktualisieren.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)  
  
7.  Nach Abschluss dieser, mehr als auf der rechten Seite kopieren Sie den Wert im Feld neben **Verbindungszeichenfolge.**  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)  
  
8.  Nun, öffnen Sie die Datei "Web.config", und Ersetzen Sie den Wert, der "ConnectionString" mit dem Wert wird die oben kopierte.  Speichern Sie die Datei "Web.config".  
  
    > [!NOTE]  
    > Die oben genannten Schritte sind erforderlich, damit an, dass die neue "ConnectionString" abgerufen werden können.  Andernfalls, wenn wir die folgenden Update-Database ausführen tritt ein Fehler auf.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)  
  
9. Wählen Sie am oberen Rand der Visual Studio, **Ansicht** -> **Other Windows** -> **-Paket-Manager-Konsole**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)  
  
10. Geben Sie unten, in der Paket-Manager-Konsole: `Enable-Migrations` und die EINGABETASTE drücken.  
  
    > [!NOTE]  
    > Wenn man die Fehlermeldung Enable-Migrations nicht als Cmdlet erkannt werden, geben Sie Install-Package EntityFramework, um die EntityFramework zu aktualisieren.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)  
  
11. Geben Sie unten, in der Paket-Manager-Konsole: `Add-Migration <anynamehere>` und die EINGABETASTE drücken.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)  
  
12. Geben Sie unten, in der Paket-Manager-Konsole: `Update-Database` und die EINGABETASTE drücken.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)  
  
## <a name="modify-the-webapi-in-visual-studio"></a>Ändern Sie die Web-API in Visual Studio  
  
#### <a name="to-modify-the-sample-web-api"></a>So ändern Sie die Beispiel-Web-API  
  
1.  Öffnen Sie das Beispiel mithilfe von Visual Studio.  
  
2.  Öffnen Sie die Datei "Web.config".  Ändern Sie die folgenden Werte ein:  
  
    -   IDA: ClientId - Geben Sie den Wert von #3 oben.  
  
    -   IDA: AppKey - Geben Sie den Wert von #5 oben.  
  
    -   IDA: GraphResourceId - Geben Sie den Wert von #11 oben.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)  
  
3.  Öffnen Sie die Datei "Startup.Auth.cs" unter dem App_Start, und nehmen Sie die folgenden Änderungen:  
  
    -   Kommentieren Sie die folgenden Zeilen:  
  
        ```  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)  
  
    -   Fügen Sie die folgenden Codeelement hinzu:  
  
        ```  
        public static readonly string Authority = "https://<your_fsname>/adfs";  
        ```  
  
        wobei < Your_fsname > mit dem DNS-Teil der Verbunddienst-Url, z.B. "ADFS.contoso.com" ersetzt wird  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_26.PNG)  
  
4.  Öffnen Sie die UserProfileController.cs-Datei, und nehmen Sie die folgenden Änderungen:  
  
    -   Kommentieren Sie die folgenden:  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));  
        ```  
  
    -   Ersetzen Sie beide vorkommen, durch Folgendes:  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)  
  
    -   Kommentieren Sie die folgenden:  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority);  
        ```  
  
    -   Ersetzen Sie beide vorkommen, durch Folgendes:  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false);  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)  
  
    -   Jetzt kommentieren Sie alle Instanzen der folgenden:  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString() + "/OAuth");  
        ```  
  
    -   Ersetzen Sie alle Vorkommen, durch Folgendes:  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString());  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)  
  
## <a name="test-the-solution"></a>Testen der Lösung  
In diesem Abschnitt werden wir die Lösung vertraulicher Client testen.  Verwenden Sie das folgende Verfahren zum Testen der Projektmappe.  
  
#### <a name="testing-the-confidential-client-solution"></a>Testen der Lösung vertraulicher client  
  
1.  Klicken Sie am oberen Rand der Visual Studio stellen Sie sicher, dass Internet Explorer ausgewählt ist, und klicken Sie auf den grünen Pfeil.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)  
  
2.  Sobald die ASP.NET-Seite wird, klicken Sie auf **registrieren**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
3.  Geben Sie einen Benutzernamen und ein Kennwort ein, und klicken Sie dann auf **registrieren**.  Dadurch wird ein lokales Konto in der SQL-Datenbank erstellt.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
4.  Beachten Sie, dass sagt nun Hello Bsimon die ASP.NET-Website.  Klicken Sie auf **Profil**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)  
  
5.  Dadurch wird eine Seite ohne Informationen und besagt, dass wir hier klicken müssen, um die Anmeldung.  Klicken Sie auf **hier**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)  
  
6.  Sie werden nun aufgefordert werden, Anmelden mit AD FS.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)  
  
## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  

