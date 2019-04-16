---
ms.assetid: 84754c23-f039-4de4-a378-853942e662df
title: "Einführung in"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dc89afc47eb78a388238e8edf5059b0bec3006ad
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="introduction"></a>Einführung in

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Angriffe auf Computerinfrastrukturen – egal ob einfach oder komplex, gewesen sein, solange der Computer verfügen. Allerdings im letzten Jahrzehnt, wurde zunehmende Anzahl von Unternehmen aller Größen, in allen Teilen der Welt angegriffen und gefährdet Möglichkeiten, die die Bedrohungslage erheblich geändert wurden. Cyberkrieg und-Kriminalität haben sich mit rekordgeschwindigkeit erhöht. "Hacktivismus", in denen Angriffe offen Positionen gelegt werden wurde Geltendmachung, wie die Motivation für eine Reihe von sicherheitsverletzungen vorgesehen, um geheime Informationen von Organisationen, zum Erstellen von Denial-of-Service verfügbar zu machen oder sogar die Infrastruktur zu zerstören. Angriffe auf öffentliche und private Institutionen mit dem Ziel deutlich die Organisationen geistigen Eigentums (IP) geworden verschafft.  
  
Keine Organisation mit einer Infrastruktur Informationstechnologie (IT) ist gegen Angriffe immun, aber wenn geeigneten Richtlinien, Prozessen und Steuerelemente implementiert werden, um die wichtigsten Segmente für IT-Infrastruktur eines Unternehmens schützen, Ausweitung der Angriffe in zu einer kompletten Kompromittierung möglicherweise verhindert. Da der Anzahl und Größe der Zugriff von außerhalb der Organisation hat Bedrohung von innen in den letzten Jahren Weltrekordergebnisse, wird in diesem Dokument häufig externe Angreifer anstelle der Missbrauch von der Umgebung von autorisierten Benutzern erläutert. Dennoch die Prinzipien und Empfehlungen in diesem Dokument dienen zum Schutz Ihrer Umgebung gegen externe Angreifer und unwissende oder böswillige.  
  
Die Informationen und Empfehlungen in diesem Dokument werden stammen aus verschiedenen Quellen und von Verfahren, die Active Directory-Installationen vor Angriffen zu schützen. Obwohl es nicht möglich, Angriffe zu verhindern, dass ist, es ist möglich, die Active Directory-Angriffsfläche zu verringern und Kontrollen zu implementieren, die machen Gefährdung des Verzeichnisses viel schwieriger für Angreifer. Dieses Dokument bietet der am häufigsten verwendeten Arten von Sicherheitsrisiken, die wir beobachteten in gefährdeten Umgebungen und die häufigsten Empfehlungen, dass wir Kunden vorgenommen haben, um die Sicherheit ihrer Active Directory-Installationen zu verbessern.  
  
## <a name="account-and-group-naming-conventions"></a>Konto und die Gruppe benennen  
Die folgende Tabelle enthält eine Anleitung für die Benennungskonventionen für die Gruppen und Konten, die im gesamten Dokument verwiesen wird in diesem Dokument verwendet. In der Tabelle enthalten, ist der Speicherort jeder Konto/Gruppe, dem Namen und wie diese Konten/Gruppen in diesem Dokument verwiesen wird.  
  


|**Konto/Gruppe Speicherort**|**Name der Konto-Gruppe**|**Wie sie in diesem Dokument verwiesen wird**|
| --- | --- | --- |   
|Active Directory - jede Domäne|Administrator|Integrierte Administratorkonto|  
|Active Directory - jede Domäne|Administratoren|Integrierte Gruppe "Administratoren (BA)"|  
|Active Directory - jede Domäne|Domänen-Admins|Gruppe der Domäne "Administratoren" (DA)|  
|Active Directory - Gesamtstruktur-Stammdomäne|Organisations-Admins|Gruppe "Organisations-Admins (EA)"|  
|Lokaler Computer-Manager (SAM) Sicherheitskontendatenbank auf Computern unter Windows Server und Arbeitsstationen, die keine Domänencontroller sind.|Administrator|Lokales Administratorkonto|  
|Lokaler Computer-Manager (SAM) Sicherheitskontendatenbank auf Computern unter Windows Server und Arbeitsstationen, die keine Domänencontroller sind.|Administratoren|Lokale Gruppe "Administratoren"|  
  
