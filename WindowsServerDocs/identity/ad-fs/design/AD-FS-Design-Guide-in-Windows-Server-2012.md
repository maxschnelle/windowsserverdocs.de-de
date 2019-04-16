---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: AD FS-Entwurfshandbuch in Windows Server 2012
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e660c1dabcc5a683fa74068ea148fd4efbeee569
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-design-guide-in-windows-server-2012"></a>AD FS-Entwurfshandbuch in Windows Server 2012

>Gilt für: Windows Server 2012
  
> [!NOTE]  
> Informationen zum Bereitstellen von AD FS unter Windows Server2012 R2 finden Sie unter [Windows Server2012 R2 AD FS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md).  
  
Können Active Directory® Federation Services \(AD FS\) mit dem Betriebssystem Windows Server® 2012 in einer Federation Services Provider Rolle nahtlos authentifizieren Benutzer alle webbasierten Diensten oder Anwendungen, die befinden sich in einer Ressourcenpartnerorganisation übernehmen, ohne dass Administratoren erstellen oder verwalten, externe Vertrauensstellungen oder Gesamtstruktur-Vertrauensstellungen zwischen den Netzwerken beider Organisationen und ohne den Benutzer ein zweites Mal anmelden müssen. Der Vorgang der Authentifizierung mit einem Netzwerk während des Zugriffs auf Ressourcen in einem anderen Netzwerk – ohne den Aufwand wiederholter Anmeldeaktionen durch Benutzer – wird als einzelne Standardparameter auf \(SSO\) bezeichnet.  
  
## <a name="about-this-guide"></a>Informationen zum Handbuch  
Dieses Handbuch enthält Empfehlungen helfen Ihnen beim Planen einer neuen Bereitstellung von AD FS, je nach den Erfordernissen Ihrer Organisation \ (auch in diesem Handbuch als Bereitstellung Goals\ bezeichnet) und des Entwurfs, die Sie erstellen möchten. Dieses Handbuch ist für die Verwendung von einem infrastrukturspezialisten oder einem Systemarchitekten vorgesehen. Lassen sich die wesentlichen Entscheidungspunkte hervorheben, mit denen Sie Ihre AD FS-Bereitstellung planen. Bevor Sie dieses Handbuch lesen, sollten Sie ein gutes Verständnis der Funktionsweise von AD FS auf einer Funktionsebene verfügen. Sie sollten auch einen umfassenden Überblick über die organisatorischen Anforderungen, die widergespiegelt werden verfügen, in der AD FS-Entwurfs.  
  
Dieses Handbuch beschreibt eine Reihe von bereitstellungszielen, die auf drei primären AD FS-Designs basieren, und erleichtert Ihnen die Entscheidung, des am besten geeigneten Designs für Ihre Umgebung. Sie können diesen bereitstellungszielen können Sie einen der folgenden umfassenden AD FS-Entwürfe oder einen benutzerdefinierten Entwurf entwickeln, der den Anforderungen Ihrer Umgebung entspricht:  
  
-   Federated-Web-SSO zur Unterstützung von Business\-zu-Business \(B2B\) und die Zusammenarbeit zwischen Geschäftseinheiten mit unabhängigen Gesamtstrukturen  
  
-   Web-SSO zur Unterstützung des Kundenzugriffs auf Anwendungen in Business\-zu-Consumer \(B2C\) Szenarien  
  
Jedem Entwurf finden Sie Richtlinien für das Erfassen der erforderlichen Daten zu Ihrer Umgebung. Dann können diese Richtlinien zum Planen und Entwerfen Ihrer AD FS-Bereitstellung. Nachdem Sie dieses Handbuch gelesen und erfassen, dokumentieren und Zuordnen der Anforderungen Ihrer Organisation abschließen, müssen Sie die nötigen Informationen zum Bereitstellen von AD FS mithilfe der Anleitungen im beginnen die [Windows Server2012 AD FS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md).  
  
## <a name="in-this-guide"></a>In diesem Handbuch  
  
-   [Identifizieren der AD FS-Bereitstellungsziele](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [Planen der Bereitstellung](Planning-Your-Deployment.md)  
  
-   [Planen der Platzierung des Verbundservers](Planning-Federation-Server-Placement.md)  
  
-   [Planen der Verbundserverproxy-Platzierung](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [Planen der AD FS-Serverkapazität](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [AnhangA: Überprüfen der AD FS-Anforderungen](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

