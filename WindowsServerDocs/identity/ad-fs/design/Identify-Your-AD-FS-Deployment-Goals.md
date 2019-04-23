---
ms.assetid: c81b8291-fba5-4b30-a43d-7feb2f4b66be
title: AD FS-Entwurfshandbuch in Windows Server 2012 R2
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f618add4c4803142b3bd7278908834a412f30999
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862571"
---
# <a name="identify-your-ad-fs-deployment-goals"></a>Identifizieren der AD FS-Bereitstellungsziele

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Ordnungsgemäße Identifizierung Ihrer Active Directory Federation Services \(AD FS\) -Bereitstellungsziele ist wichtig für den Erfolg Ihres AD FS-Entwurfs-Projekts. Priorisieren Sie und kombinieren Sie die Bereitstellungsziele, damit Sie entwerfen und Bereitstellen von AD FS mit einem iterativen Ansatz. Sie profitieren von vorhandenen, dokumentiert und vordefinierte AD FS-Bereitstellungsziele, die für die AD FS-Entwürfe relevant sind und eine funktionierende Lösung für Ihre Situation entwickeln.  
  
Frühere Versionen von AD FS wurden am häufigsten bereitgestellt, um Folgendes zu erreichen:  
  
-   Bereitstellen der Mitarbeiter oder Kunden mit einem Web\-basieren, SSO auftreten, wenn Ansprüche zugreifen\--basierte Anwendungen in Ihrem Unternehmen.  
  
-   Bereitstellen der Mitarbeiter oder Kunden mit einem Web\-basieren, die SSO-Erfahrung, um den Zugriff auf Ressourcen in beliebigen verbundpartnerorganisationen.  
  
-   Bereitstellen der Mitarbeiter oder Kunden mit einem Web\-basieren, SSO auftreten, wenn Sie Remotezugriff auf intern, Websites oder-Dienste gehostet.  
  
-   Bereitstellen der Mitarbeiter oder Kunden mit einem Web\-benutzerumgebung Einmaliger Anmeldung basiert, für den Zugriff auf Ressourcen oder Dienste in der Cloud.  
  
Zusätzlich zu diesen fügt AD FS unter Windows Server® 2012 R2-Funktionen, die Folgendes kann:  
  
-   Gerätearbeitsplatzbeitritt für einmalige Anmeldung und nahtlose zweistufige Authentifizierung. Dies ermöglicht Organisationen das Zulassen des Zugriffs mit persönlichen Geräten des Benutzers und das Risiko bei der Bereitstellung dieses Zugriffs, verwalten.  
  
-   Verwalten von Risiken mit mehreren\-Zugriffssteuerung berücksichtigen. AD FS bietet eine umfassende Autorisierung, die steuert, wer Zugriff auf welche Anwendungen hat. Dies kann auf Benutzerattributen basieren \(UPN, e-Mail-Adresse, Mitgliedschaft in Sicherheitsgruppen, Authentifizierungsstärke usw.\), Geräteattribute \(gibt an, ob das Gerät dem Arbeitsplatz beigetreten ist\) oder anforderungsattributen \(Speicherort im Netzwerk, IP-Adresse oder Benutzer-Agent\).  
  
-   Verwalten von Risiken mit zusätzlicher Multi\--Factor Authentication für sensible Anwendungen. AD FS können Sie steuern, Richtlinien dahingehend, dass möglicherweise mit mehreren\-zweistufige Authentifizierung bei global oder auf einer Basis pro Anwendung. Darüber hinaus bietet AD FS Erweiterungspunkte für alle Multi\-Faktor Anbieter, der für eine sichere und nahtlose Festlegung tief integrieren\-Erfahrung für Endbenutzer zu berücksichtigen.  
  
-   Authentifizierung und Autorisierung zur Verfügung stehen, für den Zugriff auf Web-Ressourcen aus dem extranet, die vom Webanwendungsproxy geschützt sind.  
  
Zusammenfassend lässt sich sagen, kann AD FS unter Windows Server 2012 R2 bereitgestellt werden, um in Ihrer Organisation die folgenden Ziele zu erreichen:  
  
### <a name="enable-your-users-to-access-resources-on-their-personal-devices-from-anywhere"></a>Ermöglichen Sie Benutzern Zugriff auf Ressourcen in ihren persönlichen Geräten von überall aus  
  
