---
title: Client Access Control Richtlinien in AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4d7d45b91e866b9df927620f2e214ced248b3361
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947486"
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>Steuern des Zugriffs auf Organisationsdaten mit Active Directory-Verbunddienste (AD FS)

Dieses Dokument bietet eine Übersicht über die Zugriffs Steuerung mit AD FS für lokale, Hybrid-und cloudumgebungen.

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>AD FS und bedingter Zugriff auf lokale Ressourcen
Seit der Einführung von Active Directory-Verbunddienste (AD FS) sind Autorisierungs Richtlinien verfügbar, um Benutzern den Zugriff auf Ressourcen auf der Grundlage von Attributen der Anforderung und der Ressource einzuschränken oder zuzulassen.  Wenn AD FS von Version zu Version verschoben wurde, hat sich die Implementierung dieser Richtlinien geändert.  Ausführliche Informationen zu den Features der Zugriffs Steuerung finden Sie unter:
- [Access Control Richtlinien in AD FS in Windows Server 2016](Access-Control-Policies-in-AD-FS.md)
- [Zugriffs Steuerung in AD FS in Windows Server 2012 R2](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>AD FS und bedingter Zugriff in einer Hybrid Organisation

AD FS bietet die lokale Komponente der Richtlinie für bedingten Zugriff in einem Hybrid Szenario. AD FS basierten Autorisierungs Regeln sollten für Ressourcen verwendet werden, die nicht Azure AD sind, z. b. lokale Anwendungen, die direkt mit AD FS Verbund verwendet werden.  Die cloudkomponente wird durch [Azure AD bedingten Zugriff](/azure/active-directory/active-directory-conditional-access)bereitgestellt.  Azure AD Connect stellt die Steuerungsebene bereit, die die beiden verbindet.

Wenn Sie z. b. Geräte mit Azure AD für den bedingten Zugriff auf cloudressourcen registrieren, werden die Geräte Registrierungsinformationen von der Funktion zum Zurückschreiben von Azure AD Connect Geräten lokal zur Verfügung gestellt, damit AD FS Richtlinien genutzt und erzwungen werden.  Auf diese Weise haben Sie einen konsistenten Ansatz für die Zugriffs Steuerungs Richtlinien sowohl für lokale als auch für cloudressourcen.

![Bedingter Zugriff](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Die Weiterentwicklung von Client Zugriffsrichtlinien für Office 365
Viele von Ihnen verwenden Client Zugriffsrichtlinien mit AD FS, um den Zugriff auf Office 365 und andere Microsoft Online Services auf der Grundlage von Faktoren wie dem Standort des Clients und der Art der verwendeten Client Anwendung einzuschränken.
- [Client Zugriffsrichtlinien in Windows Server 2012 R2 AD FS](Access-Control-Policies-W2K12.md)
- [Client Zugriffsrichtlinien in AD FS 2,0](Access-Control-Policies-in-AD-FS-2.md)

Einige Beispiele für diese Richtlinien sind:
- Alle Extranet-Client Zugriffe auf Office 365 blockieren
- Blockieren Sie den gesamten Extranet-Client Zugriff auf Office 365, mit Ausnahme der Geräte, die auf Exchange Online zugreifen Exchange Active Sync

Häufig besteht die zugrunde liegende Notwendigkeit hinter diesen Richtlinien darin, das Risiko von Datenlecks zu mindern, indem sichergestellt wird, dass nur autorisierte Clients, Anwendungen, die keine Daten zwischenspeichern, oder Geräte, die Remote deaktiviert werden können, Zugriff auf Ressourcen erhalten.

Obwohl die oben aufgeführten dokumentierten Richtlinien für AD FS in den dokumentierten Szenarien funktionieren, haben Sie Einschränkungen, da Sie von Client Daten abhängen, die nicht konsistent verfügbar sind.  Beispielsweise ist die Identität der Client Anwendung nur für Exchange Online-basierte Dienste verfügbar, nicht für Ressourcen wie SharePoint Online, bei denen auf dieselben Daten über den Browser oder einen "Thick Client" (z. b. Word oder Excel) zugegriffen werden kann.  Außerdem AD FS nicht die Ressource in Office 365, auf die zugegriffen wird, wie z. b. SharePoint Online oder Exchange Online.

Um diese Einschränkungen zu erfüllen und eine stabilere Methode zum Verwalten des Zugriffs auf Geschäftsdaten in Office 365 oder anderen Azure AD basierten Ressourcen zu verwenden, hat Microsoft Azure AD bedingten Zugriff eingeführt.  Azure AD Richtlinien für den bedingten Zugriff können für eine bestimmte Ressource oder für alle Ressourcen innerhalb von Office 365, SaaS oder benutzerdefinierten Anwendungen in Azure AD konfiguriert werden.  Diese Richtlinien Pivot sich auf Geräte Vertrauensstellung, Standort und andere Faktoren.

Weitere Informationen zum Azure AD bedingten Zugriff finden Sie unter [bedingter Zugriff in Azure Active Directory](/azure/active-directory/active-directory-conditional-access)

Eine wichtige Änderung, die diese Szenarios ermöglicht, ist die [moderne Authentifizierung](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/), eine neue Möglichkeit der Authentifizierung von Benutzern und Geräten, die in Office-Clients, Skype, Outlook und Browsern auf dieselbe Weise funktioniert.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zum Steuern des Zugriffs in der Cloud und lokal finden Sie unter:

- [Bedingter Zugriff in Azure Active Directory](/azure/active-directory/active-directory-conditional-access)
- [Access Control Richtlinien in AD FS 2016](Access-Control-Policies-in-AD-FS.md)
