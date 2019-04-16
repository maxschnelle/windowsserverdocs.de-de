---
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: Erstellen Sie eine AD FS 2016 vertraulicher OAuth-Clients mit Server-Seite-Anwendung
description: 
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 175c683f9097aeba4c1f06e8671183476c98aa3f
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016"></a>Erstellen Sie eine AD FS 2016 vertraulicher OAuth-Clients mit Server-Seite-Anwendung

>Gilt für: Windows Server 2016

Erstellen der ersten Oauth-Unterstützung in AD FS unter Windows Server2012 R2 AD FS 2016 bietet jetzt Unterstützung für Clients zur Verwaltung ihrer eigenen geheimen Schlüssel ein, z.B. eine App oder ein Dienst, der auf einem Webserver ausgeführt.  Diese Clients werden als vertraulich Clients bezeichnet.    
Im folgenden finden Sie ein Schema einer Web-Anwendung auf einem Webserver ausgeführt wird und fungiert als eine vertrauliche AD FS-Client:  
  
## <a name="pre-requisites"></a>Voraussetzungen  
Im folgenden finden eine Liste der erforderlichen Komponenten, die vor Abschluss dieses Dokuments erforderlich sind. In diesem Dokument wird davon ausgegangen, dass AD FS installiert ist und eine AD FS-Farm erstellt wurde.  
  
-   Ein Azure AD-Abonnement (eine kostenlose Testversion ist in Ordnung)  
  
-   GitHub-Client-Tools  
  
-   AD FS in Windows Server2016 Technical Preview 4 oder höher  
  
-   Visual Studio2013 oder höher.  
  
## <a name="create-an-application-group-in-ad-fs-2016"></a>Erstellen Sie eine Anwendungsgruppe in AD FS 2016  
Im folgende Abschnittwird beschrieben, konfigurieren Sie die Anwendungsgruppe in AD FS 2016.  
  
#### <a name="create-the-application-group"></a>Erstellen Sie die Anwendung-Gruppe  
  
1.  In AD FS-Verwaltung mit der rechten Maustaste auf die Gruppen aus, und wählen Sie **Anwendungsgruppe hinzufügen**.  
  
2.  Geben Sie auf den App-Assistenten für den Namen **ADFSOAUTHCC** und wählen Sie unter **eigenständige Anwendungen** wählen Sie die **Server-Anwendung oder Website** Vorlage.  Klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)  
  
3.  Kopieren der **Client-ID** Wert.  Es verwendet werden später als Wert für **Ida: ClientId** in der Anwendungen Web.config-Datei.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)  
  
4.  Geben Sie den folgenden für **Umleitungs-URI:** - **https://localhost:44323**.  Klicken Sie auf **hinzufügen**. Klicken Sie auf **Weiter**.  
  
5.  Auf der **Anwendungsanmeldeinformationen konfigurieren** Bildschirm, aktivieren Sie das Kontrollkästchen **generieren Sie einen gemeinsamen geheimen Schlüssel**, und kopieren Sie den geheimen Schlüssel.  Diese wird verwendet, später als Wert für **Ida: AppKey** in der Anwendungen Web.config-Datei.  Klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)  
  
6.  Auf der **Zusammenfassung** auf **Weiter**.  
  
7.  Auf der **Complete** auf **schließen**.  
  
8.  Nun auf die neue Anwendungsgruppe mit der rechten Maustaste und wählen Sie **Eigenschaften**.  
  
9. Auf **ADFSOAUTHCC Eigenschaften** klicken Sie auf **Anwendung hinzufügen**.  
  
10. Auf der **Hinzufügen einer neuen Anwendung mit Beispielanwendung** wählen **Web-API-**, und klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)  
  
