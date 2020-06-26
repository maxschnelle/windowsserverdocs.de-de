---
title: Anpassen von Anspruchs, die in id_token ausgegeben werden sollen, wenn OpenID Connect oder OAuth mit AD FS 2016 oder höher verwendet wird
description: Eine technische Übersicht über die benutzerdefinierten ID-tokenkonzepte in AD FS 2016 oder höher
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 04/29/2020
ms.topic: article
ms.prod: windows-server
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 9ffc8351c2c5033346f04e3cd4dc6f8ba4914149
ms.sourcegitcommit: fea590c092d7abcb55be2b424458faa413795f5c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/25/2020
ms.locfileid: "85372207"
---
# <a name="customize-claims-to-be-emitted-in-id_token-when-using-openid-connect-or-oauth-with-ad-fs-2016-or-later"></a>Anpassen von Anspruchs, die in id_token ausgegeben werden sollen, wenn OpenID Connect oder OAuth mit AD FS 2016 oder höher verwendet wird

## <a name="overview"></a>Übersicht

In diesem [Artikel wird](native-client-with-ad-fs.md) gezeigt, wie Sie eine APP erstellen, die AD FS für die OpenID Connect-Anmeldung verwendet. Standardmäßig gibt es jedoch nur einen festgelegten Satz von Ansprüchen, der in der id_token verfügbar ist. AD FS 2016 und spätere Versionen haben die Möglichkeit, die id_token in OpenID Connect-Szenarios anzupassen.

## <a name="when-are-custom-id-tokens-used"></a>Wann werden benutzerdefinierte ID-Token verwendet?

In bestimmten Szenarien ist es möglich, dass die Client Anwendung nicht über eine Ressource verfügt, auf die zugegriffen werden soll. Daher ist kein Zugriffs Token erforderlich. In solchen Fällen benötigt die Client Anwendung im Grunde nur ein ID-Token, aber mit einigen zusätzlichen Ansprüchen, um die Funktionalität zu unterstützen.

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>Welche Einschränkungen gelten für das erhalten von benutzerdefinierten Ansprüchen in ID-Token?

### <a name="scenario-1"></a>Szenario 1

