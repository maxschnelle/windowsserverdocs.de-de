---
ms.assetid: c81b8291-fba5-4b30-a43d-7feb2f4b66be
title: AD FS-Entwurfshandbuch in Windows Server2012 R2
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f618add4c4803142b3bd7278908834a412f30999
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="identify-your-ad-fs-deployment-goals"></a>Identifizieren der AD FS-Bereitstellungsziele

>Gilt für: Windows Server 2016, Windows Server2012 R2

Korrekt Identifizieren der Bereitstellungsziele für Active Directory Federation Services \(AD FS\) ist entscheidend für den Erfolg Ihrer AD FS-Entwurfsprojekts. Priorisieren Sie und kombinieren Sie die Bereitstellungsziele und, so, dass Sie entwerfen und Bereitstellen von AD FS mit einem iterativen Ansatz können. Sie können die Vorteile der bestehenden nutzen, dokumentiert und vordefinierte AD FS-Bereitstellungsziele, die für die AD FS-Entwürfe relevant sind und eine funktionierende Lösung für Ihre Situation entwickeln.  
  
In früheren Versionen von AD FS wurden am häufigsten bereitgestellt, um Folgendes zu erreichen:  
  
-   Bereitstellung Mitarbeiter oder Kunden mit einer webbasierten benutzerumgebung beim Zugriff auf Claims\-basierte Anwendungen in Ihrem Unternehmen.  
  
-   Bereitstellen von Mitarbeiter oder Kunden mit einer webbasierten, benutzerumgebung Zugriff auf Ressourcen in beliebigen verbundpartnerorganisationen.  
  
-   Bereitstellung Mitarbeiter oder Kunden mit einer webbasierten benutzerumgebung beim Remotezugriff auf intern Websites oder Dienste gehostet.  
  
-   Bereitstellen von Mitarbeiter oder Kunden mit einem webbasierten, SSO-Funktionen beim Zugriff auf Ressourcen oder Dienste in der Cloud.  
  
Zusätzlich zu diesen funktionell AD FS unter Windows Server® 2012 R2, mit denen Sie Folgendes erreichen können:  
  
-   Gerätearbeitsplatzbeitritt für SSO und nahtlose-Factor Authentication. Dadurch können Organisationen den Zugriff von persönlichen Geräten des Benutzers und verwalten das Risiko, dass bei der Bereitstellung dieses Zugriffs.  
  
-   Verwalten von Risiken mit Multithread-Factor Access Control. AD FS bietet eine umfassende Autorisierung, die steuert, wer Zugriff auf welche Anwendungen hat. Dies kann auf Benutzerattributen basieren \ (UPN, e-Mail, Mitgliedschaft in Sicherheitsgruppen, Authentifizierungsstärke usw. \), Geräteattribute \ (gibt an, ob das Gerät dem Arbeitsplatz Joined\ ist) oder anforderungsattributen \ (Netzwerk-Standort, IP-Adresse oder Benutzer Agent\).  
  
-   Verwalten von Risiken mit zusätzlicher Multithread-Faktor-Authentifizierung für sensible Anwendungen. AD FS können Sie steuern, Richtlinien, um potenziell Multithread-Faktor-Authentifizierung global oder für einzelne Anwendung erforderlich ist. Darüber hinaus bietet AD FS Erweiterungspunkte für beliebige Multithread-Factor Authentication-Anbieter tief für einen sicheren und nahtlosen Multithread-Faktor-Erfahrung für Endbenutzer zu integrieren.  
  
-   Bereitstellen von Funktionen zur Authentifizierung und Autorisierung für den Zugriff auf Webressourcen über das extranet, die durch den Webanwendungsproxy geschützt sind.  
  
Zusammenfassend lässt sich sagen, kann AD FS unter Windows Server 2012 R2 bereitgestellt werden, um die folgenden Ziele in Ihrer Organisation zu erreichen:  
  
### <a name="enable-your-users-to-access-resources-on-their-personal-devices-from-anywhere"></a>Aktivieren Sie die Benutzer Zugriff auf Ressourcen in ihren persönlichen Geräten überall  
  