11. Auf der **konfigurieren Sie Web-API-** Bildschirm, geben Sie Folgendes für **Bezeichner** - **https://contoso.com/WebApp**.  Klicken Sie auf **hinzufügen**. Klicken Sie auf **Weiter**.  Dieser Wert wird später verwendet werden, für die **Ida: GraphResourceId** in der Anwendungen Web.config-Datei.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)  
  
12. Auf der **Zugriffssteuerungsrichtlinie wählen** wählen **zulassen "Jeder"**, und klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)  
  
13. Auf der **Berechtigungen konfigurieren** Bildschirm, stellen Sie sicher, dass**User_impersonation** ausgewählt ist, und klicken Sie auf **Weiter**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)  
  
14. Auf der **Zusammenfassung** auf **Weiter**.  
  
15. Auf der **Complete** auf **schließen**.  
  
16. Auf der **ADFSOAUTHCC Eigenschaften** klicken Sie auf **OK**.  
  
## <a name="upgrade-the-database"></a>Aktualisieren Sie die Datenbank  
Visual Studio2015 verwendet wurde in dieser exemplarischen Vorgehensweise erstellen.   Um das Beispiel funktioniert mit Visual Studio2015 zu erhalten, müssen Sie die Datenbankdatei aktualisieren.  Gehen Sie hierzu folgendermaßen vor.  
  
In diesem Abschnittwird erläutert, wie Laden Sie das Beispiel-Web-API und aktualisieren Sie die Datenbank in Visual Studio2015.   Wir verwenden das Azure AD-Beispiel, das ist [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity).  
  
Zum Herunterladen der Beispiel-Projekt verwenden Sie Git Bash, und geben Sie Folgendes ein:  
  
```  
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git  
```  
  
![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)  
  
#### <a name="to-upgrade-the-database-file"></a>So aktualisieren Sie die Datenbankdatei  
  
1.  Öffnen Sie das Projekt in Visual Studio, ein Popup angezeigt wird, dass die App 2102 von SQL Server Express benötigt werden, oder Sie müssen die Datenbank aktualisieren.  Klicken Sie auf Ok.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)  
  
2.  Weiter Kompilieren der Anwendung durch die Auswahl der Build -> Projektmappe erstellen oben.  Dadurch werden alle NuGet-Pakete wiederhergestellt.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)  
  
3.  Wählen Sie nun oben, **Ansicht** -> **Server-Explorer**.  Sobald,, unter öffnet **Datenverbindungen**, mit der rechten Maustaste **DefaultConnection**, und wählen Sie **Verbindung ändern**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)  
  
4.  Auf **Verbindung ändern**Option **erweitert**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)  
  
5.  Auf Erweiterte Eigenschaften, suchen Sie nach Datenquelle und mithilfe der Dropdownliste aus **(LocalDb\v11.0)** auf **(LoaclDB) MSSQLLocalDB**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)  
  
6.  Klicken Sie auf Ok. Klicken Sie auf Ok.  Klicken Sie auf "Ja", um die Datenbank zu aktualisieren.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)  
  
7.  Nach Abschluss dieser, über auf der rechten Seite, kopieren Sie den Wert in das Feld neben **-Verbindungszeichenfolge.**  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)  
  
8.  Nun, öffnen Sie die Datei "Web.config", und Ersetzen Sie den Wert, der in ConnectionString mit dem Wert ist, die Sie über kopiert.  Speichern Sie die Datei "Web.config".  
  
    > [!NOTE]  
    > Die oben beschriebenen Schrittesind erforderlich, sodass wir neue ConnectionString abrufen können.  Andernfalls nach Ausführen des folgenden Update-Database wird Fehler ausgegeben.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)  
  
9. Wählen Sie oben auf der Visual Studio **Ansicht** -> **Weitere Windows** -> **Paket-Manager-Konsole**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)  
  
10. Geben Sie unten in der Paket-Manager-Konsole: `Enable-Migrations`und geben Sie dann.  
  
    > [!NOTE]  
    > Wenn Sie eine Fehlermeldung, die besagt, dass Enable-Migrations nicht als ein Cmdlet erkannt wird erhalten, geben Sie Install-Package EntityFramework, um die EntityFramework zu aktualisieren.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)  
  
