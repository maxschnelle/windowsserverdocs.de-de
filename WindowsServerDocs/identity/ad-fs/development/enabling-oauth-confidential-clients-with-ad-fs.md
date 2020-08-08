---
ms.assetid: 5a64e790-6725-4099-aa08-8067d57c3168
title: Erstellen einer serverseitigen Anwendung mithilfe von vertraulichen OAuth-Clients mit AD FS 2016 oder höher
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: 7abae35671e29b5229c5c1bf5a36ee865100bd88
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943039"
---
# <a name="build-a-server-side-application-using-oauth-confidential-clients-with-ad-fs-2016-or-later"></a>Erstellen einer serverseitigen Anwendung mithilfe von vertraulichen OAuth-Clients mit AD FS 2016 oder höher


AD FS 2016 und spätere Versionen bieten Unterstützung für Clients, die ihren eigenen geheimen Schlüssel verwalten können, z. b. eine APP oder ein Dienst, der auf einem Webserver ausgeführt wird.  Diese Clients werden als vertrauliche Clients bezeichnet.
Im folgenden finden Sie eine Schemas für eine Webanwendung, die auf einem Webserver ausgeführt wird und als vertraulicher Client für die AD FS dient:

## <a name="pre-requisites"></a>Voraussetzungen
Im folgenden finden Sie eine Liste der Voraussetzungen, die vor der Fertigstellung dieses Dokuments erforderlich sind. In diesem Dokument wird davon ausgegangen, dass AD FS installiert wurde.

-   GitHub-Client Tools

-   AD FS in Windows Server 2016 TP4 oder höher

-   Visual Studio 2013 oder höher

## <a name="create-an-application-group-in-ad-fs-2016-or-later"></a>Erstellen einer Anwendungs Gruppe in AD FS 2016 oder höher
Im folgenden Abschnitt wird beschrieben, wie Sie die Anwendungs Gruppe in AD FS 2016 oder höher konfigurieren.

#### <a name="create-the-application-group"></a>Erstellen der Anwendungs Gruppe

1.  Klicken Sie in AD FS Verwaltung mit der rechten Maustaste auf Anwendungs Gruppen, und wählen Sie **Anwendungs Gruppe hinzufügen**aus.

2.  Wählen Sie im Anwendungs Gruppen-Assistenten für **Name** den Namen **ADF-autoricc** und unter **Client-/Serveranwendungen** die Server Anwendung aus, die auf **eine Web-API-Vorlage zugreift** .  Klicken Sie auf **Weiter**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_2.PNG)

3.  Kopieren Sie den Wert für den **Client Bezeichner** .  Sie wird später als Wert für " **Ida: ClientID** " in der Anwendung web.config Datei verwendet.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_3.PNG)

4.  Geben Sie für **Umleitungs-URI Folgendes ein:**  -  **https://localhost:44323** .  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.

5.  Aktivieren Sie auf dem Bildschirm **Anwendungs Anmelde Informationen konfigurieren** die Option **einen gemeinsamen geheimen Schlüssel generieren** , und kopieren Sie den geheimen Schlüssel.  Diese wird später als Wert für " **Ida: clientsecret** " in der Anwendungs web.config Datei verwendet.  Klicken Sie auf **Weiter**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_4.PNG)

6. Geben Sie auf dem Bildschirm **Web-API konfigurieren** den folgenden Wert für **Bezeichner**ein  -  **https://contoso.com/WebApp** .  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  Dieser Wert wird später für " **Ida: graphresourceid** " in der Anwendungs web.config Datei verwendet.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_9.PNG)

7. Wählen Sie auf der Seite **Access Control Richtlinie anwenden** die Option **Alle zulassen** aus, und klicken Sie auf **weiter**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_7.PNG)

8. Vergewissern Sie sich, dass auf dem Bildschirm **Anwendungs Berechtigungen konfigurieren** die Option **OpenID** und **user_impersonation** ausgewählt sind, und klicken Sie auf **weiter**.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_8.PNG)

9. Klicken Sie auf dem Bildschirm **Zusammenfassung** auf **weiter**.

10. Klicken Sie im Bildschirm **Fertig** stellen auf **Schließen**.