## <a name="about-this-document"></a>Zu diesem Dokument  
Das Microsoft Information Security Risiko-Management (ISRM)-Organisation, das Teil von Microsoft Informationen Technologie (MSIT), kann mit Geschäftseinheiten, externe Kunden und Industry Peers zum Sammeln, Verbreitung und Definieren von Richtlinien, Verfahren und Steuerelemente. Diese Informationen können von Microsoft und unsere Kunden zum Erhöhen der Sicherheit und Verringern der Angriffsfläche von ihrer IT-Infrastrukturen verwendet werden. Die Empfehlungen in diesem Dokument basieren auf eine Reihe von Informationsquellen und Methoden, die innerhalb der MSIT und ISRM verwendet. Den folgenden Abschnitten werden weitere Informationen über die Ursprünge dieses Dokuments.  
  
### <a name="microsoft-it-and-isrm"></a>Microsoft-IT und ISRM  
Eine Reihe von Methoden und Steuerelemente wurden entwickelt, MSIT und ISRM, um die Microsoft AD DS-Gesamtstrukturen und Domänen zu schützen. Diese Steuerelemente sind allgemein anwendbar sind, haben sie in diesem Dokument integriert. SAFE-T (Solution Accelerators für neue) ist ein Team in ISRM, deren Produktarchitekturen neue Technologien zu identifizieren und sicherheitsanforderungen und Steuerelemente, um ihre Verbreitung beschleunigen definiert ist.  
  
### <a name="active-directory-security-assessments"></a>Active Directory Security Bewertungen  
In Microsoft ISRM, Bewertung, Consulting und Zugriffssteuerungseintrag (ACE) Engineering Team arbeitet mit internen Microsoft Unternehmenseinheiten und externe Kunden können Sie Anwendungs- und Sicherheitsereignisprotokoll Infrastruktur bewerten und taktische und strategische Orientierungshilfe Sicherheitsstatus Ihres Unternehmens zu erhöhen. Ein ACE-Service-Angebot ist der Active Directory-Sicherheit (Active Directory Migration Bewertung, ADSA), d. h. eine ganzheitliche Bewertung von AD DS-Umgebung eines Unternehmens, die Personen, Prozess und Technologie bewertet und kundenspezifische Empfehlungen erzeugt. Kunden sind mit Empfehlungen bereitgestellt, die auf der Organisation eindeutigen Eigenschaften, Methoden und Risikobereitschaft basieren. ADSAs wurden für Active Directory-Installationen bei Microsoft neben den unserer Kunden durchgeführt. Im Laufe der Zeit eine Reihe von Empfehlungen wurden bei Kunden mit unterschiedlichen Größen und Branchen gelten.  
  
### <a name="content-origin-and-organization"></a>Content Ursprung und Organisation  
Viele der Inhalte dieses Dokuments abgeleitet der ADSA und anderen ACE Team Bewertungen ausgeführt werden, für die betroffenen Kunden und Kunden, die keine erheblichen Gefährdung aufgetreten sind. Obwohl einzelne Kundendaten nicht zur Erstellung dieses Dokuments verwendet wurde, haben wir die am häufigsten ausgenutzten Sicherheitslücken, wir festgestellt haben, erfasst in unserer Bewertungen und Empfehlungen wurden für Kunden zur Verbesserung der Sicherheit ihrer AD DS-Installationen. Nicht alle Sicherheitsrisiken gelten für alle Umgebungen, und stellen Sie alle empfohlenen machbar ist, die in jedem Unternehmen implementiert.  
  
Dieses Dokument ist wie folgt aufgeteilt:  
  
## <a name="executive-summary"></a>Zusammenfassung  
Die zusammenfassende Übersicht, in der als eigenständiges Dokument oder in Kombination mit dem vollständigen Dokument gelesen werden kann, enthält eine Zusammenfassung der in diesem Dokument. Die zusammenfassende Übersicht enthält die am häufigsten verwendeten Angriffsvektoren, die wir beeinträchtigen kundenumgebungen, Zusammenfassung Empfehlungen feststellen für die Sicherung von Active Directory-Installationen und grundlegenden Ziele für Kunden, die neue AD DS-Gesamtstrukturen jetzt oder in der Zukunft bereitstellen möchten.  
  
