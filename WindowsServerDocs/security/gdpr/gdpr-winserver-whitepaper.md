---
title: Ihre Reise in die Datenschutz-Grundverordnung (DSGVO) für Windows Server 2016
description: Verwenden in diesen Artikel, um zu verstehen, was GDPR ist und die Produkte von Microsoft, um Ihnen den Einstieg zur Kompatibilität zu erleichtern.
ms.technology: techgroup-security
ms.topic: article
ms.date: 09/25/2017
ms.author: nirb
author: nirb-ms
ms.openlocfilehash: f196be152e339b229c4c476f73a2d4b0e7a644d5
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69980317"
---
# <a name="beginning-your-general-data-protection-regulation-gdpr-journey-for-windows-server"></a>Starten ihrer Datenschutz-Grundverordnung-Journey (dsgvo) für Windows Server 

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieser Artikel enthält Informationen zu den GDPR, einschließlich einer Beschreibung und der Produkte von Microsoft, um Ihnen den Einstieg in die Kompatibilität zu erleichtern.

## <a name="introduction"></a>Einführung
Am 25. Mai 2018 tritt ein europäisches Datenschutzgesetze in Kraft, das ein neues globales Niveau für Datenschutz, Sicherheit und Compliance festlegt.

Die allgemeine Data Protection-Richtlinie, oder GDPR, ist im Grunde über Schutz und Aktivierung des Datenschutzrechts von Personen. Die GDPR stellt strikte globale Datenschutzanforderungen über die Verwaltung und den persönlichen Schutz von Daten bei gleichzeitiger Wahrung der Auswahl des Indviduums – unabhängig davon, wo die Daten gesendet, verarbeitet oder gespeichert werden.

Microsoft und unsere Kunden bemühen sich aktuell, die Ziele des Datenschutzes der GDPR zu erzielen. Wir von Microsoft sind der Meinung, Datenschutz ist ein grundlegendes Recht, und wir glauben, dass die GDPR ein wichtiger Schritt für den Schutz und die Aktivierung des Datenschutzrechts von Personen ist. Aber wir wissen auch, dass eine GDPR wichtige Änderungen bei Organisationen weltweit erfordert.

