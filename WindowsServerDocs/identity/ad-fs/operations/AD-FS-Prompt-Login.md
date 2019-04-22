---
title: AD FS-Prompt = Login
description: Häufig gestellte Fragen für AD FS 2016
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6a4b6cfe98064181824e210be9031a0f67cb4b75
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824631"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Auffordern von Active Directory-Verbunddienste = Login-Parameter-Unterstützung
Das folgende Dokument beschreibt die systemeigene Unterstützung für den Prompt = Login-Parameter, der in AD FS verfügbar ist.

## <a name="what-is-promptlogin"></a>Neuerungen Prompt = Login?  

Einige Office 365-Anwendungen (mit aktivierter moderner Authentifizierung) senden den Prompt = Login-Parameter an Azure AD bei allen authentifizierungsanforderungen angegeben.  In der Standardeinstellung Azure AD übersetzt dies in zwei Parameter: <code> <b> wauth </b> =urn:oasis:names:tc:SAML:1.0:am:password </code>, und <code> <b> wfresh </b> =0 </code> .

Dadurch können Probleme mit dem Unternehmensintranet und Multi-Factor Authentication-Szenarien, die in der ein anderen Authentifizierungstyp als Benutzername und Kennwort gewünscht wird.  

AD FS unter Windows Server 2012 R2 mit dem Updaterollup vom Juli 2016 eingeführten systemeigenen Unterstützung für den Prompt = Login-Parameter.  Dies bedeutet, Sie haben jetzt die Möglichkeit der Konfiguration von Azure AD diesen Parameter zu senden – Ihre AD FS-Dienst wird als Teil von Azure AD und Office 365-authentifizierungsanforderungen.

### <a name="ad-fs-versions-that-support-promptlogin"></a>AD FS-Versionen, die Eingabeaufforderung unterstützen =-Anmeldung
Im folgenden finden eine Liste der AD FS-Versionen, die der Prompt = Login-Parameter unterstützt.

- AD FS unter Windows Server 2012 R2 mit dem Juli 2016 update-rollup

- AD FS unter WindowsServer 2016

## <a name="how-do-to-configure-your-azure-ad-tenant-to-send-promptlogin-to-ad-fs"></a>Wie führen Sie zum Konfigurieren von Azure AD-Mandanten zum Senden von Prompt = Login für AD FS

Verwenden Sie Azure AD PowerShell-Modul, um die Einstellung zu konfigurieren.

> [!NOTE]
> Die Prompt = Login-Funktion (von der Eigenschaft PromptLoginBehavior aktiviert) steht derzeit nur in der ["Version 1.0' Azure AD Powershell-Modul](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185), in dem die-Cmdlets haben Namen, die"Msol", wie z. B. enthalten. Set-MsolDomainFederationSettings.  Es steht derzeit nicht über "Version 2.0' Azure AD PowerShell-Modul, dessen Cmdlets Namen haben wie" Set-AzureAD\*".

So konfigurieren Sie die Prompt = Login-Verhalten, die Cmdlet-Syntax, die weiter unten:

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

 
 Die Eigenschaftswerte PreferredAuthenticationProtocol SupportsMfa und PromptLoginBehavior finden Sie die Ausgabe des Cmdlets anzeigen: ![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)
```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | fl *
 ```
> [!NOTE]
> Standardmäßig werden bei Get-MsolDomainFederationSettings ausgeführt wird werden bestimmte Eigenschaften nicht in der Konsole angezeigt.  Um diese Parameter anzuzeigen, es empfohlen wird, die Sie verwenden, die | fl * um die Ausgabe aller Eigenschaften des Objekts zu erzwingen.


Im folgenden finden weitere Informationen zu den PromptLoginBehavior-Parameter und deren Einstellungen.
   
   - <b>TranslateToFreshPasswordAuth</b> bedeutet, dass das Standardverhalten für die Azure AD senden <b>Wauth</b> und <b>Wfresh</b> auf AD FS statt mit Eingabeaufforderung =-Anmeldung
   - <b>NativeSupport</b> bedeutet, die der Prompt = Login-Parameter in AD FS gesendet werden
   - <b>Deaktivierte</b> bedeutet, dass nichts an der AD FS gesendet werden

