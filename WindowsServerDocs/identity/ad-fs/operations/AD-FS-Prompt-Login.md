---
title: AD FS prompt = Login
description: Häufig gestellte Fragen zu AD FS 2016
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.openlocfilehash: 0af0d71ad2b373f755653898ab0697b0308faa4b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940303"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Unterstützung des Parameters „prompt=login“ der Active Directory-Verbunddienste (AD FS)

Im folgenden Dokument wird die native Unterstützung für den in AD FS verfügbaren prompt = Login-Parameter beschrieben.

## <a name="what-is-promptlogin"></a>Was ist prompt = Login?

Wenn Anwendungen eine neue Authentifizierung von Azure AD anfordern müssen, was bedeutet, dass Sie Azure AD, den Benutzer erneut zu authentifizieren, auch wenn der Benutzer bereits authentifiziert wurde, kann er den `prompt=login` Parameter als Teil der Authentifizierungsanforderung an Azure AD senden.

Wenn diese Anforderung für einen Verbund Benutzer gilt, muss Azure AD den IDP wie AD FS darüber informieren, dass die Anforderung für die neue Authentifizierung gilt.

Standardmäßig wird Azure AD `prompt=login` `wfresh=0` `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` beim Senden dieser Art von Authentifizierungsanforderungen an den Verbund-IDP in und übersetzt.

Diese Parameter bedeuten Folgendes:

- `wfresh=0`: neue Authentifizierung durchführen
- `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: Benutzername/Kennwort für die neue Authentifizierungsanforderung verwenden

Dies kann Probleme mit unternehmensinternen Intranetszenarien und Multi-Factor Authentication-Szenarien verursachen, bei denen ein anderer Authentifizierungstyp als Benutzername und Kennwort, wie vom- `wauth` Parameter angefordert, gewünscht ist.

AD FS in Windows Server 2012 R2 mit dem Updaterollup vom Juli 2016 wurde die native Unterstützung für den- `prompt=login` Parameter eingeführt. Dies bedeutet, dass Azure AD diesen Parameter jetzt unverändert an AD FS Dienst im Rahmen von Azure AD-und Office 365-Authentifizierungsanforderungen senden kann.

## <a name="ad-fs-versions-that-support-promptlogin"></a>AD FS Versionen, die prompt = Login unterstützen

Im folgenden finden Sie eine Liste der AD FS Versionen, die den-Parameter unterstützen `prompt=login` .

- AD FS in Windows Server 2012 R2 mit dem Updaterollup vom Juli 2016
- AD FS in Windows Server 2016

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>Konfigurieren einer Verbund Domäne zum Senden von prompt = Login an AD FS

Verwenden Sie das Azure AD PowerShell-Modul, um die Einstellung zu konfigurieren.

> [!NOTE]
> Die `prompt=login` Funktion (durch die- `PromptLoginBehavior` Eigenschaft aktiviert) ist zurzeit nur in [Version 1,0 des Azure AD PowerShell-Moduls](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)verfügbar, in dem die Cmdlets Namen enthalten, die "MSOL" enthalten, wie z. b. Set-msoldomainfederationsettings.  Es ist zurzeit nicht über "Version 2,0" des Azure AD PowerShell-Moduls verfügbar, dessen Cmdlets Namen wie "Set-azuread \* " haben.

1. Rufen Sie zuerst die aktuellen Werte von `PreferredAuthenticationProtocol` , `SupportsMfa` und `PromptLoginBehavior` für die Verbund Domäne ab, indem Sie den folgenden PowerShell-Befehl ausführen:

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> In der Ausgabe von `Get-MsolDomainFederationSettings` werden bestimmte Eigenschaften in der Konsole standardmäßig nicht angezeigt. Um alle Eigenschaften anzuzeigen, sollten Sie `|` Ihre Ausgabe an die Pipeline übergeben, um `Format-List *` die Ausgabe aller Eigenschaften des Objekts zu erzwingen.

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> Wenn der Wert der-Eigenschaft `PromptLoginBehavior` leer ist ( `$null` ), wird das Verhalten von `TranslateToFreshPasswordAuth` verwendet.

2. Konfigurieren Sie den gewünschten Wert von, `PromptLoginBehavior` indem Sie den folgenden Befehl ausführen:

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

Im folgenden sind die möglichen Werte des `PromptLoginBehavior` -Parameters und deren Bedeutung aufgeführt:

- **Translatetofreshpasswordauth**: bedeutet das standardmäßige Azure AD Verhalten der Übersetzung `prompt=login` in `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` und `wfresh=0` .
- **Nativesupport**: bedeutet, dass der `prompt=login` Parameter unverändert an AD FS gesendet wird. Dies ist der empfohlene Wert, wenn AD FS in Windows Server 2012 R2 mit dem Updaterollup vom Juli 2016 oder höher ist.
- **Deaktiviert**: bedeutet, dass nur `wfresh=0` an AD FS gesendet wird.
