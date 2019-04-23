---
ms.assetid: 84754c23-f039-4de4-a378-853942e662df
title: Einführung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8e2717af6183944b26a71e55b36f31cef51cf2e7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831871"
---
# <a name="introduction"></a>Einführung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Angriffe auf Computerinfrastrukturen – egal ob einfach oder komplex gewesen, solange Computer verfügen. Allerdings wurden im letzten Jahrzehnt eine zunehmende Anzahl von Organisationen weltweit auf Arten angegriffen und gefährdet, die die Bedrohungslage erheblich verändert haben. Cyberkrieg und -kriminalität haben sich mit Rekordgeschwindigkeit verstärkt. "Hacktivismus", in denen Angriffe durch ganze Positionen, motiviert werden wurde häufig in Anspruch genommenen, wie die Motivation für eine Reihe von sicherheitsverletzungen vorgesehen, um Organisationen geheime Informationen zum Erstellen von Authentifizierungsversuchen-of-Service verfügbar zu machen oder sogar die Infrastruktur zu zerstören. Angriffe auf öffentliche und private Institutionen mit dem Ziel der Gewinnung der Unternehmen geistiges Eigentum (IP) geworden allgegenwärtig.  
  
Keine Organisation mit einer Infrastruktur der Informationstechnologie (IT) ist immun vor Angriffen, jedoch wenn geeigneten Richtlinien, Prozesse und Steuerelemente implementiert werden, um wichtige Teile einer Organisation Computinginfrastruktur, die Ausweitung der Angriffe aus zu schützen. möglicherweise vermeidbaren Penetrationstests Gefährdung abgeschlossen. Da die Anzahl und die Skalierung von Angriffen von außerhalb einer Organisation hat Bedrohung von innen in den letzten Jahren Weltrekordergebnisse, erläutert in diesem Dokument häufig externe Angreifer anstelle der Missbrauch von der Umgebung durch autorisierte Benutzer. Dennoch die Prinzipien und Empfehlungen in diesem Dokument dienen dem Schutz Ihrer Umgebung gegen externe Angreifer und unwissende oder böswillige interne Benutzer zu schützen.  
  
Die Informationen und Empfehlungen in diesem Dokument werden stammen aus verschiedenen Quellen und von Verfahren, die Active Directory--Installationen vor Angriffen zu schützen. Obwohl es nicht möglich, Angriffe zu verhindern, ist es möglich ist, die Active Directory-Angriffsfläche zu verringern und Kontrollen zu implementieren, die machen die Gefährdung des Verzeichnisses sehr viel schwieriger für Angreifer dar. Dieses Dokument enthält die am häufigsten verwendeten Arten von Sicherheitsrisiken haben wir beobachteten in gefährdeten Umgebungen und die häufigsten Empfehlungen, dass wir Kunden vorgenommen haben, zur Verbesserung der Sicherheit ihrer Active Directory-Installationen.  
  
## <a name="account-and-group-naming-conventions"></a>Konto und das Benennen von Konventionen  
Die folgende Tabelle enthält eine Anleitung für die Benennungskonventionen, die in diesem Dokument verwendet wird, für die Gruppen und Konten, die in diesem Dokument verwiesen wird. In der Tabelle enthalten, ist der Speicherort der einzelnen Konten oder Gruppen, dessen Name und wie diese Konten/Gruppen in diesem Dokument verwiesen wird.  
  


|**Speicherort für Konten oder Gruppen**|**Name der Konten oder Gruppen**|**Wie sie in diesem Dokument verwiesen wird**|
| --- | --- | --- |   
|Active Directory – jede Domäne|Administrator|Das integrierte Administratorkonto|  
|Active Directory – jede Domäne|Administratoren|Integrierte Gruppe "Administratoren (BA);"|  
|Active Directory – jede Domäne|Domänen-Admins|Domänen-Admins (DA)-Gruppe|  
|Active Directory - Gesamtstruktur-Stammdomäne|Organisations-Admins|Enterprise-Administratoren (EA)-Gruppe|  
|Datenbank für den lokalen Computer Security-Accounts-Manager (SAM) auf Computern unter Windows Server und Arbeitsstationen, die keine Domänencontroller sind.|Administrator|Lokales Administratorkonto|  
|Datenbank für den lokalen Computer Security-Accounts-Manager (SAM) auf Computern unter Windows Server und Arbeitsstationen, die keine Domänencontroller sind.|Administratoren|Lokale Gruppe "Administratoren"|  
  
