---
ms.assetid: 84754c23-f039-4de4-a378-853942e662df
title: Einführung
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e9df8c913db5c25b53abd1f4fd8aad1c4dbe2e54
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070662"
---
# <a name="introduction"></a>Einführung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Angriffe auf Computer Infrastrukturen, ob einfach oder komplex, sind so lange vorhanden, wie es bei Computern der gibt. Allerdings wurden im letzten Jahrzehnt eine zunehmende Anzahl von Organisationen weltweit auf Arten angegriffen und gefährdet, die die Bedrohungslage erheblich verändert haben. Cyberkrieg und -kriminalität haben sich mit Rekordgeschwindigkeit verstärkt. "Hacktivismus", bei dem Angriffe durch Aktivisten Positionen motiviert werden, wurde als Motivation für eine Reihe von Sicherheitsverletzungen beansprucht, die dazu gedacht sind, geheime Informationen von Organisationen offenzulegen, Verweigerungen zu erstellen oder sogar die Infrastruktur zu zerstören. Angriffe auf öffentliche und private Institutionen mit dem Ziel, das geistige Eigentum (IP) der Organisation zu vereinigen, sind mittlerweile allgegenwärtig.

Keine Organisation mit einer IT-Infrastruktur (IT-Infrastruktur) ist gegen Angriffe geschützt, aber wenn geeignete Richtlinien, Prozesse und Kontrollen implementiert werden, um die Schlüsselsegmente der Computerinfrastruktur eines Unternehmens zu schützen, kann die Ausweitung von Angriffen vor der Durchführung der Kompromittierung möglicherweise vermeidbar sein. Da die Anzahl und die Skalierung von Angriffen, die von außerhalb einer Organisation ausgehen, Insider Bedrohungen in den letzten Jahren unterzogen haben, werden in diesem Dokument häufig externe Angreifer behandelt, anstatt die Umgebung durch autorisierte Benutzer zu missbrauchen. Trotzdem sind die Prinzipien und Empfehlungen in diesem Dokument zum Schutz Ihrer Umgebung gegen externe Angreifer und falsche oder böswillige Insider gedacht.

Die in diesem Dokument enthaltenen Informationen und Empfehlungen stammen aus einer Reihe von Quellen und werden von Verfahren abgeleitet, die zum Schutz von Active Directory-Installationen vor Gefährdung dienen. Obwohl es nicht möglich ist, Angriffe zu verhindern, ist es möglich, die Active Directory Angriffsfläche zu reduzieren und Steuerelemente zu implementieren, die eine Gefährdung des Verzeichnisses für Angreifer erschweren. Dieses Dokument enthält die häufigsten Arten von Sicherheitsrisiken, die wir in kompromittierten Umgebungen festgestellt haben, und die gängigsten Empfehlungen, die wir an unsere Kunden gerichtet haben, um die Sicherheit Ihrer Active Directory-Installationen zu verbessern.

## <a name="account-and-group-naming-conventions"></a>Benennungs Konventionen für Konten und Gruppen
Die folgende Tabelle enthält eine Anleitung zu den Benennungs Konventionen, die in diesem Dokument für die im gesamten Dokument referenzierten Gruppen und Konten verwendet werden. In der Tabelle ist der Speicherort der einzelnen Konten/Gruppen, deren Name und die Art und Weise, wie auf diese Konten/Gruppen verwiesen wird, in diesem Dokument angegeben.



|**Konto-/gruppenspeicherort**|**Name des Kontos/der Gruppe**|**Referenziert in diesem Dokument**|
| --- | --- | --- |
|Active Directory-jede Domäne|Administrator|Integriertes Administrator Konto|
|Active Directory-jede Domäne|Administratoren|Gruppe integrierter Administratoren (BA)|
|Active Directory-jede Domäne|Domänenadministratoren|Gruppe "Domänen-Admins" (da)|
|Stamm Domäne der Active Directory-Gesamtstruktur|Organisationsadministratoren|Organisations-Admins (EA)-Gruppe|
|Security Accounts Manager (Sam)-Datenbank auf Computern, auf denen Windows Server ausgeführt wird, und Arbeitsstationen, die keine Domänen Controller sind|Administrator|Lokales Administrator Konto|
|Security Accounts Manager (Sam)-Datenbank auf Computern, auf denen Windows Server ausgeführt wird, und Arbeitsstationen, die keine Domänen Controller sind|Administratoren|Lokale Administratoren Gruppe|

