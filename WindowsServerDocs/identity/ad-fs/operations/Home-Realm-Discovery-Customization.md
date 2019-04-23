---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: Home Realm Discovery-Anpassung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1198d8b76f2ecdad728e2de6ce7a5c0d053f779f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868931"
---
# <a name="home-realm-discovery-customization"></a>Home Realm Discovery-Anpassung

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Wenn die AD FS-Client zunächst eine Ressource anfordert, hat der Ressourcenverbundserver keine Informationen über den Bereich des Clients. Der Ressourcenverbundserver antwortet dem AD FS-Client mit einem **Startbereichserkennung** Seite, in denen der Benutzer den Startbereich aus einer Liste auswählt. Die Listenwerte werden aus der Anzeigenameneigenschaft in den Anspruchsanbieter-Vertrauensstellungen entnommen. Verwenden Sie die folgenden Windows PowerShell-Cmdlets, zu ändern und Anpassen der AD FS Home Realm Discovery-Oberfläche.  
  
![Startbereich](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)  
  
> [!WARNING]  
> Beachten Sie, dass der für lokale Active Directory-Bereitstellungen angezeigt Anspruchsanbietername der Anzeigename des Verbunddiensts ist.  
  



## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>Konfigurieren des Identitätsanbieters für die Verwendung bestimmter E-Mail-Suffixe  
Eine Organisation kann einen Verbund mit mehreren Anspruchsanbietern eingehen. AD FS bietet jetzt die in\-Feld-Funktion für Administratoren, z. B. die Suffixe aufzulisten @us.contoso.com, @eu.contoso.com, die von einem Anspruchsanbieter unterstützt, und aktivieren Sie es für Suffix\-basierende Ermittlung. Klicken Sie mit dieser Konfiguration können Endbenutzer ihr organisationskonto eingeben, und AD FS wählt automatisch den entsprechenden Anspruchsanbieter aus.  
  
So konfigurieren Sie einen Identitätsanbieter \(IDP\), z. B. `fabrikam`zur Verwendung bestimmter e-Mail-Suffixe mithilfe der folgenden Windows PowerShell-Cmdlets und Syntax.  
  

`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") ` 
 
>[!NOTE]
> Wenn zwischen zwei AD FS-Server in einem Verbund zusammenfassen, legen Sie PromptLoginFederation-Eigenschaft, auf die Anspruchsanbieter-Vertrauensstellung zu ForwardPromptAndHintsOverWsFederation.  Dies ist, damit AD FS die "login_hint" und der Eingabeaufforderung des Parameters an dem IDP weiterleiten.  Dies kann erfolgen, indem Sie das folgende PowerShell-Cmdlet ausführen:
>
>`Set-AdfsclaimsProviderTrust -PromptLoginFederation ForwardPromptAndHintsOverWsFederation`

## <a name="configure-an-identity-provider-list-per-relying-party"></a>Konfigurieren einer Identitätsanbieterliste pro vertrauender Seite  
In einigen Szenarios möchte eine Organisation möglicherweise, dass Endbenutzern nur die Anspruchsanbieter angezeigt werden, die für eine Anwendung spezifisch sind, sodass nur eine Untersammlung von Anspruchsanbietern auf der Seite zur Startbereichsermittlung angezeigt wird.  
  
Zum Konfigurieren einer IDP-Liste pro vertrauender Seite Partei \(RP\), verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax.  
  
 
`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") ` 

  
## <a name="bypass-home-realm-discovery-for-the-intranet"></a>Umgehen der Startbereichsermittlung für das Intranet  
Die meisten Organisationen unterstützen nur ihr internes Active Directory für jeden Benutzer, dessen Zugriff von innerhalb der Firewall erfolgt. In diesen Fällen können Administratoren die AD FS zum Umgehen der startbereichsermittlung für das Intranet konfigurieren.  
  
Zum Umgehen der Startbereichsermittlung für das Intranet verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax.  
  

`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true ` 
 
  
> [!IMPORTANT]  
> Beachten Sie, dass wenn eine identitätsanbieterliste für eine vertrauende Seite konfiguriert wurde, auch wenn die vorherige Einstellung aktiviert wurde und der Benutzer vom Intranet zugreift, AD FS wird immer noch die startbereichsermittlung \(zur Startbereichsermittlung\) Seite. Zum Umgehen der Startbereichsermittlung in diesem Fall müssen Sie sicherstellen, dass Active Directory ebenfalls zur Identitätsanbieterliste für diese vertrauende Seite hinzugefügt wird.  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