-   Arbeitsplatzbeitritt, der Benutzern ermöglicht, ihre persönlichen Geräten dem Active Directory des Unternehmens hinzuzufügen, und dann von diesen Geräten aus nahtlos auf Unternehmensressourcen zuzugreifen.  
  
-   Vor\-Authentifizierung von Ressourcen innerhalb des Unternehmensnetzwerks, die vom webanwendungsproxy geschützt sind und über das Internet zugegriffen werden.  
  
-   Kennwortänderung, damit Benutzer von jedem Gerät aus, dass dem Arbeitsplatz beigetreten ist, ihr Kennwort ändern können, wenn es abgelaufen ist, damit sie weiterhin auf Ressourcen zugreifen können.  
  
### <a name="enhance-your-access-control-risk-management-tools"></a>Verbessern Sie Ihre Access Control Risiko-Verwaltungstools  
Verwalten von Risiken ist ein wichtiger Aspekt der Governance und Compliance in jeder IT-Organisation. Es gibt zahlreiche zugriffssteuerungs-risikomanagementverbesserungen in AD FS unter Windows Server® 2012 R2, einschließlich der folgenden:  
  
-   Flexible Kontrolle auf Grundlage von Netzwerkstandorts, um zu steuern, wie ein Benutzer authentifiziert, für den Zugriff auf einen AD FS\-gesicherte Anwendung.  
  
-   Flexible Richtlinie zu bestimmen, ob ein Benutzer zum Ausführen von mehreren muss\-Faktor-Authentifizierung anhand von Daten des Benutzers, Gerätedaten und Netzwerkstandort.  
  
-   Pro\-anwendungssteuerung SSO zu ignorieren und der Benutzer muss bei jedem Zugriff auf eine vertrauliche Anwendung Anmeldeinformationen anzugeben.  
  
-   Flexible pro\-anwendungszugriffsrichtlinie basierend auf Benutzerdaten, Gerätedaten oder Netzwerkstandort.  
  
-   AD FS Extranet Lockout ermöglicht Administratoren den Schutz von Active Directory-Konten vor böswilligen Angriffen aus dem Internet.  
  
-   Sperrung des Zugriffs für alle Arbeitsplatzbeitrittgeräte, die in Active Directory gelöscht oder deaktiviert werden.  
  
### <a name="use-ad-fs-to-enhance-the-sign-in-experience"></a>Verwenden von AD FS zur Verbesserung der der Vorzeichens\-Erfahrung  
Im folgenden sind die neuen AD FS-Funktionen in Windows Server® 2012 R2, mit denen anpassen und erweitern die SSO-Administrator\-Erfahrung:  
  
-   Einheitliche Anpassung des AD FS-Diensts, wobei die Änderungen einmal vorgenommen und dann automatisch auf die übrigen AD FS-Verbundserver einer bestimmten Farm verteilt werden.  
  
-   Aktualisiert die Anmeldung\-auf Seiten, die modern Aussehen und automatisch für verschiedene Formfaktoren.  
  
-   Unterstützung für automatisches Fallback auf Formulare\--basierte Authentifizierung für Geräte, die nicht der Unternehmensdomäne verknüpft sind, aber dennoch verwendet werden-zugriffsanforderungen von innerhalb des Unternehmensnetzwerks generieren \(Intranet\).  
  
-   Einfache Steuerelemente zur Anpassung von Firmenlogo, Abbildung, Standardlinks für IT-Support, Startseite, Datenschutz etc.  
  
-   Anpassen der Beschreibung in der Nachrichten\-in Seiten.  
  
-   Anpassung von Webdesigns.  
  
-   Home Realm Discovery, HDR \(zur Startbereichsermittlung\) basierend auf organisationssuffixes des Benutzers für verbesserten Datenschutz eines Unternehmens Partner.  
  
-   HRD-Filterung einer pro\-Anwendungsbasis, automatisch einen Bereich auszuwählen, basierend auf der Anwendung.  
  
-   Eine\-klicken Sie auf die Fehlerberichterstattung für einfachere IT zur Problembehandlung.  
  
-   Anpassbare Fehlermeldungen.  
  
-   Authentifizierungswahl durch den Benutzer, wenn mehrere Authentifizierungsanbieter verfügbar sind.  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

