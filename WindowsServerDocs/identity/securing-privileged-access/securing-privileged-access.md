---
title: Schützen des privilegierten Zugriffs
description: Phasenansatz zum Sichern des privilegierten Zugriffs
ms.prod: windows-server
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 806a2aced95421bd469ba885d4a81c219ae1b651
ms.sourcegitcommit: 457e88e5aa6be13a2bffdb8e434a8efc3698678f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548834"
---
# <a name="securing-privileged-access"></a>Schützen des privilegierten Zugriffs

>Gilt für: Windows Server

Der Schutz des privilegierten Zugriffs ist ein erster wichtiger Schritt zum Einrichten von Sicherheitsstandards für Geschäftsressourcen in modernen Unternehmen. Die Sicherheit der meisten oder aller Geschäftsressourcen in einem IT-Unternehmen hängt von der Integrität der privilegierten Konten ab, die für die Verwaltung und Entwicklung verwendet werden. Cyberangreifer zielen oft auf diese Konten und andere Elemente des privilegierten Zugriffs ab, um sich durch Angriffe zum Diebstahl von Anmeldeinformationen wie [Pass-the-Hash- und Pass-the-Ticket-Angriffe](https://www.microsoft.com/pth) Zugriff auf Daten und Systeme zu verschaffen.

Der Schutz des privilegierten Zugriffs vor entschlossenen Widersachern erfordert einen vollständigen und durchdachten Ansatz, um diese Systeme gegen Risiken zu isolieren.

## <a name="what-are-privileged-accounts"></a>Was sind privilegierte Konten?

Bevor der Schutz dieser Konten behandelt wird, werden privilegierte Konten zunächst definiert.

Privilegierte Konten wie Administratorkonten in Active Directory Domain Services verfügen über direkten oder indirekten Zugriff auf die meisten oder alle Ressourcen in einem IT-Unternehmen, weshalb eine Gefährdung dieser Konten ein großes Geschäftsrisiko darstellt.

## <a name="why-securing-privileged-access-is-important"></a>Warum ist das Schützen des privilegierten Zugriffs wichtig?

Cyberangreifer konzentrieren sich auf den privilegierten Zugriff auf Systeme wie Active Directory, um sich schnell Zugriff auf alle Daten eines Unternehmens zu verschaffen. Herkömmliche Sicherheitsansätze konzentrieren sich auf das Netzwerk und die Firewalls als primären Sicherheitsperimeter, jedoch wurde die Wirksamkeit von Netzwerksicherheitsmaßnahmen durch zwei Trends wesentlich reduziert:

* Organisationen hosten Daten und Ressourcen außerhalb der herkömmlichen Netzwerkbegrenzungen auf mobilen Unternehmenscomputern, auf Geräten wie Mobiltelefonen und Tablets, sowie in Clouddiensten und auf BYOD-Geräten (Bring Your Own Device).
* Angreifer haben durchweg die Fähigkeit nachgewiesen, dass sie mithilfe von Phishing- und anderen Web- und E-Mail-Angriffen Zugriff auf Arbeitsstationen innerhalb der Netzwerkgrenze erlangt haben.

Diese Faktoren erfordern die Erstellung eines modernen Sicherheitsperimeters mithilfe von Identitätskontrollen zur Authentifizierung und Autorisierung zusätzlich zur herkömmlichen Netzwerkbegrenzungsstrategie. Ein Sicherheitsperimeter wird hier als beständige Kontrollen zwischen Ressourcen und Bedrohungen für diese definiert. Privilegierte Konten haben gewissermaßen die Kontrolle über diesen neuen Sicherheitsperimeter, weshalb der privilegierte Zugriff geschützt werden muss.

![Diagramm, das die Identitätsebene einer Organisation zeigt](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

Ein Angreifer, der Kontrolle über ein Administratorkonto erlangt, kann die dazugehörigen Rechte nutzen, um seine Auswirkungen in der Zielorganisation wie folgt zu erhöhen:

![Diagramm, das zeigt, wie ein Widersacher, der die Kontrolle über ein Administratorkonto erlangt, die dazugehörigen Berechtigungen zum Nachteil der Zielorganisation nutzen kann](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

Die folgende Abbildung veranschaulicht zwei Pfade:

* Ein „blauer“ Pfad, bei dem ein Standardbenutzerkonto für nicht privilegierten Zugriff auf Ressourcen wie E-Mail und Webbrowser sowie für die Durchführung alltäglicher Arbeit genutzt wird.

   > [!NOTE]
   > Später beschriebene Elemente des blauen Pfads geben umfassende Umgebungsschutzmechanismen an, die über Administratorkonten hinausgehen.

* Ein „roter“ Pfad, bei dem der privilegierter Zugriff auf einem gehärteten Gerät vorliegt, um das Risiko von Phishing und anderen E-Mail-Angriffen zu reduzieren.

![Diagramm, das den separaten „Pfad“ für die Verwaltung veranschaulicht, der in dieser Anleitung eingerichtet wird, um Aufgaben, die einen privilegierten Zugriff erfordern, von standardmäßigen Benutzeraufgaben mit hohem Risiko wie Webbrowsen und E-Mail-Zugriff zu trennen](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>Roadmap zum Schutz des privilegierten Zugriffs

Diese Roadmap wurde dazu entworfen, den Nutzen Ihrer bereits bereitgestellten Microsoft-Technologien zu maximieren, Cloudtechnologien zur Erweiterung der Sicherheit zu nutzen und Sicherheitstools von Drittanbietern zu integrieren, die Sie möglicherweise bereits bereitgestellt haben.

Die Roadmap mit den Empfehlungen von Microsoft ist in 3 Phasen unterteilt:

* [Phase 1: Die ersten 30 Tage](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-1-quick-wins-with-minimal-operational-complexity)
   * Schnelle Ergebnisse mit bedeutsamen positiven Auswirkungen
* [Phase 2: 90 Tage](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-2-significant-incremental-improvements)
   * Bedeutende inkrementelle Verbesserungen
* [Phase 3: Fortlaufend](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-3-security-improvement-and-sustainment)
   * Verbesserung und Aufrechterhaltung der Sicherheit

Der Leitfaden ist so priorisiert, dass basierend auf unseren Erfahrungen mit diesen Angriffen und der Umsetzung von Lösungen die wirkungsvollsten und schnellen Umsetzungen zuerst geplant werden. 

Microsoft empfiehlt das Befolgen dieses Leitfadens zum Schützen des privilegierten Zugriffs gegen entschlossene Angreifer. Sie können diesen Leitfaden entsprechend Ihren vorhandenen Möglichkeiten und spezifischen Anforderungen in Ihren Abteilungen anpassen.

> [!NOTE]
> Der Schutz des privilegierten Zugriffs erfordert eine Vielzahl von Elementen, wie z. B. technische Komponenten (Schutzmaßnahmen für Hosts und Konten, Identitätsverwaltung usw.), sowie Änderungen an Prozessen, Verwaltungsabläufen und Kenntnissen. Die Zeitangaben in diesem Leitfaden sind Näherungswerte und basieren auf unserer Erfahrung mit Kundenlösungen. Je nach Komplexität Ihrer Umgebung und Ihren Änderungsmanagementprozessen variiert die Dauer in Ihrer Organisation.

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>Phase 1: Schnelle Ergebnisse mit minimaler Komplexität des Betriebs

Phase 1 der Roadmap konzentriert sich auf das rasche Abwehren der gängigsten Angriffsstrategien: Diebstahl und Missbrauch von Anmeldeinformationen. Phase 1 soll innerhalb von 30 Tagen implementiert werden und wird in der folgenden Abbildung veranschaulicht:

![Diagramm zu Phase 1: 1. Aufteilen von Administrator- und Benutzerkonten, 2. lokale Just-In-Time-Administratorkennwörter, 3. Phase 1 der Administratorworkstation, 4. Erkennung von Identitätsangriffen](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1. Aufteilen der Konten

Erstellen Sie ein dediziertes Konto für alle Mitarbeiter mit privilegiertem Zugriff, um Internetrisiken (Phishingangriffe, Webbrowsen) von privilegierten Zugriffskonten zu trennen. Administratoren sollten nicht mit privilegierten Konten im Web browsen, ihre E-Mails überprüfen oder alltägliche Aufgaben durchführen. Weitere Informationen hierzu finden Sie im Abschnitt [Trennen von Administratorkonten](securing-privileged-access-reference-material.md#separate-administrative-accounts) im Referenzdokument.

Führen Sie die Anweisungen im Artikel [Verwalten von Konten für den Notfallzugriff in Azure AD](/azure/active-directory/users-groups-roles/directory-emergency-access) aus, um mindestens zwei Konten für den Notfallzugriff mit dauerhaft zugewiesenen Administratorrechten für Ihre lokalen AD- und Ihre Azure AD-Umgebungen zu erstellen. Diese Konten sind nur zur Verwendung vorgesehen, wenn herkömmliche Administratorkonten eine erforderliche Aufgabe nicht durchführen können, z. B. in einer Notfallsituation.

### <a name="2-just-in-time-local-admin-passwords"></a>2. Lokale Just-In-Time-Administratorkennwörter

Unternehmen sollten sicherstellen, dass jeder Computer über ein eindeutiges lokales Administratorkennwort verfügt, um das Risiko des Diebstahls eines Kennworthashs eines lokalen Administratorkontos aus der lokalen SAM-Datenbank und die Ausnutzung für den Angriff weiterer Computer durch einen Widersacher zu verhindern. Das LAPS-Tool (Local Administrator Password Solution) kann einzigartige zufällige Kennwörter für jede Workstation und jeden Server konfigurieren und diese in Active Directory mit Schutz durch eine Zugriffssteuerungsliste (ACL) speichern. Nur zulässige autorisierte Benutzer können die Zurücksetzung dieser Kennwörter für lokale Administratorkonten anzeigen oder anfordern. Das LAPS-Tool zur Verwendung auf Workstations und Server finden Sie im [Microsoft Download Center](https://aka.ms/LAPS).

Weitere Anweisungen für den Betrieb einer Umgebung mit LAPS und Workstations mit privilegiertem Zugriff finden Sie im Abschnitt [Prinzip der vertrauenswürdigen Quelle für betriebliche Standards](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle).

### <a name="3-administrative-workstations"></a>3. Administrative Workstations

Stellen Sie als erste Sicherheitsmaßnahme für Benutzer mit Azure Active Directory und herkömmlichen lokalen Active Directory-Administratorrechten sicher, dass Windows 10-Geräte verwendet werden, die gemäß den [Standards für ein hochsicheres Windows 10-Gerät](/windows-hardware/design/device-experiences/oem-highly-secure) konfiguriert sind. Privilegierte Administratorkonten sollten nicht Mitglieder der lokalen Administratorgruppe der administrativen Workstations sein.  Rechteerweiterungen mithilfe der Benutzerzugriffssteuerung können verwendet werden, wenn Änderungen an den Workstations vorgenommen werden müssen.  Darüber hinaus sollte die Windows 10-Sicherheitsbaseline auf die Workstations angewendet werden, um den Schutz der Geräte weiter zu stärken.

### <a name="4-identity-attack-detection"></a>4. Erkennung von Identitätsangriffen

[Azure Advanced Threat Protection (ATP)](/azure-advanced-threat-protection/what-is-atp) ist eine cloudbasierte Sicherheitslösung, mit der Sie komplexe Bedrohungen, kompromittierte Identitäten und schädliche Insideraktionen gegen Ihre lokale Active Directory-Umgebung identifizieren, erkennen und untersuchen können.

## <a name="phase-2-significant-incremental-improvements"></a>Phase 2: Bedeutende inkrementelle Verbesserungen

Phase 2 baut auf Phase 1 auf und ist dazu konzipiert, innerhalb von etwa 90 Tagen implementiert zu werden. In diesem Diagramm sind die Schritte in dieser Phase dargestellt:

![Diagramm zu Phase 2: 1. Windows Hello for Business/MFA, 2. Einführung von Workstations mit privilegiertem Zugriff, 3. Just-In-Time-Berechtigungen, 4. Credential Guard, 5. Kompromittierte Anmeldeinformationen, 6. Lateral-Movement-Erkennung von Sicherheitsrisiken](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1. Erfordern von Windows Hello for Business und MFA

Administratoren können von der einfachen Handhabung von Windows Hello for Business profitieren. Administratoren können ihre komplexen Kennwörter durch sichere zweistufige Authentifizierung auf ihren Computern ersetzen. Ein Angreifer muss sowohl über das Gerät als auch über die biometrischen Informationen oder die PIN verfügen. Es ist also deutlich schwieriger, sich Zugriff ohne das Wissen des Mitarbeiters zu verschaffen. Weitere Informationen zu Windows Hello for Business und die Implementierung finden Sie im Artikel [Überblick über Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview).

Aktivieren Sie die mehrstufige Authentifizierung (MFA) für Ihre Administratorkonten in Azure AD mithilfe von Azure Multi-Factor Authentication. Aktivieren Sie mindestens die [Basisschutzrichtlinie für den bedingten Zugriff](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins). Weitere Informationen zu Azure Multi-Factor Authentication finden Sie im Artikel [Planen einer cloudbasierten Azure Multi-Factor Authentication-Bereitstellung](/azure/active-directory/authentication/howto-mfa-getstarted).

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2. Bereitstellen von Workstations mit privilegiertem Zugriff für alle Mitarbeiter mit Identitätskonten mit privilegiertem Zugriff

Sie sollten dedizierte Workstations mit privilegiertem Zugriff für alle Mitarbeiter mit privilegiertem Zugriff auf die Informationssysteme Ihrer Organisation implementieren, um privilegierte Konten weiter von Bedrohungen zu trennen, die in E-Mails, im Internet und in anderen nicht administrativen Aufgaben lauern können. Weitere Anweisungen zur Bereitstellung von Workstations mit privilegiertem Zugriff finden Sie im Artikel zu [Workstations mit privilegiertem Zugriff](privileged-access-workstations.md#paw-phased-implementation).

### <a name="3-just-in-time-privileges"></a>3. Just-In-Time-Berechtigungen

Stellen Sie Just-In-Time-Berechtigungen mithilfe einer angemessenen Lösung wie eine der folgenden oder einer Drittanbieterlösung bereit, um die Offenlegung von Berechtigungen zu reduzieren und die Transparenz ihrer Nutzung zu erhöhen:

* Verwenden Sie für Active Directory Domain Services (AD DS) die Funktion [Privileged Access Manager (PAM)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) von Microsoft Identity Manager (MIM).
* Verwenden Sie für Azure Active Directory die Funktion [Azure AD Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) .

### <a name="4-enable-windows-defender-credential-guard"></a>4. Aktivieren von Windows Defender Credential Guard

Indem Sie Credential Guard aktivieren, unterstützen Sie den Schutz von NTLM-Kennworthashs, Kerberos-TGTs (Kerberos Ticket Granting Tickets) und Anmeldeinformationen, die von Anwendungen als Domänenanmeldeinformationen gespeichert werden. Diese Funktion unterstützt die Verhinderung von Angriffen zum Diebstahl von Anmeldeinformationen, z. B. Pass-the-Hash- oder Pass-the-Ticket-Angriffe, indem das Pivotieren mithilfe gestohlener Anmeldeinformationen in der Umgebung erschwert wird. Informationen zur Funktionsweise und Bereitstellung von Credential Guard finden Sie im Artikel [Schützen abgeleiteter Domänenanmeldeinformationen mit Windows Defender Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard).

### <a name="5-leaked-credentials-reporting"></a>5. Berichterstattung zu kompromittierten Anmeldeinformationen

„Jeden Tag analysiert Microsoft über 6,5 Billionen Signale, um mögliche Bedrohungen zu identifizieren und Kunden zu schützen.“ – [Microsoft in Zahlen](https://news.microsoft.com/bythenumbers/cyber-attacks)

Aktivieren Sie Azure AD Identity Protection, um die Berichterstattung zu Benutzern mit kompromittierten Anmeldeinformationen zu beginnen, damit Sie diese wiederherstellen können. Sie können [Azure AD Identity Protection](/azure/active-directory/identity-protection/index) dazu nutzen, die Cloudumgebungen und hybriden Umgebungen Ihrer Organisation vor Bedrohungen zu schützen.

### <a name="6-azure-atp-lateral-movement-paths"></a>6. Azure ATP-Lateral-Movement-Pfade

Stellen Sie sicher, dass Besitzer von Konten mit privilegiertem Zugriff ihre Workstations mit privilegiertem Zugriff nur für die Verwaltung nutzen, damit ein kompromittiertes nicht privilegiertes Konto keinen Zugriff auf ein privilegiertes Konto über Angriffe zum Diebstahl von Anmeldeinformationen wie Pass-the-Hash oder Pass-the-Ticket erhalten kann. [Azure ATP-Lateral Movement-Pfade (LMPs)](/azure-advanced-threat-protection/use-case-lateral-movement-path) bieten eine leicht verständliche Berichterstellung, um Risiken für die Kompromittierung von privilegierten Konten zu identifizieren.

## <a name="phase-3-security-improvement-and-sustainment"></a>Phase 3: Verbesserung und Aufrechterhaltung der Sicherheit

Phase 3 der Roadmap baut auf den Schritten der Phasen 1 und 2 auf, um die Aufstellung Ihrer Sicherheit zu stärken. Phase 3 wird in der folgenden Abbildung veranschaulicht:

![Phase 3: 1. Überprüfen der rollenbasierten Zugriffssteuerung, 2. Reduzieren von Angriffsflächen, 3. Integrieren von Protokollen mit SIEM, 4. Automatisierte Vorgehensweise bei kompromittierten Anmeldeinformationen](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

Diese Funktionen bauen auf den Schritten aus den vorherigen Phasen auf und sorgen für eine proaktivere Sicherheit. Für diese Phase gibt es keine spezifische Zeitplanung. Abhängig von Ihrer individuellen Organisation kann die Implementierung mehr Zeit beanspruchen.

### <a name="1-review-role-based-access-control"></a>1. Überprüfen der rollenbasierten Zugriffssteuerung

Überprüfen Sie anhand des dreistufigen Modells im Artikel [Active Directory-Verwaltungsebenenmodell](securing-privileged-access-reference-material.md), und stellen Sie sicher, dass Administratoren der niedrigeren Ebenen nicht über administrativen Zugriff auf Ressourcen der höheren Ebenen verfügen (Gruppenmitgliedschaften, ACLs in Benutzerkonten usw.).

### <a name="2-reduce-attack-surfaces"></a>2. Reduzieren von Angriffsflächen

Stärken Sie Ihre Identitätsworkloads, einschließlich Ihrer Domänen, Domänencontroller, ADFS und Azure AD Connect, da die Kompromittierung eines dieser Systeme zur Kompromittierung weiterer Systeme in Ihrer Organisation führen könnte. Anleitungen zur Sicherung Ihrer lokalen und hybriden Identitätsumgebungen finden Sie in den Artikeln [Reduzieren der Angriffsfläche von Active Directory](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md) und [Fünf Schritte zum Schützen Ihrer Identitätsinfrastruktur](/azure/security/azure-ad-secure-steps).

### <a name="3-integrate-logs-with-siem"></a>3. Integrieren von Protokollen mit SIEM

Die Integration der Protokollierung in ein zentralisiertes SIEM-Tool kann Ihre Organisation bei der Analyse, Erkennung und Reaktion auf Sicherheitsereignisse unterstützen. Anleitungen zu Ereignissen, die in Ihrer Umgebung überwacht werden sollten, finden Sie in den Artikeln [Überwachen von Active Directory auf Anzeichen von Kompromittierung](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md) und [Anhang L: Zu überwachende Ereignisse](../ad-ds/plan/appendix-l--events-to-monitor.md).

Dies ist Teil der fortlaufenden Planung, da die Aggregation, Erstellung und Optimierung von Warnungen in einer SIEM-Lösung (Security Information and Event Management) erfahrene Analysten erfordert (im Gegensatz zum 30-tägigen Plan für Azure ATP, der vorkonfigurierte Warnungen enthält).

### <a name="4-leaked-credentials---force-password-reset"></a>4. Kompromittierte Anmeldeinformationen: Erzwingen der Kennwortzurücksetzung

Verbessern Sie Ihre Sicherheit weiterhin, indem Sie Azure AD Identity Protection erlauben, automatische Kennwortzurücksetzungen zu erzwingen, wenn die Kompromittierung eines Kennworts vermutet wird. Anweisungen zum Aktivieren dieser Funktionalität mithilfe einer Richtlinie für bedingten Zugriff finden Sie im Artikel [Verwenden von Risikoereignissen zum Auslösen von mehrstufiger Authentifizierung und Kennwortänderungen](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa).

## <a name="am-i-done"></a>Fertig?

Die Antwort lautet „Nein“.

Die böswilligen Akteure hören niemals auf, also dürfen Sie das auch nicht. Diese Roadmap kann Ihre Organisation dabei unterstützen, sich vor derzeit bekannten Bedrohungen zu schützen, während sich Angreifer stetig weiterentwickeln und ihre Strategien ausbauen. Daher wird empfohlen, dass Sie die Sicherheit als einen laufenden Prozess betrachten, der sich darauf konzentriert, die Kosten für Angreifer auf Ihre Umgebung zu steigern und ihre Erfolgsrate zu reduzieren.

Das Schützen des privilegierten Zugriffs ist zwar nicht der einzige Aspekt des Schutzprogramms Ihrer Organisation, jedoch ist es dennoch ein wichtiger Bestandteil Ihrer Sicherheitsstrategie.
