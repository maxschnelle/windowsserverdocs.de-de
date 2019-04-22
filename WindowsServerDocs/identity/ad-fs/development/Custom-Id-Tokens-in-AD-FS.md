---
title: Anpassen von Ansprüchen in ID-Token ausgegeben werden, bei Verwendung von OpenID Connect oder OAuth mit AD FS 2016
description: Eine technische Übersicht über die benutzerdefinierte Id-token-Conecpts in AD FS 2016
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 8c8e14f22a4bca5b6d32e841814a58a4b4ddca01
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820641"
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016"></a>Anpassen von Ansprüchen in ID-Token ausgegeben werden, bei Verwendung von OpenID Connect oder OAuth mit AD FS 2016

## <a name="overview"></a>Übersicht
Der Artikel [hier](enabling-openId-connect-with-ad-fs.md) wird gezeigt, wie Sie eine app erstellen, die AD FS verwendet wird, für die OpenID Connect, anmelden. Standardmäßig gibt es gibt jedoch nur einen festen Satz von Ansprüchen in ID-Token verfügbar. AD FS 2016 wurde die Möglichkeit, die "id_token" in OpenID Connect-Szenarien anzupassen.

## <a name="when-are-custom-id-token-used"></a>Wenn benutzerdefinierte ID sind, das verwendet wird?
In bestimmten Szenarien ist es möglich, dass die Clientanwendung, die sie zugreifen möchten, ist eine Ressource nicht verfügt. Aus diesem Grund ist nicht wirklich ein Zugriffstoken erforderlich. In solchen Fällen benötigt die Clientanwendung im Wesentlichen nur einen ID-token aber einige zusätzliche Ansprüche aus, um die Funktionalität zu unterstützen.

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>Was sind die Einschränkungen für das Abrufen von benutzerdefinierter Ansprüchen in ID-token?

### <a name="scenario-1"></a>Szenario 1

