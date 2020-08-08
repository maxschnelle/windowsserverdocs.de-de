---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: AD FS-Entwurfshandbuch in Windows Server 2012 R2
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 6ec9826ce2015197d96a182864807646a6b8115d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940406"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>AD FS Entwurfs Handbuch in Windows Server

Active Directory-Verbunddienste (AD FS) \( AD FS \) bietet einen vereinfachten, gesicherten Identitäts Verbund und SSO- \- \( Funktionen für einmaliges Anmelden \) für Endbenutzer, die in einem AD FS \- gesicherten Unternehmen, in Verbund Partnerorganisationen oder in der Cloud auf Anwendungen zugreifen möchten.

In Windows Server &reg; 2012 R2 umfasst AD FS einen Verbund Dienst-Rollen Dienst, der als Identitäts Anbieter fungiert, \( um Benutzer zu authentifizieren, um Sicherheits Token für Anwendungen bereitzustellen, die AD FS Vertrauen, \) oder wenn ein Verbund Anbieter \( Token von anderen Identitäts Anbietern nutzt und dann Sicherheits Token für Anwendungen bereitstellt, die AD FS Vertrauen \) .

Die Funktion der Bereitstellung von Extranetzugriff auf Anwendungen und Dienste, die von AD FS in Windows Server 2012 R2 geschützt sind, erfolgt jetzt durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy. Dies ist eine Abweichung von früheren Versionen von Windows Server, in denen diese Funktion von einem AD FS-Verbundserverproxys übernommen wurde. Webanwendungsproxy ist eine Server Rolle, die den Zugriff auf das AD FS \- Verwandte Extranetszenario und andere Extranetszenarien ermöglicht. Weitere Informationen zum webanwendungsproxy finden Sie unter Exemplarische Vorgehensweise zum [webanwendungsproxy](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280944(v=ws.11))

## <a name="about-this-guide"></a>Über diesen Leitfaden
Dieses Handbuch enthält Empfehlungen zum Planen einer neuen Bereitstellung von AD FS, basierend auf den Anforderungen Ihrer Organisation. Dieses Handbuch ist für die Verwendung durch einen Infrastrukturspezialisten oder Systemarchitekten vorgesehen. Es hebt die wichtigsten Entscheidungspunkte hervor, wenn Sie Ihre AD FS Bereitstellung planen. Bevor Sie dieses Handbuch lesen, sollten Sie wissen, wie AD FS auf einer Funktionsebene funktioniert. Weitere Informationen finden Sie unter [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md).

## <a name="in-this-guide"></a>Inhalt dieser Anleitung

-   [Identifizieren der AD FS-Bereitstellungsziele](Identify-Your-AD-FS-Deployment-Goals.md)

-   [Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)

-   [AD FS-Anforderungen](AD-FS-Requirements.md)


## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurf](../../ad-fs/AD-FS-Design.md)