## <a name="upgrade-the-database"></a>Aktualisieren der Datenbank
Visual Studio 2015 wurde zum Erstellen dieser exemplarischen Vorgehensweise verwendet.   Um das Beispiel mit Visual Studio 2015 zu erhalten, müssen Sie die Datenbankdatei aktualisieren.  Führen Sie dazu die nachfolgend aufgeführten Schritte aus.

In diesem Abschnitt wird erläutert, wie Sie die Beispiel-Web-API herunterladen und die Datenbank in Visual Studio 2015 aktualisieren.   Wir verwenden das [hier](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity)Azure AD Beispiel.

Verwenden Sie zum Herunterladen des Beispielprojekts git bash, und geben Sie Folgendes ein:

```
git clone https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity.git
```

![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_10.PNG)

#### <a name="to-upgrade-the-database-file"></a>So aktualisieren Sie die Datenbankdatei

1.  Öffnen Sie das Projekt in Visual Studio. es wird ein Popup Fenster angezeigt, in dem Sie darüber informiert werden, dass die APP SQL Server 2012 Express erfordert oder Sie ein Upgrade der Datenbank durchführen müssen.  Klicken Sie auf "OK".

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_12.PNG)

2.  Kompilieren Sie die Anwendung im nächsten Schritt, indem Sie oben > Projekt Mappe erstellen auswählen.  Dadurch werden alle nuget-Pakete wieder hergestellt.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_13.PNG)

3.  Wählen Sie oben im oberen Bereich **View**die Option  ->  **Server-Explorer**anzeigen aus.  Klicken Sie anschließend unter **Datenverbindungen**mit der rechten Maustaste auf **DefaultConnection** , und wählen Sie **Verbindung ändern**aus.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_14.PNG)

4.  Wählen Sie unter **Verbindung ändern**unter **Name der Datenbankdatei (neu oder vorhanden)** die Option **Durchsuchen** aus, und geben Sie **path\dateiname.mdf**an. Klicken Sie im Dialogfeld auf **Ja** .

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_6.PNG)

5.  Wählen Sie unter **Verbindung ändern**die Option **erweitert**aus.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_15.PNG)

6.  Suchen Sie in den erweiterten Eigenschaften nach Datenquelle, und verwenden Sie die Dropdown-Datei, um Sie von **(localdb\v11.0)** in **(localdb) \mssqllocaldb**zu ändern.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_16.PNG)

7.  Klicken Sie auf "OK". Klicken Sie auf "OK".  Klicken Sie auf Ja, um die Datenbank zu aktualisieren.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_17.PNG)

8.  Wenn dies abgeschlossen ist, kopieren Sie auf der rechten Seite den Wert in das Feld neben **Verbindungs Zeichenfolge.**

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_18.PNG)

9.  Öffnen Sie nun die Datei Web.config, und ersetzen Sie den Wert in ConnectionString durch den Wert, den Sie zuvor kopiert haben.  Speichern Sie die Datei „Web.config“.

    > [!NOTE]
    > Die obigen Schritte sind erforderlich, damit wir die neue ConnectionString-Eigenschaft erhalten können.  Andernfalls wird beim Ausführen von "Update-Database" eine Fehlermeldung ausgegeben.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_19.PNG)

10. Wählen Sie oben in Visual Studio die Option **View**  ->  **Weitere Windows**-  ->  **Paket-Manager-Konsole**anzeigen aus.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_20.PNG)

11. Geben Sie im unteren Bereich in der Paket-Manager-Konsole Folgendes ein, `Enable-Migrations` und drücken Sie die EINGABETASTE.

    > [!NOTE]
    > Wenn Sie eine Fehlermeldung erhalten, die besagt, dass enable-Migrationen nicht als Cmdlet erkannt werden, geben Sie Install-package EntityFramework ein, um das EntityFramework zu aktualisieren.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_21.PNG)

12. Geben Sie im unteren Bereich in der Paket-Manager-Konsole Folgendes ein, `Add-Migration <anynamehere>` und drücken Sie die EINGABETASTE.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_22.PNG)