### <a name="introduction"></a>Einführung in  
Dies ist der Bereich, den Sie lesen.  
  
### <a name="avenues-to-compromise"></a>Wege der Gefährdung  
Dieser Abschnitt enthält Informationen zu einigen der am häufigsten genutzt häufig Sicherheitsrisiken, die wir von Angreifern verwendet werden, Kunden Infrastrukturen manipulieren gefunden haben. In diesem Abschnitt beginnt mit der allgemeine Kategorien von Sicherheitslücken und wie sie anfänglich einzudringen Kunden Infrastrukturen Gefährdung auf zusätzliche Systeme verteilt und schließlich AD DS und Domänencontroller zum Abrufen der vollständige Kontrolle über Organisationen Gesamtstrukturen als Ziel verwendet werden.  
  
Dieser Abschnitt bietet keine detaillierte Vorschläge über jede Art von Sicherheitsrisiko, insbesondere in den Bereichen, in denen die Sicherheitslücken nicht verwendet werden, um Active Directory direkt als Ziel-Adressierung. Für jede Art von Sicherheitsrisiko, haben wir jedoch Links zu weiteren Informationen bereitgestellt, die Sie zum Entwickeln von Gegenmaßnahmen und Verringern der Angriffsfläche Ihrer Organisation verwenden können.  
  
### <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory  
In diesem Abschnitt beginnt mit der Bereitstellung Hintergrundinformationen zu privilegierten Konten und Gruppen in Active Directory, um die Informationen bereitzustellen, mit der die Gründe für die nachfolgenden Empfehlungen zum Schützen und Verwalten von privilegierten Gruppen und Konten zu verdeutlichen. Wir erläutern dann Ansätze müssen die Verwendung privilegierte Konten für die tägliche Verwaltung keine Berechtigungsebene erforderlich ist, die Gruppen wie z. B. der Gruppen Organisations-Admins (EA), Domänen-Admins (DA) und integrierte Administratoren (BA) in Active Directory gewährt wird. Als Nächstes stellen wir Richtlinien für das Sichern der privilegierte Gruppen und Konten und zum Implementieren von sicheren Verwaltungsmethoden und Systeme.  
  
Obwohl in diesem Abschnitt detaillierte Informationen zu den Einstellungen für diese Konfiguration bietet, haben wir auch Anhänge, die jede Empfehlung enthalten, die Schritt für Schritt-Anleitung zur Konfiguration, die geändert werden können oder können werden verwendet "wird als" für die Anforderungen der Organisation bereitstellen. In diesem Abschnitt abgeschlossen ist, indem Sie Informationen zum sicheren bereitstellen und Verwalten von Domänencontrollern, die zwischen den meisten repräsentative Motoröltemperatur gesicherten Systeme in der Infrastruktur sein sollte.  
  
### <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für Sicherheitsgefährdungen  
Ob Sie zuverlässige Sicherheit und Ereignissen, die Überwachung (SIEM) in Ihrer Umgebung implementiert haben oder andere Mechanismen zum Überwachen der Sicherheits der Infrastruktur verwenden, enthält dieser Abschnitt Informationen, die verwendet werden kann, um Ereignisse auf Windows-Systemen zu identifizieren, die darauf hinweisen, dass eine Organisation angegriffen wird. Wir erläutern herkömmlichen und erweiterte Überwachungsrichtlinien, einschließlich der tatsächlichen Konfiguration der überwachungsunterkategorien in den Betriebssystemen Windows 7 und Windows Vista. Dieser Abschnitt enthält umfassende Listen von Objekten und Systeme zu überwachen und ein zugehöriger Anhang enthält Ereignisse, die Sie überwachen soll, wenn das Ziel ist eine Gefährdung Zugriffsversuche erkennen.  
  
