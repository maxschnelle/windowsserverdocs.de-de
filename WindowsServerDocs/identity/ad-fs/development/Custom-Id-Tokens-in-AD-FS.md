---
title: "Anpassen der Ansprüche in ID_Token ausgegeben werden, bei Verwendung von Verbindung OpenID oder OAuth mit AD FS 2016"
description: "Eine technische Übersicht über die benutzerdefinierten ID Token Conecpts in AD FS 2016"
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: c17d50bb6d90726eafc3e585f16a7a8189a68392
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016"></a>Anpassen der Ansprüche in ID_Token ausgegeben werden, bei Verwendung von Verbindung OpenID oder OAuth mit AD FS 2016

## <a name="overview"></a>(Übersicht)
Artikel [hier](enabling-openId-connect-with-ad-fs.md) zeigt, wie Sie eine App erstellen, die AD FS verwendet für OpenID Connect anzumelden. Standardmäßig stehen jedoch nur einen festen Satz von Ansprüchen, die in der ID_Token verfügbar. AD FS 2016 hat die Möglichkeit, die ID_Token in OpenID Connect Szenarien anpassen.

## <a name="when-are-custom-id-token-used"></a>Wenn benutzerdefinierte ID sind Token verwendet?
In bestimmten Szenarien ist es möglich, dass die Client-Anwendung nicht über eine Ressource verfügt, die er zugreifen möchte. Aus diesem Grund benötigt nicht wirklich ein Zugriffstoken. In diesem Fall benötigt die Clientanwendung im Grunde nur eine ID Token ohne einige zusätzliche Ansprüche an die Funktion zu unterstützen.

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>Was sind die Einschränkungen zum Abrufen von benutzerdefinierte Ansprüche in ID Token?

### <a name="scenario-1"></a>Szenario 1

![Einschränken](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  Response_mode wird als Form_post festgelegt.
2.  Nur öffentliche Clients können benutzerdefinierte Ansprüche in ID Token abrufen
3.  Bezeichner der vertrauenden Seite sollte Client-ID identisch sein.

### <a name="scenario-2"></a>Szenario 2

![Einschränken](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

Mit [KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) auf Ihre AD FS-Server installiert
1.  Response_mode wird als Form_post festgelegt.
2.  Der Client – RP-Paar Bereich Allatclaims zuweisen.
Sie können den Bereich zuweisen, mit dem Grant-ADFSApplicationPermission-Cmdlet, wie im folgenden Beispiel dargestellt:

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-an-oauth-application-to-handle-custom-claims-in-id-token"></a>Erstellen einer Anwendung OAuth, benutzerdefinierte Ansprüche in Tokens ID behandeln
Verwenden Sie den Artikel [hier](Enabling-OpenId-Connect-with-AD-FS-2016.md) eine Anwendung-App erstellen, verwendet AD FS für OpenID Connect anzumelden. Befolgen Sie die folgenden Schritteaus, um die Anwendung für den Empfang von Token-ID mit benutzerdefinierte Ansprüche in AD FS zu konfigurieren.

### <a name="create-the-application-group-in-ad-fs-2016"></a>Erstellen Sie die Anwendung Gruppe in AD FS 2016

1.  Erstellen Sie eine Anwendungsgruppe basierend auf der neuen Vorlage, die unten angegebenen CustomTokenClient aufgerufen.

![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

2. Diese Vorlage erstellt einen vertraulichen Client. Beachten Sie die ID, und geben Sie den Rückgabewert URI als SSL-URL des VS-Projekts.

![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

3.  Wählen Sie im nächsten Schritt **generieren Sie einen gemeinsamen geheimen Schlüssel** Client Anmeldeinformationen erstellen, und kopieren Sie die Anmeldeinformationen des Clients generiert.

![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

4. Klicken Sie auf **Weiter** und fahren Sie mit den Assistenten abzuschließen.

![Client](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

### <a name="create-the-relying-party"></a>Erstellen Sie die vertrauende Seite
Um benutzerdefinierte Ansprüche in ID hinzufügen müssen Zugriffstoken indem Sie, eine RP erstellen, deren Ansprüche in das ID-Token hinzugefügt werden. Verwenden Sie den Assistenten Party Vertrauensstellung der vertrauenden Seite hinzufügen, um eine neue vertrauende Seite zu erstellen, wie unten dargestellt:
 
![Vertrauende Seite](media/Custom-Id-Tokens-in-AD-FS/rpsnap1.png)

Nachdem die vertrauende Seite erstellt wird, klicken Sie mit der rechten Maustaste auf die relying Party, und wählen Sie **bearbeiten Anspruch Ausstellungsrichtlinie** Ausstellung Anspruchsregeln hinzu. Fügen Sie die erforderlichen benutzerdefinierten Ansprüche für Token-ID, wie unten gezeigt:

![Vertrauende Seite](media/Custom-Id-Tokens-in-AD-FS/rpsnap2.png)

### <a name="assign-allatclaims-scope-to-the-pair-of-client-and-relying-party"></a>Weisen Sie das Paar des Clients und vertrauenden "Allatclaims"-Bereich
Weisen Sie den neuen Allatclaims Bereich wie im folgenden Beispiel mithilfe von PowerShell auf AD FS-Server (ändern Sie die ClientID und Server:

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "5db77ce4-cedf-4319-85f7-cc230b7022e0" -ServerRoleIdentifier "https://customidrp1/" -ScopeNames "allatclaims","openid"
```

>[!NOTE]
>Ändern Sie die ClientRoleIdentifier und ServerRoleIdentifier gemäß Ihrer App-Einstellungen

## <a name="test-the-custom-claims-in-id-token"></a>Testen Sie die benutzerdefinierte Ansprüche in Token-ID

Klicken Sie dann sehen mit der gleichen Bit der Code, den Sie immer auf Ansprüche verwendet haben, die zusätzliche Ansprüche Sie, die Bestandteil der ID_Token werden.
Z.B. in eine .NET MVC-Beispiel-App öffnen Sie eine der Dateien, und geben Sie Code wie den folgenden:


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
>Bitte beachten Sie, dass der Ressourcen-Parameter in der Anforderung Oauth2 erforderlich ist.
>
>Ungültige Beispiel:
>
>**HTTPS & 58; / / sts.contoso.com/adfs/oauth2/authorize?response_type=id_Token&scope=openid&redirect_uri=https&58;//myportal/auth&nonce=b3ceb943fc756d927777&Client_id=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7&state=42c2c156aef47e8d0870&resource=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7**
>
>Gutes Beispiel:
>
>**HTTPS & 58; / / sts.contoso.com/adfs/oauth2/authorize?response_type=id_Token&scope=openid&redirect_uri=https&58;//myportal/auth&nonce=b3ceb943fc756d927777&Client_id=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7&state=42c2c156aef47e8d0870&resource=https&58;//customidrp1/**
>
>Wenn der Parameter für die Ressource in der Anforderung ist, dass ein Fehler oder ein Token ohne benutzerdefinierte Ansprüche, die angezeigt werden können.

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  