![Einschränken](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1. `response_mode`ist festgelegt als`form_post`
2. Nur öffentliche Clients können benutzerdefinierte Ansprüche im ID-Token erhalten.
3. Der Bezeichner der vertrauenden Seite (Web-API-Bezeichner) muss mit dem Client Bezeichner identisch sein

### <a name="scenario-2"></a>Szenario 2

![Einschränken](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

Das Sicherheitsupdate [KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) oder höher ist auf Ihren AD FS-Servern installiert.
1. `response_mode`wird als form_post festgelegt
2. Sowohl öffentliche als auch vertrauliche Clients können benutzerdefinierte Ansprüche im ID-Token erhalten.
3. Weisen `allatclaims` Sie dem Client – RP-paar den Gültigkeitsbereich zu.

Sie können den Bereich mithilfe des- `Grant-ADFSApplicationPermission` Cmdlets zuweisen, wie im folgenden Beispiel gezeigt:

```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-and-configuring-an-oauth-application-to-handle-custom-claims-in-id-token"></a>Erstellen und Konfigurieren einer OAuth-Anwendung zum Verarbeiten von benutzerdefinierten Ansprüchen in ID-Token

Führen Sie die folgenden Schritte aus, um die Anwendung in AD FS zum Empfangen des ID-Tokens mit benutzerdefinierten Ansprüchen zu erstellen und zu konfigurieren.

### <a name="create-and-configure-an-application-group-in-ad-fs-2016-or-later"></a>Erstellen und Konfigurieren einer Anwendungs Gruppe in AD FS 2016 oder höher

1. Klicken Sie in AD FS Verwaltung mit der rechten Maustaste auf Anwendungs Gruppen, und wählen Sie **Anwendungs Gruppe hinzufügen**aus.
2. Geben Sie im Anwendungs Gruppen-Assistenten für den Namen **ADF-so** ein, und wählen Sie unter Client-Server Anwendungen die native Anwendung aus, die auf **eine Webanwendungsvorlage zugreift** . Klicken Sie auf **Weiter**.

   ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

3. Kopieren Sie den Wert für den **Client Bezeichner** .  Sie wird später als Wert für "Ida: ClientID" in der Anwendung web.config Datei verwendet.
4. Geben Sie für **Umleitungs-URI Folgendes ein:**  -  **https://localhost:44320/** .  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.

   ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

5. Geben Sie auf dem Bildschirm **Web-API konfigurieren** den folgenden Wert für **Bezeichner**ein  -  **https://contoso.com/WebApp** .  Klicken Sie auf **Hinzufügen**. Klicken Sie auf **Weiter**.  Dieser Wert wird später für " **Ida: ResourceId** " in der Anwendungs web.config Datei verwendet.

   ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

6. Wählen Sie auf dem Bildschirm **Wählen Sie Access Control Richtlinie** die Option **Alle zulassen** aus, **und klicken Sie**

   ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

7. Vergewissern Sie sich, dass auf dem Bildschirm **Anwendungs Berechtigungen konfigurieren** die Option **OpenID** und **allatclaims** ausgewählt sind, und klicken Sie auf **weiter**.

   ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap5.PNG)

8. Klicken Sie auf dem Bildschirm **Zusammenfassung** auf **weiter**.

   ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap6.PNG)

9. Klicken Sie im Bildschirm **Fertig** stellen auf **Schließen**.
10. Klicken Sie in AD FS Verwaltung auf Anwendungs Gruppen, um eine Liste aller Anwendungs Gruppen zu erhalten. Klicken Sie mit der rechten Maustaste auf **ADF** , und wählen Sie **Eigenschaften**aus. Wählen Sie **ADF-so-Web-API** aus, und klicken Sie auf **Bearbeiten...**

    ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap7.PNG)

11. Wählen Sie auf der **Seite ADF-so-Web-API-Eigenschaften** die Registerkarte Ausstellungs **Transformationsregeln** aus, und klicken Sie auf **Regel hinzufügen.**

    ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap8.PNG)

12. Wählen **Sie auf** der Seite **Assistent zum Hinzufügen von Transformations Anspruchs Regeln** die Option **Ansprüche mithilfe einer benutzerdefinierten Regel senden** aus der Dropdown-Dropdown-Dropdown

    ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap9.PNG)

13. Geben Sie im **Assistenten zum Hinzufügen von Transformations Anspruchs Regeln** im Fenster " **Anspruchs Regel Name** " den Namen " **forcustomittel Token** " und in **benutzerdefinierte Regel**die folgende Anspruchs Regel ein. Klicken Sie auf **Fertig stellen**.

    ```
    x:[]
    => issue(claim=x);
    ```

    ![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap10.PNG)

    > [!NOTE]
    > Sie können auch PowerShell verwenden, um die `allatclaims` Bereiche und zuzuweisen `openid` .

    ``` powershell
    Grant-AdfsApplicationPermission -ClientRoleIdentifier "[Client ID from #3 above]" -ServerRoleIdentifier "[Identifier from #5 above]" -ScopeNames "allatclaims","openid"
    ```

### <a name="download-and-modify-the-sample-application-to-emit-custom-claims-in-id_token"></a>Herunterladen und Ändern der Beispielanwendung zum Ausgeben von benutzerdefinierten Ansprüchen in id_token

In diesem Abschnitt wird erläutert, wie Sie die Beispiel-Web-App herunterladen und in Visual Studio ändern. Wir verwenden das Azure AD Beispiel, das Sie [hier](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/1-WebApp-OIDC)finden.

Verwenden Sie zum Herunterladen des Beispielprojekts git bash, und geben Sie Folgendes ein:

```
git clone https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/1-WebApp-OIDC
```

![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_1.PNG)

#### <a name="to-modify-the-app"></a>So ändern Sie die APP

1. Öffnen Sie das Beispiel mithilfe von Visual Studio.
2. Erstellen Sie die APP neu, sodass alle fehlenden nugets wieder hergestellt werden.
3. Öffnen Sie die Datei web.config.  Ändern Sie die folgenden Werte so, dass Sie wie folgt aussehen:

   ```xml
   <add key="ida:ClientId" value="[Replace this Client Id from #3 above under section Create and configure an Application Group in AD FS 2016 or later]" />
   <add key="ida:ResourceID" value="[Replace this with the Web API Identifier from #5 above]"  />
   <add key="ida:ADFSDiscoveryDoc" value="https://[Your ADFS hostname]/adfs/.well-known/openid-configuration" />
   <!--<add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" />
   <add key="ida:AADInstance" value="https://login.microsoftonline.com/{0}" />-->
   <add key="ida:PostLogoutRedirectUri" value="[Replace this with the Redirect URI from #4 above]" />
   ```

   ![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_2.png)

4. Öffnen Sie die Datei Startup.auth.cs, und nehmen Sie die folgenden Änderungen vor:

   - Optimieren Sie die Initialisierungs Logik der OpenID Connect-Middleware mit den folgenden Änderungen:

      ```cs
      private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
      //private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
      //private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
      private static string metadataAddress = ConfigurationManager.AppSettings["ida:ADFSDiscoveryDoc"];
      private static string resourceId = ConfigurationManager.AppSettings["ida:ResourceID"];
      private static string postLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"];
      ```

   - Kommentieren Sie Folgendes aus:

      ```cs
      //string Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);
      ```

      ![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_3.png)

   - Ändern Sie die Optionen für die OpenID Connect-Middleware wie folgt:

      ```cs
      app.UseOpenIdConnectAuthentication(
          new OpenIdConnectAuthenticationOptions
          {
              ClientId = clientId,
              //Authority = authority,
              Resource = resourceId,
              MetadataAddress = metadataAddress,
              PostLogoutRedirectUri = postLogoutRedirectUri,
              RedirectUri = postLogoutRedirectUri
      ```

      ![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_4.png)

5. Öffnen Sie die Datei HomeController.cs, und nehmen Sie die folgenden Änderungen vor:

   - Fügen Sie Folgendes hinzu:

      ```cs
      using System.Security.Claims;
      ```

   - Aktualisieren Sie die- `About()` Methode wie unten dargestellt:

      ```cs
      [Authorize]
      public ActionResult About()
      {
          ClaimsPrincipal cp = ClaimsPrincipal.Current;
          string userName = cp.FindFirst(ClaimTypes.WindowsAccountName).Value;
          ViewBag.Message = String.Format("Hello {0}!", userName);
          return View();
      }
      ```

      ![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_5.png)

### <a name="test-the-custom-claims-in-id-token"></a>Testen der benutzerdefinierten Ansprüche im ID-Token

Nachdem die obigen Änderungen vorgenommen wurden, drücken Sie F5. Dadurch wird die Beispielseite angezeigt. Klicken Sie auf anmelden.

![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_6.PNG)

Sie werden auf die AD FS Anmeldeseite umgeleitet. Melden Sie sich bei Azure an.

![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_7.PNG)

Wenn dies erfolgreich ist, sollten Sie sehen, dass Sie jetzt angemeldet sind.

![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_8.png)

Klicken Sie auf den Link About . Sie sehen "Hello [username]", das aus dem username-Anspruch im ID-Token abgerufen wird.

![OpenID AD FS](media/Custom-Id-Tokens-in-AD-FS/AD_FS_OpenID_9.png)

## <a name="next-steps"></a>Nächste Schritte

[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)