![Einschränken](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  Response_mode wird als Form_post festgelegt.
2.  Nur öffentliche Clients können benutzerdefinierte Ansprüche in ID token abrufen
3.  Relying Party Identifier sollte Client-ID identisch sein.

### <a name="scenario-2"></a>Szenario 2

![Einschränken](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

Mit [KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) auf Ihren AD FS-Servern installiert
1.  Response_mode wird als Form_post festgelegt.
2.  Weisen Sie Bereich Allatclaims an den Client – die RP-Paar ein.
Sie können den Bereich zuweisen, mit dem Cmdlet Grant-ADFSApplicationPermission, wie im folgenden Beispiel dargestellt:

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-an-oauth-application-to-handle-custom-claims-in-id-token"></a>Erstellen einer OAuth-Anwendung zur Handhabung von benutzerdefinierter Ansprüchen in ID-token
Verwenden Sie den Artikel [hier](Enabling-OpenId-Connect-with-AD-FS-2016.md) eine app für die Anwendung zu erstellen, verwendet AD FS für die OpenID Connect anmelden. Klicken Sie dann die Schritte unten aus, um die Anwendung für den Empfang von ID-Token mit benutzerdefinierter Ansprüche in AD FS zu konfigurieren.

### <a name="create-the-application-group-in-ad-fs-2016"></a>Erstellen Sie die Anwendungsgruppe in AD FS 2016

1.  Erstellen Sie eine Anwendungsgruppe, die basierend auf die neue Vorlage für die unten gezeigte CustomTokenClient aufgerufen.

![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

2. Diese Vorlage erstellt einen vertraulichen Client. Beachten Sie den Bezeichner, und geben Sie den URI zurück, als die SSL-URL des Visual Studio-Projekts.

![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

3.  Wählen Sie im nächsten Schritt **generieren Sie einen gemeinsamen geheimen Schlüssel** Client-Anmeldeinformationen erstellen, und kopieren Sie die Anmeldeinformationen des Clients generiert.

![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

4. Klicken Sie auf **Weiter** , und fahren fort, um den Assistenten abzuschließen.

![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

### <a name="create-the-relying-party"></a>Erstellen der vertrauenden Seite
Zum Hinzufügen von benutzerdefinierter Ansprüchen in ID müssen token, um eine vertrauende Seite zu erstellen, deren Ansprüche im ID-Token hinzugefügt werden. Mit der Partei Vertrauensstellung der vertrauenden Seite hinzufügen-Assistenten können Sie um eine neue relying Party zu erstellen, wie unten gezeigt:
 
![Vertrauende Seite](media/Custom-Id-Tokens-in-AD-FS/rpsnap1.png)

Nachdem die vertrauende Seite erstellt wird, klicken Sie mit der rechten Maustaste auf die Partei der vertrauenden Seite, und wählen **bearbeiten Anspruch Ausstellungsrichtlinie** anspruchsausgaberegeln hinzufügen. Fügen Sie die erforderlichen benutzerdefinierten Ansprüche für ID-Token an, wie unten dargestellt:

![Vertrauende Seite](media/Custom-Id-Tokens-in-AD-FS/rpsnap2.png)

### <a name="assign-allatclaims-scope-to-the-pair-of-client-and-relying-party"></a>Das Paar aus Client und der vertrauenden Seite "Allatclaims" Bereich zuweisen
Weisen Sie den neuen Allatclaims Bereich wie im folgenden Beispiel mithilfe von PowerShell für AD FS-Server (ändern Sie die Client-ID und den Server:

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "5db77ce4-cedf-4319-85f7-cc230b7022e0" -ServerRoleIdentifier "https://customidrp1/" -ScopeNames "allatclaims","openid"
```

>[!NOTE]
>Ändern Sie die ClientRoleIdentifier und ServerRoleIdentifier gemäß den Einstellungen Ihrer Anwendung

## <a name="test-the-custom-claims-in-id-token"></a>Testen Sie die benutzerdefinierten Ansprüche im ID-token

Klicken Sie dann sehen mit demselben Bit des Codes, die Sie immer verwendet haben, auf die Ansprüche, die zusätzliche Ansprüche Sie, die Teil des ID-Tokens werden sollen.
Beispielsweise in einer .NET MVC-Beispiel-app öffnen Sie eines der Controllerdateien, und geben Sie Code wie den folgenden:


``` code
    [Authorize]
    public ActionResult About()
    {

        ClaimsPrincipal cp = ClaimsPrincipal.Current;

        string userName = cp.FindFirst(ClaimTypes.GivenName).Value;
        ViewBag.Message = String.Format("Hello {0}!", userName);
        return View();

    }

```

>[!NOTE]
>Bedenken Sie bitte, dass der Ressourcenparameter in der Oauth2-Anforderung erforderlich ist.
>
>Ungültige Beispiel:
>
>**HTTPS&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token & Scope = Openid & umleitungs-URI = Https&#58;//myportal/auth & Nonce = b3ceb943fc756d927777 & Client_id = 6db3ec2a-075a - 4c 72-9b22-ca7ab60cb4e7 & Status = 42c2c156aef47e8d0870 & Resource = 6db3ec2a-075a - 4c 72-9b22-ca7ab60cb4e7**
>
>Gutes Beispiel:
>
>**HTTPS&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token & Scope = Openid & umleitungs-URI = Https&#58;//myportal/auth & Nonce = b3ceb943fc756d927777 & Client_id = 6db3ec2a-075a - 4c 72-9b22-ca7ab60cb4e7 & Status = 42c2c156aef47e8d0870 & Resource = Https&#58;//customidrp1/ & Response_mode = Form_post**
>
>Wenn der Ressourcenparameter nicht in der Anforderung ist erhalten Sie möglicherweise einen Fehler oder ein Token ohne jede benutzerdefinierte Ansprüche.

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