Wir haben unser Engagement für die GDPR beschrieben und wie wir unsere Kunden unterstützen. Diese finden Sie in dem Blogbeitrag [Mit Microsoft-Cloud GDPR-kompatibel werden](https://blogs.microsoft.com/on-the-issues/2017/02/15/get-gdpr-compliant-with-the-microsoft-cloud/#hv52B68OZTwhUj2c.99) von unseren Chief Privacy Officer [Brendon Lynch](https://blogs.microsoft.com/on-the-issues/author/brendonlynch/) und dem Blogbeitrag [Sichern Sie Ihre Vertrauensstellung mit vertraglichen Verpflichtungen für die allgemeine Data Protection Verordnung](https://blogs.microsoft.com/on-the-issues/2017/04/17/earning-trust-contractual-commitments-general-data-protection-regulation/#6QbqoGWXCLavGM63.99) von [Rich Sauer](https://blogs.microsoft.com/on-the-issues/author/rsauer/) - Microsoft Corporate Vice President & Deputy General Counsel.

Auch wenn Ihrer Reise in die GDPR-Kompatibilität eine große Herausforderung zu sein scheint, wir sind hier, um Sie zu unterstützen. Spezifische Informationen über die GDPR, unsere Verpflichtungen und wie Sie Ihre Reise beginnen finden Sie im [GDPR-Abschnitt im Microsoft Trust Center](https://www.microsoft.com/en-us/trustcenter/privacy/gdpr).

## <a name="gdpr-and-its-implications"></a>GDPR und seine Folgen
Der GDPR ist eine komplexe Verordnung, die möglicherweise wesentliche Änderungen in Bezug auf das Sammeln, Verwenden und Verwalten von persönlichen Daten erfordert. Microsoft hilft seit langem seinen Kunden komplexe Bestimmungen zu befolgen, und bei der Vorbereitung auf den GDPR sind wir Ihr Partner auf dem Weg.

GDPR erzwingt Regeln für Organisationen, die Waren anbieten und an Personen in der Europäischen Union (EU) verkaufen, oder die Daten für Mitglieder der EU sammeln und analysieren, unabhängig davon, wo sich diese Unternehmen befinden. Im Folgenden finden Sie die Schlüsselelemente der GDPR:

- **Erweiterte persönliche Datenschutz Rechte.** Ein stärkerer Datenschutz für Einwohner der EU, um sicherzustellen, dass sie die Zugriffsberechtigung für den Zugriff auf ihre persönlichen Daten erhalten, Ungenauigkeiten in diesen Daten korrigieren, diese löschen können, bei der Verarbeitung ihrer persönlichen Daten Einspruch erheben und diese verschieben können.

- **Erhöhung der Aufgaben zum Schutz personenbezogener Daten.** Verstärkte Verantwortlichkeit von Organisationen, die personenbezogene Daten verwalten, mehr Klarheit der Verantwortung bei der Einhaltung der Kompatibilität.

- **Obligatorische Berichte zu personenbezogenen Datenverletzungen.** Organisationen, die Kontrolle über persönliche Daten haben müssen ihren zuständigen Behörden unverzüglich persönliche Datenverstöße melden, die die Rechte und Grundfreiheiten von Personen gefährden, und wenn möglich innerhalb von 72 Stunden nachdem die Verletzung bekannt wird.

Wie erwartet hat die GDPR einen erheblichen Einfluss auf Ihr Unternehmen und erfordert eventuell die Datenschutzrichtlinien zu aktualisieren, Datenschutzkontrollen und -verstoßprozeduren zu implementieren und zu stärken, transparente Richtlinien bereitzustellen und in IT und Schulungen weite zu investieren. Mit Microsoft Windows 10 können Sie effektiv und effizient einige der folgenden Anforderungen in den Griff bekommen.

## <a name="personal-and-sensitive-data"></a>Persönliche und vertrauliche Daten
Als Teil Ihres Aufwands zur Einhaltung der GDPR müssen Sie wissen, wie Verordnung persönliche und vertrauliche Daten definiert und wie diese Definitionen auf Daten Ihrer Organisation zutrifft. Basierend auf diesem Verständnis können Sie ermitteln, wo diese Daten erstellt, verarbeitet, verwaltet und gespeichert werden.

Die GDPR betrachtet persönliche Daten als alle Informationen im Zusammenhang mit einer bestimmten oder bestimmbare natürlichen Person. Dies bedeutet eine direkte Identifizierung (z. B. Ihr vollständiger Name) und eine indirekte Identifizierung (z. B. bestimmte Informationen, die Sie als Datenverweis identifiziert). Die GDPR verdeutlich, dass das Konzept der persönlichen Daten Online-IDs (z. B. IP-Adressen, mobile Geräte-IDs) und Positionsdaten umfasst.

Die GDPR führt spezifische Definitionen für genetische Daten (z. B. eine Person Gene Sequenz) und biometrische Daten ein. Genetische Daten und biometrische Daten werden zusammen mit anderen untergeordneten Kategorien von persönlichen Daten (persönliche Daten, die die ethnische Herkunft, politische Stellungnahmen, religiöse oder philosophische Werte oder Mitgliedschaften in Gewerkschaften offenlegen: Daten bezüglich Ihrer Gesundheit; oder Daten über das Sexualleben oder die sexueller Orientierung einer Person) werden als vertrauliche persönliche Daten unter der GDPR behandelt. Vertrauliche persönliche Daten sind besonders geschützt und erfordern in der Regel die ausdrückliche Zustimmung einer Person, wo diese Daten verarbeitet werden sollen.

### <a name="examples-of-info-relating-to-an-identified-or-identifiable-natural-person-data-subject"></a>Beispiele für Informationen über eine bestimmte oder bestimmbare natürliche Person (Datenbetreff)
Diese Liste enthält Beispiele für verschiedene Arten von Informationen, die über GDPR geregelt werden. Diese Liste ist nicht vollständig.

-   Name

-   ID-Nummer (wie Sozialversicherungsnummer)

-   Wohnortdaten (z. B. die Privatadresse)

-   Online-ID (z. B. die E-Mail-Adresse, der Bildschirmname, die IP-Adresse, Geräte-IDs)

-   Pseudonyme Daten (z. B. einen Schlüssel zur Personenidentität verwenden)

-   Genetische Daten (z. B. biologische Stichproben einer Person)

-   Biometrische Daten (z. B. Fingerabdrücke, Gesichtserkennung)

## <a name="getting-started-on-the-journey-towards-gdpr-compliance"></a>Erste Schritte auf dem Weg in Richtung GDPR-Kompatibilität
Da der Schritt zur GDPR-Kompatibilität vieles umfasst, wird dringend empfohlen, mit den Vorbereitungen nicht bis zum Erzwingen der Richtlinien zu warten. Sie sollten Ihre Privatsphäre- und die Daten-Verwaltungsverfahren jetzt überprüfen. Es wird empfohlen, dass Sie Ihre Reise in die GDPR-Kompatibilität durch den Fokus auf vier wichtige Schritte beginnen:

-   **Stellen.** Identifizieren Sie Ihre persönlichen Daten und wo sie sich befinden. 

-   **Stelligen.** Steuern, wie auf persönliche Daten zugegriffen und wie sie verwendet werden.

-   **Schützen.** Richten Sie Sicherheitsmechanismen ein, um zu verhindern, erkennen und auf Sicherheitsrisiken und Datenschutzverletzungen zu reagieren.  

-   **Ver.** Reagieren Sie auf Datenanforderungen, melden Sie Datenschutzverletzungen, und behalten Sie die erforderliche Dokumentation.

    ![Diagramm zur Funktionsweise der 4 Schritte für GDPR und wie sie zusammen funktionieren](../media/GDPR-Windows-Server-Overview/gdpr-steps-diagram.png)

Für die einzelnen Schritte haben wir Beispiel-Tools, Ressourcen und Funktionen in verschiedenen Microsoft-Lösungen beschrieben, die verwendet werden können, um die Anforderungen des Schritts einzuhalten. Dieser Artikel ist zwar kein umfassendes Leitfaden, aber wir haben Links für Sie eingefügt, um weitere Informationen zu erhalten. Weitere Informationen finden Sie im Abschnitt zur dsgvo im [Microsoft Trust Center](https://www.microsoft.com/en-us/trustcenter/privacy/gdpr).

## <a name="windows-server-security-and-privacy"></a>Sicherheit und Datenschutz für Windows Server
Die dsgvo erfordert, dass Sie geeignete technische und organisatorische Sicherheitsmaßnahmen implementieren, um persönliche Daten und Verarbeitungssysteme zu schützen. Im Zusammenhang mit der dsgvo verarbeiten Ihre physischen und virtuellen Serverumgebungen möglicherweise persönliche und vertrauliche Daten. Die Verarbeitung kann jeden Vorgang oder jede Gruppe von Vorgängen, z. b. Datenerfassung, Speicherung und Abruf, bedeuten.

Die Möglichkeit, diese Anforderung zu erfüllen und geeignete Maßnahmen für die technische Sicherheit zu implementieren, muss die Bedrohungen widerspiegeln, die Ihnen in der zunehmend feindlichen IT-Umgebung von heute ausgesetzt sind Sicherheitsbedrohungen sind heute extrem aggressiv und hartnäckig. In früheren Jahren konzentrierten sich böswillige Angreifer hauptsächlich auf die Anerkennung in der Community für ihre Angriffe oder die Begeisterung, ein System vorübergehend offline geschaltet zu haben. Seitdem haben sich die Motive der Angreifer in Richtung Geldgier geändert, und sie behalten die Gewalt über Geräte und Daten, bis die Besitzer das geforderte Lösegeld bezahlen.

Aktuelle Angriffe konzentrieren sich zunehmend auf den Diebstahl geistigen Eigentums im großen Umfang, die zielgerichtete Systemzersetzung, die zu finanziellen Verlusten führen kann, und jetzt sogar Cyber-Terrorismus, durch den die Sicherheit von Personen und Unternehmen sowie nationale Interessen auf der ganzen Welt bedroht sind. Diese Angreifer sind üblicherweise hochqualifizierte Einzelpersonen und Sicherheitsexperten, von denen einige in Nationalstaaten beschäftigt sind, die über große Budgets und scheinbar unbegrenzte menschliche Ressourcen verfügen. Bedrohungen wie diese erfordern einen Ansatz, der dieser Herausforderung gerecht wird.

Diese Bedrohungen sind nicht nur ein Risiko für Ihre Fähigkeit, die Kontrolle über persönliche oder vertrauliche Daten zu behalten, sondern sie sind ein wesentliches Risiko für Ihr gesamten Unternehmen. Beachten Sie die neuesten Daten von McKinsey, Ponemon Institute, Verizon und Microsoft:

- Die durchschnittliche Kosten für den Typ der Datenverstöße, den die GDPR erwartet, beträgt 3,5 Milliarden USD.

- 63 % dieser Verstößen sind schwache oder gestohlene Kennwörter, mit denen Sie handeln müssen und die die GDPR erwartet.

- Über 300.000 neue Schadsoftware-Beispiele werden jeden Tag erstellt und verbreitet und machen Ihre Aufgabe des Schutzes von Daten noch schwieriger.

Wie bei den jüngsten Ransomware-Angriffen, die einmal als schwarze Plage des Internets bezeichnet werden, werden Angreifer nach größeren Zielen weitergegeben, die sich möglicherweise mit schwerwiegenden Konsequenzen beschäftigen können. Die dsgvo schließt Maßnahmen ein, die ihre Systeme, einschließlich Desktops und Laptops, zur Verfügung stellen, die tatsächlich persönliche und sensible datenreiche Ziele enthalten.

Zwei wichtige Prinzipien haben eine Anleitung und Fortsetzung bei der Entwicklung von Windows:

- **Sicherung.** Die Daten unsere Software und Dienste im Auftrag unserer Kunden sollten vor Schäden geschützt werden und werden nur auf angemessene Weise verwendet oder geändert. Sicherheitsmodelle sollten Entwicklern auf einfache Weise vertraut sein, um Ihre Anwendungen zu verstehen und zu erstellen.

- **Datenschutz.** Benutzer sollten Steuern, wie Ihre Daten verwendet werden. Die Richtlinien für die Verwendung von Informationen sollten für den Benutzer klar sein. Benutzer sollten steuern können, wann und ob Sie Informationen erhalten, um Ihre Zeit optimal zu nutzen. Es sollte einfach sein, dass Benutzer die geeignete Verwendung Ihrer Informationen angeben können, einschließlich der Steuerung der Verwendung von gesendeten e-Mails.

Microsoft hat sich im Hinblick auf diese Prinzipien nicht wie vor kurzem vom CEO von Microsoft, Satya NADELLA, 

> "_Wenn sich die weltweiter ändert und sich die geschäftlichen Anforderungen weiterentwickeln, sind einige Dinge konsistent: die Nachfrage nach Sicherheit und Datenschutz durch einen Kunden._ "

Bei der Einhaltung der dsgvo ist es wichtig, die Rolle ihrer physischen und virtuellen Server beim Erstellen, zugreifen, verarbeiten, speichern und Verwalten von Daten zu verstehen, die als persönliche und potenziell sensible Daten in der dsgvo qualifiziert sein können. Windows Server bietet Funktionen, mit deren Hilfe Sie die dsgvo-Anforderungen erfüllen können, um geeignete technische und organisatorische Sicherheitsmaßnahmen zum Schutz persönlicher Daten zu implementieren.

Die Sicherheitslage von Windows Server 2016 ist kein Bolt-on. Es ist ein architekturprinzip. Und Sie können in vier Prinzipale am besten verstanden werden:

- **Schützen.** Fortlaufender Fokus und Innovation bei präventiven Maßnahmen blockieren bekannter Angriffe und bekannter Schadsoftware.

- **Auf.** Umfassende Überwachungstools, die Sie dabei unterstützen, Abweichungen zu erkennen und schneller auf Angriffe zu reagieren.

- **Reagieren.** Führende Antwort-und Wiederherstellungs Technologien sowie Deep Consulting-Know-how.

- **Isol.** Isolieren Sie Betriebssystemkomponenten und Daten Geheimnisse, schränken Sie Administratorrechte ein, und Messen Sie die Host Integrität streng.

Mit Windows Server ist die Fähigkeit, die Arten von Angriffen zu schützen, zu erkennen und zu schützen, die zu Datenverletzungen führen können, erheblich verbessert. Angesichts der strengen Anforderungen hinsichtlich der Verletzung der Benachrichtigung innerhalb der GDPR, und um sicherzustellen, dass Ihre Desktop- und Laptop-Systeme auch gegen Risiken gesichert sind, verringern Sie das Risiko kostspieliger Verletzungsanalysen und Benachrichtigungen.

Im folgenden Abschnitt erfahren Sie, wie Windows Server Funktionen bereitstellt, die sich in der Phase "schützen" ihrer dsgvo-Kompatibilitäts Journey ganz direkt befinden. Diese Funktionen fallen in drei Schutz Szenarien:

- **Schützen Sie Ihre Anmelde Informationen, und beschränken Sie Administratorrechte.** Windows Server 2016 hilft bei der Implementierung dieser Änderungen, um zu verhindern, dass Ihr System als Ausgangspunkt für weitere Eindring Versuche verwendet wird.

- **Sichern Sie das Betriebssystem, um Ihre apps und die Infrastruktur auszuführen.** Windows Server 2016 bietet Schutz Ebenen, die verhindern, dass externe Angreifer Schadsoftware ausführen oder Sicherheitsrisiken ausnutzen.

- **Sichere Virtualisierung.** Windows Server 2016 ermöglicht die sichere Virtualisierung mit abgeschirmten Virtual Machines und geschütztem Fabric. Dies hilft Ihnen, Ihre virtuellen Computer auf vertrauenswürdigen Hosts in Ihrem Fabric zu verschlüsseln und auszuführen, um Sie besser vor böswilligen Angriffen zu schützen.

Diese Funktionen, die unten ausführlicher erläutert werden, mit Verweisen auf bestimmte dsgvo-Anforderungen, basieren auf dem erweiterten Geräteschutz, der die Integrität und Sicherheit des Betriebssystems und der Daten gewährleistet.

Eine Schlüssel Bereitstellung innerhalb der dsgvo ist der Schutz von Daten nach Entwurf und standardmäßig, und unterstützt Sie bei der Erfüllung dieser Bereitstellung in Windows 10, wie z. b. der BitLocker-Geräteverschlüsselung. BitLocker verwendet die Trusted Platform Module (TPM)-Technologie, die hardwarebasierte, sicherheitsrelevante Funktionen bereitstellt. Dieser kryptografieprozessorchip umfasst mehrere physische Sicherheitsmechanismen, um ihn zu manipulieren, und Schadsoftware kann die Sicherheitsfunktionen des TPM nicht manipulieren.

Der Chip umfasst mehrere physische Sicherheitsmechanismen, die ihn manipulationssicher machen, und Schadsoftware ist nicht in der Lage, die TPM-Sicherheitsfunktionen zu manipulieren. Die wichtigsten Vorteile der TPM-Technologie bestehen in ihren Möglichkeiten. Sie können:

-   Kryptografieschlüssel generieren, speichern und deren Einsatz beschränken.

-   TPM-Technologie für die Plattformgeräteauthentifizierung nutzen. Sie verwenden dazu den eindeutigen RSA-Schlüssel des TPMs, der in sich selbst geschrieben ist.

-   Plattformintegrität gewährleisten, indem Sicherheitsmessungen vorgenommen und gespeichert werden.

Zusätzliche erweiterte Schutzmaßnahmen für Ihr Betriebssystem ohne Datenschutzverletzungen umfassen „Windows Trusted Boot”, das die Integrität des Systems gewährleistet, indem es sicherstellt, das die Schadsoftware nicht vor den Verteidigungseinrichtungen des Systems gestartet werden kann.

## <a name="windows-server-supporting-your-gdpr-compliance-journey"></a>Windows Server: Unterstützung ihrer dsgvo-Compliance-Journey
Wichtige Features in Windows Server können Sie bei der effizienten und effektiven Implementierung der Sicherheits-und Datenschutzmechanismen unterstützen, die für die Einhaltung der dsgvo erforderlich sind. Obwohl die Verwendung dieser Features nicht die Konformität gewährleistet, unterstützen Sie Ihre Bemühungen, dies zu tun.

Das Server Betriebssystem befindet sich in einer strategischen Schicht in der Infrastruktur einer Organisation und bietet neue Möglichkeiten, Schutz Ebenen vor Angriffen zu schaffen, die Daten stehlen und Ihr Unternehmen unterbrechen könnten. Wichtige Aspekte der dsgvo, wie z. b. Datenschutz, Datenschutz und Access Control müssen innerhalb Ihrer IT-Infrastruktur auf Serverebene adressiert werden.

Windows Server 2016 trägt zum Schutz der Identitäts-, Betriebssystem-und Virtualisierungsebene bei, um die häufigen Angriffsvektoren zu blockieren, die für den unerlaubten Zugriff auf Ihre Systeme verwendet werden: gestohlene Anmelde Informationen, Schadsoftware und ein kompromittiertes virtualisierungsfabric. Zusätzlich zu den Sicherheitsrisiken, die in Windows Server 2016 integriert sind, unterstützen die Sicherheitskomponenten, die in Windows Server integriert sind, Compliance-Anforderungen für die wichtigsten behördlichen 

Diese Identitäts-, Betriebssystem-und virtualisierungschutzmaßnahmen ermöglichen es Ihnen, Ihr Rechenzentrum mit Windows Server als virtuellen Computer in einer beliebigen Cloud zu schützen und die Fähigkeit von Angreifern einzuschränken, Anmelde Informationen zu kompromittieren, Schadsoftware zu starten und nicht erkannt zu werden. Netzwerk. Ebenso bietet Windows Server 2016 bei der Bereitstellung als Hyper-V-Host eine Sicherheitsgarantie für Ihre Virtualisierungsumgebungen durch geschützte Virtual Machines und verteilte Firewallfunktionen. Mit Windows Server 2016 wird das Server Betriebssystem zu einem aktiven Teilnehmer in ihrer Datacenter-Sicherheit.

### <a name="protect-your-credentials-and-limit-administrator-privileges"></a>Schützen Sie Ihre Anmelde Informationen, und beschränken Sie Administratorrechte. 
Die Kontrolle über den Zugriff auf personenbezogene Daten und die Systeme, die diese Daten verarbeiten, ist ein Bereich mit der dsgvo, der bestimmte Anforderungen umfasst, einschließlich des Zugriffs durch Administratoren. Privilegierte Identitäten sind Konten mit erhöhten Rechten, wie z. b. Benutzerkonten, die Mitglieder der Gruppe "Domänen Administratoren", "Organisations Administratoren", "lokale Administratoren" oder "Hauptbenutzer" sind. Diese Identitäten können auch Konten enthalten, denen direkt Berechtigungen erteilt wurden, z. b. das Ausführen von Sicherungen, das Herunterfahren des Systems oder andere Rechte, die im Knoten zuweisen von Benutzerrechten in der Konsole der lokalen Sicherheitsrichtlinie aufgeführt sind.

Als allgemeines Zugriffs Steuerungs Prinzip und Inline mit der dsgvo müssen Sie diese privilegierten Identitäten vor Kompromittierung durch potenzielle Angreifer schützen. Zuerst ist es wichtig zu verstehen, wie Identitäten kompromittiert werden. Anschließend können Sie planen, um zu verhindern, dass Angreifer Zugriff auf diese privilegierten Identitäten erhalten.

#### <a name="how-do-privileged-identities-get-compromised"></a>Wie werden privilegierte Identitäten kompromittiert?
Privilegierte Identitäten können kompromittiert werden, wenn Organisationen nicht über Richtlinien zum Schutz verfügen. Im Folgenden finden Sie entsprechende Beispiele:

- **Mehr Berechtigungen als erforderlich sind.** Eines der häufigsten Probleme besteht darin, dass Benutzer über mehr Berechtigungen verfügen, als für die Ausführung ihrer Auftrags Funktion erforderlich sind. Beispielsweise kann ein Benutzer, der DNS verwaltet, ein AD-Administrator sein. In den meisten Fällen wird dies durchgeführt, um zu vermeiden, dass unterschiedliche Verwaltungsebenen konfiguriert werden müssen. Wenn ein solches Konto jedoch kompromittiert wird, hat der Angreifer automatisch erhöhte Rechte.

- **Ständig mit erhöhten Rechten angemeldet.** Ein weiteres häufiges Problem ist, dass Benutzer mit erhöhten Rechten diese für unbegrenzte Zeit verwenden können. Dies gilt sehr häufig für IT-Experten, die sich mit einem privilegierten Konto bei einem Desktop Computer anmelden, angemeldet bleiben und das privilegierte Konto zum Durchsuchen des Internets und zum Verwenden von e-Mails verwenden (typische IT-Arbeitsaufgaben Funktionen). Durch die unbegrenzte Dauer privilegierter Konten ist das Konto anfälliger für Angriffe und erhöht die Wahrscheinlichkeit, dass das Konto gefährdet wird.

- **Social Engineering Research.** Die meisten Bedrohungen der Anmelde Informationen beginnen mit der Untersuchung der Organisation und Durchführung durch Social Engineering. Beispielsweise kann ein Angreifer einen e-Mail-Phishing-Angriff durchführen, um legitime Konten (aber nicht unbedingt Konten mit erhöhten Rechten) zu kompromittieren, die Zugriff auf das Netzwerk einer Organisation haben. Der Angreifer verwendet dann diese gültigen Konten, um zusätzliche Untersuchungen in Ihrem Netzwerk durchzuführen und privilegierte Konten zu identifizieren, die administrative Aufgaben ausführen können. 

- **Nutzen Sie Konten mit erhöhten Rechten.** Selbst bei einem normalen, nicht erhöhten Benutzerkonto im Netzwerk können Angreifer Zugriff auf Konten mit erhöhten Berechtigungen erhalten. Eine der gängigeren Methoden hierfür ist die Verwendung der Pass-the-Hash-oder Pass-the-Token-Angriffe. Weitere Informationen zu den Verfahren Pass-the-Hash und andere Verfahren zum Diebstahl von Anmelde Informationen finden Sie in den Ressourcen auf der [Seite Pass-the-Hash (PTH)](https://technet.microsoft.com/dn785092.aspx).

Es gibt natürlich andere Methoden, mit denen Angreifer privilegierte Identitäten identifizieren und kompromittieren können (wobei täglich neue Methoden erstellt werden). Daher ist es wichtig, dass Sie Verfahren für Benutzer einrichten, die sich mit Konten mit geringsten Berechtigungen anmelden, um die Möglichkeit zu verringern, dass Angreifer Zugriff auf privilegierte Identitäten erhalten. In den folgenden Abschnitten werden die Funktionen beschrieben, mit denen Windows Server diese Risiken mindern kann.

#### <a name="just-in-time-admin-jit-and-just-enough-admin-jea"></a>Just-in-time admin (JIT) und Just Enough admin (Jea)
Obwohl der Schutz vor Pass-the-Hash-oder Pass-The-Ticket-Angriffen wichtig ist, können Administrator Anmelde Informationen weiterhin auf andere Weise gestohlen werden, einschließlich Social Engineering, verärgerten Employees und Brute-Force. Daher ist es nicht nur so weit wie möglich, Anmelde Informationen zu isolieren, sondern auch die Reichweite von Berechtigungen auf Administratorebene einzuschränken, falls diese kompromittiert sind.

Heute sind zu viele Administrator Konten überlastet, auch wenn Sie nur einen Zuständigkeitsbereich haben. Beispielsweise werden einem DNS-Administrator, der einen sehr schmalen Satz von Berechtigungen zum Verwalten von DNS-Servern benötigt, häufig Berechtigungen auf Administratorebene erteilt. Außerdem gibt es keine Beschränkung, wie lange Sie verwendet werden können, da diese Anmelde Informationen für die Dauerhaftigkeit erteilt werden.

Jedes Konto mit unnötigen Berechtigungen auf Domänen Administratorebene erhöht die Angriffsfläche für Angreifer, die Anmelde Informationen kompromittieren möchten. Um die Angriffsfläche für Angriffe zu minimieren, sollten Sie nur den spezifischen Satz von rechten bereitstellen, den ein Administrator für den Auftrag benötigt – und nur für das Zeitfenster, das zum Abschluss benötigt wird.

Mithilfe der eben ausreichenden Administration und Just-in-Time-Verwaltung können Administratoren die spezifischen Berechtigungen anfordern, die Sie für das genaue Zeitfenster benötigen, das benötigt wird. Für einen DNS-Administrator können Sie z. b. mithilfe von PowerShell nur eine ausreichende Verwaltung aktivieren, um einen begrenzten Satz von Befehlen zu erstellen, die für die DNS-Verwaltung verfügbar sind.

Wenn der DNS-Administrator einen Ihrer Server aktualisieren muss, fordert er den Zugriff zum Verwalten von DNS mithilfe von Microsoft Identity Manager 2016 an. Der Anforderungs Workflow kann einen Genehmigungsprozess einschließen, z. b. die zweistufige Authentifizierung, bei dem das Mobiltelefon des Administrators aufgerufen werden kann, um Ihre Identität zu bestätigen, bevor die angeforderten Berechtigungen erteilt werden. Nach der Erteilung gewähren diese DNS-Berechtigungen den Zugriff auf die PowerShell-Rolle für DNS für eine bestimmte Zeitspanne.

Stellen Sie sich dieses Szenario vor, wenn die Anmelde Informationen des DNS-Administrators gestohlen wurden. Da den Anmelde Informationen keine Administratorrechte zugeordnet sind, konnte der Angreifer zunächst nicht auf den DNS-Server – oder andere Systeme – zugreifen, um Änderungen vorzunehmen. Wenn der Angreifer versucht hat, Berechtigungen für den DNS-Server anzufordern, werden Sie von der zweistufigen Authentifizierung aufgefordert, Ihre Identität zu bestätigen. Da der Angreifer wahrscheinlich nicht über das Mobiltelefon des DNS-Administrators verfügt, schlägt die Authentifizierung fehl. Dadurch wird der Angreifer vom System gesperrt und die IT-Organisation benachrichtigt, dass die Anmelde Informationen kompromittiert werden könnten.

Außerdem verwenden viele Organisationen die kostenlose [lokale Administrator Kenn Wort Lösung (Runden)](http://aka.ms/laps) als einfachen, aber leistungsfähigen JIT-Verwaltungsmechanismus für Ihre Server-und Client Systeme. Die Runden Funktion ermöglicht die Verwaltung von lokalen Konto Kennwörtern für in die Domäne eingebundener Computer. Kenn Wörter werden in Active Directory (AD) gespeichert und von Access Control Liste (ACL) geschützt, sodass nur berechtigte Benutzer Sie lesen oder deren zurück Setzung anfordern können.

Wie im Leitfaden zur [Entschärfung von Windows](https://www.microsoft.com/en-us/download/confirmation.aspx?id=54095)-Anmelde Informationen vermerkt, 

> "_die Tools und Techniken, die kriminelle zum Durchführen von Diebstahl von Anmelde Informationen und zum wieder verwenden von Angriffen verwenden, werden durch böswillige Angreifer leichter gefunden. Der Diebstahl von Anmelde Informationen basiert häufig auf Betriebspraktiken oder dem verfügbar machen von Benutzer Anmelde Informationen, sodass effektive entschärfungen einen ganzheitlichen Ansatz erfordern, der Personen, Prozesse und Technologien adressiert. Außerdem basieren diese Angriffe darauf, dass der Angreifer Anmelde Informationen stiehlt, nachdem ein System zum Erweitern oder beibehalten des Zugriffs kompromittiert wurde, sodass Organisationen rasch Verletzungen durch Implementieren von Strategien aufweisen müssen, die verhindern, dass Angreifer in einer kompromittiertes Netzwerk._ "

Eine wichtige Entwurfs Überlegungen für Windows Server bestand darin, den Diebstahl von Anmelde Informationen zu mindern – insbesondere abgeleitete Anmelde Informationen. Anmelde Informationen Guard bietet eine deutlich verbesserte Sicherheit vor dem Diebstahl und der Wiederverwendung abgeleiteter Anmelde Informationen, indem eine bedeutende Architektur Änderung in Windows implementiert wurde, um hardwarebasierte Isolations Angriffe auszuschließen, anstatt einfach zu versuchen, gegen Sie schützen.

Bei der Verwendung von Windows Defender Anmelde Informationen Guard, NTLM und Kerberos abgeleitete Anmelde Informationen werden mithilfe der virtualisierungsbasierten Sicherheit geschützt, aber die Verfahren und Tools zum Diebstahl von Anmelde Informationen, die in vielen gezielten Angriffen verwendet werden, werden blockiert. Im Betriebssystem ausgeführte Schadsoftware mit Administratorberechtigungen kann geheime Schlüssel, die durch die virtualisierungsbasierte Sicherheit geschützt sind, nicht extrahieren. Obwohl Windows Defender Credential Guard eine leistungsstarke Entschärfung ist, werden permanente Bedrohungs Angriffe wahrscheinlich zu neuen Angriffstechniken verschoben, und Sie sollten auch Device Guard, wie unten beschrieben, zusammen mit anderen Sicherheitsstrategien und-Architekturen integrieren.

#### <a name="windows-defender-credential-guard"></a>Windows Defender Credential Guard
Windows Defender Anmelde Informationen Guard verwendet virtualisierungsbasierte Sicherheit, um Anmelde Informationen zu isolieren, sodass Kennworthashes oder Kerberos-Tickets nicht abgefangen werden. Er verwendet einen völlig neuen, isolierten lokalen Sicherheits Autorität (Local Security Authority, LSA), der für den Rest des Betriebssystems nicht zugänglich ist. Alle Binärdateien, die von der isolierten LSA verwendet werden, werden mit Zertifikaten signiert, die überprüft werden, bevor Sie in der geschützten Umgebung gestartet werden, sodass Pass-the-Hash-Typen Angriffe vollständig wirkungslos werden.

Windows Defender Credential Guard verwendet Folgendes:

- Virtualisierungsbasierte Sicherheit (erforderlich). Ebenfalls erforderlich:

    - CPU mit 64 Bit

    - Erweiterungen der CPU-Virtualisierung sowie erweiterte Seitentabellen

    - Windows-Hypervisor

- Sicherer Start (erforderlich)

- TPM 2.0, entweder diskret oder firmwarebasiert (aufgrund der Hardwarebindung bevorzugt)

Sie können Windows Defender Anmelde Informationen Guard verwenden, um privilegierte Identitäten zu schützen, indem Sie die Anmelde Informationen und die Ableitungen von Anmelde Informationen unter Windows Server 2016 schützen. Weitere Informationen zu den Anforderungen von Windows Defender Credential Guard finden Sie unter [schützen abgeleiteter Domänen Anmelde Informationen mit Windows Defender Credential Guard](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard).

#### <a name="windows-defender-remote-credential-guard"></a>Windows Defender Remote Credential Guard
Windows Defender Remote Credential Guard unter Windows Server 2016 und Windows 10 Anniversary Update unterstützt auch den Schutz von Anmelde Informationen für Benutzer mit Remote Desktop Verbindungen. Zuvor musste sich jede Person, die Remotedesktopdienste verwendet, bei Ihrem lokalen Computer anmelden und sich dann erneut anmelden, wenn Sie eine Remote Verbindung mit dem Zielcomputer durchgeführt hat. Dieser zweite Anmelde Name übergibt Anmelde Informationen an den Zielcomputer und macht Sie für Pass-the-Hash-oder Pass-The-Ticket-Angriffe verfügbar.

Mit Windows Defender Remote Credential Guard implementiert Windows Server 2016 einmaliges Anmelden für Remotedesktop Sitzungen, sodass der Benutzername und das Kennwort nicht erneut eingegeben werden müssen. Stattdessen werden die Anmelde Informationen verwendet, die Sie bereits zum Anmelden an Ihrem lokalen Computer verwendet haben. Um Windows Defender Remote Credential Guard verwenden zu können, müssen die Remotedesktop Client und der Server die folgenden Anforderungen erfüllen:

- Muss einer Active Directory Domäne beitreten und sich in derselben Domäne oder in einer Domäne mit einer Vertrauensstellung befinden.

- Muss die Kerberos-Authentifizierung verwenden.

- Muss mindestens Windows 10, Version 1607 oder Windows Server 2016 ausführen.  

- Die Remotedesktop klassische Windows-APP ist erforderlich. Die Remotedesktop universelle Windows-Plattform-App unterstützt nicht Windows Defender Remote Credential Guard.

Sie können Windows Defender Remote Credential Guard aktivieren, indem Sie eine Registrierungs Einstellung auf dem Remotedesktop Server und Gruppenrichtlinie oder einen Remotedesktopverbindung Parameter auf dem Remotedesktop Client verwenden. Weitere Informationen zum Aktivieren von Windows Defender Remote Credential Guard finden Sie unter [Schützen von Remotedesktop Anmelde Informationen mit Windows Defender Remote Credential Guard](https://docs.microsoft.com/windows/access-protection/remote-credential-guard). Wie bei Windows Defender Credential Guard können Sie Windows Defender Remote Credential Guard verwenden, um privilegierte Identitäten unter Windows Server 2016 zu schützen.

### <a name="secure-the-operating-system-to-run-your-apps-and-infrastructure"></a>Sichern des Betriebssystems zum Ausführen von apps und Infrastrukturen
Das verhindern von Cyberbedrohungen erfordert auch das Auffinden und Blockieren von Schadsoftware und Angriffen, die die Kontrolle über die Standard Betriebssysteme Ihrer Infrastruktur erlangen. Wenn Angreifer ein Betriebssystem oder eine Anwendung für die Ausführung in einer nicht vordefinierten, nicht realisierbaren Weise erhalten können, verwenden Sie wahrscheinlich dieses System, um böswillige Aktionen auszuführen. Windows Server 2016 bietet Schutz Ebenen, die verhindern, dass externe Angreifer Schadsoftware ausführen oder Sicherheitsrisiken ausnutzen. Das Betriebssystem übernimmt eine aktive Rolle beim Schutz von Infrastruktur und Anwendungen, indem Administratoren auf Aktivitäten hingewiesen werden, die darauf hindeuten, dass ein System verletzt wurde.

#### <a name="windows-defender-device-guard"></a>Windows Defender Device Guard
Windows Server 2016 enthält Windows Defender Device Guard, um sicherzustellen, dass nur vertrauenswürdige Software auf dem Server ausgeführt werden kann. Mithilfe der virtualisierungsbasierten Sicherheit kann durch die IT-Abteilung eingeschränkt werden, welche Binärdateien auf dem System basierend auf der Richtlinie der Organisation ausgeführt werden können. Wenn etwas anderes als die angegebenen Binärdateien ausgeführt werden soll, wird es von Windows Server 2016 blockiert, und der fehlgeschlagene Versuch wird protokolliert, damit Administratoren erkennen können, dass eine potenzielle Verletzung aufgetreten ist. Die Warnungs Benachrichtigung ist ein wichtiger Bestandteil der Anforderungen hinsichtlich der Einhaltung der dsgvo.

Windows Defender Device Guard ist auch in PowerShell integriert, sodass Sie autorisieren können, welche Skripts auf Ihrem System ausgeführt werden können. In früheren Versionen von Windows Server konnten Administratoren die Code Integritäts Erzwingung umgehen, indem Sie einfach die Richtlinie aus der Codedatei löschen. Mit Windows Server 2016 können Sie eine Richtlinie konfigurieren, die von Ihrer Organisation signiert wird, sodass nur eine Person mit Zugriff auf das Zertifikat, mit dem die Richtlinie signiert wurde, die Richtlinie ändern kann.

#### <a name="control-flow-guard"></a>Ablaufsteuerungsschutz 
Windows Server 2016 umfasst auch integrierten Schutz gegen einige Klassen von Speicher Beschädigungen. Das Patchen Ihrer Server ist wichtig, aber es besteht immer die Möglichkeit, dass Schadsoftware für ein Sicherheitsrisiko entwickelt wird, das noch nicht identifiziert wurde. Einige der gängigsten Methoden zum Ausnutzen dieser Sicherheitsrisiken sind die Bereitstellung ungewöhnlicher oder extremer Daten für ein ausgelaufendes Programm. Ein Angreifer kann z. b. ein Pufferüberlauf-Sicherheitsrisiko ausnutzen, indem er mehr Eingaben für ein Programm als erwartet bereitstellt und den vom Programm reservierten Bereich zum Speichern einer Antwort überschreitet. Dadurch kann der angrenzende Arbeitsspeicher beschädigt werden, der möglicherweise einen Funktionszeiger enthält.

Wenn das Programm diese Funktion aufruft, kann es zu einem unbeabsichtigten Speicherort springen, der vom Angreifer angegeben wird. Diese Angriffe werden auch als Jump-Oriented Programming-Angriffe (jop) bezeichnet. Der Ablauf Steuerungs Schutz verhindert Jop-Angriffe, indem strenge Einschränkungen für den Anwendungscode festgelegt werden, – insbesondere indirekte Aufrufe. Es werden vereinfachte Sicherheitsüberprüfungen hinzugefügt, um den Satz von Funktionen in der Anwendung zu identifizieren, die gültige Ziele für indirekte Aufrufe sind. Wenn eine Anwendung ausgeführt wird, überprüft Sie, ob diese indirekten callziele gültig sind.

Wenn bei der Überprüfung des Ablauf Steuerungs Schutzes zur Laufzeit ein Fehler auftritt, beendet Windows Server 2016 das Programm sofort und unterbricht alle Exploits, die versuchen, indirekt eine ungültige Adresse aufzurufen. Der Ablauf Steuerungs Schutz bietet eine wichtige zusätzliche Schutz Ebene für Device Guard. Wenn eine aufgeführte Anwendung kompromittiert wurde, kann Sie von Device Guard nicht überprüft werden, da das Device Guard-Screening sehen würde, dass die Anwendung signiert wurde und als vertrauenswürdig eingestuft wird.

Da der Ablauf Steuerungs Schutz jedoch erkennen kann, ob die Anwendung in einer nicht vordefinierten, nicht ordnungsgemäß ausgeführten Reihenfolge ausgeführt wird, würde der Angriff fehlschlagen, wodurch verhindert wird, dass die kompromittierte Anwendung ausgeführt wird. Diese Schutzmaßnahmen erleichtern Angreifern das Einfügen von Schadsoftware in Software, die unter Windows Server 2016 ausgeführt wird.

Entwickler, die Anwendungen entwickeln, in denen persönliche Daten verarbeitet werden, werden empfohlen, den Ablauf Steuerungs Schutz (Control Flow Guard, cfg) in Ihren Anwendungen zu aktivieren Diese Funktion ist in Microsoft Visual Studio 2015 verfügbar und wird unter "cfg-fähige" Versionen von Windows – den x86-und x64-Releases für Desktop und Server von Windows 10 und Windows 8.1 Update (KB3000850) ausgeführt. Sie müssen CFG nicht für jeden Teil Ihres Codes aktivieren, da eine Mischung aus cfg-aktiviertem und nicht cfg aktiviertem Code problemlos ausgeführt werden kann. Wenn aber cfg nicht für den gesamten Code aktiviert werden kann, können Lücken im Schutz geöffnet werden. Außerdem funktioniert der cfg-aktivierte Code in den "cfg-nicht-"-Versionen von Windows einwandfrei und ist daher vollständig kompatibel mit diesen.

#### <a name="windows-defender-antivirus"></a>Windows Defender Antivirus
Windows Server 2016 umfasst die branchenführenden, aktiven Erkennungsfunktionen von Windows Defender zum Blockieren bekannter Schadsoftware. Windows Defender Antivirus (AV) kann zusammen mit Windows Defender Device Guard und Ablauf Steuerungs Schutz verwendet werden, um zu verhindern, dass bösartiger Code jeglicher Art auf Ihren Servern installiert wird. Diese Einstellung ist standardmäßig aktiviert – der Administrator muss keine Maßnahmen ergreifen, um mit der Arbeit zu beginnen. Windows Defender AV ist auch für die Unterstützung der verschiedenen Server Rollen in Windows Server 2016 optimiert. In der Vergangenheit nutzten die Angreifer Shells wie z. b. PowerShell, um bösartigen Binär Code zu starten. In Windows Server 2016 ist PowerShell nun in Windows Defender AV integriert, um vor dem Starten des Codes Schadsoftware zu überprüfen.

Windows Defender AV ist eine integrierte antischadsoftwarelösung, die die Verwaltung von Sicherheits-und Antischadsoftware für Desktops, tragbare Computer und Server ermöglicht. Windows Defender AV wurde seit der Einführung in Windows 8 erheblich verbessert. Windows Defender Antivirus in Windows Server verwendet einen mehrstufigen Ansatz, um Antischadsoftware zu verbessern:

- **Von der Cloud bereitgestellter Schutz** erkennt und blockiert neue Schadsoftware innerhalb von Sekunden, auch wenn die Schadsoftware bisher noch nie vorgekommen ist.

- **Umfassender lokaler Kontext** verbessert die Identifizierung von Schadsoftware. Windows Server informiert Windows Defender AV nicht nur über Inhalte wie Dateien und Prozesse, sondern auch über den Speicherort der Inhalte, wo Sie gespeichert wurden und vieles mehr. 

- **Umfassende globale Sensoren** helfen dabei, Windows Defender AV auf dem neuesten Stand zu halten und selbst die neuesten Schadsoftware zu berücksichtigen. Dies erfolgt auf zwei Arten: durch Sammeln der Daten des umfassenden lokalen Kontexts von Endpunkten und das zentrale Analysieren dieser Daten.

- **Manipulationsschutz** schützt Windows Defender AV selbst gegen Angriffe durch Schadsoftware. Beispielsweise verwendet Windows Defender AV geschützte Prozesse, wodurch verhindert wird, dass nicht vertrauenswürdige Prozesse versuchen, Windows Defender AV-Komponenten, deren Registrierungsschlüssel usw. zu manipulieren.

- **Features auf Unternehmensebene** ermöglichen IT-Experten die Tools und Konfigurationsoptionen, die erforderlich sind, um Windows Defender AV zu einer Lösung für die Unternehmens-Antischadsoftware zu machen

#### <a name="enhanced-security-auditing"></a>Verstärkte Sicherheitsüberwachung 
Windows Server 2016 warnt Administratoren aktiv durch die verstärkte Sicherheitsüberprüfung, die ausführlichere Informationen bereitstellt, die zur schnelleren Erkennung von Angriffen und forensischen Analysen verwendet werden können. Es protokolliert Ereignisse von Ablauf Steuerungs Schutz, Windows Defender Device Guard und anderen Sicherheitsfeatures an einem Ort, sodass Administratoren leichter feststellen können, welche Systeme gefährdet sind.

Zu den neuen Ereignis Kategorien gehören:

- **Überwachen der Gruppenmitgliedschaft.** Ermöglicht es Ihnen, die Gruppen Mitgliedschafts Informationen im Anmelde Token eines Benutzers zu überwachen. Ereignisse werden generiert, wenn Gruppenmitgliedschaften auf dem PC aufgelistet oder abgefragt werden, auf dem die Anmelde Sitzung erstellt wurde. 
 
- **Überwachen der PNP-Aktivität.** Ermöglicht Ihnen, zu überwachen, wann Plug & amp; Play ein externes Gerät erkennt – das möglicherweise Schadsoftware enthält. PNP-Ereignisse können verwendet werden, um Änderungen an der System Hardware zu verfolgen. Im Ereignis ist eine Liste der Hardwarehersteller-IDs enthalten.

Windows Server 2016 lässt sich problemlos mit den SIEM-Systemen (Security Incident Management), wie z. b. Microsoft Operations Management Suite (OMS), integrieren, die die Informationen zu potenziellen Sicherheitsverletzungen in Intelligence-Berichte integrieren können. Die Tiefe der von der erweiterten Überwachung bereitgestellten Informationen ermöglicht es Sicherheitsteams, potenzielle Verletzungen schneller und effektiver zu erkennen und darauf zu reagieren.

### <a name="secure-virtualization"></a>Sichere Virtualisierung
Unternehmen virtualisieren heute alles, was Sie können, von SQL Server zu SharePoint auf Active Directory-Domäne Controller. Virtuelle Computer (Virtual Machines, VMS) vereinfachen die Bereitstellung, Verwaltung, Verwaltung und Automatisierung Ihrer Infrastruktur. Wenn es jedoch um die Sicherheit geht, werden gefährdete virtualisierungsfabrics zu einem neuen Angriffsvektor, der schwer gegen – schwer zu verteidigen ist. Aus Gründen der dsgvo sollten Sie sich Gedanken über den Schutz von VMS machen, wenn Sie physische Server schützen, einschließlich der Verwendung der VM-TPM-Technologie.

Windows Server 2016 ändert grundlegend, wie Unternehmen die Virtualisierung sichern können, indem Sie mehrere Technologien einschließen, die es Ihnen ermöglichen, virtuelle Maschinen zu erstellen, die nur in Ihrem eigenen Fabric ausgeführt werden. Schutz vor der Speicherung, dem Netzwerk und den Host Geräten, auf denen Sie ausgeführt werden.

#### <a name="shielded-virtual-machines"></a>Abgeschirmte virtuelle Computer
Die gleichen Dinge, die virtuelle Computer so einfach zu migrieren, zu sichern und zu replizieren, erleichtern das ändern und Kopieren von Daten. Bei einem virtuellen Computer handelt es sich lediglich um eine Datei, sodass er nicht im Netzwerk, im Speicher, in Sicherungen oder an anderen Orten geschützt ist. Ein weiteres Problem ist, dass fabricadministratoren – ob es sich um einen Speicher Administrator oder einen Netzwerkadministrator handelt – Zugriff auf alle virtuellen Computer haben.

Ein kompromittierter Administrator im Fabric kann problemlos zu kompromittierten Daten auf virtuellen Computern führen. Alle Angreifer müssen die kompromittierten Anmelde Informationen verwenden, um beliebige VM-Dateien auf ein USB-Laufwerk zu kopieren und diese aus der Organisation zu kopieren, in der von jedem anderen System aus auf diese VM-Dateien zugegriffen werden kann. Wenn einer dieser gestohlenen VMS ein Active Directory Domänen Controller wäre, könnte der Angreifer den Inhalt problemlos anzeigen und sofort verfügbare Brute-Force-Techniken verwenden, um die Kenn Wörter in der Active Directory Datenbank zu knacken und Ihnen schließlich Zugriff zu gewähren. für alle anderen Elemente in Ihrer Infrastruktur.

Windows Server 2016 führt abgeschirmte Virtual Machines (abgeschirmte VMS) ein, um den Schutz vor Szenarien wie dem soeben beschriebenen Szenario zu erleichtern. Abgeschirmte VMS enthalten ein virtuelles TPM-Gerät, mit dem Organisationen die BitLocker-Verschlüsselung auf die virtuellen Computer anwenden und sicherstellen können, dass Sie nur auf vertrauenswürdigen Hosts ausgeführt werden, um Schutz vor gefährdeten Speicher-, Netzwerk-und Host Administratoren zu bieten. Abgeschirmte VMS werden mithilfe von VMS der Generation 2 erstellt, die Unified Extensible Firmware Interface-Firmware (UEFI) unterstützen und über ein virtuelles TPM verfügen.

#### <a name="host-guardian-service"></a>Host-Überwachungsdienst
Neben abgeschirmten VMS ist der Host-Überwachungsdienst eine wesentliche Komponente zum Erstellen eines sicheren virtualisierungsfabrics. Seine Aufgabe besteht darin, die Integrität eines Hyper-V-Hosts zu bestätigen, bevor eine abgeschirmte VM gestartet oder zu diesem Host migriert werden kann. Sie enthält die Schlüssel für abgeschirmte VMS und gibt Sie erst frei, wenn die Sicherheits Integrität gewährleistet ist. Es gibt zwei Möglichkeiten, wie Sie Hyper-V-Hosts zum Bestätigen des Host-Überwachungs Diensts auffordern können.

Der erste und sicherste Nachweis ist der Hardware vertrauenswürdige Nachweis. Diese Lösung erfordert, dass Ihre abgeschirmten VMS auf Hosts mit TPM 2,0-Chips und UEFI 2.3.1 ausgeführt werden. Diese Hardware ist erforderlich, um die vom Host-Überwachungsdienst benötigten Informationen zur Start-und Betriebssystem-Kernel Integrität bereitzustellen, um sicherzustellen, dass der Hyper-V-Host nicht manipuliert wurde.

IT-Organisationen haben eine Alternative zur Verwendung von Administrator vertrauenswürdigem Nachweis. Dies ist möglicherweise wünschenswert, wenn die TPM 2,0-Hardware in Ihrer Organisation nicht verwendet wird. Dieses Nachweis Modell ist einfach bereitzustellen, weil Hosts einfach in eine Sicherheitsgruppe eingefügt werden und der Host-Überwachungsdienst so konfiguriert ist, dass abgeschirmte VMS auf Hosts ausgeführt werden können, die Mitglieder der Sicherheitsgruppe sind. Bei dieser Methode gibt es keine komplexe Messung, um sicherzustellen, dass der Host Computer nicht manipuliert wurde. Allerdings ist es nicht möglich, dass unverschlüsselte VMS auf USB-Laufwerken die Tür durchlaufen oder dass die VM auf einem nicht autorisierten Host ausgeführt wird. Dies liegt daran, dass die VM-Dateien nicht auf Computern ausgeführt werden, die nicht in der angegebenen Gruppe vorhanden sind. Wenn Sie noch nicht über TPM 2,0-Hardware verfügen, können Sie mit dem Administrator vertrauenswürdigen Nachweis beginnen und zum Hardware vertrauenswürdigen Nachweis wechseln, wenn die Hardware aktualisiert wird.

#### <a name="virtual-machine-trusted-platform-module"></a>Virtueller Computer Trusted Platform Module
Windows Server 2016 unterstützt TPM für virtuelle Computer, sodass Sie erweiterte Sicherheitstechnologien wie BitLocker® Laufwerk Verschlüsselung auf virtuellen Computern unterstützen können. Sie können die TPM-Unterstützung auf jedem virtuellen Hyper-v-Computer der Generation 2 mithilfe des Hyper-v-Managers oder des Windows PowerShell-Cmdlets Enable-vmtpm aktivieren.

Sie können das virtuelle TPM (vtpm) schützen, indem Sie die lokalen Kryptografieschlüssel verwenden, die auf dem Host gespeichert oder im Host-Überwachungsdienst gespeichert sind. Obwohl der Host-Überwachungsdienst mehr Infrastruktur benötigt, bietet er auch mehr Schutz.

#### <a name="distributed-network-firewall-using-software-defined-networking"></a>Verteilte Netzwerk Firewall mit Software-Defined Networking
Eine Möglichkeit, den Schutz in virtualisierten Umgebungen zu verbessern, besteht darin, das Netzwerk so zu segmentieren, dass es VMS nur mit den spezifischen Systemen kommunizieren kann, die für die Funktion erforderlich sind Wenn Ihre Anwendung z. b. keine Verbindung mit dem Internet herstellen muss, können Sie Sie partitionieren, sodass diese Systeme als Ziele von externen Angreifern entfernt werden. Das Software-Defined Networking (SDN) in Windows Server 2016 umfasst eine verteilte Netzwerk Firewall, die es Ihnen ermöglicht, die Sicherheitsrichtlinien, mit denen Ihre Anwendungen vor Angriffen innerhalb oder außerhalb eines Netzwerks geschützt werden können, dynamisch zu erstellen. Diese verteilte Netzwerk Firewall fügt Ihrer Sicherheit Ebenen hinzu, indem Sie Ihre Anwendungen im Netzwerk isolieren können. Richtlinien können überall in Ihrer virtuellen Netzwerkinfrastruktur angewendet werden, wobei der VM-zu-VM-Datenverkehr, der VM-zu-Host-Datenverkehr oder der VM-zu-Internet-Datenverkehr bei Bedarf isoliert wird – entweder für einzelne Systeme, die möglicherweise kompromittiert oder Programm gesteuert über mehrere Subnetze. Mit den Software definierten Netzwerkfunktionen von Windows Server 2016 können Sie eingehenden Datenverkehr auch an virtuelle Geräte außerhalb von Microsoft weiterleiten oder spiegeln. Beispielsweise können Sie den gesamten e-Mail-Datenverkehr über ein virtuelles Barracuda-Gerät senden, um zusätzlichen Schutz vor Spam Filtern zu erhalten. Dies ermöglicht es Ihnen, auf einfache Weise zusätzliche Sicherheit sowohl lokal als auch in der Cloud zu ermöglichen.

### <a name="other-gdpr-considerations-for-servers"></a>Weitere dsgvo-Überlegungen zu Servern
Die dsgvo beinhaltet explizite Anforderungen für die Verletzung von Verletzungen, bei denen eine persönliche Datenverletzung bedeutet: "_eine Sicherheitsverletzung, die zu versehentlicher oder gesetzlicher Zerstörung, Verlust, Änderung, nicht autorisierter Offenlegung oder Zugriff auf personenbezogene Daten führt. übertragen, gespeichert oder anderweitig verarbeitet._ "  Natürlich können Sie nicht fortfahren, um die strengen Anforderungen an die dsgvo-Benachrichtigung innerhalb von 72 Stunden zu erfüllen, wenn Sie die Sicherheitslücke überhaupt nicht erkennen können.

Wie im Windows-Security Center Whitepaper angemerkt, [Posten Sie Folgendes: Umgang mit erweiterten Bedrohungen](http://wincom.blob.core.windows.net/documents/Post_Breach_Dealing_with_Advanced_Threats_Whitepaper.pdf)

> "_Anders als bei der vor-und nach Verletzung geht die nach Verletzung davon aus, dass bereits eine Verletzung aufgetreten ist – fungiert als Flight Recorder und Crime Scene Investigator (CSI). Die nach Verletzung bietet Sicherheitsteams die Informationen und Toolsets, die benötigt werden, um Angriffe zu identifizieren, zu untersuchen und darauf zu reagieren, die andernfalls nicht erkannt werden, und unter dem Netz._ "

In diesem Abschnitt erfahren Sie, wie Sie mithilfe von Windows Server Ihre dsgvo-Benachrichtigungs Verpflichtungen erfüllen können. Dies beginnt mit dem Verständnis der zugrunde liegenden Bedrohungs Daten, die Microsoft zur Verfügung steht und die für Ihren Vorteil gesammelt und analysiert werden, und wie Sie über Windows Defender Advanced Threat Protection (ATP) für Sie von entscheidender Bedeutung sein können.

#### <a name="insightful-security-diagnostic-data"></a>Aufschlussreiche Sicherheitsdiagnosedaten
Seit fast zwei Jahrzehnten hat Microsoft Bedrohungen in nützliche Informationen verwandelt, mit denen die Plattform und der Schutz von Kunden unterstützt werden können. Dank der großen Computing-Vorteile von heute durch die Cloud, finden wir neue Verwendungsmöglichkeiten für unsere umfangreiche Analysemodule, die von der Bedrohungserkennung verursacht und zum Schutz unserer Kunden sind.

Durch das Anwenden einer Kombination von automatisierten und manuellen Prozessen, Machine Learning und menschlichen Experten, können wir ein intelligentes Security-Diagramm erstellen, das von sich selbst lernt und sich in Echtzeit weiter entwickelt, um neue Bedrohungen für unsere Produkte zu erkennen und darauf zu reagieren.

![Microsoft Intelligence-Sicherheits Diagramm](../media/GDPR-Windows-Server-Overview/gdpr-intelligent-security-graph.png)

Der Umfang der Bedrohungs Intelligenz von Microsoft umfasst im wesentlichen Milliarden von Datenpunkten: 35 Milliarden monatlich Überprüfte Nachrichten, 1 Milliarde Kunden in Unternehmens-und consumersegmenten, die auf 200 + Cloud-Dienste und 14 Milliarden Authentifizierungen täglich zugreifen. Alle diese Daten werden in Ihrem Auftrag von Microsoft zusammengeführt, um die intelligent Security Graph zu erstellen, die Ihnen helfen, Ihre Front-Door-Sicherheit auf dynamische Weise zu schützen, weiterhin produktiv zu bleiben und die Anforderungen der dsgvo zu erfüllen.

#### <a name="detecting-attacks-and-forensic-investigation"></a>Erkennen von Angriffen und forensische Untersuchung
Auch die besten Endpoint-Schutzmaßnahmen können irgendwann überwunden werden, da Cyberangriffe mehr ausgefeilt und zielgerichtet sind. Zwei Funktionen können zur Unterstützung der Erkennung möglicher Sicherheitsverletzungen verwendet werden: Windows Defender Advanced Threat Protection (ATP) und Microsoft Advanced Threat Analytics (ATA).

Windows Defender Advanced Threat Protection (ATP) hilft Ihnen, fortgeschrittene Angriffe zu erkennen und untersuchen und auf Datenschutzverletzungen im Netzwerk zu reagieren. Die Typen der Datenverletzung, die für die dsgvo durch technische Sicherheitsmaßnahmen geschützt werden müssen, um die fortlaufende Vertraulichkeit, Integrität und Verfügbarkeit von persönlichen Daten und Verarbeitungssystemen sicherzustellen.

Zu den wichtigsten Vorteilen von Windows Defender ATP zählen die folgenden:

- **Erkennen der nicht erkennbaren.** Sensoren, die tief in den Kernel des Betriebssystems, Windows-Sicherheitsexperten und eindeutige Optiken integriert sind, von über 1 Milliarde Computern und Signalen über alle Microsoft-Dienste hinweg.

- **Integriert, nicht fett formatiert.** Ohne Agent, mit hoher Leistung und minimaler Auswirkung, cloudbasiert; einfache Verwaltung ohne Bereitstellung. 

- **Einzelner Glasbereich für Windows-Sicherheit.** Erkunden Sie den umfangreichen Zeitraum von 6 Monaten, Machine-Timeline und Vereinheitlichung von Sicherheits Ereignissen von Windows Defender ATP, Windows Defender Antivirus und Windows Defender Device Guard.

- **Leistungsfähigkeit von Microsoft Graph.** Nutzt das Microsoft Intelligence Security Graph, um die Erkennung und Untersuchung mit dem Office 365 ATP-Abonnement zu integrieren, um Angriffe zurückverfolgen und darauf reagieren zu können.

Weitere Informationen finden Sie unter [Neuigkeiten im Windows Defender ATP Creators Update – Vorschau](https://blogs.microsoft.com/microsoftsecure/2017/03/13/whats-new-in-the-windows-defender-atp-creators-update-preview/).

ATA ist ein lokales Produkt, mit dem Identitäts Gefährdung in einer Organisation erkannt werden kann. ATA kann Netzwerk Datenverkehr für Authentifizierungs-, Autorisierungs-und Informations Sammel Protokolle (z. b. Kerberos, DNS, RPC, NTLM und andere Protokolle) erfassen und analysieren. ATA verwendet diese Daten, um ein Verhaltensprofil für Benutzer und andere Entitäten in einem Netzwerk zu erstellen, damit Anomalien und bekannte Angriffsmuster erkannt werden können. In der folgenden Tabelle sind die von ATA erkannten Angriffstypen aufgeführt.


|Angreitertyp |Beschreibung |
|---------|---------|
|Böswillige Angriffe |Diese Angriffe werden erkannt, indem Sie nach Angriffen aus einer bekannten Liste von Angriffstypen suchen, einschließlich:<ul><li>Pass-The-Ticket (PTT)</li><li>Pass-the-Hash (PTH)</li><li>Overpass-the-Hash</li><li>Gefälschtes PAC (MS14-068)</li><li>Golden Ticket</li><li>Böswillige Replikationen</li><li>Erkundung</li><li>Brute-Force</li><li>Remote Ausführung</li></ul>Eine umfassende Liste der gefundenen böswilligen Angriffe und deren Beschreibung finden Sie unter [welche verdächtigen Aktivitäten können von ATA erkannt werden?](https://docs.microsoft.com/advanced-threat-analytics/understand-explore/ata-threats).|
|Ungewöhnliches Verhalten |Diese Angriffe werden mithilfe der Verhaltensanalyse erkannt und verwenden Machine Learning, um fragwürdige Aktivitäten zu identifizieren, einschließlich:<ul><li>Anormale Anmeldungen</li><li>Unbekannte Bedrohungen</li><li>Kenn Wort Freigabe</li><li>Lateral Movement</li></ul>|
|Sicherheitsprobleme und-Risiken |Diese Angriffe werden erkannt, wenn Sie die aktuelle Netzwerk-und Systemkonfiguration betrachten, einschließlich:<ul><li>Unterbrochene Vertrauensstellung</li><li>Schwache Protokolle</li><li>Bekannte Protokoll Sicherheitsanfälligkeiten</li></ul>|

Mithilfe von ATA können Sie Angreifer erkennen, die versuchen, privilegierte Identitäten zu kompromittieren. Weitere Informationen zum Bereitstellen von ATA finden Sie in den Themen Plan, Entwurf und Bereitstellung in der [Advanced Threat Analytics-Dokumentation](https://docs.microsoft.com/advanced-threat-analytics/).

## <a name="related-content-for-associated-windows-server-2016-solutions"></a>Verwandte Inhalte für zugehörige Windows Server 2016-Lösungen

- **Windows Defender Antivirus:** https://www.youtube.com/watch?v=P1aNEy09NaI und https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10

- **Windows Defender Advanced Threat Protection:** https://www.youtube.com/watch?v=qxeGa3pxIwg und https://docs.microsoft.com/windows/threat-protection/windows-defender-atp/configure-server-endpoints-windows-defender-advanced-threat-protection

- **Windows Defender Device Guard:** https://www.youtube.com/watch?v=F-pTkesjkhI und https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide

- **Windows Defender Credential Guard:** https://www.youtube.com/watch?v=F-pTkesjkhI und https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard

- **Ablauf Steuerungs Schutz:** https://msdn.microsoft.com/library/windows/desktop/mt637065(v=vs.85).aspx

- **Sicherheit und Sicherheit:** https://docs.microsoft.com/windows-server/security/security-and-assurance

## <a name="disclaimer"></a>Haftungsausschluss
Dieser Artikel enthält einen Kommentar über die GDPR wie Microsoft ihn ab dem Datum der Veröffentlichung interpretiert. Wir haben sehr viel Zeit mit der GDPR verbracht und wir glauben, dass wir über ihre Absicht und Bedeutung im Klaren sind und diese so dargestellt haben. Die Anwendung der GDPR ist jedoch äußerst tatsachenspezifisch, und die Aspekte und Interpretationen der GDPR sind nicht definitiv beigelegt.

Daher dient dieser Artikel nur zu Informationszwecken und sollte nicht zuverlässig als rechtlicher Hinweise angesehen werden oder um zu bestimmen, wie die GDPR für Sie und Ihr Unternehmen angewendet wird. Wir empfehlen Ihnen, die mit einem gesetzlich qualifizierten Experten zusammen zu arbeiten, um die GDPR zu besprechen, wie sie speziell für Ihre Organisation angewendet wird und wie sie am besten funktioniert, um Kompatibilität zu gewährleisten.

MICROSOFT GIBT IN BEZUG AUF DIE INFORMATIONEN IN DIESEM ARTIKEL KEINERLEI GEWÄHRLEISTUNG, WEDER AUSDRÜCKLICH NOCH KONKLUDENT. Dieser Artikel wird auf "as-is"-Basis bereitgestellt. Die in diesem Artikel gegebenen Informationen und Ansichten, darunter URLs und andere Verweise auf Internetseiten, können ohne vorherige Ankündigung geändert werden.

Dieser Artikel stellt Ihnen keinerlei Rechte am geistigen Eigentum eines beliebigen Microsoft-Produkts zur Verfügung.  Dieser Artikel darf nur für interne Zwecke kopiert und verwendet werden.  

Veröffentlicht: September 2017<br>
Version 1.0<br>
© 2017 Microsoft. Alle Rechte vorbehalten.


