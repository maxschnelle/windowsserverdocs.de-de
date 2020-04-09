---
ms.assetid: c81b8291-fba5-4b30-a43d-7feb2f4b66be
title: AD FS-Entwurfshandbuch in Windows Server 2012 R2
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1bc898ba858cf49a71edcb89b10981d0bc8c1986
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853073"
---
# <a name="identify-your-ad-fs-deployment-goals"></a>Identifizieren der AD FS-Bereitstellungsziele

Die korrekte Identifizierung Ihrer Active Directory-Verbunddienste (AD FS) \(AD FS\) Bereitstellungs Ziele ist entscheidend für den Erfolg Ihres AD FS Entwurfsprojekts. Priorisieren Sie die Bereitstellungs Ziele und kombinieren Sie Sie, damit Sie AD FS mit einem iterativen Ansatz entwerfen und bereitstellen können. Sie können vorhandene, dokumentierte und vordefinierte AD FS Bereitstellungs Ziele nutzen, die für die AD FS Entwürfe relevant sind, und eine funktionierende Lösung für Ihre Situation entwickeln.  
  
Frühere Versionen von AD FS wurden am häufigsten bereitgestellt, um Folgendes zu erreichen:  
  
-   Bereitstellung einer Web\-basierten und einmaligen Anmeldung für Ihre Mitarbeiter oder Kunden beim Zugriff auf Anspruchs\-basierte Anwendungen in Ihrem Unternehmen.  
  
-   Stellen Sie Ihren Mitarbeitern oder Kunden eine Web\-basierte, einmalige SSO-Funktion für den Zugriff auf Ressourcen in einer beliebigen Verbund Partnerorganisation bereit.  
  
-   Bereitstellung einer Web\-basierten und einmaligen Anmeldung für Ihre Mitarbeiter oder Kunden beim Remote Zugriff auf Intern gehostete Websites oder-Dienste.  
  
-   Bereitstellung einer Web\-basierten und einmaligen Anmeldung für Ihre Mitarbeiter oder Kunden beim Zugriff auf Ressourcen oder Dienste in der Cloud.  
  
Zusätzlich zu diesen Features bietet AD FS in Windows Server&reg; 2012 R2 Funktionen, mit deren Hilfe Sie Folgendes erreichen können:  
  
-   Gerätearbeitsplatzbeitritt für einmalige Anmeldung und nahtlose zweistufige Authentifizierung. Dies ermöglicht es Organisationen, den Zugriff von persönlichen Geräten des Benutzers zuzulassen und das Risiko bei der Bereitstellung dieses Zugriffs zu verwalten.  
  
-   Verwalten von Risiken mit der Zugriffs Steuerung für mehrere\-Faktoren. AD FS bietet eine umfassende Autorisierung, die steuert, wer Zugriff auf welche Anwendungen hat. Dies kann auf Benutzer Attributen \(UPN, e-Mail-Adresse, Mitgliedschaft in Sicherheitsgruppen, Authentifizierungs Stärke usw.\), Geräte Attribute \(, ob das Gerät mit dem Arbeitsplatz verknüpft ist\) oder Anforderungs Attribute \(Netzwerkadresse, IP-Adresse oder Benutzer-Agent\).  
  
-   Verwalten von Risiken mit zusätzlicher Multi\-Factor Authentication für sensible Anwendungen. AD FS ermöglicht es Ihnen, Richtlinien zu steuern, um ggf. eine globale Multi\-Faktor-Authentifizierung oder pro Anwendung zu erfordern. Außerdem bietet AD FS Erweiterbarkeits Punkte für alle Anbieter von mehreren\-Faktoren, die eine nahtlose Integration in eine sichere und nahtlose Multi\--Faktor für Endbenutzer ermöglichen.  
  
-   Bereitstellen von Authentifizierungs-und Autorisierungs Funktionen für den Zugriff auf Webressourcen, die vom webanwendungsproxy geschützt werden.  
  
Zusammenfassend kann AD FS in Windows Server 2012 R2 bereitgestellt werden, um in Ihrer Organisation die folgenden Ziele zu erreichen:  
  
### <a name="enable-your-users-to-access-resources-on-their-personal-devices-from-anywhere"></a>Ermöglichen Sie Ihren Benutzern, von überall aus auf Ressourcen auf Ihren persönlichen Geräten zuzugreifen.  
  