## <a name="about-this-document"></a>Informationen zu diesem Dokument
Die Organisation Microsoft Information Security and Risk Management (isrm), die Teil von Microsoft Information Technology (MSIT) ist, arbeitet mit internen Geschäftseinheiten, externen Kunden und Branchen Peers zusammen, um Richtlinien, Verfahren und Steuerelemente zu erfassen, zu verteilen und zu definieren. Diese Informationen können von Microsoft und unseren Kunden verwendet werden, um die Sicherheit zu erhöhen und die Angriffsfläche Ihrer IT-Infrastrukturen zu verringern. Die Empfehlungen in diesem Dokument basieren auf einer Reihe von Informationsquellen und-Methoden, die in MSIT und isrm verwendet werden. Die folgenden Abschnitte enthalten weitere Informationen zu den Ursprüngen dieses Dokuments.

### <a name="microsoft-it-and-isrm"></a>Microsoft IT und isrm
Es wurden eine Reihe von Methoden und Steuerelementen in MSIT und isrm entwickelt, um die Microsoft AD DS-Gesamtstrukturen und-Domänen zu sichern. Wenn diese Steuerelemente allgemein anwendbar sind, wurden Sie in dieses Dokument integriert. Safe-T (Solution Accelerators für aufstrebende Technologien) ist ein Team innerhalb von isrm, dessen Satzung darin besteht, neue Technologien zu identifizieren und Sicherheitsanforderungen und-Kontrollen zu definieren, um Ihre Akzeptanz zu beschleunigen.

### <a name="active-directory-security-assessments"></a>Sicherheitsbewertungen Active Directory
Innerhalb von Microsoft isrm arbeitet das Assessment-, Consulting-und Engineering-Team mit internen Microsoft-Geschäftseinheiten und externen Kunden zusammen, um die Anwendungs-und Infrastruktur Sicherheit zu bewerten und taktische und strategische Anleitungen bereitzustellen, um die Sicherheitslage des Unternehmens zu erhöhen. Bei einem ACE-Dienst Angebot handelt es sich um die Active Directory Security Assessment (ADSA), bei der es sich um eine ganzheitliche Bewertung der AD DS Umgebung einer Organisation handelt, die Personen, Prozesse und Technologien bewertet und kundenspezifische Empfehlungen erzeugt. Kunden erhalten Empfehlungen, die auf den besonderen Merkmalen, Praktiken und Risikobereitschaft der Organisation basieren. Zusätzlich zu den Kunden von Microsoft wurden adsas für Active Directory Installationen bei Microsoft ausgeführt. Im Laufe der Zeit wurde eine Reihe von Empfehlungen für Kunden mit unterschiedlichen Größen und branchenfest gestellt.

### <a name="content-origin-and-organization"></a>Ursprung und Organisation der Inhalte
Ein Großteil des Inhalts dieses Dokuments wird von den ADSA-und anderen ACE-Team Bewertungen abgeleitet, die für kompromittierte Kunden und Kunden durchgeführt wurden, die keinen erheblichen Kompromiss hatten. Obwohl die einzelnen Kundendaten nicht zum Erstellen dieses Dokuments verwendet wurden, haben wir die am häufigsten genutzten Sicherheitslücken gesammelt, die wir in unseren Bewertungen identifiziert haben, sowie die Empfehlungen, die wir an unsere Kunden gerichtet haben, um die Sicherheit Ihrer AD DS Installationen zu verbessern. Nicht alle Sicherheitsrisiken gelten für alle Umgebungen, und auch nicht alle Empfehlungen können in jedem Unternehmen implementiert werden.

Dieses Dokument ist wie folgt organisiert:

## <a name="executive-summary"></a>Kurzfassung
Die Zusammenfassung der Executive, die als eigenständiges Dokument oder in Kombination mit dem vollständigen Dokument gelesen werden kann, enthält eine allgemeine Zusammenfassung dieses Dokuments. In der Zusammenfassung der Zusammenfassungen sind die häufigsten Angriffsvektoren, die wir zur Gefährdung von Kundenumgebungen verwendet haben, zusammenfassende Empfehlungen zum Sichern von Active Directory Installationen und grundlegende Ziele für Kunden, die jetzt oder in Zukunft neue AD DS-Gesamtstrukturen bereitstellen möchten.

