---
ms.assetid: ''
title: Client Access Control-Richtlinien in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cc91cd9a446c8ca30471b65374ca99a7bd49d369
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882371"
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>Steuern des Zugriffs auf Unternehmensdaten mit Active Directory-Verbunddienste

Dieses Dokument bietet einen Überblick über die Zugriffssteuerung mit AD FS vor Ort, Hybrid- und Cloud-Szenarien.  

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>AD FS und bedingten Zugriff auf lokale Ressourcen 
Seit der Einführung von Active Directory Federation Services waren Autorisierungsrichtlinien einschränken oder ermöglichen Benutzerzugriff auf Ressourcen, die auf Grundlage von Attributen der Anforderung und die Ressource verfügbar.  Da AD FS von Version zu Version verschoben wurde, wie diese Richtlinien implementiert wurden hat sich geändert.  Ausführliche Informationen zu den Features zur Zugriffssteuerung nach Version finden Sie unter:
- [Richtlinien für die Zugriffssteuerung in AD FS unter WindowsServer 2016](Access-Control-Policies-in-AD-FS.md)
- [Zugriffssteuerung in AD FS unter Windows Server 2012 R2](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>AD FS und bedingten Zugriff in einem Hybrid-Unternehmen  

AD FS verfügt, die auf lokale-Komponente der Richtlinie für bedingten Zugriff in einem hybridszenario. AD FS-basierten Autorisierungsregeln sollten verwendet werden für nicht-Azure AD-Ressourcen, wie z. B. lokale Anwendungen im direkten Verbund mit AD FS.  Die Clouddienst-Komponente erfolgt über [bedingtem Azure AD Access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access).  Azure AD Connect bietet die Steuerungsebene, die die beiden verbindet.

Z. B. beim Registrieren von Geräten mit Azure AD für den bedingten Zugriff auf Cloud-Ressourcen des Azure AD Connect-Geräts Zurückschreiben, dass die Funktion zur Verfügung Registrierungsinformationen Gerät lokal für die AD FS-Richtlinien zu nutzen und zu erzwingen.  Auf diese Weise haben Sie einen einheitlichen Ansatz für den Zugriff auf Richtlinien für die Zugriffssteuerung sowohl auf lokale und cloudbasierte Ressourcen.  

![Für den bedingten Zugriff](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Die Entwicklung von Clientzugriffsrichtlinien für Office 365
Viele von Ihnen sind Clientzugriffsrichtlinien mit AD FS verwenden, beschränken Sie den Zugriff auf Office 365 und andere Microsoft Online Services basierend auf Faktoren wie den Speicherort des Clients und den Typ der Clientanwendung verwendet wird.  
- [Client-Zugriffsrichtlinien in Windows Server 2012 R2 AD FS](Access-Control-Policies-W2K12.md)
- [Clientzugriffsrichtlinien in AD FS 2.0](Access-Control-Policies-in-AD-FS-2.md)

Einige Beispiele für diese Richtlinien sind:
- Blockieren des gesamten extranet Clientzugriffs auf Office 365
- Blockieren des gesamten extranet Clientzugriffs auf Office 365, mit Ausnahme von Geräten, die Zugriff auf Exchange Online für Exchange Active Sync

Häufig zugrunde liegenden erforderlich hinter diesen Richtlinien zum Verringern Risiko potenzieller Datenlecks leuchten nur autorisierte Clients, Anwendungen, die Daten nicht zwischengespeichert ist oder Geräte, die Remote deaktiviert werden können, können den Zugriff auf Ressourcen erhalten.

Während der oben aufgeführten dokumentierten Richtlinien für AD FS in bestimmten Szenarien dokumentiert arbeiten zu können, müssen sie Einschränkungen, da sie Client-Daten abhängen, die nicht durchgängig verfügbar sind, ist.  Z. B. wurde die Identität der Clientanwendung nur verfügbar für Exchange Online mithilfe von Diensten und nicht für Ressourcen wie SharePoint Online, in denen die gleichen Daten über den Browser oder ein thick-Client wie Word oder Excel zugegriffen werden können.  Außerdem ist die AD FS keine Kenntnis von der Ressource in Office 365 auf die zugegriffen wird, wie SharePoint Online oder Exchange Online.

Um diese Einschränkungen zu beheben, und geben Sie eine stabilere Möglichkeit, Richtlinien zum Verwalten des Zugriffs auf Geschäftsdaten in Office 365 oder andere Ressourcen von Azure AD-basierten, wurde eingeführt, Microsoft Azure AD für bedingten Zugriff.  Azure AD-bedingte Zugriffsrichtlinien können für eine bestimmte Ressource oder für einzelne oder alle Ressourcen in Office 365, SaaS oder benutzerdefinierten Anwendungen in Azure AD konfiguriert werden.  Diese Richtlinien auf dem Gerät Vertrauensstellung, Speicherort und andere Faktoren pivotieren.

Weitere Informationen zu Azure AD für bedingten Zugriff finden Sie unter [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)

Ist eine aktivieren diese Szenarios schlüsseländerung [moderne Authentifizierung](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/), eine neue Art der Authentifizierung von Benutzern und Geräten, die die gleiche Weise wie für Office-Clients, Skype, Outlook und Browser funktioniert.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Steuerung des Zugriffs über die Cloud und lokal finden Sie unter:

- [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
- [Richtlinien für die Zugriffssteuerung in AD FS 2016](Access-Control-Policies-in-AD-FS.md)
