---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: Bereitstellungshandbuch für ADFS unter Windows Server 2012
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3e555d1003878e12320cb8557bd205ac24e1bbb3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882441"
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Bereitstellungshandbuch für ADFS unter Windows Server 2012

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können Active Directory® Federation Services \(AD FS\) mit dem Betriebssystem Windows Server® 2012, um eine Verbund-identitätsverwaltungslösung zu erstellen, die verteilte Identifikation, erweitert-Authentifizierung und Web-Autorisierungsdienste\--basierte Anwendungen über Unternehmens- und plattformübergreifend hinweg. Durch die Bereitstellung von AD FS können Sie die vorhandenen Identitätsverwaltungsfunktionen Ihrer Organisation auf das Internet erweitern.  
  
Die Bereitstellung von AD FS ermöglicht Ihnen Folgendes:  
  
-   Geben Sie Ihre Mitarbeiter oder Kunden mit einem Web\-basieren, einzelne\-anmelden\-auf \(SSO\) Erfahrung bei Bedarf Remotezugriff auf intern gehostete Websites oder-Dienste.  
  
-   Geben Sie Ihre Mitarbeiter oder Kunden mit einem Web\-basieren, SSO auftreten, wenn sie plattformübergreifende zugreifen\-Organisation Websites oder Dienste von Ort diesseits der Firewalls Ihres Netzwerks.  
  
-   Geben Sie Ihre Mitarbeiter oder Kunden reibungslosen Zugriff auf Web\-basierend Ressourcen in einer beliebigen verbundpartnerorganisation im Internet, ohne dass Mitarbeiter oder Kunden sich mehr als einmal anmelden.  
  
-   Behalten Sie vollständige Kontrolle über Mitarbeiter- oder Kundenidentitäten, ohne Verwendung von anderen\-Anbietern \(Windows Live ID, Liberty Alliance usw.\).  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Dieses Handbuch ist für die Verwendung von Systemadministratoren und System Engineers vorgesehen. Es bietet eine detaillierte Anleitung zum Bereitstellen einer AD FS-Entwurfs, der von Ihnen oder einem infrastrukturspezialisten oder einem Systemarchitekten in Ihrem Unternehmen bereits vorausgewählt wurde.  
  
Wenn Sie noch keinen Entwurf ausgewählt wurde, sollten Sie warten, bis Sie die Anweisungen in diesem Handbuch zu befolgen, nachdem Sie die Entwurfsoptionen im gelesen haben die [AD FS-Entwurfshandbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) und die meisten ausgewählt haben entsprechenden Entwurf für Ihre Organisation. Weitere Informationen zur Verwendung dieses Handbuch mit einem Design, das bereits ausgewählt wurde, finden Sie unter [Implementieren Ihrer AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md).  
  
Nach dem Auswählen des Entwurfs im Entwurfshandbuch und die erforderliche Informationen zu Ansprüchen, Tokentypen, attributspeichern und anderen Elementen zu sammeln, können Sie dieses Handbuch verwenden, Ihre AD FS-Entwurfs in Ihrer produktionsumgebung bereitstellen. Dieses Handbuch enthält die Schritte zum Bereitstellen der folgenden primären AD FS-Entwürfe:  
  
-   Web-SSO  
  
-   Federated-Web-SSO  
  
Verwenden Sie die Prüflisten im [Implementieren Ihrer AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md) zu ermitteln, wie sich mit den Anweisungen in diesem Handbuch zum Bereitstellen bestimmten Entwurfs. Weitere Informationen zu Hardware- und softwareanforderungen für die Bereitstellung von AD FS, finden Sie unter den [Anhang A: Überprüfen der AD FS-Anforderungen](https://technet.microsoft.com/library/ff678034.aspx) in der AD FS-Design Guide.  
  
### <a name="what-this-guide-does-not-provide"></a>Nicht in diesem Handbuch enthaltene Informationen  
Folgendes ist in diesem Handbuch nicht enthalten:  
  
-   Die Anleitungen in Bezug auf den Zeitpunkt und Ort für das Platzieren von Verbundservern, Verbundserverproxys oder Web-Server in Ihrer vorhandenen Netzwerkinfrastruktur. Weitere Informationen finden Sie unter [Planen der Verbundserverplatzierung](https://technet.microsoft.com/library/dd807069.aspx) und [Planen der Verbundserverproxy-Platzierung](https://technet.microsoft.com/library/dd807130.aspx) in AD FS-Entwurfshandbuch.  
  
-   Anleitung für die Verwendung von Zertifizierungsstellen \(CAs\) zum Einrichten der AD FS  
  
-   Anleitungen zum Einrichten oder Konfigurieren von bestimmten Web\--basierte Anwendungen  
  
-   Spezifische Anweisungen für das Einrichten einer Testlaborumgebung  
  
-   Informationen zum Anpassen von Verbund-Anmeldebildschirmen, web.config-Dateien oder der Konfigurationsdatenbank  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung  
  
-   [Planen der Bereitstellung von AD FS](Planning-to-Deploy-AD-FS.md)  
  
-   [Implementieren von AD FS Plan entwerfen](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [Prüfliste: Implementieren eines Web-SSO-Entwurfs](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [Konfigurieren von Partnerorganisationen](Configuring-Partner-Organizations.md)  
  
-   [Konfigurieren von Anspruchsregeln](Configuring-Claim-Rules.md)  
  
-   [Bereitstellen von Verbundservern](Deploying-Federation-Servers.md)  
  
-   [Bereitstellen von Verbundserverproxys](Deploying-Federation-Server-Proxies.md)  
  
-   [Interaktion mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)  
