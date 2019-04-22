---
title: Sichern des privilegierten Zugriffs
description: Phasen zum Schützen des privilegierten Zugriffs
ms.prod: windows-server-threshold
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 0d54a94d51a4d1e0a1d28f78ec39bf16bc3d9100
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822011"
---
# <a name="securing-privileged-access"></a>Sichern des privilegierten Zugriffs

>Gilt für: Windows Server

Der Schutz des privilegierten Zugriffs ist ein erster wichtiger Schritt zum Einrichten von Sicherheitsstandards für Geschäftsressourcen in modernen Unternehmen. Die Sicherheit der meisten oder aller Geschäftsressourcen in einer IT-Organisation hängt von der Integrität der privilegierten Konten verwendet, um zu verwalten, verwalten und entwickeln ab. Cyberangreifer häufig Ziel, diese Konten und andere Elemente des privilegierten Zugriffs für den Zugriff auf Daten und Systeme, die mithilfe von Angriffen mit gestohlenen Anmeldeinformationen wie [Pass-the-Hash und Pass-the-Ticket](https://www.microsoft.com/pth).

Schützen des privilegierten Zugriffs gegen entschlossene, müssen Sie einen vollständigen und durchdachten Ansatz, diese Systeme gegen Risiken zu isolieren.

## <a name="what-are-privileged-accounts"></a>Was sind die privilegierten Konten?

Bevor wir erörtern diese sichern können privilegierte Konten zu definieren.

Privilegierte Konten wie Administratoren von Active Directory Domain Services direkten oder indirekten Zugriff auf die meisten oder alle Ressourcen in einer IT-Organisation vornehmen einer Gefährdung dieser Konten eine wichtige geschäftliche Risiko.

## <a name="why-securing-privileged-access-is-important"></a>Warum ist das Sichern des privilegierten Zugriffs wichtig?

Cyberangreifer Zielen auf privilegierten Zugriff auf Systeme, z. B. Active Directory (AD) für den Zugriff auf alle Unternehmen schnell Daten ausgerichtet. Herkömmliche Sicherheitsansätze haben den Schwerpunkt auf das Netzwerk und Firewalls als primärer Sicherheitsbereich, aber die Wirksamkeit der Netzwerksicherheit hat durch zwei Trends wesentlich gemindert wurde:

* Organisationen hosten Daten und Ressourcen außerhalb der herkömmlichen Netzwerkgrenze auf mobilen unternehmensrechnern, Geräten wie Mobiltelefonen und Tablets, cloud Services, und bringen Sie Ihre eigenen Geräte (BYOD)
* Angreifer haben durchweg die Fähigkeit nachgewiesen, dass sie mithilfe von Phishing- und anderen Web- und E-Mail-Angriffen Zugriff auf Arbeitsstationen innerhalb der Netzwerkgrenze erlangt haben.

Diese Faktoren erforderlich machen, erstellen eine moderne Sicherheitsbereich Out-of-Authentifizierung und-Autorisierung Identity-Steuerelemente, zusätzlich zu der herkömmlichen Netzwerk Umkreis-Strategie. Hier ein Sicherheitsbereich wird als ein konsistenter Satz von Steuerelementen zwischen Ressourcen und die Gefahren für sie definiert. Privilegierte Konten sind effektiv Kontrolle über diese neuen Sicherheitsbereich zu betrachten, daher ist es wichtig, den privilegierten Zugriff zu schützen.

![Diagramm, das die Identitätsebene einer Organisation zeigt](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

Ein Angreifer, der die Kontrolle über ein Administratorkonto erlangt, kann diese Berechtigungen verwenden, um die Auswirkungen der Zielorganisation zu erhöhen, wie unten dargestellt:

![Diagramm, das zeigt, wie ein Widersacher, der die Kontrolle über ein Administratorkonto erlangt, die dazugehörigen Berechtigungen zum Nachteil der Zielorganisation nutzen kann](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

Die folgende Abbildung zeigt zwei Pfade:

* Ein "blue" Pfad, in denen ein Standardbenutzerkonto für nicht privilegierten Zugriff auf Ressourcen wie e-Mail und Webbrowsen und die tägliche Arbeit verwendet wird, werden ausgeführt.

   > [!NOTE]
   > Blaue Pfad-Elemente, die später beschrieben anzugeben, umfassende environmental Schutzmaßnahmen, die über den Administratorkonten hinausgehen.

* Ein "Rot" Pfad, in die privilegierten Zugriff auf einem Gerät mit verstärkter Sicherheit, um das Risiko von Phishing und anderen Web- und e-Mail-Angriffen zu verringern auftritt.

![Diagramm der separaten "Path" für die Verwaltung, die dieser Anleitung eingerichtet zum Isolieren der Aufgaben, die privilegierten Zugriff von standardmäßigen Benutzeraufgaben hohem Risiko wird wie Websuchen und e-Mail-Zugriff](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>Roadmap für privilegierten Zugriff schützen

Die Roadmap dient zur Maximierung der Verwendung von Microsoft-Technologien, die Sie bereits bereitgestellt haben, nutzen Sie cloudtechnologien, um die Sicherheit zu verbessern, und integrieren alle 3. Sicherheitstools anderer Anbieter, die Sie möglicherweise bereits bereitgestellt haben.

Die Empfehlungen von Microsoft-Roadmap ist in 3 Phasen unterteilt:

* [Phase 1: 30 Tage]()
   * Schnelle, gewinnen mit aussagekräftigen positive Auswirkung.
* [Phase 2: 90 Tage]()
   * Signifikante inkrementelle Verbesserungen.
* [Phase 3: Ongoing]()
   * Verbesserung der Sicherheit und Sustainment.

Der Leitfaden ist so priorisiert, dass basierend auf unseren Erfahrungen mit diesen Angriffen und der Umsetzung von Lösungen die wirkungsvollsten und schnellen Umsetzungen zuerst geplant werden. 

Microsoft empfiehlt das Befolgen dieses Leitfadens zum Schützen des privilegierten Zugriffs gegen entschlossene Angreifer. Sie können diesen Leitfaden entsprechend Ihren vorhandenen Möglichkeiten und spezifischen Anforderungen in Ihren Abteilungen anpassen.

> [!NOTE]
> Der Schutz des privilegierten Zugriffs erfordert eine Vielzahl von Elementen, wie z. B. technische Komponenten (Schutzmaßnahmen für Hosts und Konten, Identitätsverwaltung usw.), sowie Änderungen an Prozessen, Verwaltungsabläufen und Kenntnissen. Die Zeitangaben in diesem Leitfaden sind Näherungswerte und basieren auf unserer Erfahrung mit Kundenlösungen. Je nach Komplexität Ihrer Umgebung und Ihren Änderungsmanagementprozessen variiert die Dauer in Ihrer Organisation.

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>Phase 1: Schnelle, gewinnen mit minimaler Komplexität des Betriebs

Phase 1 der Roadmap konzentriert sich auf das rasche abwehren der am häufigsten verwendeten Angriffsstrategien Diebstahl von Anmeldeinformationen und Missbrauch. Phase 1 soll in ungefähr 30 Tage implementiert werden und wird in diesem Diagramm dargestellt:

![Phase 1-Diagramm: 1. Separate Administratoren und Benutzer-Konto, 2. Just-in-Time lokale Administratorkennwörter, 3. Admin-Arbeitsstation Phase 1, 4. Identität angriffserkennung](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1. Separate Konten

Können Sie das Trennen von Internetrisiken (Phishing-Angriffen, Browsen im Web) von privilegierten Konten zugreifen kann, erstellen Sie ein dediziertes Konto für alle Mitarbeiter mit privilegiertem Zugriff. Administratoren sollten nicht im Web durchsuchen werden, überprüfen ihre e-Mail-Adresse und Produktivität für tägliche Aufgaben ausgeführt werden mit höher privilegierten Konten. Weitere Informationen hierzu finden Sie im Abschnitt [Trennen von Administratorkonten](securing-privileged-access-reference-material.md#separate-administrative-accounts) von ist das Referenzdokument.

Befolgen Sie die Anweisungen im Artikel [verwalten notfallzugriffs-Konten in Azure AD](/azure/active-directory/users-groups-roles/directory-emergency-access) zum Erstellen von mindestens zwei notfallzugriffs-Konten, mit dauerhaft zugewiesenen Administratorrechten, sowohl Ihre lokalen AD und Azure AD Umgebungen . Diese Konten sind nur für die Verwendung bei der herkömmlichen Administratorkonten nicht zum Ausführen einer erforderlichen Aufgabe z. B. in können eine im Fall eines Notfalls.

### <a name="2-just-in-time-local-admin-passwords"></a>2. Just-in-Time-Kennwörtern für lokale Administratoren

Zum Minimieren des Risikos eines Angreifers auf andere Computer missbraucht einen lokaler Administrator-Konto-Kennworthash aus der lokalen SAM-Datenbank stehlen und Administratorkontokennworts sollten Organisationen sicherstellen, dass auf jedem Computer ein eindeutiger lokaler Administrator-Kennwort ist. Kann das Tool lokale Administrator Password Solution (LAPS) eindeutige zufällig generierte Kennwörter konfigurieren, auf jeder Arbeitsstation und Server speichern in Active Directory (AD) durch eine ACL geschützt. Nur berechtigte autorisierte Benutzer lesen oder das Zurücksetzen der diese Kennwörter des lokalen Administratorkontos anfordern. Sie erhalten die LAPS für die Verwendung auf Arbeitsstationen und Server von [im Microsoft Download Center](http://Aka.ms/LAPS).

Zusätzliche Hinweise zum Betreiben einer Umgebung mit LAPS und PAWs finden Sie im Abschnitt [betriebliche Standards basierend auf dem Prinzip der vertrauenswürdigen Quelle](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle).

### <a name="3-administrative-workstations"></a>3. Arbeitsstationen für Administratoren

Als erste Sicherheitsmaßnahme für Benutzer mit Azure Active Directory und herkömmlichen lokalen Active Directory-Administratorrechten, sicher, dass sie Windows 10-Geräte mit konfiguriert die [Standards für die eine äußerst sichere Windows 10-Gerät](/windows-hardware/design/device-experiences/oem-highly-secure). 

### <a name="4-identity-attack-detection"></a>4. Identität angriffserkennung

[Azure Advanced Threat Protection (ATP)](/azure-advanced-threat-protection/what-is-atp) ist untersuchen eine cloudbasierten sicherheitslösung, die identifiziert, erkennt und hilft Ihnen, Bedrohungen, die gefährdete Identitäten und böswillige Insider-Aktionen richtet sich an Ihrem lokalen Active Directory-Umgebung.

## <a name="phase-2-significant-incremental-improvements"></a>Phase 2: Inkrementelle Verbesserungen, die erhebliche

Phase 2 baut auf der Arbeit in Phase 1 und soll in ungefähr 90 Tagen abgeschlossen werden. In diesem Diagramm sind die Schritte in dieser Phase dargestellt:

![Diagramm für Phase 2: 1. Windows Hello für Unternehmen / MFA, 2. PAW-3-Rollouts. Just-in-Time-Berechtigungen, 4. Credential Guard, 5. Kompromittierte Anmeldeinformationen, 6. Lateral Movement-Erkennung von Sicherheitslücken](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1. Windows Hello for Business und MFA erforderlich

Administratoren können von der benutzerfreundlichkeit in Windows Hello for Business verknüpft ist, profitieren. Administratoren können ihre komplexe Kennwörter durch starke zweistufige Authentifizierung auf Ihren eigenen Computern ersetzen. Ein Angreifer muss das Gerät und an die biometrische Informationen oder die PIN, es ist sehr viel schwieriger für den Zugriff des Mitarbeiters mit Kenntnis. Weitere Informationen zu Windows Hello for Business und den Pfad zur Einführung finden Sie im Artikel [Windows Hello for Business – Übersicht](/windows/security/identity-protection/hello-for-business/hello-overview)

Aktivieren Sie Multi-Factor Authentication (MFA) für Ihre Administratorkonten in Azure AD mithilfe von Azure MFA. Auf mindestens aktivieren die [Baseline-Schutzrichtlinie für den bedingten Zugriff](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins) Weitere Informationen zu Azure Multi-Factor Authentication finden Sie im Artikel [Bereitstellen von Cloud-basierten Azure Multi-Factor Authentication](/azure/active-directory/authentication/howto-mfa-getstarted)

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2. Bereitstellen von PAWS für alle privilegierten Identitäten Zugriff Kontoinhaber

Den Prozess des Trennens von privilegierter Konten vor Bedrohungen, die in e-Mail-Adresse, Browsen im Web und andere nicht administrative Aufgaben finden Sie den Vorgang fortsetzen, sollten Sie dedizierte Privileged Access Workstations (PAW) für alle Mitarbeiter mit privilegiertem Zugriff zum Implementieren Ihrer Informationssystemen der Organisation. Weitere Anleitungen für die PAW-Bereitstellung finden Sie im Artikel [Privileged Access Workstations](privileged-access-workstations.md#paw-phased-implementation).

### <a name="3-just-in-time-privileges"></a>3. Just-in-Time-Berechtigungen

Um die offenlegungszeit von Berechtigungen, und steigern Einblick in die Verwendung, bieten Sie Privilegien Just-in-Time (JIT) über eine geeignete Lösung wie die folgenden oder andere Lösungen von Drittanbietern:

* Verwenden Sie für Active Directory Domain Services (AD DS) die Funktion [Privileged Access Manager (PAM)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) von Microsoft Identity Manager (MIM).
* Verwenden Sie für Azure Active Directory die Funktion [Azure AD Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) .

### <a name="4-enable-windows-defender-credential-guard"></a>4. Aktivieren von Windows Defender Credential Guard

Aktivieren Credential Guard schützt NTLM-Kennworthashes, Kerberos Ticket Granting Tickets und Anmeldeinformationen, die von Anwendungen als Anmeldeinformationen für die Domäne gespeichert. Dadurch wird verhindert, dass anmeldeinformationsdiebstahls, wie z. B. Pass-the-Hash- oder Pass-The-Ticket durch Erhöhen der Schwierigkeit in der Umgebung mit gestohlenen Anmeldeinformationen pivotieren. Informationen zur Funktionsweise von Credential Guard und Bereitstellen von finden Sie im Artikel [schützen abgeleiteter Domänenanmeldeinformationen mit Windows Defender Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard).

### <a name="5-leaked-credentials-reporting"></a>5. Kompromittierte Anmeldeinformationen, die berichterstellung

"Täglich, analysiert Microsoft über 6.5 Billionen Signale, um neue Bedrohungen identifizieren und schützen Sie Kunden" - [Microsoft durch die Zahlen](https://news.microsoft.com/bythenumbers/cyber-attacks)

Aktivieren Sie Microsoft Azure AD Identity Protection, um Benutzer mit kompromittierten Anmeldeinformationen zu melden, damit Sie sie beheben können. [Azure AD Identity Protection](/azure/active-directory/identity-protection/index) genutzt werden kann, um Hilfe von Ihrer Organisation, die Cloud-und hybridumgebungen vor Bedrohungen zu schützen.

### <a name="6-azure-atp-lateral-movement-paths"></a>6. Azure ATP-Lateral-Movement-Pfade

Sicherstellen von privilegierten Zugriffskonto Platzhalter verwenden ihre PAW für die Verwaltung, so dass eine kompromittierte nicht privilegierte Konten auf ein privilegiertes Konto über anmeldeinformationsdiebstahls, wie z. B. Pass-the-Hash- oder Pass-The-Ticket zugreifen können. [Azure-ATP, Lateral-Movement-Pfade (LMPs)](/azure-advanced-threat-protection/use-case-lateral-movement-path) bietet einfach um zu verstehen, um zu identifizieren, in dem privilegierte Konten kompromittieren Öffnen möglicherweise reporting.

## <a name="phase-3-security-improvement-and-sustainment"></a>Phase 3: Verbesserung der Sicherheit und sustainment

Phase 3 des Leitfadens baut auf der Schritte in den Phasen 1 und 2 zum Ihren Sicherheitsstatus zu verbessern. Phase 3 ist in diesem Diagramm visuell dargestellt:

![Phase 3: 1. Review RBAC, 2. Reduzieren Sie Attack Surfaces 3. Integrieren von Protokollen mit SIEM, 4. Automatisierung mit kompromittierten Anmeldeinformationen](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

Diese Funktionen zu den Schritten aus vorherigen Phasen erstellt und verschieben Sie die Sicherheit in eine proaktivere Sicherheitslage. Diese Phase ist keine bestimmte Zeitachse und dauert möglicherweise länger, implementieren Sie basierend auf Ihrem Unternehmen.

### <a name="1-review-role-based-access-control"></a>1. Überprüfen Sie die rollenbasierte Zugriffssteuerung

Anhand der drei mehrstufigen Modells in diesem Artikel beschriebenen [Active Directory-verwaltungsebenenmodell](securing-privileged-access-reference-material.md), überprüfen Sie, und stellen Sie sicher, niedrigere Tarif Administratoren haben keinen administrativen Zugriff auf Ressourcen auf höheren Ebenen (Gruppenmitgliedschaften, ACLs für Benutzerkonten usw....).

### <a name="2-reduce-attack-surfaces"></a>2. Reduzieren von angriffsoberflächen

Schützen Ihre Identität Workloads, einschließlich Domänen, Domänencontroller, AD FS und Azure AD Connect als eine dieser Systeme beeinträchtigen könnten dazu führen, Gefährdung anderer Systeme in Ihrer Organisation. Die Artikel [die Active Directory-Angriffsfläche verkleinern](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md) und [fünf Schritte zum Sichern Ihrer Identitätsinfrastruktur](/azure/security/azure-ad-secure-steps) bieten eine Anleitung zum Sichern von lokalen und hybride Identität-Umgebungen.

### <a name="3-integrate-logs-with-siem"></a>3. Integrieren von Protokollen in SIEM-System

Integrieren von Protokollierung in einem zentralisierten SIEM-Tool können sich auf Ihrer Organisation analysieren, zu erkennen und reagieren auf Sicherheitsereignisse aus. Die Artikel [Überwachen von Active Directory signiert der Gefährdung](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md) und [Anhang L: Zu überwachende Ereignisse](../ad-ds/plan/appendix-l--events-to-monitor.md) bieten eine Anleitung für Ereignisse, die in Ihrer Umgebung überwacht werden soll.

Dies ist Teil der abgesehen von den plan aggregieren, erstellen und Optimieren von Warnungen in einem und sicherheitsverwaltung (SIEM) erfordert erfahrene Analysten (im Gegensatz zu Azure ATP in einem 30-Tage-Plan aus dem Feld Warnungen enthält)

### <a name="4-leaked-credentials---force-password-reset"></a>4. Kompromittierte Anmeldeinformationen – das Zurücksetzen des Kennworts erzwingen

Weiter verbessern, Ihren Sicherheitsstatus durch Aktivieren der Azure AD Identity Protection das Zurücksetzen von Kennwörtern automatisch zu erzwingen, wenn die Kennwörter der Gefährdung verdächtigt werden. Die Anleitung finden Sie im Artikel [verwenden Risikoereignisse, die Multi-Factor Authentication-Trigger und der kennwortänderungen](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa) wird erläutert, wie dies mithilfe einer Richtlinie für bedingten Zugriff zu ermöglichen.

## <a name="am-i-done"></a>Fertig?

Die Antwort ist keine.

Die Bösewichte nicht beenden, daher können Sie. Roadmap für die diese unterstützen Ihre Organisation, die Schutz vor Bedrohungen derzeit bekannt, da Angreifern ständig weiterentwickelt und verschoben werden. Es wird empfohlen, dass Sie die Sicherheit als laufenden Prozess mit Schwerpunkt auf die Kosten steigen und die Erfolgsquote der Angreifer, die für Ihre Umgebung anzeigen.

Es ist zwar nicht der einzige Teil Ihrer Organisation Sicherheitsprogramms Sichern des privilegierten Zugriffs ist eine wichtige Komponente Ihrer Sicherheitsstrategie.