13. Geben Sie im unteren Bereich in der Paket-Manager-Konsole Folgendes ein, `Update-Database` und drücken Sie die EINGABETASTE.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_23.PNG)

## <a name="modify-the-webapi-in-visual-studio"></a>Ändern der WebAPI in Visual Studio

#### <a name="to-modify-the-sample-web-api"></a>So ändern Sie die Beispiel-Web-API

1.  Öffnen Sie das Beispiel mithilfe von Visual Studio.

2.  Öffnen Sie die Datei web.config.  Ändern Sie die folgenden Werte:

    -   Ida: ClientID: Geben Sie den Wert aus #3 im obigen Abschnitt Erstellen der Anwendungs Gruppe ein.

    -   Ida: clientsecret: Geben Sie den Wert aus #5 im obigen Abschnitt Erstellen der Anwendungs Gruppe ein.

    -   Ida: graphresourceid: Geben Sie den Wert aus #6 im obigen Abschnitt Erstellen der Anwendungs Gruppe ein.

    ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_24.PNG)

3.  Öffnen Sie die Datei Startup.auth.cs unter App_Start, und nehmen Sie die folgenden Änderungen vor:

    -   Kommentieren Sie die folgenden Zeilen:

        ```
        //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
        //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        //public static readonly string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
        ```

    -   Fügen Sie Folgendes an der Stelle ein:

        ```
        public static readonly string Authority = "https://<your_fsname>/adfs";
        ```

        Dabei wird <your_fsname> durch den DNS-Teil ihrer Verbund Dienst-URL ersetzt, z. b. ADFS.contoso.com

        ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_25.PNG)

4.  Öffnen Sie die Datei UserProfileController.cs, und nehmen Sie die folgenden Änderungen vor:

    -   Kommentieren Sie Folgendes aus:

        ```
        //authContext = new AuthenticationContext(Startup.Authority, new TokenDbCache(userObjectID));
        ```

    -   Ersetzen Sie beide Vorkommen durch Folgendes:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false, new TokenDbCache(userObjectID));
        ```

        ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_27.PNG)

    -   Kommentieren Sie Folgendes aus:

        ```
        //authContext = new AuthenticationContext(Startup.Authority);
        ```

    -   Ersetzen Sie beide Vorkommen durch Folgendes:

        ```
        authContext = new AuthenticationContext(Startup.Authority, false);
        ```

        ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_28.PNG)

    -   Kommentieren Sie nun alle Instanzen der folgenden Schritte aus:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString() + "/OAuth");
        ```

    -   Ersetzen Sie alle Vorkommen durch Folgendes:

        ```
        Uri redirectUri = new Uri(Request.Url.GetLeftPart(UriPartial.Authority).ToString());
        ```

        ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_34.PNG)

## <a name="test-the-solution"></a>Testen der Projektmappe
In diesem Abschnitt wird die vertrauliche Client Lösung getestet.  Verwenden Sie das folgende Verfahren, um die Lösung zu testen.

#### <a name="testing-the-confidential-client-solution"></a>Testen der Lösung für vertrauliche Clients

1. Stellen Sie oben in Visual Studio sicher, dass Internet Explorer ausgewählt ist, und klicken Sie auf den grünen Pfeil.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_36.png)

2. Nachdem die Seite ASP.net angezeigt wird, klicken Sie oben rechts auf der Seite auf **registrieren** .  Geben Sie einen Benutzernamen und ein Kennwort ein, **und klicken Sie** dann auf  Dadurch wird ein lokales Konto in der SQL-Datenbank erstellt.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_31.PNG)

3. Beachten Sie, dass die ASP.NET-Website "Hello!" lautet abby@contoso.com .  Klicken Sie auf **Profile**.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_32.PNG)

4. Dadurch wird eine Seite ohne Informationen angezeigt, und Sie müssen hier klicken, um sich anzumelden.  Klicken Sie **hier**.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_33.PNG)

5. Sie werden nun aufgefordert, sich bei AD FS anzumelden.

   ![AD FS OAuth](media/Enabling-Oauth-Confidential-Clients-with-AD-FS-2016/AD_FS_Confidential_35.PNG)

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)
