---
ms.assetid: c81b8291-fba5-4b30-a43d-7feb2f4b66be
title: kennzeichnen Sie Ihre AD FS Bereitstellungs Ziele.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 3705d9c1e5675c233e91df9b5f1e73f68ce4b34c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945302"
---
# <a name="identify-your-ad-fs-deployment-goals"></a>Identifizieren der AD FS-Bereitstellungsziele

Die korrekte Identifizierung Ihrer Active Directory-Verbunddienste (AD FS) \( AD FS \) Bereitstellungs Ziele ist entscheidend für den Erfolg des AD FS Entwurfsprojekts. Priorisieren Sie die Bereitstellungs Ziele und kombinieren Sie Sie, damit Sie AD FS mit einem iterativen Ansatz entwerfen und bereitstellen können. Sie können vorhandene, dokumentierte und vordefinierte AD FS Bereitstellungs Ziele nutzen, die für die AD FS Entwürfe relevant sind, und eine funktionierende Lösung für Ihre Situation entwickeln.

Frühere Versionen von AD FS wurden am häufigsten bereitgestellt, um Folgendes zu erreichen:

-   Bereitstellung eines webbasierten einmaligen Anmeldens für Ihre Mitarbeiter oder Kunden \- beim Zugriff \- auf Anspruchs basierte Anwendungen in Ihrem Unternehmen.

-   Bereitstellung eines webbasierten einmaligen Anmeldens für Ihre Mitarbeiter oder Kunden \- für den Zugriff auf Ressourcen in beliebigen Verbund Partnerorganisationen.

-   Bereitstellung eines webbasierten einmaligen Anmeldens für Ihre Mitarbeiter oder Kunden \- beim Remote Zugriff auf Intern gehostete Websites oder Dienste.

-   Bereitstellung eines webbasierten einmaligen Anmeldens für Ihre Mitarbeiter oder Kunden \- beim Zugriff auf Ressourcen oder Dienste in der Cloud.

Zusätzlich zu diesen Features bietet AD FS in Windows Server &reg; 2012 R2 Funktionen, mit deren Hilfe Sie Folgendes erreichen können:

-   Gerätearbeitsplatzbeitritt für einmalige Anmeldung und nahtlose zweistufige Authentifizierung. Dies ermöglicht es Organisationen, den Zugriff von persönlichen Geräten des Benutzers zuzulassen und das Risiko bei der Bereitstellung dieses Zugriffs zu verwalten.

-   Verwalten von Risiken mit der mehrstufigen \- Zugriffs Steuerung. AD FS bietet eine umfassende Autorisierung, die steuert, wer Zugriff auf welche Anwendungen hat. Dies kann auf Benutzer Attribut \( -UPN, e-Mail-Adresse, Mitgliedschaft in Sicherheitsgruppen, Authentifizierungs Stärke usw. \) , Geräte Attributen, \( ob es sich um einen Arbeitsplatz Beitritt \) oder einen \( Netzwerk Speicherort, eine IP-Adresse oder einen Benutzer-Agent für Anforderungs Attribute handelt \) .

-   Verwalten von Risiken mit zusätzlicher mehrstufiger \- Authentifizierung für sensible Anwendungen. AD FS ermöglicht es Ihnen, Richtlinien zu steuern, um potenziell eine mehrstufige \- Authentifizierung Global oder pro Anwendung zu erfordern. Außerdem bietet AD FS Erweiterbarkeits Punkte für jeden Multi \- -Factor-Anbieter, um eine nahtlose Integration für Endbenutzer zu gewährleisten \- .

-   Bereitstellen von Authentifizierungs-und Autorisierungs Funktionen für den Zugriff auf Webressourcen, die vom webanwendungsproxy geschützt werden.

Zusammenfassend kann AD FS in Windows Server 2012 R2 bereitgestellt werden, um in Ihrer Organisation die folgenden Ziele zu erreichen:

### <a name="enable-your-users-to-access-resources-on-their-personal-devices-from-anywhere"></a>Ermöglichen Sie Ihren Benutzern, von überall aus auf Ressourcen auf Ihren persönlichen Geräten zuzugreifen.

