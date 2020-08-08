---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: Anpassung der Startbereichs Ermittlung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b747d29aa4ceba7d7f3a12fc5a6a74155e058050
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954246"
---
# <a name="home-realm-discovery-customization"></a>Anpassung der Startbereichs Ermittlung


Wenn der AD FS Client zuerst eine Ressource anfordert, hat der Ressourcen Verbund Server keine Informationen zum Bereich des Clients. Der Ressourcen Verbund Server antwortet dem AD FS-Client mit einer Seite zur **Client Bereichs** Ermittlung, auf der der Benutzer den Startbereich aus einer Liste auswählt. Die Listenwerte werden aus der Anzeigenameneigenschaft in den Anspruchsanbieter-Vertrauensstellungen entnommen. Verwenden Sie die folgenden Windows PowerShell-Cmdlets, um die AD FS Home Realm Discovery-Funktion zu ändern und anzupassen.

![Startbereich](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)

> [!WARNING]
> Beachten Sie, dass der für lokale Active Directory-Bereitstellungen angezeigt Anspruchsanbietername der Anzeigename des Verbunddiensts ist.




## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>Konfigurieren des Identitätsanbieters für die Verwendung bestimmter E-Mail-Suffixe
Eine Organisation kann einen Verbund mit mehreren Anspruchsanbietern eingehen. AD FS bietet Administratoren nun die \- Möglichkeit, die Suffixe (z. b.,) aufzulisten, die @us.contoso.com @eu.contoso.com von einem Anspruchs Anbieter unterstützt werden, und Sie für die Suffix-basierte Ermittlung zu aktivieren \- . Mit dieser Konfiguration können Endbenutzer ihr Organisationskonto eingeben, und AD FS wählen automatisch den entsprechenden Anspruchsanbieter aus.

\( \) `fabrikam` Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um einen Identitäts Anbieter-IDP wie z. b. für die Verwendung bestimmter e-Mail-Suffixe zu konfigurieren


`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") `

>[!NOTE]
> Legen Sie beim Verbund zwischen zwei AD FS Servern die promptloginfederation-Eigenschaft für die Anspruchs Anbieter-Vertrauensstellung auf forwardpromptandhintsoverwsfederation fest.  Dadurch wird AD FS die login_hint und die Eingabeaufforderung an den IDP weiterleiten.  Dies kann durch Ausführen des folgenden PowerShell-Cmdlets erreicht werden:
>
>`Set-AdfsclaimsProviderTrust -PromptLoginFederation ForwardPromptAndHintsOverWsFederation`

## <a name="configure-an-identity-provider-list-per-relying-party"></a>Konfigurieren einer Identitätsanbieterliste pro vertrauender Seite
In einigen Szenarios möchte eine Organisation möglicherweise, dass Endbenutzern nur die Anspruchsanbieter angezeigt werden, die für eine Anwendung spezifisch sind, sodass nur eine Untersammlung von Anspruchsanbietern auf der Seite zur Startbereichsermittlung angezeigt wird.

Verwenden Sie zum Konfigurieren einer IDP-Liste \( pro \) Vertrauender Seite das folgende Windows PowerShell-Cmdlet und die folgende Syntax.


`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") `


## <a name="bypass-home-realm-discovery-for-the-intranet"></a>Umgehen der Startbereichsermittlung für das Intranet
Die meisten Organisationen unterstützen nur ihr internes Active Directory für jeden Benutzer, dessen Zugriff von innerhalb der Firewall erfolgt. In diesen Fällen können Administratoren AD FS so konfigurieren, dass die Startbereichs Ermittlung für das Intranet umgangen wird.

Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um die HRD für das Intranet zu umgehen.


`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true `


> [!IMPORTANT]
> Beachten Sie Folgendes: Wenn eine Identitäts Anbieterliste für eine vertrauende Seite konfiguriert wurde, wird die Seite für die Startbereichs Ermittlung weiterhin angezeigt, obwohl die vorherige Einstellung aktiviert wurde und der Benutzer vom AD FS Intranet aus auf Sie zugreift \( \) . Zum Umgehen der Startbereichsermittlung in diesem Fall müssen Sie sicherstellen, dass Active Directory ebenfalls zur Identitätsanbieterliste für diese vertrauende Seite hinzugefügt wird.

## <a name="additional-references"></a>Weitere Verweise
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