## <a name="about-this-document"></a>Zu diesem Dokument  
Die Organisation Microsoft Information Security and Risk Management (ISRM), die Teil von den Microsoft-Technologie (MSIT) ist, funktioniert mit internen Geschäftseinheiten, externe Kunden und Branche Peers zu erfassen, verbreiten und Richtlinien zu definieren, Methoden, und Steuerelemente. Diese Informationen können von Microsoft und unseren Kunden die Sicherheit erhöhen und verringern die Angriffsfläche ihrer IT-Infrastrukturen verwendet werden. Die Empfehlungen in diesem Dokument basieren auf eine Reihe von Quellen und Methoden, die in MSIT und ISRM verwendet. Die folgenden Abschnitte enthalten weitere Informationen über die Herkunft dieses Dokuments.  
  
### <a name="microsoft-it-and-isrm"></a>Microsoft IT und ISRM  
Eine Reihe von Methoden und Steuerelemente wurden entwickelt, MSIT und ISRM zum Schutz des Microsoft AD DS-Gesamtstrukturen und Domänen. Diese Steuerelemente allgemein anwendbar sind, wurden sie in diesem Dokument integriert. SAFE-T (Solution Accelerators für die neue Technologien) ist ein Team in ISRM, deren Charta um neue Technologien zu identifizieren, und klicken Sie zum Definieren von sicherheitsanforderungen und Steuerelemente zur Beschleunigung der Einführung ist.  
  
### <a name="active-directory-security-assessments"></a>Active Directory Security Assessment  
In Microsoft ISRM, Bewertung, Beratung und Zugriffssteuerungseintrag (ACE) Engineering-Team arbeitet mit internen Geschäftseinheiten von Microsoft und externe Kunden können Sie Anwendungs- und Infrastrukturprobleme Sicherheit zu bewerten und taktischen und strategische Anleitung dienen zum Erhöhen der Sicherheitsstatus des Unternehmens. Ein ACE-Service-Angebot ist die Active Directory-Sicherheit (Active Directory Migration Bewertung, ADSA), handelt es sich eine ganzheitliche Bewertung der AD DS-Umgebung eines Unternehmens, die bewertet die Menschen, Prozesse und Technologie und erstellt Empfehlungen auf der kundenspezifischen. Kunden werden Empfehlungen bereitgestellt, die in der Organisation eindeutige Merkmale, Vorgehensweisen und risikobewertungen an basieren. ADSAs wurden für die Active Directory-Installationen von Microsoft, zusätzlich zu den Kunden durchgeführt. Im Laufe der Zeit wurden einige Empfehlungen gefunden, die für Kunden, die unterschiedliche Größen und Branchen angewendet werden.  
  
### <a name="content-origin-and-organization"></a>Ursprung und Organisation der Inhalte  
Ein Großteil der Inhalt dieses Dokuments stammen aus der ADSA und anderen ACE-Team Bewertung für gefährdete Kunden und Kunden, die keine erheblichen Gefährdung aufgetreten sind. Obwohl die Daten der einzelnen Kunden nicht zur Erstellung dieses Dokuments verwendet wurde, haben wir die am häufigsten ausgenutzten Sicherheitslücken, wir haben ermittelt, gesammelt haben wir in unserer Analyse und die Empfehlungen für Kunden vorgenommen, zur Verbesserung der Sicherheit ihrer AD DS Installationen. Nicht alle Sicherheitsrisiken gelten für alle Umgebungen, und auch nicht alle Empfehlungen können in jedem Unternehmen implementiert werden.  
  
In diesem Dokument sind wie folgt gegliedert:  
  
## <a name="executive-summary"></a>Kurzfassung  
Die zusammenfassende Übersicht, in der als eigenständiges Dokument oder in Kombination mit dem vollständigen Dokument gelesen werden kann, bietet es sich um eine Zusammenfassung der in diesem Dokument. In der Zusammenfassung Executive enthalten sind die am häufigsten verwendeten Angriffsvektoren, die wir beobachtet haben, gefährdet kundenumgebungen, Zusammenfassung Empfehlungen zum Absichern von Active Directory-Installationen und grundlegenden Ziele für Kunden, die neue AD DS bereitstellen möchten Gesamtstrukturen jetzt oder in der Zukunft.  
  