-   Arbeitsplatzbeitritt, der Benutzern ermöglicht, ihre persönlichen Geräten dem Active Directory des Unternehmens hinzuzufügen, und dann von diesen Geräten aus nahtlos auf Unternehmensressourcen zuzugreifen.

-   \-Vorauthentifizierung von Ressourcen innerhalb des Unternehmensnetzwerks, die durch den webanwendungsproxy geschützt sind und auf die über das Internet zugegriffen wird.

-   Kennwortänderung, damit Benutzer von jedem Gerät aus, dass dem Arbeitsplatz beigetreten ist, ihr Kennwort ändern können, wenn es abgelaufen ist, damit sie weiterhin auf Ressourcen zugreifen können.

### <a name="enhance-your-access-control-risk-management-tools"></a>Verbessern der Zugriffs Steuerungs Tools für die Risiko Verwaltung
Verwalten von Risiken ist ein wichtiger Aspekt der Governance und Compliance in jeder IT-Organisation. In AD FS in Windows Server 2012 R2 gibt es viele Verbesserungen der Zugriffs Steuerungs-Risiko Verwaltung &reg; , einschließlich der folgenden:

-   Flexible Steuerelemente basierend auf der Netzwerkadresse, um zu steuern, wie sich ein Benutzer authentifiziert, um auf eine AD FS \- gesicherte Anwendung zuzugreifen.

-   Flexible Richtlinie, um zu bestimmen, ob ein Benutzer \- die mehrstufige Authentifizierung basierend auf den Daten des Benutzers, den Gerätedaten und dem Netzwerk Speicherort durchführen muss.

-   Hiermit wird pro \- Anwendungssteuerung das einmalige Anmelden ignoriert, und der Benutzer wird gezwungen, bei jedem Zugriff auf eine sensible Anwendung Anmelde Informationen einzugeben.

-   Flexible \- Zugriffsrichtlinien pro Anwendung basierend auf Benutzerdaten, Gerätedaten oder Netzwerkstandort.

-   AD FS Extranet Lockout ermöglicht Administratoren den Schutz von Active Directory-Konten vor böswilligen Angriffen aus dem Internet.

-   Sperrung des Zugriffs für alle Arbeitsplatzbeitrittgeräte, die in Active Directory gelöscht oder deaktiviert werden.

### <a name="use-ad-fs-to-enhance-the-sign-in-experience"></a>Verwenden Sie AD FS, um das Anmeldeverfahren zu verbessern. \-
Im folgenden finden Sie neue AD FS Funktionen in Windows Server &reg; 2012 R2, die es dem Administrator ermöglichen, den Anmeldevorgang anzupassen und zu verbessern \- :

-   Einheitliche Anpassung des AD FS-Diensts, wobei die Änderungen einmal vorgenommen und dann automatisch auf die übrigen AD FS-Verbundserver einer bestimmten Farm verteilt werden.

-   Aktualisierte Anmelde \- Seiten, die modern Aussehen und sich automatisch auf verschiedene Formular Faktoren abstimmen.

-   Unterstützung für automatisches Fall Back auf Formular \- basierte Authentifizierung für Geräte, die nicht mit der Unternehmens Domäne verknüpft sind, aber weiterhin verwendet werden, um Zugriffs Anforderungen innerhalb des Unternehmensnetzwerks zu generieren \( \) .

-   Einfache Steuerelemente zur Anpassung von Firmenlogo, Abbildung, Standardlinks für IT-Support, Startseite, Datenschutz etc.

-   Anpassung der Beschreibungs Meldungen auf den Anmelde \- Seiten.

-   Anpassung von Webdesigns.

-   Die Startbereichs Ermittlung \( \) basiert auf dem Suffix der Organisation des Benutzers, um den Schutz der Partner eines Unternehmens zu verbessern.

-   Die HRD filtert pro \- Anwendung, um automatisch einen Bereich auf der Grundlage der Anwendung auszuwählen.

-   Eine \- Klick-Fehlerberichterstattung für einfachere IT-Problembehandlung.

-   Anpassbare Fehlermeldungen.

-   Authentifizierungswahl durch den Benutzer, wenn mehrere Authentifizierungsanbieter verfügbar sind.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)


