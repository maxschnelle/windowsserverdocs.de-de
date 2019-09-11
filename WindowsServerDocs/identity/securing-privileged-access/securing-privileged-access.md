---
title: Sichern des privilegierten Zugriffs
description: Stufenweise Vorgehensweise zum Sichern des privilegierten Zugriffs
ms.prod: windows-server-threshold
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 9080f7209660b225d795219127a71ece479855d1
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869229"
---
# <a name="securing-privileged-access"></a>Sichern des privilegierten Zugriffs

>Gilt für: Windows Server

Der Schutz des privilegierten Zugriffs ist ein erster wichtiger Schritt zum Einrichten von Sicherheitsstandards für Geschäftsressourcen in modernen Unternehmen. Die Sicherheit der meisten oder aller Geschäftsressourcen in einer IT-Organisation hängt von der Integrität der privilegierten Konten ab, die für die Verwaltung, Verwaltung und Entwicklung verwendet werden. Cyberangreifer richten diese Konten und andere Elemente des privilegierten Zugriffs häufig ein, um Zugriff auf Daten und Systeme mithilfe von Angriffen zum Diebstahl von Anmelde Informationen wie [Pass-the-Hash und Pass-The-Ticket](https://www.microsoft.com/pth)zu erhalten.

Zum Schutz des privilegierten Zugriffs gegen entschlossene Angreifer müssen Sie einen umfassenden und durchdachten Ansatz ergreifen, um diese Systeme von Risiken zu isolieren.

## <a name="what-are-privileged-accounts"></a>Was sind privilegierte Konten?

Bevor wir erläutern, wie Sie geschützt werden, können Sie privilegierte Konten definieren.

Privilegierte Konten wie Administratoren von Active Directory Domain Services haben direkten oder indirekten Zugriff auf die meisten oder alle Ressourcen in einer IT-Organisation. Dies führt zu einem kompromittieren dieser Konten zu einem erheblichen Geschäftsrisiko.

## <a name="why-securing-privileged-access-is-important"></a>Warum ist das Sichern des privilegierten Zugriffs von Bedeutung?

Cyberangreifer konzentrieren sich auf den privilegierten Zugriff auf Systeme wie Active Directory (AD), um schnell Zugriff auf alle Ziel Daten von Organisationen zu erhalten. Herkömmliche Sicherheits Ansätze haben sich auf das Netzwerk und Firewalls als primären Sicherheitsbereich konzentriert, aber die Effektivität der Netzwerksicherheit wurde durch zwei Trends erheblich beeinträchtigt:

* Organisationen werden Daten und Ressourcen außerhalb der herkömmlichen Netzwerk Grenze auf mobilen PCs, Geräten wie Mobiltelefonen und Tablets, Clouddiensten und Bring your own Device (BYOD) gehostet.
* Angreifer haben durchweg die Fähigkeit nachgewiesen, dass sie mithilfe von Phishing- und anderen Web- und E-Mail-Angriffen Zugriff auf Arbeitsstationen innerhalb der Netzwerkgrenze erlangt haben.

Diese Faktoren erfordern zusätzlich zur herkömmlichen Netzwerk Umkreis Strategie das Entwickeln eines modernen Sicherheits Umkreises aus Authentifizierungs-und Autorisierungs Identitätskontrollen. Hier ist ein Sicherheitsbereich definiert, der als konsistente Gruppe von Steuerelementen zwischen Assets und Bedrohungen definiert ist. Privilegierte Konten steuern den neuen Sicherheits Umkreis, sodass es wichtig ist, den privilegierten Zugriff zu schützen.

![Diagramm, das die Identitätsebene einer Organisation zeigt](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

Ein Angreifer, der die Kontrolle über ein Administrator Konto erlangt, kann diese Berechtigungen verwenden, um seine Auswirkung auf die Zielorganisation zu erhöhen, wie unten dargestellt:

![Diagramm, das zeigt, wie ein Widersacher, der die Kontrolle über ein Administratorkonto erlangt, die dazugehörigen Berechtigungen zum Nachteil der Zielorganisation nutzen kann](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

Die Abbildung unten zeigt zwei Pfade:

* Ein "blauer" Pfad, in dem ein Standardbenutzer Konto für den nicht privilegierten Zugriff auf Ressourcen wie e-Mail und Webbrowser und tägliche Arbeit verwendet wird.

   > [!NOTE]
   > Blaue Pfad Elemente, die später beschrieben werden, weisen auf einen umfassenden Umweltschutz hin, der über die Administrator Konten hinausgeht

* Ein "Roter" Pfad, in dem privilegierter Zugriff auf einem festgeschriebenen Gerät erfolgt, um das Risiko von Phishing und anderen Web-und e-Mail-Angriffen zu verringern

![Diagramm, das den separaten "Pfad" für die Verwaltung anzeigt, die in der Roadmap zum isolieren privilegierter Zugriffs Tasks von hochriskanten Standardbenutzer Aufgaben wie dem Webbrowser und dem Zugriff auf e-Mails eingerichtet wird](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>Roadmap zum Sichern des privilegierten Zugriffs

Die Roadmap dient zum Maximieren der Verwendung von Microsoft-Technologien, die Sie bereits bereitgestellt haben, nutzen cloudtechnologien, um die Sicherheit zu erhöhen, und integrieren Sicherheitstools von Drittanbietern, die Sie möglicherweise bereits bereitgestellt haben.

Die Roadmap für Microsoft-Empfehlungen ist in drei Phasen unterteilt:

* [Phase 1: Erste 30 Tage]()
   * Schneller Gewinn mit sinnvollen positiven Auswirkungen.
* [Phase 2: 90 Tage]()
   * Bedeutende inkrementelle Verbesserung.
* [Phase 3: Ende]()
   * Sicherheitsverbesserung und-Erhaltung.

Der Leitfaden ist so priorisiert, dass basierend auf unseren Erfahrungen mit diesen Angriffen und der Umsetzung von Lösungen die wirkungsvollsten und schnellen Umsetzungen zuerst geplant werden. 

Microsoft empfiehlt das Befolgen dieses Leitfadens zum Schützen des privilegierten Zugriffs gegen entschlossene Angreifer. Sie können diesen Leitfaden entsprechend Ihren vorhandenen Möglichkeiten und spezifischen Anforderungen in Ihren Abteilungen anpassen.

> [!NOTE]
> Der Schutz des privilegierten Zugriffs erfordert eine Vielzahl von Elementen, wie z. B. technische Komponenten (Schutzmaßnahmen für Hosts und Konten, Identitätsverwaltung usw.), sowie Änderungen an Prozessen, Verwaltungsabläufen und Kenntnissen. Die Zeitangaben in diesem Leitfaden sind Näherungswerte und basieren auf unserer Erfahrung mit Kundenlösungen. Je nach Komplexität Ihrer Umgebung und Ihren Änderungsmanagementprozessen variiert die Dauer in Ihrer Organisation.

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>Phase 1: Schneller Gewinn mit minimaler Betriebs Komplexität

Phase 1 der Roadmap konzentriert sich auf die schnelle Entschärfung der am häufigsten verwendeten Angriffstechniken für Diebstahl und Missbrauch von Anmelde Informationen. Phase 1 ist so konzipiert, dass Sie in ungefähr 30 Tagen implementiert wird und in diesem Diagramm dargestellt wird:

![Phase 1-Diagramm: 1. Trennen Sie Administrator-und Benutzerkonto, 2. Just-in-Time-lokale Administrator Kennwörter, 3. Verwaltungs Arbeitsstation 1, 4. Erkennung von Identitäts Angriffen](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1. Getrennte Konten

Erstellen Sie ein dediziertes Konto für alle Mitarbeiter mit privilegiertem Zugriff, um Internet Risiken (Phishingangriffe, Webbrowsen) von privilegierten Zugriffs Konten zu trennen. Administratoren sollten das Internet nicht durchsuchen, Ihre e-Mail-nach Gängen überprüfen und alltägliche Produktivitäts Aufgaben mit Konten mit hohen Berechtigungen ausführen. Weitere Informationen hierzu finden Sie im Abschnitt [separate Administrator Konten](securing-privileged-access-reference-material.md#separate-administrative-accounts) des Referenzdokuments.

Befolgen Sie die Anleitungen im Artikel [Verwalten von Notfall Zugriffs Konten in Azure AD](/azure/active-directory/users-groups-roles/directory-emergency-access) , um mindestens zwei Konten für den Notfall Zugriff mit dauerhaft zugewiesenen Administratorrechten in Ihrer lokalen AD-und Azure AD-Umgebung zu erstellen. Diese Konten dienen nur der Verwendung, wenn herkömmliche Administrator Konten keine erforderliche Aufgabe ausführen können, wie z. b. bei einem Notfall.

### <a name="2-just-in-time-local-admin-passwords"></a>2. Just-in-Time-lokale Administrator Kennwörter

Um das Risiko zu verringern, dass ein Angreifer ein Kennwort für ein lokales Administrator Konto aus der lokalen SAM-Datenbank stiehlt und den Angriff auf andere Computer missbraucht, sollten Organisationen sicherstellen, dass jeder Computer über ein eindeutiges lokales Administrator Kennwort verfügt. Das Tool für lokale Administrator Kenn Wort Lösungen (Laps) kann auf jeder Arbeitsstation eindeutige zufällige Kenn Wörter konfigurieren, und der Server speichert Sie in Active Directory (AD), die durch eine ACL geschützt sind. Nur berechtigte autorisierte Benutzer können das Zurücksetzen der Kenn Wörter für die lokalen Administrator Konten lesen oder anfordern. Sie können die Runden für die Verwendung auf Arbeitsstationen und Servern im [Microsoft Download Center](http://Aka.ms/LAPS)abrufen.

Weitere Anleitungen zum Betreiben einer Umgebung mit runden und Pfoten finden Sie im Abschnitt [Betriebsstandards basierend auf dem Prinzip der sauberen Quelle](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle).

### <a name="3-administrative-workstations"></a>3. Administrative Arbeitsstationen

Als erste Sicherheitsmaßnahme für Benutzer mit Azure Active Directory und herkömmlichen lokalen Active Directory Administratorrechten müssen Sie sicherstellen, dass Sie Windows 10-Geräte verwenden, die mit den [Standards für ein äußerst sicheres Windows 10-Gerät konfiguriert sind. ](/windows-hardware/design/device-experiences/oem-highly-secure). Privilegierte Administrator Konten sollten nicht Mitglied der lokalen Administrator Gruppe der administrativen Arbeitsstationen sein.  Die Berechtigungs Erweiterung über Benutzer Access Control (UAC) kann verwendet werden, wenn Konfigurationsänderungen an den Arbeitsstationen erforderlich sind.  Außerdem sollte die Windows 10-Sicherheitsbaseline auf die Arbeitsstationen angewendet werden, um das Gerät weiter zu Härten.

### <a name="4-identity-attack-detection"></a>4. Erkennung von Identitäts Angriffen

Bei [Azure Advanced Threat Protection (ATP)](/azure-advanced-threat-protection/what-is-atp) handelt es sich um eine cloudbasierte Sicherheitslösung, die erweiterte Bedrohungen, kompromittierte Identitäten und schädliche Insider-Aktionen, die auf Ihre lokale Active Directory gerichtet sind, identifiziert, erkennt und unterstützt. Umgebung.

## <a name="phase-2-significant-incremental-improvements"></a>Phase 2: Bedeutende inkrementelle

Phase 2 baut auf den in Phase 1 abgeschlossenen Arbeiten auf und ist für die Ausführung in ungefähr 90 Tagen vorgesehen. In diesem Diagramm sind die Schritte in dieser Phase dargestellt:

![Diagramm der Phase 2: 1. Windows Hello for Business/MFA, 2. PW-Rollout, 3. Just-in-time-Berechtigungen, 4. Credential Guard, 5. Kompromittierte Anmelde Informationen, 6. Erkennung von Lateral Movement-Sicherheitsrisiken](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1. Windows Hello for Business und MFA erforderlich

Administratoren können von der Benutzerfreundlichkeit profitieren, die mit Windows Hello for Business verknüpft ist. Administratoren können Ihre komplexen Kenn Wörter durch eine starke zweistufige Authentifizierung auf ihren PCs ersetzen. Ein Angreifer muss sowohl über das Gerät als auch über die biometrische Info oder PIN verfügen. es ist viel schwieriger, ohne das Wissen des Mitarbeiters Zugriff zu erhalten. Weitere Informationen zu Windows Hello for Business und zum Rollout des Pfads finden Sie im Artikelübersicht über [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview) .

Aktivieren Sie die mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) für Ihre Administrator Konten in Azure AD mithilfe von Azure MFA. Mindestens Informationen zu Azure Multi-Factor Authentication finden [Sie im Artikel Bereitstellen einer](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins) [cloudbasierten Azure-Multi-Factor Authentication](/azure/active-directory/authentication/howto-mfa-getstarted) .

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2. Bereitstellen von PW für alle privilegierten Identitäts Zugriffs Kontoinhaber

Wenn Sie den Prozess der Trennung privilegierter Konten von Bedrohungen in e-Mail, Webbrowser und anderen nicht administrativen Aufgaben fortsetzen, sollten Sie dedizierte privilegierte Zugriffs Arbeitsstationen (PW) für alle Mitarbeiter mit privilegiertem Zugriff auf Ihre Informationssysteme der Organisation. Weitere Anleitungen zur Bereitstellung von bereit Stellungen finden Sie im Artikel [privilegierte Zugriffs](privileged-access-workstations.md#paw-phased-implementation)Arbeitsstationen.

### <a name="3-just-in-time-privileges"></a>3. Just-in-time-Berechtigungen

Um die Verfügbarkeit von Berechtigungen zu verringern und den Einblick in ihre Verwendung zu erhöhen, können Sie Berechtigungen Just-in-time (JIT) mithilfe einer geeigneten Lösung wie den folgenden oder anderen Lösungen von Drittanbietern bereitstellen:

* Verwenden Sie für Active Directory Domain Services (AD DS) die Funktion [Privileged Access Manager (PAM)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) von Microsoft Identity Manager (MIM).
* Verwenden Sie für Azure Active Directory die Funktion [Azure AD Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) .

### <a name="4-enable-windows-defender-credential-guard"></a>4. Aktivieren von Windows Defender Credential Guard

Durch das Aktivieren von Credential Guard können NTLM-Kennworthashes, die Kerberos-Ticket Gewährung und die von Anwendungen als Domänen Anmelde Informationen gespeicherten Anmelde Informationen geschützt werden. Mit dieser Funktion können Angriffe durch Diebstahl von Anmelde Informationen verhindert werden, z. b. Pass-the-Hash oder Pass-The-Ticket, indem die Schwierigkeit der Pivotierung in der Umgebung mithilfe gestohlener Anmelde Informationen erhöht wird. Informationen zur Funktionsweise von Credential Guard und zur Bereitstellung finden Sie im Artikel [schützen abgeleiteter Domänen Anmelde Informationen mit Windows Defender Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard).

### <a name="5-leaked-credentials-reporting"></a>5. Berichterstattung über kompromittierte

"Täglich analysiert Microsoft über 6,5 Billionen Signale, um neue Bedrohungen zu erkennen und Kunden zu schützen"- [Microsoft durch die Zahlen](https://news.microsoft.com/bythenumbers/cyber-attacks)

Aktivieren Sie Microsoft Azure AD Identity Protection, um Berichte zu Benutzern mit kompromittierten Anmelde Informationen zu melden, damit Sie Sie beheben können. [Azure AD Identity Protection](/azure/active-directory/identity-protection/index) können genutzt werden, um Ihre Organisation beim Schutz von Cloud-und Hybrid Umgebungen vor Bedrohungen zu unterstützen.

### <a name="6-azure-atp-lateral-movement-paths"></a>6. Azure ATP lateral Movement-Pfade

Stellen Sie sicher, dass privilegierte Zugriffs Kontoinhaber ihre PW nur für die Verwaltung verwenden, sodass ein kompromittiertes nicht privilegiertes Konto nicht über Angriffe zum Diebstahl von Anmelde Informationen (z. b. Pass-the-Hash oder Pass-The-Ticket) Zugriff auf ein privilegiertes Konto erhalten kann. [Azure ATP lateral Movement-Pfade (LMPS)](/azure-advanced-threat-protection/use-case-lateral-movement-path) bietet eine leicht verständliche Berichterstellung, um zu ermitteln, wo privilegierte Konten möglicherweise für eine Gefährdung offen sind.

## <a name="phase-3-security-improvement-and-sustainment"></a>Phase 3: Verbesserung der Sicherheit und Nachhaltigkeit

Phase 3 der Roadmap baut auf den Schritten in den Phasen 1 und 2 auf, um den Sicherheitsstatus zu erhöhen. Phase 3 wird visuell in diesem Diagramm dargestellt:

![Phase 3: 1. Überprüfen Sie RBAC, 2. Reduzieren Sie Angriffsflächen, 3. Integrieren Sie Protokolle mit Seim, 4. Automatisierung kompromittierte Anmelde Informationen](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

Diese Funktionen bauen auf den Schritten aus den vorherigen Phasen auf und verlagern Ihre Verteidigungsmaßnahmen in einen proaktiven Zustand. Diese Phase verfügt über keine bestimmte Zeitachse und kann je nach Organisation mehr Zeit in Anspruch nehmen.

### <a name="1-review-role-based-access-control"></a>1. Überprüfen der rollenbasierten Zugriffs Steuerung

Überprüfen Sie mithilfe des dreistufigen Modells, das im Artikel [Active Directory Modell der administrativen Ebene](securing-privileged-access-reference-material.md)beschrieben ist, und stellen Sie sicher, dass Administratoren der niedrigeren Ebene keinen administrativen Zugriff auf Ressourcen höherer Ebene haben (Gruppenmitgliedschaften, ACLs für Benutzerkonten usw.).

### <a name="2-reduce-attack-surfaces"></a>2. Verringern von Angriffsflächen

Härten ihrer identitätsworkloads, einschließlich Domänen, Domänen Controllern, ADFS und Azure AD Connect, dass die Gefährdung eines dieser Systeme zu einer Gefährdung anderer Systeme in Ihrer Organisation führen könnte. In den Artikeln, [die die Active Directory Angriffsfläche](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md) und [fünf Schritte zum Sichern Ihrer Identitäts Infrastruktur reduzieren,](/azure/security/azure-ad-secure-steps) finden Sie Anleitungen zum Schützen Ihrer lokalen und Hybriden Identitäts Umgebungen.

### <a name="3-integrate-logs-with-siem"></a>3. Integrieren von Protokollen in Siem

Wenn Sie die Protokollierung in ein zentrales Siem-Tool integrieren, können Sie Ihre Organisation beim Analysieren, erkennen und reagieren auf Sicherheitsereignisse unterstützen. In den Artikeln [überwachen Active Directory Anzeichen für Kompromittierung](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md) und [Anhang L: Zu über](../ad-ds/plan/appendix-l--events-to-monitor.md) Wachende Ereignisse bieten Anleitungen zu Ereignissen, die in Ihrer Umgebung überwacht werden sollen.

Dies ist ein Bestandteil des Plans, denn das aggregierten, erstellen und Optimieren von Warnungen in einem Sicherheits-und Ereignismanagement (SIEM) erfordert erfahrene Analysten (im Gegensatz zu Azure ATP im 30-tägigen Plan, der standardmäßig Warnungen umfasst).

### <a name="4-leaked-credentials---force-password-reset"></a>4. Kompromittierte Anmelde Informationen: Zurücksetzen des Kennworts

Verbessern Sie weiterhin Ihren Sicherheitsstatus, indem Sie Azure AD Identity Protection die automatische Kenn Wort zurück Setzung erzwingen, wenn Kenn Wörter als kompromittiert werden. Die Anleitung im Artikel [Verwenden von Risiko Ereignissen zum Auslösung von Multi-Factor Authentication und Kenn Wort Änderungen](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa) erläutert, wie Sie dies mithilfe einer Richtlinie für bedingten Zugriff aktivieren.

## <a name="am-i-done"></a>Fertig?

Die kurze Antwort lautet "Nein".

Die Leute werden nie angehalten, und Sie können es auch nicht. Diese Roadmap unterstützt Ihre Organisation beim Schutz vor derzeit bekannten Bedrohungen, da Angreifer ständig weiterentwickelt werden und sich verlagern. Wir empfehlen Ihnen, die Sicherheit als laufenden Prozess anzusehen, der sich auf die Kostensenkung und die Erfolgsrate von Angreifern konzentriert, die auf Ihre Umgebung abzielen.

Obwohl es nicht der einzige Teil des Sicherheitsprogramms Ihrer Organisation ist, ist das Sichern des privilegierten Zugriffs ein wichtiger Bestandteil Ihrer Sicherheitsstrategie.