### <a name="introduction"></a>Einführung  
Dies ist der Abschnitt, die, den Sie lesen.  
  
### <a name="avenues-to-compromise"></a>Wege der Gefährdung  
Dieser Abschnitt enthält Informationen zu einigen der am häufigsten häufig genutzt, Sicherheitsrisiken, die wir gefunden haben, um die von Angreifern verwendet werden, um Kunden Infrastrukturen zu gefährden. Dieser Abschnitt beginnt mit allgemeinen Kategorien von Sicherheitsrisiken und wie sie genutzt werden, um anfänglich durchdringen Kunden Infrastrukturen Gefährdung über zusätzliche Systeme hinweg verteilt und später abzielt AD DS und der Domänencontroller zum Abrufen der vollständigen Steuerung des Unternehmens Gesamtstrukturen.  
  
Dieser Abschnitt bietet keine detaillierte Empfehlungen zur Adressierung von jeder Art von Sicherheitsrisiko, insbesondere in den Bereichen, die in denen die Sicherheitslücken nicht verwendet werden, um direkt auf die Active Directory als Ziel. Für jede Art von Sicherheitsrisiko, haben wir allerdings Links zu weiteren Informationen bereitgestellt, die Sie verwenden können, Gegenmaßnahmen entwickeln und reduzieren die Angriffsfläche Ihrer Organisation.  
  
### <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory  
Dieser Abschnitt beginnt, durch die Bereitstellung von Informationen über privilegierte Konten und Gruppen in Active Directory, die Informationen bereitzustellen, können die Gründe für die nachfolgenden Empfehlungen zum Sichern und Verwalten von privilegierten Gruppen verdeutlichen und Konten. Dann besprechen wir Ansätze, um den Bedarf reduzieren, der höher privilegierte Konten für die tägliche Verwaltung verwenden, das kein Berechtigungsebene erfordert, das Gruppen wie z. B. das Enterprise-Administratoren (EA), Domänen-Admins (DA) und integrierte gewährt wird Administratoren (BA)-Gruppen in Active Directory. Anschließend geben wir Anleitungen zum Sichern von privilegierten Gruppen und Konten und zum Implementieren von sicheren administrative Verfahren und Systemen.  
  
Obwohl in diesem Abschnitt ausführliche Informationen zu diesen Konfigurationseinstellungen enthält, haben wir auch eingefügt, Anhänge für jede Empfehlung ein, die schrittweise konfigurationsanweisungen zu, die möglich verwendet bieten "wird als" oder geändert werden kann, für die Anforderungen der Organisation. In diesem Abschnitt wird durch die Bereitstellung von Informationen zum sicheren bereitstellen und Verwalten von Domänencontrollern, die für die meisten repräsentative Motoröltemperatur gesicherte Systeme in der Infrastruktur werden beendet.  
  
### <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für einen Kompromiss  
Dieser Abschnitt enthält Informationen, die zum Identifizieren der Ereignisse in Windows verwendet werden kann, ob Sie implementiert haben, robuste Sicherheit und Überwachung (SIEM) in Ihrer Umgebung oder andere Mechanismen zum Überwachen der Sicherheits der Infrastruktur verwenden, Systeme, die können bedeuten, dass eine Organisation angegriffen werden wird. Herkömmliche und erweiterten Überwachungsrichtlinien, einschließlich der tatsächlichen Konfiguration der von überwachungsunterkategorien in den Betriebssystemen Windows 7 und Windows Vista besprochen. Dieser Abschnitt enthält umfassende Listen von Objekten und Systeme zu überwachen, und ein zugeordnete Anhang enthält Ereignisse, die für die Sie überwachen sollten, wenn das Ziel ist die Gefährdung Versuche zu erkennen.  
  
