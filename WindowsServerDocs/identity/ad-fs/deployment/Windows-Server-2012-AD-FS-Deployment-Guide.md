---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: Bereitstellungshandbuch für AD FS unter Windows Server 2012
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a995cf956a6416a01f40c468b4e5d339609a6fb7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940854"
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Bereitstellungshandbuch für AD FS unter Windows Server 2012


Sie können Active Directory &reg; \( Verbund Dienste AD FS \) mit dem Betriebssystem Windows Server 2012 verwenden &reg; , um eine Verbund-Identitäts Verwaltungs Lösung zu erstellen, mit der verteilte Identifizierungs-, Authentifizierungs-und Autorisierungs Dienste auf webbasierte \- Anwendungen über Organisation-und Platt Form Grenzen hinweg erweitert werden. Durch Bereitstellen von AD FS können Sie die vorhandenen Identitäts Verwaltungsfunktionen Ihrer Organisation auf das Internet erweitern.

Die Bereitstellung von AD FS ermöglicht Ihnen Folgendes:

-   Stellen Sie Ihren Mitarbeitern oder Kunden ein \- webbasiertes einmaliges Anmelden (SSO) zur Verfügung, \- \- \( \) Wenn Sie Remote Zugriff auf Intern gehostete Websites oder Dienste benötigen.

-   Stellen Sie Ihren Mitarbeitern oder Kunden eine webbasierte, einmalige SSO-Benutzeranmeldung bereit \- , wenn Sie über \- die Firewalls Ihres Netzwerks auf Organisations übergreifende Websites oder Dienste zugreifen.

-   Sorgen Sie für Ihre Mitarbeiter oder Kunden für einen nahtlosen Zugriff auf webbasierte \- Ressourcen in einer beliebigen Verbund Partnerorganisation im Internet, ohne dass sich Mitarbeiter oder Kunden mehr als einmal anmelden müssen.

-   Behalten Sie die komplette Kontrolle über Ihre Mitarbeiter-oder Kunden Identitäten, ohne andere Anmelde \- Anbieter ( \( Windows Live ID, Liberty Alliance usw.) zu verwenden \) .

## <a name="about-this-guide"></a>Über diesen Leitfaden
Dieses Handbuch ist für die Verwendung von Systemadministratoren und System Engineers vorgesehen. Hier finden Sie ausführliche Anleitungen zum Bereitstellen eines AD FS Entwurfs, der von Ihnen oder einem Infrastruktur Spezialisten oder Systemarchitekten in Ihrer Organisation vorab ausgewählt wurde.

Wenn noch kein Entwurf ausgewählt wurde, empfiehlt es sich, die Anweisungen in diesem Handbuch zu befolgen, bis Sie die Entwurfs Optionen im [AD FS Entwurfs Handbuch in Windows Server 2012](../design/ad-fs-design-guide-in-windows-server-2012.md) und den am besten geeigneten Entwurf für Ihre Organisation ausgewählt haben. Weitere Informationen zur Verwendung dieses Handbuchs mit einem bereits ausgewählten Entwurf finden [Sie unter Implementieren des AD FS Entwurfs Plans](Implementing-Your-AD-FS-Design-Plan.md).

Nachdem Sie den Entwurf im Entwurfs Handbuch ausgewählt und die erforderlichen Informationen zu Ansprüchen, Tokentypen, Attribut speichern und anderen Elementen gesammelt haben, können Sie dieses Handbuch verwenden, um den AD FS Entwurf in Ihrer Produktionsumgebung bereitzustellen. Dieses Handbuch enthält die Schritte zum Bereitstellen eines der folgenden primären AD FS-Entwürfe:

-   Web-SSO

-   Federated-Web-SSO

Verwenden Sie die Prüf Listen unter [Implementieren des AD FS Entwurfs Plans](Implementing-Your-AD-FS-Design-Plan.md) , um zu bestimmen, wie die Anweisungen in diesem Handbuch zum Bereitstellen eines bestimmten Entwurfs verwendet werden. Informationen zu Hardware-und Softwareanforderungen für die Bereitstellung von AD FS finden Sie im [Anhang A: Überprüfen von AD FS Anforderungen](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678034(v=ws.11)) im Entwurfs Handbuch für AD FS.

### <a name="what-this-guide-does-not-provide"></a>Nicht in diesem Handbuch enthaltene Informationen
Folgendes ist in diesem Handbuch nicht enthalten:

-   Leitfaden zum Zeitpunkt und zum Platzieren von Verbund Servern, Verbund Server Proxys oder Webservern in Ihrer vorhandenen Netzwerkinfrastruktur. Informationen zu diesen Informationen finden Sie unter Planen der Platzierung des Verbund [Servers](../design/planning-federation-server-placement.md) und Planen der Platzierung des Verbund [Server Proxys](../design/planning-federation-server-proxy-placement.md) im AD FS Entwurfs Handbuch.

-   Leitfaden für die Verwendung von \( Zertifizierungs \) stellen-CAS zum Einrichten von AD FS

-   Leitfaden zum Einrichten oder Konfigurieren bestimmter \- webbasierter Anwendungen

-   Spezifische Anweisungen für das Einrichten einer Testlaborumgebung

-   Informationen zum Anpassen von Verbund-Anmeldebildschirmen, web.config-Dateien oder der Konfigurationsdatenbank

## <a name="in-this-guide"></a>Inhalt dieser Anleitung

-   [Planen der Bereitstellung von AD FS](Planning-to-Deploy-AD-FS.md)

-   [Implementieren des AD FS-Entwurfsplans](Implementing-Your-AD-FS-Design-Plan.md)

-   [Prüfliste: Implementieren eines Web-SSO-Entwurfs](Checklist--Implementing-a-Web-SSO-Design.md)

-   [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](Checklist--Implementing-a-Federated-Web-SSO-Design.md)

-   [Konfigurieren von Partner Organisationen](Configuring-Partner-Organizations.md)

-   [Konfigurieren von Anspruchsregeln](Configuring-Claim-Rules.md)

-   [Bereitstellen von Verbundservern](Deploying-Federation-Servers.md)

-   [Bereitstellen von Verbundserverproxys](Deploying-Federation-Server-Proxies.md)

-   [Interagieren mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)