-   Arbeitsplatzbeitritt, die Benutzern auf ihren persönlichen Geräten zu Active Directory des Unternehmens und daher erhalten Zugriff und nahtlos, wenn Sie auf Unternehmensressourcen von diesen Geräten zugreifen.  
  
-   Registrierungseintragswert-Authentifizierung von Ressourcen innerhalb des Unternehmensnetzwerks, die vom webanwendungsproxy geschützt und aus dem Internet zugegriffen werden.  
  
-   Kennwort ändern, damit Benutzer von jedem mit dem Arbeitsplatz verbundenen Gerät ihr Kennwort ändern, wenn ihr Kennwort abgelaufen ist, damit sie den Zugriff auf Ressourcen fortgesetzt werden können.  
  
### <a name="enhance-your-access-control-risk-management-tools"></a>Verbessern Sie Ihre Zugriff Steuerelement Risiko-Management-tools  
Verwalten von Risiken ist ein wichtiger Aspekt der Governance und Compliance in jeder IT-Organisation. Es gibt zahlreiche Zugriffskontrolle risikomanagementverbesserungen in AD FS unter Windows Server® 2012 R2, u. a. folgende:  
  
-   Flexible Kontrolle auf Grundlage des Netzwerkstandorts, um zu steuern, wie ein Benutzer authentifiziert, um eine AD-FS\-gesicherte Anwendung zuzugreifen.  
  
-   Flexible Richtlinien, um festzustellen, ob ein Benutzer Multithread-Faktor-Authentifizierung auf Basis der Daten des Benutzers, Gerätedaten und Netzwerkstandort durchführen muss.  
  
-   Per\-Anwendung-Steuerelement, um SSO zu ignorieren und der Benutzer bei jedem Zugriff auf eine vertrauliche Anwendung Anmeldeinformationen anzugeben.  
  
-   Flexible Per\ Anwendung Zugriffsrichtlinie basierend auf Benutzerdaten, Gerätedaten oder Netzwerkstandort.  
  
-   AD FS Extranet Lockout Administratoren ermöglicht den Schutz von Active Directory-Konten vor brute-Force-Angriffen aus dem Internet.  
  
-   Sperrung des Zugriffs für alle dem Arbeitsplatz verbundenen Gerät, die in Active Directory gelöscht oder deaktiviert ist.  
  
### <a name="use-ad-fs-to-enhance-the-sign-in-experience"></a>Verwenden Sie zur Verbesserung der Erfahrung Standardparameter in AD FS  
Im folgenden sind die neuen AD FS-Funktionen in Windows Server® 2012 R2, mit denen Administratoren anpassen und Verbessern der Arbeitsmöglichkeiten Standardparameter in:  
  
-   Einheitliche Anpassung des AD FS-Diensts, in dem die Änderungen einmal vorgenommen und dann automatisch mit dem Rest der AD FS-Verbundserver in einer bestimmten Farm verteilt werden.  
  
-   Aktualisierte Standardparameter in Seiten, die modern Aussehen und automatisch für verschiedene Formfaktoren.  
  
-   Unterstützung für automatisches Fallback auf Forms\ basierende Authentifizierung für Geräte, die der corporate-Domäne angeschlossen sind, aber dennoch verwendet werden, generieren Anforderungen aus dem Unternehmensnetzwerk \(intranet\).  
  
-   Einfache Steuerelemente zum Anpassen der Firmenlogo, Abbildung, Standardlinks für IT-Support, Startseite, Datenschutz.  
  
-   Anpassung beschreibender Meldungen auf den Seiten Standardparameter-in.  
  
-   Anpassung von Webdesigns.  
  
-   Home Realm Discovery \(HRD\) basierend auf organisationssuffixes des Benutzers für verbesserten Datenschutz Partner des Unternehmens.  
  
-   HRD Filterung auf Basis Per\-Anwendung automatisch basierten auf der Anwendung Bereich auswählen.  
  
-   Einmaligen Klick-Fehlerberichterstattung für einfachere IT zur Problembehandlung.  
  
-   Anpassbare Fehlermeldungen.  
  
-   Benutzer-authentifizierungswahl, wenn mehrere Authentifizierungsanbieter verfügbar sind.  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurfshandbuch in Windows Server2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