### <a name="introduction"></a>Einführung
Dies ist der Abschnitt, den Sie jetzt lesen.

### <a name="avenues-to-compromise"></a>Wege der Gefährdung
Dieser Abschnitt enthält Informationen zu einigen der am häufigsten genutzten Sicherheitsrisiken, die von Angreifern zum kompromittieren der Infrastruktur von Kunden verwendet wurden. Dieser Abschnitt beginnt mit allgemeinen Kategorien von Sicherheitsrisiken und deren Verwendung, um die Infrastruktur der Kunden zunächst zu durchdringen, Kompromittierung auf zusätzliche Systeme weiterzuleiten und schließlich AD DS und Domänen Controllern als Ziel zu dienen, um vollständige Kontrolle über die Gesamtstrukturen der Organisationen

Dieser Abschnitt enthält keine ausführlichen Empfehlungen zur Behandlung der einzelnen Sicherheitsrisiken, insbesondere in den Bereichen, in denen die Sicherheitsrisiken nicht zum direkten Ziel Active Directory verwendet werden. Allerdings haben wir für jede Art von Sicherheits Anfälligkeit Links zu zusätzlichen Informationen bereitgestellt, mit denen Sie Gegenmaßnahmen entwickeln und die Angriffsfläche Ihrer Organisation reduzieren können.

### <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory
In diesem Abschnitt werden zunächst Hintergrundinformationen zu privilegierten Konten und Gruppen in Active Directory bereitgestellt, um die Informationen bereitzustellen, mit denen die Gründe für das Sichern und verwalten privilegierter Gruppen und Konten erläutert werden. Anschließend werden die Ansätze erläutert, um die Notwendigkeit zu verringern, Konten mit hohen Berechtigungen für die tägliche Verwaltung zu verwenden. Dies erfordert nicht die Berechtigungsebene, die Gruppen wie Organisations-Admins (Enterprise Admins, EA), Domänen-Admins (da) und integrierten Administratoren (BA) in Active Directory gewährt werden. Als Nächstes stellen wir eine Anleitung zum Sichern der privilegierten Gruppen und Konten sowie zum Implementieren sicherer administrativer Verfahren und Systeme bereit.

Obwohl dieser Abschnitt ausführliche Informationen zu diesen Konfigurationseinstellungen enthält, haben wir auch Anhänge für jede Empfehlung eingefügt, die schrittweise Konfigurations Anweisungen bereitstellen, die "wie besehen" oder für die Anforderungen der Organisation geändert werden können. In diesem Abschnitt werden Informationen zur sicheren Bereitstellung und Verwaltung von Domänen Controllern bereitgestellt, die in der-Infrastruktur zu den strengsten gesicherten Systemen gehören.

### <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für einen Kompromiss
Wenn Sie in Ihrer Umgebung robuste Sicherheitsinformationen und Ereignisüberwachung (SIEM) implementiert haben oder andere Mechanismen zur Überwachung der Sicherheit der Infrastruktur verwenden, finden Sie in diesem Abschnitt Informationen, die zur Identifizierung von Ereignissen auf Windows-Systemen verwendet werden können, die möglicherweise darauf hindeuten, dass eine Organisation angegriffen wird. Wir erörtern die herkömmlichen und erweiterten Überwachungs Richtlinien, einschließlich der effektiven Konfiguration der Überwachungs Unterkategorien in den Betriebssystemen Windows 7 und Windows Vista. Dieser Abschnitt enthält umfassende Liste der zu überwachenden Objekte und Systeme, und in einem zugeordneten Anhang werden Ereignisse aufgelistet, die Sie überwachen sollten, wenn das Ziel das Erkennen von kompromittierten versuchen ist.

