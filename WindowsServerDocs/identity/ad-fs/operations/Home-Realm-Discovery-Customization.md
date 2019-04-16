---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: Home Realm Discovery-Anpassung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 328c313b2d5bf174f6e6af20cd91ac9620edac82
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="home-realm-discovery-customization"></a>Home Realm Discovery-Anpassung

>Gilt für: Windows Server 2016, Windows Server2012 R2

Wenn der AD FS-Client Anfangs eine Ressource anfordert, hat der Ressourcenverbundserver keine Informationen über den Bereich des Clients. Der Ressourcenverbundserver antwortet dem AD FS-Client mit einem **Startbereichserkennung** Seite, in dem der Benutzer den Startbereich aus einer Liste auswählt. Die Listenwerte werden aus der anzeigenameneigenschaft in den Anspruchsanbieter-Vertrauensstellungen aufgefüllt. Verwenden Sie die folgenden Windows PowerShell-Cmdlets, zu ändern und die AD FS Home Realm Discovery-Erfahrung anzupassen.  
  
![Startbereich](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)  
  
> [!WARNING]  
> Beachten Sie, dass die Anspruchsanbieter-Namen, der für die lokale Active Directory der Anzeigename des Verbunddiensts ist.  
  
## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>Konfigurieren des Identitätsanbieters Verwendung bestimmter e-Mail-Suffixe  
Eine Organisation kann mit mehreren Anspruchsanbietern verbinden. AD FS bietet jetzt die Taste-Administratoren, die Suffixe aufzulisten @us.contoso.com, @eu.contoso.com, d. h. von einem Anspruchsanbieter unterstützt werden und für Suffix\-basierte Erkennung zu aktivieren. Mit dieser Konfiguration können Endbenutzer ihre organisationskonto eingeben, und AD FS wählt automatisch den entsprechenden Anspruchsanbieter aus.  
  
So konfigurieren Sie als Identitätsanbieter \(IDP\), z. B. `fabrikam`, zur Verwendung bestimmter e-Mail-Suffixe das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  

`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") ` 
 
  
## <a name="configure-an-identity-provider-list-per-relying-party"></a>Konfigurieren eine identitätsanbieterliste pro vertrauende Seite Party  
Für einige Szenarien sollten Organisationen Endbenutzern nur die Anspruchsanbieter angezeigt, die für eine Anwendung spezifisch sind, damit nur eine Teilmenge der Anspruchsanbieter werden auf der Seite zur startbereichsermittlung angezeigt.  
  
Konfigurieren eine IDP-Liste pro vertrauender Seite \(RP\) Partei, verwenden Sie die folgenden Windows PowerShell-Cmdlet und die folgende Syntax.  
  
 
`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") ` 

  
## <a name="bypass-home-realm-discovery-for-the-intranet"></a>Umgehen der Startbereichsermittlung für das intranet  
Die meisten Organisationen unterstützen nur ihr internes Active Directory für jeden Benutzer, die innerhalb der Firewall aus zugreift. In diesen Fällen können Administratoren AD FS zum Umgehen der startbereichsermittlung für das Intranet konfigurieren.  
  
Zum Umgehen der Startbereichsermittlung für das Intranet verwenden Sie die folgenden Windows PowerShell-Cmdlet und die folgende Syntax.  
  

`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true ` 
 
  
> [!IMPORTANT]  
> Sie zeigt Beachten Sie, dass wenn eine identitätsanbieterliste für eine der vertrauenden Seite Party konfiguriert wurde, obwohl die vorherige Einstellung aktiviert wurde, und der Benutzer zugreift, aus dem Intranet, AD FS immer noch die Seite zur startbereichsermittlung \(HRD\). Zum Umgehen der Startbereichsermittlung in diesem Fall müssen Sie sicherstellen, dass "Active Directory" auch die IDP-Liste für diese vertrauende Seite hinzugefügt wird.  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