11. Geben Sie unten in der Paket-Manager-Konsole: `Add-Migration <anynamehere>`und geben Sie dann.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)  
  
12. Geben Sie unten in der Paket-Manager-Konsole: `Update-Database`und geben Sie dann.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)  
  
## <a name="modify-the-webapi-in-visual-studio"></a>Ändern der WebApi in Visual Studio  
  
#### <a name="to-modify-the-sample-web-api"></a>So ändern Sie die Beispiel-Web-API  
  
1.  Öffnen Sie das Beispiel mit Visual Studio.  
  
2.  Öffnen Sie die Datei "Web.config".  Ändern Sie die folgenden Werte:  
  
    -   IDA: ClientId - Geben Sie den Wert von 3 oben.  
  
    -   IDA: AppKey - Geben Sie den Wert von 5 oben.  
  
    -   IDA: GraphResourceId - Geben Sie den Wert von 11 oben.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)  
  
3.  Öffnen Sie die Datei Startup.Auth.cs unter App_Start, und nehmen Sie die folgenden Änderungen:  
  
    -   Kommentieren Sie die folgenden Zeilen:  
  
        ```  
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];  
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];  
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)  
  
    -   Fügen Sie Folgendes an der Stelle hinzu:  
  
        ```  
        public static readonly string Authority = "https://<your_fsname>/adfs";  
        ```  
  
        Wobei < Your_fsname > mit dem DNS-Teil der Ihrem Verbunddienst-Url, z.B. adfs.contoso.com ersetzt  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_26.PNG)  
  
4.  Öffnen Sie die Datei UserProfileController.cs, und nehmen Sie die folgenden Änderungen:  
  
    -   Kommentieren Sie die folgenden:  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));  
        ```  
  
    -   Ersetzen Sie beide Vorgänge durch Folgendes:  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)  
  
    -   Kommentieren Sie die folgenden:  
  
        ```  
        //authContext = new AuthenticationContext(Startup.Authority);  
        ```  
  
    -   Ersetzen Sie beide Vorgänge durch Folgendes:  
  
        ```  
        authContext = new AuthenticationContext(Startup.Authority, false);  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)  
  
    -   Jetzt kommentieren Sie alle Instanzen der folgenden:  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString() + "/OAuth");  
        ```  
  
    -   Ersetzen Sie alle Vorkommen durch Folgendes:  
  
        ```  
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority.ToString());  
        ```  
  
        ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)  
  
## <a name="test-the-solution"></a>Testen Sie die Lösung  
In diesem Abschnittwerden wir die vertraulichen Clientprojektmappe zu testen.  Verwenden Sie das folgende Verfahren, um die Projektmappe zu testen.  
  
#### <a name="testing-the-confidential-client-solution"></a>Testen die vertrauliche Client-Lösung  
  
1.  Am Anfang von Visual Studio stellen Sie sicher, dass Internet Explorer aktiviert ist, und klicken Sie auf den grünen Pfeil.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)  
  
2.  Nachdem die Seite ASP.Net eingeblendet wird, klicken Sie auf **registrieren**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
3.  Geben Sie einen Benutzernamen und ein Kennwort ein, und klicken Sie dann auf **registrieren**.  Dadurch wird ein lokales Konto in der SQL-Datenbank erstellt.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)  
  
4.  Beachten Sie besagt nun die Website ASP.NET Hello Bsimon!.  Klicken Sie auf **Profil**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)  
  
5.  Dadurch wird eine Seite ohne Informationen und besagt, dass wir hier klicken müssen, um anmelden.  Klicken Sie auf **hier**.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)  
  
6.  Sie werden jetzt AD FS Anmelden aufgefordert.  
  
    ![AD FS Oauth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)  
  
## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  