### <a name="planning-for-compromise"></a>Planen der Gefährdung  
Dieser Abschnitt beginnt, durch "schrittweises Back" aus der technischen Details zu konzentrieren, Prinzipien und Vorgängen, die implementiert werden können, um zu ermitteln, die Benutzern, Anwendungen und Systemen, die wichtigsten nicht nur für die IT-Infrastruktur sind jedoch für das Unternehmen. Nach dem ermitteln, was die wichtigsten, um die Stabilität und den Betrieb Ihrer Organisation ist, kann Ihr Schwerpunkt auf einzuschränken, und Sichern von diesen Ressourcen, ob diese geistiges Eigentum oder Personen und Systemen sind. In einigen Fällen einzuschränken, und Sichern von Ressourcen ausgeführt werden können in die vorhandene AD DS-Umgebung, während in anderen Fällen sollten Sie kleine, separate "Zellen" implementieren, mit denen Sie eine sichere Grenze um kritische Ressourcen herzustellen und diese Ports überwachen Assets präziser als weniger wichtige Komponenten. Ein Konzept namens "creative Zerstörung" handelt es sich einen Mechanismus mit dem legacy-Anwendungen und Systemen lässt durch neue Lösungen zu erstellen, wird erläutert, und der Abschnitt endet mit Empfehlungen, die helfen können, um eine sicherere Umgebung durch verwalten Das Kombinieren von Geschäfts- und IT-Informationen, um einen detaillierten Überblick über die neuerungen eine normale Betriebszustand zu erstellen. Wissen Sie, was für eine Organisation normal ist, können Anomalien, die Angriffe und schränkt möglicherweise leichter identifiziert werden.  
  
### <a name="summary-of-best-practice-recommendations"></a>Zusammenfassung der Best Practice-Empfehlungen  
Dieser Abschnitt enthält eine Tabelle, die die Empfehlungen in diesem Dokument werden zusammengefasst und sortiert diese nach relative Priorität und zusätzlich zur Bereitstellung von Links zu, in dem Weitere Informationen zu jeder Empfehlung im Dokument und dessen Anhänge gefunden werden kann.  
  
### <a name="appendices"></a>Anhänge  
Anhänge sind in diesem Dokument erweitern, die Informationen in den Text des Dokuments enthalten. Die Liste der Anhänge und eine kurze Beschreibung der einzelnen enthalten ist in der folgenden Tabelle.  
  
 
|**Anhang**|**Beschreibung**|
| --- | --- | 
|[Anhang B: Privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)|Enthält Hintergrundinformationen, mit dem Sie die Benutzer und Gruppen, denen, die Sie sich konzentrieren sollten, die zum Sichern, da sie von Angreifern zu beeinträchtigen und zu zerstörender auch Ihrer Active Directory-Installation genutzt werden können.|  
|[Anhang C: Geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)|Enthält Informationen zu geschützten Gruppen in Active Directory. Es enthält auch Informationen für begrenzte Anpassungen (entfernen) von Gruppen, die geschützte Gruppen gelten und AdminSDHolder und SDProp betroffen sind.|  
|[Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)|Enthält Richtlinien, um das Administratorkonto in jeder Domäne in der Gesamtstruktur zu sichern.|  
|[Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)|Enthält Richtlinien zum Sichern der Gruppe "Organisations-Admins" in der Gesamtstruktur.|  
|[Anhang F: Schützen von Domänenadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)|Enthält Richtlinien zum Sichern der Gruppe "Domänen-Admins" in jeder Domäne in der Gesamtstruktur.|  
|[Anhang G: Schützen von Administratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)|Enthält Richtlinien, um die integrierte Administratorengruppe in jeder Domäne in der Gesamtstruktur zu sichern.|  
|[Anhang H: Schützen lokaler Administratorkonten und-Gruppen](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)|Enthält Richtlinien, um sichere lokale Administratorkonten und die Administratorgruppe für die Domäne eingebundenen Server und Arbeitsstationen.|  
|[Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)|Enthält Informationen zum Erstellen von Konten, die über eingeschränkte Berechtigungen und repräsentative Motoröltemperatur gesteuert werden können, jedoch können verwendet werden, um privilegierten Gruppen in Active Directory auffüllen, wenn temporäre erhöhte Rechte erforderlich sind.|  
|[Anhang L: Zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)|Listet die Ereignisse, die Sie in Ihrer Umgebung überwachen soll.|  
|[Anhang M: Links zu Dokumenten und empfohlene Lektüre](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)|Enthält eine Liste der empfohlene Literatur. Enthält auch eine Liste mit Links zu externen Dokumenten und den URLs, sodass Leser Ausdrucke dieses Dokuments diese Informationen zugreifen können.|  
  