### <a name="planning-for-compromise"></a>Planen der Gefährdung  
In diesem Abschnitt beginnt, schrittweise"zurück" aus technischen Details konzentriert sich auf Prinzipien und Prozesse, die implementiert werden können, zum Identifizieren von Benutzern, Anwendungen und Systemen, die nicht nur auf die IT-Infrastruktur, die wichtigsten sind aber für das Unternehmen. Nach dem ermitteln, was besonders wichtig, um die Stabilität und die Vorgänge der Organisation ist, können Sie sich konzentrieren zum Trennung und zum Sichern dieser Ressourcen, ob diese geistiges Eigentum, Personen oder Systeme sind. In einigen Fällen Trennung und Sichern von Ressourcen können durchgeführt werden in Ihrer vorhandenen AD DS-Umgebung, während in anderen Fällen sollten Sie kleine, separate "Zellen" implementieren, mit denen Sie zum Herstellen einer sicheren Grenze, um diese Daten und überwachen diese Ressourcen strengere als weniger wichtige Komponenten. Ein Konzept mit der Bezeichnung "creative Zerstörung" wird mit dem legacy-Anwendungen und Systemen gelöscht werden können durch neue Lösungen erstellen einen Mechanismus wird beschrieben und im Abschnitt endet mit Empfehlungen, mit deren Hilfe eine sicherere Umgebung durch die Kombination von Unternehmen und IT-Informationen erstellt ein genaues Bild der normalen Betriebsstatus verwalten können. Sie bereits wissen, was für eine Organisation normal ist, können Auffälligkeiten, die darauf Angriffe und schränkt hinweisen leichter identifiziert werden.  
  
### <a name="summary-of-best-practice-recommendations"></a>Übersicht über bewährte Methoden  
Dieser Abschnitt enthält eine Tabelle, die die Empfehlungen in diesem Dokument vorgenommen werden zusammengefasst und ordnet sie nach relative Priorität, zusätzlich zum Bereitstellen von Links zu, in denen Weitere Informationen über jede Empfehlung im Dokument und Anlagen gefunden werden kann.  
  
### <a name="appendices"></a>Anhängen  
Anhänge sind in diesem Dokument beitragen, die Informationen in den Hauptteil des Dokuments enthalten. Die Liste der Anlagen und eine kurze Beschreibung der einzelnen ist in der folgenden Tabelle.  
  
 
|**Anhang**|**Beschreibung**|
| --- | --- | 
|[Anhang B: privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)|Enthält Hintergrundinformationen, die hilft Ihnen, die Benutzer und Gruppen, die Sie sich konzentrieren sollten zum Sichern, da sie von Angreifern gefährden und sogar löschen Ihrer Active Directory-Installation genutzt werden können.|  
|[Anhang C: geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)|Enthält Informationen zu geschützten Gruppen in Active Directory. Darüber hinaus enthält es Informationen beschränkt Anpassungen (Entfernung) von Gruppen, die gelten als geschützte Gruppen und von AdminSDHolder und SDProp betroffen sind.|  
|[Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)|Enthält Richtlinien, um das Administratorkonto in jeder Domäne in der Gesamtstruktur zu sichern.|  
|[Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)|Enthält Richtlinien, um die Gruppe "Organisations-Admins" in der Gesamtstruktur zu sichern.|  
|[Anhang F: Schützen von Domänenadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)|Enthält Richtlinien, um die Gruppe "Domänen-Admins" in jeder Domäne in der Gesamtstruktur zu sichern.|  
|[Anhang G: Schützen von Administratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)|Enthält Richtlinien zum Schutz der integrierten Administratorengruppe in jeder Domäne in der Gesamtstruktur.|  
|[Anhang H: schützen lokaler Administratorkonten und-Gruppen](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)|Enthält Richtlinien, um sichere lokale Administratorkonten und-Administratoren auf dem Domäne verbundene Server und Arbeitsstationen.|  
|[Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)|Enthält Informationen zum Erstellen von Konten, die Berechtigungen eingeschränkt und repräsentative Motoröltemperatur gesteuert werden können, aber kann zum Auffüllen von privilegierter Gruppen in Active Directory, wenn temporäre erhöhte Rechte erforderlich sind.|  
|[Anhang L: zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)|Listet die Ereignisse, die Sie in Ihrer Umgebung überwachen soll.|  
|[Anhang M: Links dokumentieren und empfohlene Lektüre](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)|Enthält eine Liste der empfehlenswerte Lektüre. Enthält auch eine Liste mit Links zu externen Dokumenten und ihre URLs, so dass Leser Kopien von diesem Dokument diese Informationen zugreifen können.|  
  


