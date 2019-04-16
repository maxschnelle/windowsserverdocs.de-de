---
ms.assetid: 
title: Steuerung des Zugriffs Clientrichtlinien in AD FS
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5e1e1b907e6fccbf2b9906106d3360bd9a6fd69d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>Steuern des Zugriffs auf Unternehmensdaten mit Active Directory-Verbunddienste

Dieses Dokument bietet einen Überblick über die Steuerung des Zugriffs mit AD FS über lokal, Hybrid und Cloud-Szenarien.  

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>AD FS und bedingten Zugriff auf lokale Ressourcen 
Seit der Einführung von Active Directory Federation Services wurden Autorisierungsrichtlinien einschränken oder ermöglichen Benutzern den Zugriff auf Ressourcen auf Grundlage der Attribute der Anforderung und die Ressource zur Verfügung steht.  Als AD FS nach Version verschoben wurde, wurde wie diese Richtlinien umgesetzt werden geändert.  Ausführliche Informationen zu den Features der Access-Control von Version finden Sie unter:
- [Zugriffssteuerungsrichtlinien in AD FS unter Windows Server 2016](Access-Control-Policies-in-AD-FS.md)
- [Zugriffssteuerung in AD FS unter Windows Server2012 R2](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>AD FS und bedingten Zugriff in einer Hybrid-Organisation  

AD FS bietet, die auf lokalen Komponente der Richtlinie für bedingten Zugriff in einem hybridszenario. AD FS-basierten Autorisierungsregeln für verwendet werden soll nicht Azure AD-Ressourcen, z.B. auf lokale Anwendungen federated direkt in AD FS.  Die cloudkomponente erfolgt über [Azure AD bedingten Zugriff](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access).  Azure AD Connect bietet die Steuerelement-Ebene Verbinden der beiden.

Wenn beispielsweise Sie Geräte mit Azure AD für bedingten Zugriff auf Cloudressourcen registrieren, das Azure AD Connect-Gerät schreiben wieder macht Geräteinformationen Registrierung verfügbar lokal für AD FS-Richtlinien nutzen, und erzwingen.  Auf diese Weise können Sie einen konsistenten Ansatz für den Zugriff auf Richtlinien für sowohl in lokalen und Cloud-Ressourcen.  

![Bedingter Zugriff](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Die Weiterentwicklung von Client-Richtlinien für Office365
Viele von Ihnen sind Clientrichtlinien mit AD FS verwenden, begrenzen Sie den Zugriff auf Office365 und andere Microsoft Online Services anhand verschiedener Faktoren wie den Speicherort des Clients und den Typ der Clientanwendung verwendet wird.  
- [Client-Richtlinien in Windows Server2012 R2 AD FS](Access-Control-Policies-W2K12.md)
- [Client-Richtlinien in AD FS 2.0](Access-Control-Policies-in-AD-FS-2.md)

Einige Beispiele für diese Richtlinien:
- Alle Extranet den Clientzugriff auf Office365 blockieren
- Blockieren Sie aller Extranet Clientzugriff auf Office365, mit Ausnahme der Geräte, die Zugriff auf Exchange Active Sync Exchange Online

Häufig die zugrunde liegenden erforderlich hinter dieser Richtlinien ist, um das Risiko von Datenlecks verringern, indem sichergestellt wird nur autorisierte Clients, Anwendungen, die Daten nicht zwischengespeichert werden, oder Geräte, die Remote deaktiviert werden können, erhalten Zugriff auf Ressourcen.

Während der oben genannten dokumentierten Richtlinien für AD FS in bestimmten Szenarien dokumentiert arbeiten, können sie Einschränkungen, da sie von Clientdaten abhängen, die nicht ständig verfügbar ist.  Z.B. wurde die Identität der Clientanwendung nur für Exchange Online basierte Dienste und für Ressourcen wie SharePoint Online, in denen die gleichen Daten über den Browser oder einen thick Client z.B. Word oder Excel zugegriffen werden möglicherweise nicht verfügbar.  AD FS ist außerdem unabhängig von der Ressource in Office365 zugegriffen wird, z.B. SharePoint Online oder Exchange Online.

Um diese Einschränkungen und stabilere die Möglichkeit, verwenden Sie Richtlinien, um den Zugriff auf Geschäftsdaten in Office365 oder anderen Azure AD-Basis-Ressourcen zu verwalten, Microsoft Azure AD bedingten Zugriff eingeführt wurde.  Azure AD-bedingte Zugriffsrichtlinien können für eine bestimmte Ressource oder für alle Ressourcen in Office365, SaaS oder benutzerdefinierte Anwendungen in Azure AD konfiguriert werden.  Diese Richtlinien pivot-Vertrauensstellung der Geräte, Standort und anderen Faktoren.

Weitere Informationen zu Azure AD bedingten Zugriff finden Sie unter [bedingten Zugriff in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access)

Eine wichtige Änderung aktivieren diese Szenarien ist [moderne Authentifizierung](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/), einer neuen Art der Authentifizierung von Benutzern und Geräten, die die gleiche Weise in Office-Clients, Skype, Outlook und Browsern funktioniert.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Steuerung des Zugriffs auf die Cloud und lokal finden Sie unter:

- [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access)
- [Zugriffssteuerungsrichtlinien in AD FS 2016](Access-Control-Policies-in-AD-FS.md)