### <a name="planning-for-compromise"></a>Planen der Gefährdung
In diesem Abschnitt geht es um die "Rücksprung" von technischen Details, um sich auf Prinzipien und Prozesse zu konzentrieren, die implementiert werden können, um die Benutzer, Anwendungen und Systeme zu identifizieren, die nicht nur für die IT-Infrastruktur, sondern auch für das Unternehmen von entscheidender Bedeutung sind. Nachdem Sie ermittelt haben, was für die Stabilität und den Betrieb Ihrer Organisation am wichtigsten ist, können Sie sich auf das Trennen und sichern dieser Assets konzentrieren, egal ob es sich um geistiges Eigentum, Personen oder Systeme handelt. In einigen Fällen kann das aufteilen und Sichern von Assets in Ihrer vorhandenen AD DS Umgebung erfolgen. in anderen Fällen sollten Sie jedoch die Implementierung von kleinen, separaten "Zellen" in Erwägung gezogen werden, die es Ihnen ermöglichen, eine sichere Grenze um wichtige Ressourcen zu schaffen und diese Objekte flexibler zu überwachen als weniger kritische Komponenten. Ein Konzept namens "Creative Zerstörung", bei dem es sich um einen Mechanismus handelt, mit dem ältere Anwendungen und Systeme durch das Erstellen neuer Lösungen eliminiert werden können, finden Sie unter. der Abschnitt endet mit Empfehlungen, die Ihnen helfen, eine sicherere Umgebung zu erhalten, indem Sie Geschäfts-und IT-Informationen kombinieren, um ein detailliertes Bild der normalen Betriebsstatus zu erstellen. Wenn Sie wissen, was für eine Organisation normal ist, können Anomalien, die auf Angriffe und Kompromisse hindeuten können, leichter identifiziert werden.

### <a name="summary-of-best-practice-recommendations"></a>Zusammenfassung der Empfehlungen zu bewährten Methoden
Dieser Abschnitt enthält eine Tabelle, in der die Empfehlungen in diesem Dokument zusammengefasst und nach relativer Priorität sortiert werden. Außerdem werden Links zu bereitgestellt, wo weitere Informationen zu den einzelnen Empfehlungen im Dokument und seinen Appendices zu finden sind.

### <a name="appendices"></a>Anhänge
In diesem Dokument sind Appendices enthalten, um die im Hauptteil des Dokuments enthaltenen Informationen zu erweitern. Die folgende Tabelle enthält die Liste der Anhänge und eine kurze Beschreibung der einzelnen Anhänge.


|**Anhang**|**Beschreibung**|
| --- | --- |
|[Anhang B: Privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)|Bietet Hintergrundinformationen, die Ihnen helfen, die Benutzer und Gruppen zu identifizieren, auf die Sie sich konzentrieren sollten, da Sie von Angreifern genutzt werden können, um Ihre Active Directory-Installation zu gefährden und sogar zu zerstören.|
|[Anhang C: Geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)|Enthält Informationen zu geschützten Gruppen in Active Directory. Sie enthält außerdem Informationen für die eingeschränkte Anpassung (Entfernung) von Gruppen, die als geschützte Gruppen angesehen werden und von AdminSDHolder und SDPROP betroffen sind.|
|[Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)|Enthält Richtlinien zum Sichern des Administrator Kontos in jeder Domäne in der Gesamtstruktur.|
|[Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)|Enthält Richtlinien zum Sichern der Gruppe "Organisations-Admins" in der Gesamtstruktur.|
|[Anhang F: Schützen von Domänenadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)|Enthält Richtlinien zum Sichern der Gruppe "Domänen-Admins" in jeder Domäne in der Gesamtstruktur.|
|[Anhang G: Schützen von Administratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)|Enthält Richtlinien zum Sichern der integrierten Gruppe "Administratoren" in jeder Domäne in der Gesamtstruktur.|
|[Anhang H: Schützen lokaler Administratorkonten und -gruppen](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)|Enthält Richtlinien zum Sichern von lokalen Administrator Konten und Administratoren Gruppen auf in die Domäne eingebundenen Servern und Arbeitsstationen.|
|[Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)|Stellt Informationen zum Erstellen von Konten mit eingeschränkten Rechten bereit und kann stringente gesteuert werden. Sie können jedoch auch zum Auffüllen privilegierter Gruppen in Active Directory verwendet werden, wenn eine temporäre Erhöhung erforderlich ist.|
|[Anhang L: Zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)|Listet Ereignisse auf, für die Sie in Ihrer Umgebung überwachen sollten.|
|[Anhang M: Links zu Dokumenten und empfohlene Lektüre](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)|Enthält eine Liste der empfohlenen Lesevorgänge. Enthält außerdem eine Liste mit Links zu externen Dokumenten und deren URLs, damit Leser von fest Kopien dieses Dokuments auf diese Informationen zugreifen können.|



