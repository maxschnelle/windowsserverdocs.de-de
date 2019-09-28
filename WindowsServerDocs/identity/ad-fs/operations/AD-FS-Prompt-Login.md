---
title: AD FS prompt = Login
description: Häufig gestellte Fragen zu AD FS 2016
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ba43d591d429e589a990dfdfc4a4992ffa4a6ef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358548"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory-Verbunddienste (AD FS) prompt = Unterstützung von Anmelde Parametern

Im folgenden Dokument wird die native Unterstützung für den in AD FS verfügbaren prompt = Login-Parameter beschrieben.

## <a name="what-is-promptlogin"></a>Was ist prompt = Login?

Wenn Anwendungen eine neue Authentifizierung von Azure AD anfordern müssen, was bedeutet, dass Sie Azure AD, den Benutzer erneut zu authentifizieren, auch wenn der Benutzer bereits authentifiziert wurde, kann er den `prompt=login` Parameter als Teil der Authentifizierung an Azure AD senden. Anforderung.

Wenn diese Anforderung für einen Verbund Benutzer gilt, muss Azure AD den IDP wie AD FS darüber informieren, dass die Anforderung für die neue Authentifizierung gilt.

Standardmäßig wird Azure AD beim `prompt=login` senden `wfresh=0` dieser Art von Authentifizierungsanforderungen an den Verbund-IDP in und `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` übersetzt.

Diese Parameter bedeuten Folgendes:

- `wfresh=0`: neue Authentifizierung durchführen
- `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: Benutzername/Kennwort für die neue Authentifizierungsanforderung verwenden

Dies kann Probleme mit unternehmensinternen Intranetszenarien und Multi-Factor Authentication-Szenarien verursachen, bei denen ein anderer Authentifizierungstyp als `wauth` Benutzername und Kennwort, wie vom-Parameter angefordert, gewünscht ist.  

AD FS in Windows Server 2012 R2 mit dem Updaterollup vom Juli 2016 wurde die native `prompt=login` Unterstützung für den-Parameter eingeführt. Dies bedeutet, dass Azure AD diesen Parameter jetzt unverändert an AD FS Dienst im Rahmen von Azure AD-und Office 365-Authentifizierungsanforderungen senden kann.

## <a name="ad-fs-versions-that-support-promptlogin"></a>AD FS Versionen, die prompt = Login unterstützen

Im folgenden finden Sie eine Liste der AD FS Versionen, die `prompt=login` den-Parameter unterstützen.

- AD FS in Windows Server 2012 R2 mit dem Updaterollup vom Juli 2016
- AD FS in Windows Server 2016

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>Konfigurieren einer Verbund Domäne zum Senden von prompt = Login an AD FS

Verwenden Sie das Azure AD PowerShell-Modul, um die Einstellung zu konfigurieren.

> [!NOTE]
> Die `prompt=login` Funktion (durch die `PromptLoginBehavior` -Eigenschaft aktiviert) ist zurzeit nur in [Version 1,0 des Azure AD PowerShell-Moduls](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)verfügbar, in dem die Cmdlets Namen enthalten, die "MSOL" enthalten, wie z. b. Set-msoldomainfederationsettings.  Es ist zurzeit nicht über "Version 2,0" des Azure AD PowerShell-Moduls verfügbar, dessen Cmdlets Namen wie "Set-azuread\*" haben.

1. Rufen Sie zuerst die aktuellen Werte `PreferredAuthenticationProtocol`von `SupportsMfa`, und `PromptLoginBehavior` für die Verbund Domäne ab, indem Sie den folgenden PowerShell-Befehl ausführen:

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> In der Ausgabe `Get-MsolDomainFederationSettings` von werden bestimmte Eigenschaften in der Konsole standardmäßig nicht angezeigt. Um alle Eigenschaften anzuzeigen, sollten Sie Ihre Ausgabe`|`an die Pipeline übergeben `Format-List *` , um die Ausgabe aller Eigenschaften des Objekts zu erzwingen.

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> Wenn die `PreferredAuthenticationMethod` -Eigenschaft leer ist`$null`(), bedeutet dies das Standard `TranslateToFreshPasswordAuth`Verhalten von.

2. Konfigurieren Sie den gewünschten Wert `PromptLoginBehavior` von, indem Sie den folgenden Befehl ausführen:

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

Im folgenden sind die möglichen Werte `PromptLoginBehavior` des-Parameters und deren Bedeutung aufgeführt:

- **Translatetofreshpasswordauth**: bedeutet das standardmäßige Azure AD Verhalten der `prompt=login` über `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` Setzung `wfresh=0`in und.
- **Nativesupport**: bedeutet, dass `prompt=login` der Parameter unverändert an AD FS gesendet wird. Dies ist der empfohlene Wert, wenn AD FS in Windows Server 2012 R2 mit dem Updaterollup vom Juli 2016 oder höher ist.
- **Deaktiviert**: bedeutet, dass `wfresh=0` nur an AD FS gesendet wird.
