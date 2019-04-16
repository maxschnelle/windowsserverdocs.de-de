---
title: AD FS-Aufforderung = Anmeldung
description: "Häufig gestellte Fragen für AD FS 2016"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8b98cdc27c9bd01d9855e98965f59ebe5257ed5c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory Federation Services auffordern = Anmelde-Parameter-Unterstützung
Im folgenden Dokument wird die systemeigene Unterstützung für den Prompt = Anmelde-Parameter, der in AD FS verfügbar ist.

## <a name="what-is-promptlogin"></a>What's Prompt = Anmelde?  

Einige Office365-Anwendungen (mit modernen Authentifizierung aktiviert) senden Parameters Anmeldenamen Aufforderung = an Azure AD als Teil jeder Authentifizierungsanforderung.  Standardmäßig Azure AD übersetzt diese in zwei Parameter: <code><b>wauth</b>=urn:oasis:names:tc:SAML:1.0:am:password</code>, und <code><b>wfresh</b>=0</code>.

Dadurch können Probleme mit dem Unternehmensintranet und Multi-Factor Authentication-Szenarien, in dem ein Authentifizierungstyp als Benutzername und Kennwort gewünscht wird.  

AD FS unter Windows Server2012 R2 mit Updaterollup vom Juli2016 eingeführt systemeigene Unterstützung für den Prompt = Anmelde-Parameter.  Dies bedeutet, Sie haben jetzt die Möglichkeit der Konfiguration von Azure AD, senden diesen Parameter-AD FS-Dienst wird als Teil der Azure AD und Office365-Authentifizierungsanforderungen.

### <a name="ad-fs-versions-that-support-promptlogin"></a>AD FS-Versionen, die Aufforderung unterstützen = Anmeldung
Im folgenden finden eine Liste der AD FS-Versionen, die Parameters Anmeldenamen Aufforderung = unterstützen.

- Updaterollup für AD FS unter Windows Server2012 R2 mit der Juli2016

- AD FS unter Windows Server 2016

## <a name="how-do-to-configure-your-azure-ad-tenant-to-send-promptlogin-to-ad-fs"></a>Vorgehensweise zum Konfigurieren Ihrer Azure AD-Mandantenverwaltungs Aufforderung senden = melden Sie sich bei AD FS

Verwenden Sie das Azure AD-PowerShell-Modul, um die Einstellung konfigurieren.

> [!NOTE]
> Die Aufforderung = Anmeldefunktionen (durch die Eigenschaft PromptLoginBehavior aktiviert) steht derzeit nur in den [' Version 1.0' Azure AD-PowerShell-Modul](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185), in dem die Cmdlets haben Namen, die "Msol", z.B. Set-MsolDomainFederationSettings enthalten.  Es ist derzeit nicht verfügbar über ' Version 2.0' Azure AD-PowerShell-Modul, dessen Cmdlets Namen weisen wie "festlegen-AzureAD\ *".

So konfigurieren Sie die Eingabeaufforderung = melden Sie sich Verhalten, das folgende Cmdlet-Syntax:

Beispiel 1:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -PreferredAuthenticationProtocol <your current protocol setting> 
```

Beispiel 2:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -SupportsMfa <$True|$False>
```

Beispiel 3:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

 
 Die Eigenschaftswerte PreferredAuthenticationProtocol SupportsMfa und PromptLoginBehavior finden, indem Sie die Ausgabe des Cmdlets: ![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)
```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | fl *
 ```
> [!NOTE]
> Standardmäßig beim Get-MsolDomainFederationSettings ausführen werden bestimmte Eigenschaften nicht in der Konsole angezeigt.  Um diese Parameter anzuzeigen, es empfohlen wird, die Sie verwenden, die | fl * erzwingen Sie die Ausgabe des aller Eigenschaften des Objekts.


Im folgenden finden weitere Informationen zu den PromptLoginBehavior-Parameter und dessen Einstellungen.
   
   - <b>TranslateToFreshPasswordAuth</b> bedeutet, dass das Standardverhalten für die Azure AD zum Senden von <b>Wauth</b> und <b>Wfresh</b> zu AD FS anstatt Aufforderung = Anmeldung
   - <b>NativeSupport</b> bedeutet, die als AD FS Parameters Anmeldenamen Aufforderung = gesendet werden
   - <b>Deaktivierte</b> bedeutet, dass nichts wird gesendet werden, um AD FS