-   Arbeitsplatzbeitritt, der Benutzern ermöglicht, ihre persönlichen Geräten dem Active Directory des Unternehmens hinzuzufügen, und dann von diesen Geräten aus nahtlos auf Unternehmensressourcen zuzugreifen.  
  
-   Vorab\-Authentifizierung von Ressourcen innerhalb des Unternehmensnetzwerks, die durch den webanwendungsproxy geschützt sind und auf die über das Internet zugegriffen wird.  
  
-   Kennwortänderung, damit Benutzer von jedem Gerät aus, dass dem Arbeitsplatz beigetreten ist, ihr Kennwort ändern können, wenn es abgelaufen ist, damit sie weiterhin auf Ressourcen zugreifen können.  
  
### <a name="enhance-your-access-control-risk-management-tools"></a>Verbessern der Zugriffs Steuerungs Tools für die Risiko Verwaltung  
Verwalten von Risiken ist ein wichtiger Aspekt der Governance und Compliance in jeder IT-Organisation. Es gibt viele Verbesserungen der Zugriffs Steuerungs-Risikomanagement in AD FS in Windows Server&reg; 2012 R2, einschließlich der folgenden:  
  
-   Flexible Steuerelemente basierend auf der Netzwerkadresse, um zu steuern, wie sich ein Benutzer authentifiziert, um auf eine AD FS\-gesicherte Anwendung zuzugreifen.  
  
-   Flexible Richtlinie, um zu bestimmen, ob ein Benutzer eine Multi\-Factor Authentication auf der Grundlage der Daten des Benutzers, der Gerätedaten und der Netzwerkadresse ausführen muss.  
  
-   Pro\-Anwendungssteuerung, um SSO zu ignorieren und den Benutzer zu zwingen, bei jedem Zugriff auf eine sensible Anwendung Anmelde Informationen einzugeben.  
  
-   Flexibel pro\-Anwendungs Zugriffs Richtlinie basierend auf Benutzerdaten, Gerätedaten oder Netzwerkstandort.  
  
-   AD FS Extranet Lockout ermöglicht Administratoren den Schutz von Active Directory-Konten vor böswilligen Angriffen aus dem Internet.  
  
-   Sperrung des Zugriffs für alle Arbeitsplatzbeitrittgeräte, die in Active Directory gelöscht oder deaktiviert werden.  
  
### <a name="use-ad-fs-to-enhance-the-sign-in-experience"></a>Verwenden Sie AD FS, um die Anmelde\-zu verbessern.  
Im folgenden finden Sie neue AD FS Funktionen in Windows Server&reg; 2012 R2, mit denen Administratoren die Anmelde\-anpassen und verbessern können:  
  
-   Einheitliche Anpassung des AD FS-Diensts, wobei die Änderungen einmal vorgenommen und dann automatisch auf die übrigen AD FS-Verbundserver einer bestimmten Farm verteilt werden.  
  
-   Aktualisierte Anmelde\-auf Seiten, die modern Aussehen und sich automatisch auf verschiedene Formular Faktoren beschränken.  
  
-   Unterstützung für automatisches Fall Back auf Formular\-basierte Authentifizierung für Geräte, die nicht mit der Unternehmens Domäne verknüpft sind, aber weiterhin verwendet werden, um Zugriffs Anforderungen aus dem Unternehmensnetzwerk \(Intranet\)zu generieren.  
  
-   Einfache Steuerelemente zur Anpassung von Firmenlogo, Abbildung, Standardlinks für IT-Support, Startseite, Datenschutz etc.  
  
-   Anpassung der Beschreibungs Meldungen in den Anmelde\-in Seiten.  
  
-   Anpassung von Webdesigns.  
  
-   Die Startbereichs Ermittlung \(HRD\) basierend auf dem Organisations Suffix des Benutzers, um den Schutz der Partner eines Unternehmens zu verbessern.  
  
-   Die HRD filtert pro\-Anwendung, um einen Bereich auf der Grundlage der Anwendung automatisch auszuwählen.  
  
-   Eine\-auf Fehlerberichterstattung für einfachere IT-Problembehandlung klicken.  
  
-   Anpassbare Fehlermeldungen.  
  
-   Authentifizierungswahl durch den Benutzer, wenn mehrere Authentifizierungsanbieter verfügbar sind.  
  
## <a name="see-also"></a>Weitere Informationen  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

