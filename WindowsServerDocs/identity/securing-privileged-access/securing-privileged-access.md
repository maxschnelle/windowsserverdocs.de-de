---
title: "Schützen des privilegierten Zugriffs"
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: eb83903204b00ef6c1eb116554ec54bc2211a399
ms.sourcegitcommit: 7b01b54032ec56432116626e08fbd92508c3a7d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="securing-privileged-access"></a>Schützen des privilegierten Zugriffs

>Gilt für: Windows Server 2016

Der Schutz des privilegierten Zugriff wird ein erster wichtiger Schrittzum Einrichten von Sicherheitsstandards für Geschäftsressourcen in modernen Unternehmen ist. Die Sicherheit der meisten oder aller Geschäftsressourcen in einem Unternehmen hängt von der Integrität der privilegierten Konten, die zum Verwalten von IT-Systeme. Auf diese Konten und andere Elemente des privilegierten Zugriffs für den Zugriff auf bestimmte Daten und Systeme, die mithilfe der Methoden des Anmeldeinformationsdiebstahls wie schnell cyberangreifer ausgerichtet [Pass-the-Hash und Pass-the-Ticket](https://www.microsoft.com/pth).

Schutz des administrativen Zugriffs gegen festgestellt, dass entschlossene Angreifer erforderlich ist, sollten Sie einen vollständigen und durchdachten Ansatzes, um diese Systeme gegen Risiken zu isolieren. Diese Abbildungzeigt die drei Phasen von Empfehlungen zum Trennen und Schützen der Verwaltung in diesem Leitfaden:

![Diagramm der die drei Phasen von Empfehlungen zum Trennen und Schützen der Verwaltung in diesem Leitfaden](../media/securing-privileged-access/PAW_LP_Fig1.JPG)

Roadmap Ziele:

-   **plan für 2 bis 4 Wochen**: rasches abwehren die am häufigsten verwendeten Angriffsstrategien

-   **plan für 1 bis 3 Monate**: Aufbauen von Transparenz und Kontrolle der Aktivitäten von Administratoren

-   **6 Plan für**: weiterhin von Schutzmaßnahmen zum Erreichen einer proaktiveren Sicherheitslage

Microsoft empfiehlt, dass Sie dieses Leitfadens zum Schützen des privilegierten Zugriffs gegen entschlossene befolgen. Sie können diesen Leitfaden entsprechend Ihren vorhandenen Möglichkeiten und spezifischen Anforderungen in Ihrer Organisation anpassen.

> [!NOTE]
> Der Schutz des privilegierten erfordert Zugriff einer breiten Palette von Elemente, z.B. technische Komponenten (Schutzmaßnahmen für Hosts, Konto Schutzmaßnahmen, identitätsverwaltung usw.) sowie Änderungen an Prozessen, und Methoden für die Verwaltung und Kenntnisse.

## <a name="why-is-securing-privileged-access-important"></a>Warum ist Schützen des privilegierten Zugriffs wichtig?
In den meisten Unternehmen ist die Sicherheit der meisten oder aller Geschäftsressourcen hängt von der Integrität der privilegierten Konten, die zum Verwalten von IT-Systeme. Cyberangreifer konzentrieren sich auf den privilegierten Zugriff auf Systeme wie Active Directory für den Zugriff auf alle Organisationen schnell Daten vorgesehen.

Herkömmliche Sicherheitsansätze haben den Schwerpunkt auf die Ausgang und ausgehende Punkten eines Unternehmensnetzwerks als primären Sicherheitsumfang verwenden, aber die Wirksamkeit von wurde durch zwei Trends deutlich verringert wurde:

-   Organisationen hosten Daten und Ressourcen außerhalb der herkömmlichen Netzwerkgrenze auf mobilen unternehmensrechnern, Geräten wie Mobiltelefonen und Tablets, Cloud-Dienste und BYOD-Geräte

-   Angreifer haben eine Fähigkeit zum Zugreifen auf Arbeitsstationen innerhalb des Netzwerks mithilfe von Phishing- und anderen Web- und E-Mail-Angriffen gezeigt.

Die natürliche Ersatz für die Netzwerk-Sicherheitsumfang in einem komplexen modernen Unternehmen ist die Authentifizierung und Autorisierung Steuerelemente in einer Organisation Identität Ebene. Privilegierte administrative Konten haben gewissermaßen die Kontrolle über diese neuen "Sicherheitsumfang" daher es wichtig ist, den privilegierten Zugriff zu schützen:

![Diagramm einer Organisation Identität Ebene](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

Ein Widersacher, der die Kontrolle über ein Administratorkonto erlangt nutzen kann ihren Gewinn auf Kosten der Zielorganisation verfolgen, wie im folgenden dargestellt:

![Das Diagramm zeigt, wie ein Widersacher, der die Kontrolle über ein Administratorkonto erlangt diese Berechtigungen verwenden kann, ihren Gewinn Nachteil der Zielorganisation verfolgen](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

Weitere Informationen zu den Arten von Angriffen, die häufig für Angreifer Kontrolle über Administratorkonten führen, finden Sie auf der [Pass The Hash Website](https://www.microsoft.com/pth) Whitepapers, Videos und vieles mehr.

Diese Abbildungzeigt den separaten "Kanal" für die Verwaltung, die der in dieser Anleitung eingerichtet wird, um die Systemzugriff-Aufgaben von standardmäßigen Benutzeraufgaben mit hohem Risiko wie Websuchen und E-Mail-Zugriff zu isolieren.

![Diagramm der separaten "Kanals" für die Verwaltung, der in dieser Anleitung eingerichtet wird, um die Systemzugriff-Aufgaben von standardmäßigen Benutzeraufgaben mit hohem Risiko wie Websuchen und E-Mail-Zugriff zu isolieren](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

Da der Angreifer die Steuerung des privilegierten Zugriffs mithilfe verschiedener Methoden erhalten, kann erfordert diese Risikominderung ein ganzheitliches und detaillierte technische vorgehen, wie in diesem Leitfaden erläutert. Die Roadmap wird gehärtet und die Elemente in Ihrer Umgebung, die privilegierten Zugriff ermöglichen, indem Schutzmaßnahmen in jedem Bereich der Spalte "Abwehr" in dieser Abbildung:

![Tabelle zeigt Angriffs- und abwehrspalten](../media/securing-privileged-access/PAW_LP_Fig5.JPG)

## <a name="security-privileged-access-roadmap"></a>Sicherheit des privilegierten Zugriffs roadmap
Die Roadmap dient zum Optimieren der Verwendung von Technologien, die Sie möglicherweise bereits bereitgestellt, nutzen Sie wichtige aktueller und künftiger sicherheitstechnologien und integrieren Sie alle 3. Sicherheitstools Sie möglicherweise bereits bereitgestellt haben.

Die Empfehlungen von Microsoft-Roadmap ist in 3 Phasen unterteilt:

-   Plan für 2 bis 4 Wochen: rasches abwehren der am häufigsten verwendeten Angriffsstrategien

-   Plan für 1 bis 3Monate: Aufbauen von Transparenz und kontrollieren der Aktivitäten von Administratoren

-   6 + Monat planen – weiterhin von Schutzmaßnahmen zum Erreichen einer proaktiveren Sicherheitslage

Jede Phase des Leitfadens dient zum Auslösen der Kosten und Schwierigkeiten von Angreifern Angriffe von privilegierten Zugriff für den lokalen und Cloudressourcen. Der Leitfaden ist so priorisiert so planen Sie die wirkungsvollsten und die umsetzungen zuerst basierend auf unseren Erfahrungen mit diesen Angriffen und der Implementierung der Lösung.

> [!NOTE]
> Die Zeitangaben in diesem Leitfaden sind Näherungswerte und basieren auf unserer Erfahrung mit kundenlösungen. Die Dauer ist in Ihrer Organisation je nach Komplexität Ihrer Umgebung und Ihren Änderungsmanagementprozessen abhängig.

### <a name="security-privileged-access-roadmap-stage-1"></a>Sicherheit Schutz des privilegierten Zugriffs: Phase 1
Phase 1 des Leitfadens konzentriert sich auf das rasche abwehren der am häufigsten verwendeten Angriffsstrategien Diebstahl und Missbrauch. Phase 1 soll in ungefähr 2 bis 4 Wochen realisiert werden und wird in diesem Diagramm dargestellt:

![Die Abbildungzeigt, dass Phase 1 soll in ungefähr 2 bis 4 Wochen realisiert werden](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

Phase 1 des Leitfadens privilegierten Zugriffs umfasst folgende Komponenten:

**1. Separates Administratorkonto für Administratoraufgaben**

Zu einfacheren Trennen von Internetrisiken (Phishingangriffe, Surfen im Web) aus Administratorrechte besitzen, erstellen Sie ein dediziertes Konto für alle Mitarbeiter mit Administratorrechten ausführen. Weitere Informationen finden in der veröffentlichten PAW-Anweisungen enthalten ist [hier](http://Aka.ms/CyberPAW).

**2. Privilegierten Zugriff Arbeitsstationen Phase 1: Active Directory-Administratoren**

Zu einfacheren Trennen von Internetrisiken (Phishingangriffe, Surfen im Web) von Domänenadministratorrechten, erstellen Sie dedizierte privilegierten Zugriff Arbeitsstationen für Mitarbeiter mit Active Directory-Administratorrechten. Dies ist der erste Schrittdes PAW-Programm und Phase 1 der veröffentlichten Anleitung [hier](http://Aka.ms/CyberPAW).

**3. Eindeutige lokale Administratorkennwörter für Arbeitsstationen**

**4. Eindeutige lokale Administratorkennwörter für Server**

Um das Risiko, dass ein Angreifer stiehlt ein lokaler Administrator-Konto-Kennworthash aus der lokalen SAM-Datenbank und missbraucht auf andere Computer zu verringern, sollten Sie das LAPS-Tool verwenden, eindeutige zufällig generierte Kennwörter auf allen Arbeitsstationen und Servern konfigurieren und registrieren Sie diese Kennwörter in Active Directory. Sie erhalten die lokalen Administrator-Kennwort-Lösung für die Verwendung auf Arbeitsstationen und Servern [hier](http://Aka.ms/LAPS).

Finden Sie zusätzliche Hinweise zum Betreiben einer Umgebung mit LAPS und PAWs [hier](http://aka.ms/securitystandards).

### <a name="security-privileged-access-roadmap-stage-2"></a>Sicherheit Schutz des privilegierten Zugriffs: Phase 2
Phase 2 baut auf Schutzmaßnahmen aus Phase 1 und soll in ungefähr 1 bis 3Monaten realisiert werden. In diesem Diagramm werden die Schrittein dieser Phase dargestellt:

![Das Diagramm zeigt die Stufen der Phase 2](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

**1. PAW Phasen 2 und 3: alle Administratoren und zusätzliche Härtung**

Zum Trennen von Internetrisiken von alle privilegierten Administratorkonten fahren Sie mit der PAW, die Sie in Phase 1 gestartet, und richten Sie dedizierte Arbeitsstationen für alle Mitarbeiter mit privilegiertem Zugriff. Dies entspricht den Phasen 2 und 3 des Leitfadens veröffentlicht [hier](http://Aka.ms/CyberPAW).

**2. Zeitgebundene Berechtigungen (keine permanenten Administratoren)**

Zum Verkürzen der Dauer von Berechtigungen und steigern der Transparenz ihrer Verwendung, erteilen Sie Berechtigungen Just-in-Time (JIT) mithilfe einer entsprechend Lösung, z.B. der nachstehend:

-   Verwenden Sie für die Active Directory-Domänendienste (AD DS), Microsoft Identity Manager (MIM) des [Privileged Access Manager (PAM)](https://technet.microsoft.com/en-us/library/mt150258.aspx) Funktion.

-   Verwenden Sie für Azure Active Directory, [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM) Funktion.

**3. Mehrstufige Authentifizierung für zeitgebundene erhöhte Rechte**

Um den Sicherheitsgrad der Administratorauthentifizierung zu erhöhen, sollten Sie Multi-Factor Authentication vor dem Erteilen von Berechtigungen erforderlich.
Dies kann MIM PAM-Privileged Access Manager mithilfe von Azure Multi-Factor Authentication (MFA) erfolgen.

**4. Just Enough Administration (JEA) für die Wartung von Domänencontrollern**

Um die Anzahl der Konten mit Domänenadministratorberechtigungen und zugehörige Risiken zu verringern, verwenden Sie das Feature nur Enough Administration (JEA) in PowerShell, um allgemeine Wartungsvorgänge auf Domänencontrollern auszuführen. Die JEA-Technologie ermöglicht bestimmten Benutzern bestimmte Verwaltungsaufgaben auf Servern (wie Domänencontrollern) auszuführen, ohne Ihnen Administratorrechte. Laden Sie diese Anleitung aus [TechNet](http://aka.ms/JEA).

**5. Verkleinern der Angriffsfläche von Domänen und Domänencontrollern**

Um die Chancen von Angreifern die Kontrolle über eine Gesamtstruktur zu reduzieren, sollten Sie die Pfade verkürzen, die ein Angreifer die Kontrolle über Domänencontroller bzw. Objekte unter der Kontrolle der Domäne. Führen Sie die Anleitungen, die dieses Risikos veröffentlicht [hier](http://aka.ms/HardenAD).

**6. Erkennung von Angriffen**

Aktive Diebstähle von Anmeldeinformationen und Identität Sichtbarkeit befallen Angriffe, damit Sie rasch auf Vorfälle reagieren und den Schaden eindämmen können bereitstellen und konfigurieren [Microsoft Advanced Threat Analytics (ATA)](https://www.microsoft.com/ata).

Vor der Installation von ATA sollten Sie sicherstellen, dass Sie verfügen über einen Prozess um eine Sicherheitsvorfällen, die ggf. von ATA erkannt werden kann.

-   Weitere Informationen zum Einrichten eines Prozesses für die Reaktion auf Sicherheitsvorfälle finden Sie unter [Reaktion auf Sicherheitsvorfälle IT](https://aka.ms/irr) und "Reaktion auf verdächtige Aktivitäten" und "Wiederherstellung nach einem Sicherheitsvorfall"-Abschnitte [Mitigating Pass-the-Hash and Other Credential Theft](https://www.microsoft.com/pth), Version 2.

-   Weitere Informationen zum beauftragen von Microsoft-Diensten zur Unterstützung beim Vorbereiten Ihrer IR-Vorgang für ATA-Ereignisse und Bereitstellen von ATA erzeugt, wenden Sie sich an Ihren Microsoft-Mitarbeiter durch den Zugriff auf [auf dieser Seite](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

-   Zugriff [auf dieser Seite](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx) für Weitere Informationen zum beauftragen von Microsoft zur Unterstützung bei der Untersuchung und Wiederherstellung nach Incidents

-   Zum Implementieren von ATA befolgen Sie die verfügbare Bereitstellungshandbuch [hier](http://aka.ms/ata).

### <a name="security-privileged-access-roadmap-stage-3"></a>Sicherheit Schutz des privilegierten Zugriffs: Phase 3
Phase 3 des Leitfadens baut auf Schutzmaßnahmen aus den Phasen 1 und 2 zu stärken und Gegenmaßnahmen für das gesamte Spektrum hinzufügen. Phase 3 wird in diesem Diagramm visuell dargestellt:

![Diagramm, das Phase 3](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

Diese Funktionen werden bauen auf den Schutzmaßnahmen aus den vorherigen Phasen auf und sorgen in eine proaktivere Sicherheitslage.

**1. Modernisieren von Rollen und Delegierungsmodell**

Um Sicherheitsrisiken zu verringern, sollten Sie alle Aspekte Ihrer Rollen und Delegierungsmodell Delegierungsmodells ein wesentlicher Grundsatz gerecht zu Administratorrollen für Cloud-Dienst und werden an den Regeln des Tier-Modells neu entwerfen. Dieses Modell sollte die JIT- und JEA Funktionen bereitgestellt, die in früheren Phasen als auch Aufgabe Automatisierung Technologie zum Erreichen dieser Ziele nutzen.

**2. Smartcard- oder Passport-Authentifizierung für alle Administratoren**

Um die Sicherheitsstufe und Verwendbarkeit der Administratorauthentifizierung zu erhöhen, sollten Sie strenge Authentifizierung für alle Administratorkonten in Azure Active Directory und in Ihrer Windows Server Active Directory (einschließlich Konten im Verbund mit einem Cloud-Dienst) gehostet erfordern.

**3. Verwaltungsgesamtstruktur für Active Directory-Administratoren**

Um den stärksten Schutz für Active Directory-Administratoren zu bieten, richten Sie eine Umgebung, die keine sicherheitsabhängigkeiten auf Active Directory Ihrer Produktionsumgebung und aus Angriffe von allen Systemen in Ihrem Unternehmen isoliert ist. Weitere Informationen auf der ESAE-Architektur [auf dieser Seite](http://aka.ms/esae).

**4. Codeintegritätsrichtlinie für Domänencontroller (Server2016)**

Um das Risiko, dass nicht autorisierte Programme auf den Domänencontrollern Angreifer Angriff Abläufe und unbeabsichtigte administrative Fehler zu beschränken, konfigurieren Sie Windows Server2016-Codeintegrität für Kernelmodus (Treiber) und Benutzermodus (Anwendungen) zu, dass nur autorisierte ausführbare Dateien auf dem Computer ausführen.

**5. Abgeschirmte VMs für virtuelle Domänencontroller (Server2016 Hyper-V-Fabric)**

Verwenden Sie diese neue Server2016 Hyper-V-Funktion um virtualisierte Domänencontroller von Angriffsvektoren zu schützen, die inhärente Verlust eines virtuellen Computers, der physischen Sicherheit nutzen, um zu verhindern, dass den Diebstahl von Active Directory geheime Schlüssel von virtuellen Domänencontrollern. Mit dieser Lösung können Sie der Generation 2 VMs zum Schützen von Daten gegen Überprüfung, Diebstahl und Manipulation durch Speicher- und Administratoren als auch den Zugriff auf VMs gegen Angriffe von Hyper-V-Host Administratoren Härten verschlüsseln.

## <a name="am-i-done"></a>Fertig?
Dieses Leitfadens lernen starken privilegierten Zugriff Schutzmaßnahmen gegen Angriffe Sie, die derzeit zur Verfügung widersachern genutzt werden. Leider Sicherheitsrisiken werden ständig weiterentwickelt, und UMSCHALT, daher wird empfohlen, dass Sie die Sicherheit als laufenden Prozess konzentriert sich auf die Kosten steigen und reduziert die Erfolgsrate der Angreifer, die für Ihre Umgebung anzeigen.

Der Schutz des privilegierten Zugriffs ist ein erster wichtiger Schrittzum Einrichten von Sicherheitsstandards für Geschäftsressourcen in modernen Unternehmen, aber es ist nicht nur ein Teil eines kompletten-Programms, das Elemente wie Richtlinie, Operations, Informationssicherheit, Server, Anwendungen, PCs, Geräte, cloudfabric und andere Komponenten der Sicherheitsmaßnahmen, die Sie benötigen.

Weitere Informationen zum Erstellen einer vollständigen Sicherheits-Roadmap finden Sie im Abschnitt "Pflichten des Kunden und Roadmap" Microsoft Cloud Security for Enterprise Architects Dokument verfügbar [hier](http://aka.ms/securecustomer).

Weitere Informationen zum beauftragen von Microsoft Services zur Unterstützung bei diesen Themen erhalten Sie von Ihrem Microsoft-Partner oder [auf dieser Seite](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

### <a name="related-topics"></a>Verwandte Themen
[Geschmack of Premier: How to Pass-the-Hash und anderen Formen des Diebstahls von Anmeldeinformationen zu verringern](https://channel9.msdn.com/Blogs/Taste-of-Premier/Taste-of-Premier-How-to-Mitigate-Pass-the-Hash-and-Other-Forms-of-Credential-Theft)

[Microsoft Advanced Threat Analytics](http://aka.ms/ata)

[Schützen Sie abgeleiteter Domänenanmeldeinformationen mit Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx)

[Device Guard – Überblick](https://technet.microsoft.com/en-us/library/dn986865(v=vs.85).aspx)

[Schützen von wertvollen Assets mit sicheren Arbeitsstationen](https://msdn.microsoft.com/en-us/library/mt186538.aspx)

[Isolierter Benutzermodus in Windows10 mit Dave Probert (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-in-Windows-10-with-Dave-Probert)

[Isolierte Benutzermodusprozesse und Features in Windows10 mit Logan Gabriel (Channel 9)](http://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-Processes-and-Features-in-Windows-10-with-Logan-Gabriel)

[Informationen zu Prozessen und Features im isolierten Benutzermodus von Windows10 mit Dave Probert (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/More-on-Processes-and-Features-in-Windows-10-Isolated-User-Mode-with-Dave-Probert)

[Verringern den Diebstahl von Anmeldeinformationen mithilfe der Windows10 isolierter Benutzermodus (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Mitigating-Credential-Theft-using-the-Windows-10-Isolated-User-Mode)

[Aktivieren der strengen KDC-Überprüfung in Windows-Kerberos](https://www.microsoft.com/en-us/download/details.aspx?id=6382)

[Neues bei der Kerberosauthentifizierung für Windows Server 2012](https://technet.microsoft.com/library/hh831747.aspx)

[Zur Authentifizierungsmechanismussicherung für AD DS in Windows Server 2008 R2-Leitfaden](https://technet.microsoft.com/library/dd378897(v=ws.10).aspx)

[Trusted Platform Module](https://docs.microsoft.com/en-us/windows/device-security/tpm/trusted-platform-module-overview)
