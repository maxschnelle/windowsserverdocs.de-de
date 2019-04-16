---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: Windows Server2012 AD FS-Bereitstellungshandbuch
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3e555d1003878e12320cb8557bd205ac24e1bbb3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server2012 AD FS-Bereitstellungshandbuch

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können Active Directory® Federation Services \(AD FS\) mit dem Betriebssystem Windows Server® 2012 um Verbund-identitätsverwaltungslösung zu erstellen, die verteilten identifizierungs-, Authentifizierung und Autorisierungsdienste auf webbasierte Anwendungen über Organisation- und Plattformgrenzen erstreckt. Durch die Bereitstellung von AD FS können Sie die vorhandenen Identitätsverwaltungsfunktionen Ihrer Organisation auf dem Internet erweitern.  
  
Sie können AD FS bereitstellen:  
  
-   Bieten Sie Mitarbeiter oder Kunden mit einem webbasierten, Singlethread-Standardparameter auf \(SSO\) Erfahrung beim Remotezugriff auf intern gehostete Websites oder Diensten erforderlich.  
  
-   Bieten Sie Ihre Mitarbeiter oder Kunden mit einer webbasierten, SSO-Funktionen, beim Zugriff auf Cross\ organisationsübergreifende Websites oder Diensten innerhalb der Firewalls Ihres Netzwerks.  
  
-   Bieten Sie Mitarbeiter oder Kunden nahtlosen Zugriff auf webbasierte Ressourcen in einer beliebigen verbundpartnerorganisation im Internet, ohne dass Mitarbeiter oder Kunden sich mehr als einmal anmelden.  
  
-   Behalten Sie die vollständige Kontrolle über Mitarbeiter- oder Kundenidentitäten ohne Verwendung von anderen Anbietern Standardparameter auf \ (Windows Live ID, Liberty Alliance und Others\).  
  
## <a name="about-this-guide"></a>Informationen zum Handbuch  
Dieses Handbuch ist für die Verwendung von Systemadministratoren und System Engineers vorgesehen. Es bietet eine detaillierte Anleitung zum Bereitstellen eines AD FS-Entwurfs, das von Ihnen oder einem infrastrukturspezialisten oder einem Systemarchitekten in Ihrem Unternehmen vorausgewählt wurde.  
  
Wenn Sie noch keinen Entwurf ausgewählt wurde, wird empfohlen, Sie warten, bis die Anweisungen in diesem Handbuch bis befolgen, wenn Sie die Entwurfsoptionen im geprüft haben die [AD FS-Entwurfshandbuch in Windows Server2012](https://technet.microsoft.com/library/dd807036.aspx) und Entwurf am besten für Ihre Organisation ausgewählt haben. Weitere Informationen zur Verwendung dieses Handbuch mit einem Design, das bereits ausgewählt wurde, finden Sie unter [Implementieren Ihrer AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md).  
  
Nach dem Auswählen des Entwurfs im Entwurfshandbuch und dem Zusammentragen der erforderlichen Informationen zu Ansprüchen, Tokentypen, attributspeichern und anderen Elementen können dieser Anleitung Sie Ihre AD FS-Entwurfs in Ihrer Produktionsumgebung bereitstellen. Dieses Handbuch enthält eine schrittweise Anleitung zum Bereitstellen der folgenden primären AD FS-Entwürfe:  
  
-   Web-SSO  
  
-   Federated-Web-SSO  
  
Verwenden Sie die Prüflisten im [Implementieren Ihrer AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md) zu ermitteln, wie sich mit den Anweisungen in diesem Handbuch bestimmten Entwurf bereitstellen. Informationen zu Hardware- und softwareanforderungen für die Bereitstellung von AD FS finden Sie unter der [AnhangA: Überprüfen der AD FS-Anforderungen](https://technet.microsoft.com/library/ff678034.aspx) in AD FS-Entwurfshandbuch.  
  
### <a name="what-this-guide-does-not-provide"></a>Was dieses Handbuch bietet keine  
Dieses Handbuch ist nicht enthalten:  
  
-   Hilfestellung bezüglich wann und wo Sie Verbundservern, Verbundserverproxys oder Webservern in der vorhandenen Netzwerkinfrastruktur zu platzieren. Weitere Informationen hierzu finden Sie unter [Planen der Platzierung des Verbundservers](https://technet.microsoft.com/library/dd807069.aspx) und [Planen der Verbundserverproxy-Platzierung](https://technet.microsoft.com/library/dd807130.aspx) in AD FS-Entwurfshandbuch.  
  
-   Anleitung zur Verwendung der Zertifizierung Behörden \(CAs\) zum Einrichten von AD FS  
  
-   Anweisungen zum Einrichten oder konfigurieren bestimmte webbasierter Anwendungen  
  
-   Richten Sie die Anweisungen, die für das Einrichten einer Testumgebung sind.  
  
-   Informationen zum Anpassen von Verbund-Anmeldebildschirmen, Web.config-Dateien oder die Konfigurationsdatenbank.  
  
## <a name="in-this-guide"></a>In diesem Handbuch  
  
-   [Planen der Bereitstellung von AD FS](Planning-to-Deploy-AD-FS.md)  
  
-   [Implementieren des AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [Prüfliste: Implementieren eines Web-SSO-Entwurfs](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [Konfigurieren von Partnerorganisationen](Configuring-Partner-Organizations.md)  
  
-   [Konfigurieren von Anspruchsregeln](Configuring-Claim-Rules.md)  
  
-   [Bereitstellen von Verbundservern](Deploying-Federation-Servers.md)  
  
-   [Bereitstellen von Verbundserverproxys](Deploying-Federation-Server-Proxies.md)  
  
-   [Interaktion mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)  
