---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: AD FS-Entwurfshandbuch in Windows Server 2012
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3f2a6df6a9c9a5cbdfa9c64bc6521e92f4982a15
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191735"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>AD FS-Entwurfshandbuch in WindowsServer 


  
> [!NOTE]  
> Informationen zum Bereitstellen von AD FS unter Windows Server 2012 R2, finden Sie unter [Windows Server 2012 R2 AD FS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md).  
  
Sie können Active Directory® Federation Services \(AD FS\) mit dem Windows Server® 2012-Betriebssystem in einem Verbund-services-Rolle verwenden, um Ihre Benutzer auf Internet nahtlos zu authentifizieren\--basierte Dienste oder Anwendungen, die befinden sich in einer Ressourcenpartnerorganisation übernehmen, ohne die Notwendigkeit von Administratoren erstellt oder gewahrt, externe Vertrauensstellungen oder Gesamtstruktur-Vertrauensstellungen zwischen den Netzwerken beider Organisationen und ohne die Notwendigkeit der Benutzer auf ein zweites Mal anmelden. Der Vorgang der Authentifizierung mit einem Netzwerk beim Zugriff auf Ressourcen in einem anderen Netzwerk – ohne den Aufwand wiederholter Anmeldeaktionen durch Benutzer – wird als einmaliges Anmelden bezeichnet\-auf \(SSO\).  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Dieser Leitfaden bietet Empfehlungen helfen Ihnen beim Planen einer neuen Bereitstellung von AD FS, basierend auf den Anforderungen Ihrer Organisation \(auch in diesem Handbuch als Bereitstellungsziele bezeichnet\) und des gewünschten Entwurfs, die Sie erstellen möchten. Dieses Handbuch ist für die Verwendung durch einen Infrastrukturspezialisten oder Systemarchitekten vorgesehen. Planen der AD FS-Bereitstellung lassen sich die wesentlichen Entscheidungspunkte hervorheben. Bevor Sie dieses Handbuch lesen, sollten Sie ein gutes Verständnis der Funktionsweise von AD FS auf einer Funktionsebene verfügen. Sie sollten auch einen fundierten Überblick über die organisatorischen Anforderungen, die widergespiegelt werden haben, klicken Sie in Ihrer AD FS-Entwurfs.  
  
Dieses Handbuch beschreibt eine Reihe von bereitstellungszielen, die auf drei primären AD FS basieren, und erleichtert Ihnen die Entscheidung, die am besten geeigneten Entwurfs für Ihre Umgebung. Sie können diesen bereitstellungszielen einen der folgenden umfassenden AD FS Entwürfe oder einen benutzerdefinierten Entwurf entwickeln, der den Anforderungen Ihrer Umgebung entspricht:  
  
-   Federated-Web-SSO zur Unterstützung von Business\-zu\-Business \(B2B\) Szenarien und die Zusammenarbeit zwischen Geschäftseinheiten mit unabhängigen Gesamtstrukturen zu unterstützen.  
  
-   Web-SSO zur Unterstützung des Kundenzugriffs auf Anwendungen in Unternehmen\-zu\-Consumer \(B2C\) Szenarien  
  
Sie finden zu jedem Entwurf Richtlinien für das Erfassen der erforderlichen Daten zu Ihrer Umgebung. Sie können diese Richtlinien dann verwenden, zum Planen und Entwerfen von AD FS-Bereitstellung. Nachdem Sie dieses Handbuch gelesen und abgeschlossen haben, sammeln, dokumentieren und Zuordnen der Anforderungen Ihrer Organisation, die erforderlichen Informationen zum Bereitstellen von AD FS mithilfe der Anleitungen im haben die [Windows Server 2012 AD FS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md).  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung  
  
-   [Identifizieren der AD FS-Bereitstellungsziele](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [Planen Ihrer Bereitstellung](Planning-Your-Deployment.md)  
  
-   [Planen der Verbundserverplatzierung](Planning-Federation-Server-Placement.md)  
  
-   [Planen der Verbundserverproxy-Platzierung](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [Planen der AD FS-Serverkapazität](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [Anhang A: Überprüfen der AD FS-Anforderungen](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

