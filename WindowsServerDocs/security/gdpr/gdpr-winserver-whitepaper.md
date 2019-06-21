---
title: Ihre Reise in die Datenschutz-Grundverordnung (DSGVO) für Windows Server 2016
description: Verwenden in diesen Artikel, um zu verstehen, was GDPR ist und die Produkte von Microsoft, um Ihnen den Einstieg zur Kompatibilität zu erleichtern.
keywords: Vertraulichkeit, GDPR
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 09/25/2017
ms.author: nirb
ms.openlocfilehash: 1c374c00573e87594eeeab620face9ea9acaa531
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284205"
---
# <a name="beginning-your-general-data-protection-regulation-gdpr-journey-for-windows-server"></a>Beginnen Ihre Journey allgemeine Datenschutz-Grundverordnung (DSGVO) für Windows Server 

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

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

- **Erweiterter Datenschutzrechte.** Ein stärkerer Datenschutz für Einwohner der EU, um sicherzustellen, dass sie die Zugriffsberechtigung für den Zugriff auf ihre persönlichen Daten erhalten, Ungenauigkeiten in diesen Daten korrigieren, diese löschen können, bei der Verarbeitung ihrer persönlichen Daten Einspruch erheben und diese verschieben können.

- **Verbesserte die Verpflichtung zum Schutz personenbezogener Daten.** Verstärkte Verantwortlichkeit von Organisationen, die personenbezogene Daten verwalten, mehr Klarheit der Verantwortung bei der Einhaltung der Kompatibilität.

- **Obligatorische personenbezogenen Daten einer sicherheitsverletzung meldet.** Organisationen, die Kontrolle über persönliche Daten haben müssen ihren zuständigen Behörden unverzüglich persönliche Datenverstöße melden, die die Rechte und Grundfreiheiten von Personen gefährden, und wenn möglich innerhalb von 72 Stunden nachdem die Verletzung bekannt wird.

Wie erwartet hat die GDPR einen erheblichen Einfluss auf Ihr Unternehmen und erfordert eventuell die Datenschutzrichtlinien zu aktualisieren, Datenschutzkontrollen und -verstoßprozeduren zu implementieren und zu stärken, transparente Richtlinien bereitzustellen und in IT und Schulungen weite zu investieren. Mit Microsoft Windows 10 können Sie effektiv und effizient einige der folgenden Anforderungen in den Griff bekommen.

## <a name="personal-and-sensitive-data"></a>Persönliche und vertrauliche Daten
Als Teil Ihres Aufwands zur Einhaltung der GDPR müssen Sie wissen, wie Verordnung persönliche und vertrauliche Daten definiert und wie diese Definitionen auf Daten Ihrer Organisation zutrifft. Auf Basis dieser verstehen, dass Sie können ermitteln, wo die Daten erstellt wurde, verarbeitet, verwaltet und gespeichert.

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

-   **Entdecken Sie.** Identifizieren Sie Ihre persönlichen Daten und wo sie sich befinden. 

-   **Verwalten.** Steuern, wie auf persönliche Daten zugegriffen und wie sie verwendet werden.

-   **Schützen.** Richten Sie Sicherheitsmechanismen ein, um zu verhindern, erkennen und auf Sicherheitsrisiken und Datenschutzverletzungen zu reagieren.  

-   **Bericht.** Reagieren Sie auf Datenanforderungen, melden Sie Datenschutzverletzungen, und behalten Sie die erforderliche Dokumentation.

    ![Diagramm zur Funktionsweise der 4 Schritte für GDPR und wie sie zusammen funktionieren](../media/GDPR-Windows-Server-Overview/gdpr-steps-diagram.png)

Für die einzelnen Schritte haben wir Beispiel-Tools, Ressourcen und Funktionen in verschiedenen Microsoft-Lösungen beschrieben, die verwendet werden können, um die Anforderungen des Schritts einzuhalten. Während dieser Artikel ist eine umfassende Anleitung für die "Gewusst-wie" nicht, wir haben die Links für weitere Details erhalten Sie eingefügt und Weitere Informationen finden Sie in der [DSGVO-Abschnitt, der im Microsoft Trust Center](https://www.microsoft.com/en-us/trustcenter/privacy/gdpr).

## <a name="windows-server-security-and-privacy"></a>Windows Server-Sicherheit und Datenschutz
Die DSGVO müssen Sie geeignete technische und organisatorische Maßnahmen zum Schutz personenbezogener Daten und Systeme zur Verarbeitung zu implementieren. Im Rahmen der DSGVO sind in Ihrer physischen und virtuellen Server-Umgebungen möglicherweise persönliche und vertrauliche Daten verarbeiten. Verarbeitung kann das bedeuten Vorgang oder jede Gruppe von Vorgängen, z. B. die Datensammlung, speichern und abrufen.

Ihre Fähigkeit, diese Anforderung zu erfüllen und entsprechende technische Sicherheitsmaßnahmen implementiert wiedergeben muss die Bedrohungen, die in zunehmend feindlichen heutigen IT-Umgebung auftreten. Sicherheitsbedrohungen sind heute extrem aggressiv und hartnäckig. In früheren Jahren konzentrierten sich böswillige Angreifer hauptsächlich auf die Anerkennung in der Community für ihre Angriffe oder die Begeisterung, ein System vorübergehend offline geschaltet zu haben. Seitdem haben sich die Motive der Angreifer in Richtung Geldgier geändert, und sie behalten die Gewalt über Geräte und Daten, bis die Besitzer das geforderte Lösegeld bezahlen.

Aktuelle Angriffe konzentrieren sich zunehmend auf den Diebstahl geistigen Eigentums im großen Umfang, die zielgerichtete Systemzersetzung, die zu finanziellen Verlusten führen kann, und jetzt sogar Cyber-Terrorismus, durch den die Sicherheit von Personen und Unternehmen sowie nationale Interessen auf der ganzen Welt bedroht sind. Diese Angreifer sind üblicherweise hochqualifizierte Einzelpersonen und Sicherheitsexperten, von denen einige in Nationalstaaten beschäftigt sind, die über große Budgets und scheinbar unbegrenzte menschliche Ressourcen verfügen. Bedrohungen wie diese erfordern einen Ansatz, der dieser Herausforderung gerecht wird.

Diese Bedrohungen sind nicht nur ein Risiko für Ihre Fähigkeit, die Kontrolle über persönliche oder vertrauliche Daten zu behalten, sondern sie sind ein wesentliches Risiko für Ihr gesamten Unternehmen. Beachten Sie die neuesten Daten aus McKinsey, Ponemon Institute, Verizon und Microsoft:

- Die durchschnittliche Kosten für den Typ der Datenverstöße, den die GDPR erwartet, beträgt 3,5 Milliarden USD.

- 63 % dieser Verstößen sind schwache oder gestohlene Kennwörter, mit denen Sie handeln müssen und die die GDPR erwartet.

- Über 300.000 neue Schadsoftware-Beispiele werden jeden Tag erstellt und verbreitet und machen Ihre Aufgabe des Schutzes von Daten noch schwieriger.

Wie bei der letzten Ransomware-Angriffen, einmal aufgerufen, die schwarzen immer wieder plagt des Internets, setupbegrüßungsbildschirm Angreifer nach größeren Zielen, die sich leisten können, um weitere Aspekte mithilfe von potenziell katastrophalen Konsequenzen zu bezahlen. Die DSGVO enthält zur Folge haben, die machen Ihre Systeme, einschließlich Desktops und Laptops, die tatsächlich umfassende Ziele persönliche und vertrauliche Daten enthalten.

Zwei der wichtigsten Prinzipien geführten haben und weiterhin die Entwicklung von Windows:

- **Sicherheit.** Die Daten, die im Auftrag von unseren Kunden unsere Software und Dienste speichern sollten vor Schäden geschützt und verwendet oder nur auf entsprechende Weise geändert werden. Sicherheitsmodelle sollte für Entwickler einfach zu verstehen und in ihre Anwendungen zu erstellen.

- **Datenschutz.** Benutzer muss Kontrolle über die wie ihre Daten verwendet werden. Richtlinien für die Verwendung der Informationen sollte für den Benutzer. Benutzer sollten Kontrolle über sein, wenn und diese Informationen, um Sie bestmöglich nutzen ihre Zeit erhalten. Es dürfte für Benutzer an entsprechende Verwendung ihrer Informationen, einschließlich der Kontrolle über der Verwendung von e-Mail-Adresse ist, dass sie senden.

Microsoft geblieben gegen diese Prinzipien erwähnt wie kürzlich von Microsoft Chef Satya Nadella fest, 

> "_Während die ganzen Welt weiterhin ändern und geschäftlichen Anforderungen wächst, sind einige Dinge konsistent: eines Kunden bei Bedarf auf Sicherheit und Datenschutz._ "

Wie Sie arbeiten, um die Einhaltung der DSGVO, Grundlegendes zur Rolle der physischen und virtuellen Server erstellen, den Zugriff auf, verarbeiten, speichern und Verwalten von Daten, die als persönlich gelten können, und möglicherweise vertrauliche Daten in der DSGVO wichtig ist. Windows Server bietet Funktionen, mit denen Sie mit den DSGVO-Anforderungen zum Implementieren der entsprechenden technischen und organisatorischen Sicherheitsmaßnahmen, zum Schützen personenbezogener Daten erfüllen.

Der Sicherheitsstatus für Windows Server 2016 keine Bolt; Es handelt sich um architekturprinzip. Und sie können am besten in vier Prinzipale verstanden werden:

- **Schützen.** Laufende Fokus und Innovationen auf Vorbeugemaßnahmen; bekannte Angriffe und bekannter Schadsoftware blockiert.

- **Erkennen.** Umfassende Tools zum Erkennen von Anomalien und reagieren auf Angriffe schneller zu überwachen.

- **Reagieren.** Führende Reaktions- und Technologien sowie umfassende Kenntnisse consulting.

- **Isolieren.** Isolieren von Betriebssystem-Komponenten und geheime Schlüssel, Administratorrechte zu beschränken und hostintegrität gründlich zu messen.

Mit Windows Server ist Ihre Fähigkeit, zu schützen, zu erkennen und Abwehr von den Arten von Angriffen, die zu sicherheitsverletzungen von Daten führen können, erheblich verbessert. Angesichts der strengen Anforderungen hinsichtlich der Verletzung der Benachrichtigung innerhalb der GDPR, und um sicherzustellen, dass Ihre Desktop- und Laptop-Systeme auch gegen Risiken gesichert sind, verringern Sie das Risiko kostspieliger Verletzungsanalysen und Benachrichtigungen.

In den folgenden Abschnitt, sehen Sie, wie Windows Server Funktionen bereitstellt, die direkt in der Phase "Schützen" Ihre grundverordnung passen. Diese Funktionen fallen in drei schutzszenarien:

- **Schützen Sie Ihre Anmeldeinformationen ein, und begrenzen Sie Administratorrechte.** Windows Server 2016 können Sie die Implementierung dieser Änderungen, um zu verhindern, dass Ihr System als einen Startpunkt für weitere Angriffe verwendet wird.

- **Sichern Sie das Betriebssystem zum Ausführen Ihrer apps und Infrastruktur.** Windows Server 2016 bietet Schutzebenen, die Ihnen hilft, um externer Angreifer Schadsoftware ausgeführt oder Ausnutzen von Sicherheitslücken zu blockieren.

- **Sichern der Visualisierung.** Windows Server 2016 ermöglicht die sichere Visualisierung mit abgeschirmten VMs and dem geschützten Fabric. Dadurch können Sie die zu verschlüsseln, und führen Sie Ihre virtuellen Computer auf vertrauenswürdigen Hosts im Fabric, besser vor Angriffen schützen.

Diese Funktionen ausführlicher unten mit Verweisen auf DSGVO-Anforderungen für bestimmte, basieren auf Erweiterte des Schutzes, die dabei hilft, die Integrität und Sicherheit des Betriebssystems und der Daten zu verwalten.

Eine wichtige Bereitstellung innerhalb der DSGVO ist Schutz von Daten von Entwurf und werden standardmäßig und helfen, Ihre Daten, um diese Bereitstellung zu erfüllen, werden Features in Windows 10, z. B. BitLocker-Geräteverschlüsselung. BitLocker verwendet die Trusted Platform Module (TPM)-Technologie, die hardwarebasierte, sicherheitsbezogene Funktionen bereitstellt. Dieser Prozessor Crypto-Chip enthält mehrere physische Sicherheitsmechanismen, um Schutz vor Missbrauch zu erleichtern, und Malware kann nicht um die Sicherheitsfunktionen des TPM zu manipulieren.

Der Chip umfasst mehrere physische Sicherheitsmechanismen, die ihn manipulationssicher machen, und Schadsoftware ist nicht in der Lage, die TPM-Sicherheitsfunktionen zu manipulieren. Die wichtigsten Vorteile der TPM-Technologie bestehen in ihren Möglichkeiten. Sie können:

-   Kryptografieschlüssel generieren, speichern und deren Einsatz beschränken.

-   TPM-Technologie für die Plattformgeräteauthentifizierung nutzen. Sie verwenden dazu den eindeutigen RSA-Schlüssel des TPMs, der in sich selbst geschrieben ist.

-   Plattformintegrität gewährleisten, indem Sicherheitsmessungen vorgenommen und gespeichert werden.

Zusätzliche erweiterte Schutzmaßnahmen für Ihr Betriebssystem ohne Datenschutzverletzungen umfassen „Windows Trusted Boot”, das die Integrität des Systems gewährleistet, indem es sicherstellt, das die Schadsoftware nicht vor den Verteidigungseinrichtungen des Systems gestartet werden kann.

## <a name="windows-server-supporting-your-gdpr-compliance-journey"></a>WindowsServer: Unterstützung der Umsetzung der Verordnung DSGVO
Wichtige Features in Windows Server können Sie effizient und effektiv die Sicherheits- und Datenschutzmechanismen implementieren, die die DSGVO für die Kompatibilität erforderlich sind. Während die Verwendung dieser Features der Konformität Ihrer nicht garantieren, unterstützen sie Ihre bemühungen dazu.

Das Server-Betriebssystem befindet sich auf ein strategischer Ebene in einer Organisation Infrastruktur Sitzungsebene ermöglicht, neue Möglichkeiten zum Schutzebenen vor Angriffen zu erstellen, die Daten zu stehlen und Ihr Unternehmen unterbrechen kann. Wichtige Aspekte der dsgvo werden geteilt wie z. B. Privacy by Design, den Schutz von Daten und Access Control innerhalb Ihrer IT-Infrastruktur auf der Ebene berücksichtigt werden müssen.

Arbeiten zum Schutz der Identität, Betriebssystem und Ebenen der Virtualisierung, Windows Server 2016 mit Ihrer Hilfe können die häufigen Angriffsmethoden verwendet, um unerlaubten Zugriff auf Ihre Systeme zu erhalten: Diebstahl von Anmeldeinformationen, Malware und eine kompromittierte Virtualisierungs-Fabric. Zusätzlich zu reduzieren, Geschäftsrisiken, erstellt die Sicherheitskomponenten in Windows Server 2016-Hilfe Erfüllung von Complianceanforderungen für wichtige Regierungsbehörden und Industrie Sicherheitsvorschriften. 

Diese Identität, Betriebssystem und Virtualisierung Schutzmaßnahmen ermöglichen es Ihnen, Ihr Datencenter mit Windows Server als virtuellen Computer in einer beliebigen Cloud besser zu schützen, und begrenzen Sie die Fähigkeit von Angreifern, Anmeldeinformationen gefährden, Malware zu starten und im unentdeckt bleiben Ihre Netzwerk. Dementsprechend bietet als Hyper-V-Host bereitgestellt wird, Windows Server 2016 die Sicherheit für Ihre Virtualisierungsumgebungen durch abgeschirmte VMs und verteilten Firewall-Funktionen. Mithilfe von Windows Server 2016 wird das Server-Betriebssystem ein aktiver Teilnehmer in Ihre Datencenter-sicherheitslösungen.

### <a name="protect-your-credentials-and-limit-administrator-privileges"></a>Schützen Sie Ihre Anmeldeinformationen und Einschränken von Administratorrechten 
Steuerung des Zugriffs auf personenbezogene Daten und die Systeme, die diese Daten verarbeiten, einen Bereich mit der DSGVO, die bestimmte Anforderungen, einschließlich des Zugriffs von Administratoren ist. Privilegierte Identitäten sind alle Konten, die erhöhte Rechte, z. B. Benutzerkonten zu haben, die von der Domänen-Admins, Organisations-Admins, lokale Administratoren oder sogar erfahrene Benutzer Gruppen angehören. Diese Identitäten können auch Konten enthalten, die Berechtigungen direkt, wie z. B. das Ausführen von Sicherungen, Herunterfahren des Systems oder sonstigen Rechte aufgeführt, die im Knoten "Zuweisen von Benutzerrechten" in der Konsole Lokale Sicherheitsrichtlinie gewährt wurden.

Als Prinzip der allgemeinen Zugriff-Steuerelement und in einer Reihe mit der DSGVO müssen Sie diese privilegierten Identitäten vor der Gefährdung durch potenzielle Angreifer zu schützen. Zunächst ist es wichtig zu verstehen, wie Identitäten gefährdet sind; Anschließend können Sie planen, um zu verhindern, dass Angreifer Zugriff auf diese privilegierten Identitäten.

#### <a name="how-do-privileged-identities-get-compromised"></a>Wie kompromittiert privilegierte Identitäten erhalten?
Privilegierte Identitäten können gefährdet zu erhalten, wenn Organisationen keine Richtlinien, um sie zu schützen. Im Folgenden finden Sie entsprechende Beispiele:

- **Mehr Berechtigungen als erforderlich sind.** Eine der am häufigsten auftretenden Probleme ist, dass Benutzer mehr Berechtigungen als erforderlich, um ihre Funktion auszuführen sind. Beispielsweise kann ein Benutzer, die DNS verwaltet ein AD-Administrator sein. In den meisten Fällen wird dadurch vermeiden Sie die der verschiedenen Verwaltungsebenen konfiguriert werden muss. Aber wenn ein solches Konto gefährdet ist, hat der Angreifer automatisch erhöhte Rechte.

- **Angemeldet ständig erhöhten Rechten aus.** Ein weiteres häufiges Problem ist, Benutzer mit erhöhten Rechten für unbegrenzte Zeit verwendet werden können. Dies ist häufig bei der IT-Experten, die auf einem Desktopcomputer, die mit einem privilegierten Konto anmelden, angemeldet zu bleiben, und verwenden das privilegierte Konto, um das Web durchsuchen und e-Mail-Adresse verwenden (typische IT-Arbeit Auftrag Funktionen). Unbegrenzte Dauer von privilegierten Konten können das Konto anfälliger für Angriffe und erhöht die Wahrscheinlichkeit, dass das Konto gefährdet ist.

- **Social-Engineering-Research.** Die meisten Anmeldeinformationen Bedrohungen beginnen mit der Erforschung der Organisationsstatus, und klicken Sie dann über Social-Engineering durchgeführt. Beispielsweise kann ein Angreifer einen e-Mail-Phishing Angriff Gefährdung Berechtigte Konten (aber nicht unbedingt Konten mit erhöhten Rechten), die Zugriff auf die im Netzwerk einer Organisation durchführen. Klicken Sie dann verwendet der Angreifer diese gültigen Konten aus, um zusätzliche Forschung in Ihrem Netzwerk durchzuführen und privilegierte Konten zu identifizieren, die administrative Aufgaben ausführen können. 

- **Nutzen Sie die Konten mit erhöhten Rechten.** Sogar mit einem normalen, ohne erhöhte Rechte Benutzerkonto im Netzwerk können Angreifer Zugriff auf Konten mit erhöhten Berechtigungen erhalten. Eines der gängigeren Methoden dieser Vorgehensweise wird dazu die Verwendung der Pass-the-Hash oder Pass-the-Token-Angriffe. Weitere Informationen zu den Pass-the-Hash und anderen Techniken zum Diebstahl von Anmeldeinformationen finden Sie auf die Ressourcen auf der [Pass-the-Hash (PtH) Seite](https://technet.microsoft.com/dn785092.aspx).

Es gibt selbstverständlich weitere Methoden, mit denen Angreifer zu identifizieren und Manipulieren von privilegierten Identitäten (mit neuen Methoden, die jeden Tag erstellt wird). Es ist daher wichtig, dass Sie Methoden für die Benutzer mit geringsten Rechten Konten reduzieren Sie die Fähigkeit von Angreifern für den Zugriff auf privilegierte Identitäten Anmelden einrichten. In den folgenden Abschnitten beschreiben die Funktionen, in denen Windows Server diese verringern können.

#### <a name="just-in-time-admin-jit-and-just-enough-admin-jea"></a>Just-in-Time-Verwaltung (JIT)- und Just Enough Administration (JEA)
Beim Schutz vor Pass-the-Hash- oder Pass-the-Ticket-Angriffen wichtig, die Anmeldeinformationen des Administrators immer noch andere Art und Weise ist, wie z.B. Social-Engineering und verärgerte Mitarbeiter brute-Force-gestohlen werden können. Aus diesem Grund zusätzlich zum Isolieren von Anmeldeinformationen, die so weit wie möglich, möchten Sie auch eine Möglichkeit, um die Reichweite von Administratorrechte zu beschränken, für den Fall, dass sie kompromittiert werden.

Heute sind zu viele Administratorkonten überprivilegierten, auch wenn sie nur eine Zuständigkeitsbereich verfügen. Beispielsweise wird eine DNS-Administrator, einen eingeschränkten Satz von Berechtigungen zum Verwalten von DNS-Server erforderlich sind, häufig Administratorrechten Domäne gewährt. Darüber hinaus, da diese Anmeldeinformationen für coreschemas gewährt werden, gibt es keine Beschränkung für wie lange sie verwendet werden können.

Jedes Konto mit Administratorrechten unnötige Domäne nimmt Ihre Anfälligkeit für Angriffe, die nach Anmeldeinformationen gefährden zu. Um die Angriffsfläche für Angriffe zu minimieren, möchten Sie geben nur den bestimmten Satz von rechten, die ein Administrator muss für die Aufgabe – und nur für das Zeitfenster erforderlich, um es auszuführen.

Just Enough Administration mit Just-in-Time-Verwaltung, können Administratoren die bestimmten Berechtigungen, die sie für das genaue Fenster der benötigten Zeit benötigen anfordern. Ein DNS-Administrator Sie können z. B. Verwenden von PowerShell zum Aktivieren der Just Enough Administration eine begrenzte Anzahl von Befehlen zu erstellen, die für die DNS-Verwaltung verfügbar sind.

Wenn der DNS-Administrator ein Update an einem der ihr Server vornehmen muss, würden sie den Zugriff zum Verwalten von DNS mit der Microsoft Identity Manager 2016 anfordern. Die Request-Workflow kann einen Genehmigungsprozess wie z. B. zwei-Faktor-Authentifizierung enthalten, der aufrufen, das Mobiltelefon des Administrators, um seine Identität zu überprüfen, bevor die angeforderten Berechtigungen erteilt. Sobald gewährt, die DNS-Berechtigungen den Zugriff auf die Rolle "PowerShell" für DNS für eine bestimmte Zeitspanne bereitstellen.

Dieses Szenario stellen Sie sich vor, wenn der DNS-Administratoranmeldeinformationen gestohlen wurden. Zuerst, da die Anmeldeinformationen ohne Administratorrechte verbunden haben, wäre nicht der Angreifer für den Zugriff auf die DNS-Server – oder anderen Systemen – keine Änderungen vornehmen kann. Wenn der Angreifer versucht haben, Berechtigungen für den DNS-Server anfordern, darum zweistufige Authentifizierung sie ihre Identität bestätigen. Da wahrscheinlich nicht, dass der Angreifer Mobiltelefon für DNS-Administrator verfügt, wird die Authentifizierung fehl. Dies würde den Angreifer aus dem System sperren und Warnung von der IT-Organisation, dass die Anmeldeinformationen möglicherweise gefährdet sind.

Darüber hinaus viele Organisationen verwenden die kostenlose [lokalen Administrator Password Solution (LAPS)](http://aka.ms/laps) als eine einfache und dennoch leistungsstarke JIT verwaltungsmechanismus für ihre Server und Client-Systeme. Die LAPS ermöglicht die Verwaltung der Kennwörter von lokalen Konten von in Domänen eingebundene Computer. Kennwörter in Active Directory (AD) gespeichert und geschützt durch Zugriffssteuerungsliste (ACL), und daher nur berechtigte Benutzer lesen oder die Zurücksetzung anfordern können.

Wie erwähnt in der [Windows Credential Theft Mitigation Guide](https://www.microsoft.com/en-us/download/confirmation.aspx?id=54095), 

> "_verwenden Sie die Kriminellen Tools und Techniken zum Diebstahl von Anmeldeinformationen ausführen und Wiederverwendung von Angriffen zu verbessern, die Angreifer finden das einfacher, ihre Ziele zu erreichen. Diebstahl von Anmeldeinformationen verwendet häufig Betriebsverfahren oder Benutzer Offenlegung von Anmeldeinformationen, effektive Schutzmaßnahmen auf einen ganzheitlichen Ansatz benötigen Sie ein, der Adressen der Personen, Prozesse und Technologie. Darüber hinaus diese Angriffe basieren auf der Angreifer, der Diebstahl von Anmeldeinformationen nach Beeinträchtigung eines Systems zum Erweitern oder Zugriff beizubehalten, sodass Organisationen sicherheitsverletzungen schnell enthalten müssen durch die Implementierung von Strategien, die verhindern, dass Angreifer frei verschieben, und bleiben ein kompromittierten Netzwerk._ "

Eine wichtige designüberlegung für Windows Server wurde Credential Theft entschärfen – insbesondere abgeleiteten Anmeldeinformationen. Credential Guard bietet wesentlich verbesserte Sicherheit für abgeleiteten den Diebstahl und Wiederverwendung implementieren eine wesentliche architektonische Änderung in Windows soll helfen, Hardware-basierte Isolation-Angriffe zu verhindern, anstatt einfach versuchen davor zu schützen.

Viele Angriffe werden blockiert, während mithilfe von Windows Defender Credential Guard, NTLM und Kerberos abgeleitete Anmeldeinformationen geschützt sind, mit der virtualisierungsbasierten Sicherheit, den Diebstahl von Anmeldeinformationen Angriffstechniken, und in Tools verwendet. Im Betriebssystem ausgeführte Schadsoftware mit Administratorberechtigungen kann geheime Schlüssel, die durch die virtualisierungsbasierte Sicherheit geschützt sind, nicht extrahieren. Während Windows Defender Credential Guard über eine leistungsstarke Lösung ist, Angriffe dauerhafte Bedrohung wird, die wahrscheinlich UMSCHALTTASTE gedrückt, um neue Angriffsmethoden und Sie Device Guard, auch wie unten beschrieben, zusammen mit anderen Sicherheitsstrategien und den Architekturen nutzen sollten.

#### <a name="windows-defender-credential-guard"></a>Windows Defender Credential Guard
Windows Defender Credential Guard verwendet virtualisierungsbasierte Sicherheit, um Anmeldeinformationen zu isolieren, verhindert, dass das Kennworthashes oder Kerberos-Tickets abgefangen wird. Er verwendet ein völlig neues isolierten Local Security Authority (LSA) Onlineprozess, der für den Rest des Betriebssystems nicht zugänglich ist. Alle Binärdateien, die von isolierten LSA verwendet werden mit Zertifikaten signiert, die überprüft werden, bevor Sie starten sie in der geschützten Umgebung, sodass Pass-the-Hash Art von Angriffen völlig unwirksam.

Windows Defender Credential Guard verwendet:

- Virtualisierungsbasierte Sicherheit (erforderlich). Zusätzliche Anforderungen:

    - CPU mit 64 Bit

    - CPU-Virtualisierungserweiterungen sowie erweiterte Seitentabellen

    - Windows-Hypervisor

- Sicherer Start (erforderlich)

- TPM 2.0, entweder diskret oder firmwarebasiert (aufgrund der Hardwarebindung bevorzugt)

Sie können Windows Defender Credential Guard verwenden, um privilegierte Identitäten zu schützen, durch den Schutz der Anmeldeinformationen und die Teile der Anmeldeinformationen unter Windows Server 2016. Weitere Informationen zu Windows Defender Credential Guard finden Sie unter [schützen abgeleiteter Domänenanmeldeinformationen mit Windows Defender Credential Guard](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard).

#### <a name="windows-defender-remote-credential-guard"></a>Windows Defender Remote Credential Guard
Windows Defender Remote Credential Guard unter Windows Server 2016 und Windows 10 Anniversary Update schützt auch Anmeldeinformationen für Benutzer mit Remotedesktopverbindungen. Jede Person, die Remote Desktop Services müssten zuvor, melden Sie sich bei ihrem lokalen Computer, und klicken Sie dann erforderlich, damit Sie melden Sie sich erneut, wenn sie eine Remoteverbindung mit ihren Zielcomputer ausgeführt werden. Diese zweite Anmeldung Anmeldeinformationen übergeben würde, auf den Zielcomputer, für die Pass-the-Hash verfügbar zu machen oder Pass-the-Ticket-Angriffen.

Mit Windows Defender Remote Credential Guard implementiert Windows Server 2016 einmaliges Anmelden für Remotedesktopsitzungen, der Clientzugriffsrichtlinie mehr Ihrem Benutzernamen und Kennwort erneut eingeben. Stattdessen nutzt er die Anmeldeinformationen, die Sie bereits verwendet haben, melden Sie sich auf Ihren lokalen Computer. Um Windows Defender Remote Credential Guard verwenden zu können, müssen der Remotedesktop-Client und Server die folgenden Anforderungen erfüllen:

- Muss einer Active Directory-Domäne angehören und werden in der gleichen Domäne oder einer Domäne mit einer Vertrauensstellung.

- Kerberos-Authentifizierung muss verwendet werden.

- Muss ausgeführt werden, mindestens Windows 10, Version 1607 oder Windows Server 2016.  

- Der Remotedesktop klassischen Windows-app ist erforderlich. Die Remote Desktop universelle Windows-Plattform-app unterstützt keine Windows Defender Remote Credential Guard.

Sie können Windows Defender Remote Credential Guard aktivieren, indem Sie eine registrierungseinstellung auf dem Remotedesktop-Server und der Gruppenrichtlinie oder einen Remote Desktop Connection-Parameter auf dem Remotedesktop-Client verwenden. Weitere Informationen zum Aktivieren von Windows Defender Remote Credential Guard finden Sie unter [Schützen von Remotedesktop-Anmeldeinformationen mit Remote Credential Guard in Windows Defender](https://docs.microsoft.com/windows/access-protection/remote-credential-guard). Mit Windows Defender Credential Guard können Windows Defender Remote Credential Guard Sie zum Schutz des privilegierte Identitäten unter Windows Server 2016.

### <a name="secure-the-operating-system-to-run-your-apps-and-infrastructure"></a>Sichern Sie das Betriebssystem zum Ausführen Ihrer apps und Infrastruktur
Verhindert cyberbedrohungen erfordert auch suchen, und blockieren Schadsoftware und Angriffe, bei die unter Kontrolle bringen, indem subverting die Standardmethoden Betrieb Ihrer Infrastruktur zu suchen. Wenn der Angreifer ein Betriebssystem oder die Anwendung für die Ausführung in eine nicht vorab festgelegten, nicht geeignete Möglichkeit erhalten, verwenden sie wahrscheinlich das System, um böswilligen Aktionen ausführen. Windows Server 2016 bietet Schutzebenen, die die externe Angreifer Schadsoftware ausgeführt oder Ausnutzen von Sicherheitslücken zu verhindern. Das Betriebssystem übernimmt eine aktive Rolle beim Schutz von Infrastruktur und Anwendungen Warnungsadministratoren Aktivität, der angibt, dass ein System verletzt wurde.

#### <a name="windows-defender-device-guard"></a>Windows Defender Device Guard
Windows Server 2016 umfasst Windows Defender Device Guard, um sicherzustellen, dass nur vertrauenswürdige Software auf dem Server ausgeführt werden kann. Verwenden die virtualisierungsbasierte Sicherheit, können sie einschränken, welche Binärdateien auf dem System basierend auf der Richtlinie der Organisation ausgeführt werden können. Wenn nichts, als die angegebene Binärdateien versucht, auszuführen, wird Windows Server 2016 wird sie gesperrt, und den gescheiterte Versuch protokolliert, sodass Administratoren sehen können, dass es sich bei eine mögliche sicherheitsverletzung aufgetreten ist. Breach Notification ist ein wichtiger Bestandteil der die Anforderungen für die Einhaltung der dsgvo.

Windows Defender Device Guard ist auch mit PowerShell integriert, sodass Sie autorisieren können, welche Skripts auf Ihrem System ausgeführt werden können. In früheren Versionen von Windows Server konnten Administratoren Code Integrity Erzwingung umgehen, indem Sie einfach die Richtlinie löschen, aus der Codedatei verwendet wird. Mit Windows Server 2016 können Sie eine Richtlinie konfigurieren, die von Ihrer Organisation angemeldet ist, sodass nur eine Person mit Zugriff auf das Zertifikat, das die Richtlinie signiert die Richtlinie ändern kann.

#### <a name="control-flow-guard"></a>Ablaufsteuerungsschutz 
Windows Server 2016 enthält auch integrierten Schutz gegen einige Fälle von speicherbeschädigungsangriffen. Patchen von Ihren Servern ist wichtig, aber besteht immer die Möglichkeit, dass Malware kann für ein Sicherheitsrisiko, das noch nicht identifiziert wurden entwickelt werden. Einige der am häufigsten verwendeten Methoden für diese Sicherheitslücken ausgenutzt werden ungewöhnliche oder extreme Daten an ein ausgeführtes Programm bereitstellen. Beispielsweise kann ein Angreifer eine Pufferüberlaufschwachstelle ausnutzen, indem Sie die weitere Eingabe in ein Programm als erwartet, und Sie den Bereich reserviert, die von der Anwendung übersteigen, die eine Antwort enthalten soll. Dies kann benachbarte beschädigt werden, die einen Funktionszeiger enthalten kann.

Wenn die Anwendung mit dieser Funktion aufgerufen wird, kann es dann zu eine nicht beabsichtigte Position gemäß der Angreifer springen. Diese Angriffe sind auch bekannt als Jump-oriented programming (JOP)-Angriffe. Control Flow Guard verhindert JOP-Angriffe, indem eine enge Einschränkungen platzieren, welcher Anwendungscode ausgeführt – insbesondere indirekte werden kann Anweisungen aufrufen. Er fügt hinzu, dass einfache Sicherheit überprüft werden, um den Satz von Funktionen in der Anwendung zu identifizieren, die als gültige Ziele für indirekte Aufrufe sind. Wenn eine Anwendung ausgeführt wird, überprüft er, dass diese indirekte Aufrufziele gültig sind.

Wenn die Control Flow Guard zur Laufzeit fehlschlägt, Windows Server 2016 wird sofort beendet das Programm, unterbrechen alle Exploit, der versucht, eine ungültige Adresse indirekt aufrufen. Ablaufsteuerungsschutz bietet eine wichtige zusätzliche Schutzschicht Device Guard. Wenn eine Anwendung zugelassenen kompromittiert wurde, wäre es von Device Guard, deaktiviert ausführen können, da die Device Guard Screening angezeigt würde, dass die Anwendung signiert wurde, und gilt als vertrauenswürdige.

Aber da Control Flow Guard erkannt werden können, ob die Anwendung in einer nicht vorab festgelegten, unbrauchbaren Reihenfolge ausgeführt wird, der Angriff würde fehlschlagen, verhindern die gefährdete Anwendung ausgeführt wird. Zusammen erschwert diese Schutzmaßnahmen noch sehr Angreifern beim Einfügen von Schadsoftware in Software unter Windows Server 2016 ausgeführt wird.

Entwickler von Anwendungen, in dem personenbezogene Daten behandelt werden, wird empfohlen, die (Control Flow Guard, CFG) in ihre Anwendungen zu ermöglichen. Dieses Feature steht in Microsoft Visual Studio 2015 und auf "CFG-fähigen" Versionen von Windows ausgeführt wird – die X86- und X64-releases für Desktop- und Server von Windows 10 und Windows 8.1 Update (KB3000850). Sie haben keine CFG für jeden Teil des Codes zu aktivieren, eine Mischung aus CFG aktiviert und die nicht-CFG aktiviert Code einwandfrei ausgeführt. Aber nicht CFG für den gesamten Code zu aktivieren, kann Lücken in der Schutzgruppe öffnen. Darüber hinaus CFG Code funktioniert gut auf "CFG-fähigen" Windows-Versionen aktiviert und ist daher vollständig kompatibel mit ihnen.

#### <a name="windows-defender-antivirus"></a>Windows Defender Antivirus
Windows Server 2016 enthält der Branche führenden, aktive Erkennungsfunktionen von Windows Defender auf bekannte Schadsoftware zu blockieren. Windows-Verwaltungsinstrumentation (Windows Defender Antivirus, AV) kann zusammen mit Windows Defender Device Guard und Control Flow Guard, um zu verhindern, dass bösartiger Code jeglicher Art, die auf den Servern installiert wird. Ist es standardmäßig aktiviert – der Administrator muss nicht keinen Aktionen für sie arbeiten. Windows Defender Antivirus ist auch zur Unterstützung der verschiedenen Serverrollen in Windows Server 2016 optimiert. In der Vergangenheit verwendet Angreifer-Shells wie PowerShell, um böswillige binären Code zu starten. In Windows Server 2016 ist PowerShell jetzt mit Windows Defender Antivirus zum Scannen nach Schadsoftware vor dem Starten des Codes integriert.

Windows Defender Antivirus ist eine integrierte Antischadsoftware-Lösung, die Sicherheits-und Antischadsoftware für Desktopcomputer, tragbare Computer und Server bereitstellt. Windows Defender Antivirus erkannt wurde erheblich verbessert, da es in Windows 8 eingeführt wurde. Windows Defender Antivirus auf Windows Server verwendet einen mehrgleisigen Ansatz, um Antischadsoftware zu verbessern:

- **Von der Cloud bereitgestellter Schutz** erkennt und blockiert neue Schadsoftware innerhalb von Sekunden, auch wenn die Schadsoftware bisher noch nie vorgekommen ist.

- **Umfassender lokaler Kontext** verbessert die Identifizierung von Schadsoftware. Windows Server informiert Windows Defender Antivirus erkannt, nicht nur Informationen zu Inhalt, wie Dateien und Prozesse, sondern auch, in dem der Inhalt stammt, wo sie gespeichert wurden und vieles mehr. 

- **Umfangreiche globale Sensoren** sorgen Sie für Windows Defender Antivirus aktuelle und auch die neuesten Malware kennen. Dies erfolgt auf zwei Arten: durch Sammeln der Daten des umfassenden lokalen Kontexts von Endpunkten und das zentrale Analysieren dieser Daten.

- **Vor Manipulation** können Windows Defender Antivirus selbst vor Angriffen durch Schadsoftware zu schützen. Beispielsweise verwendet die Windows Defender Antivirus geschützt-Prozesse, die verhindert, dass nicht vertrauenswürdige Prozesse versuchen, Windows Defender Antivirus-Komponenten, Registrierungsschlüssel, manipulieren und so weiter.

- **Professionelle Funktionen** bieten IT-Experten, die Tools und die Konfigurationsoptionen erforderlich, Windows Defender Antivirus eine Antischadsoftware-Lösung für leistungsstarkes stellen.

#### <a name="enhanced-security-auditing"></a>Erweiterter sicherheitsüberwachung 
Windows Server 2016 benachrichtigt aktiv Administratoren potenzielle sicherheitsverletzung Versuche bei der Überwachung von erhöhte Sicherheit, die ausführlichere Informationen bereitstellt, die für schnellere Erkennung und forensische Analysen verwendet werden kann. Protokolliert Ereignisse von Control Flow Guard, Windows Defender Device Guard und andere Sicherheitsfunktionen an einem Ort, erleichtert es Administratoren, um zu bestimmen, welche Systeme gefährdet sein können.

Neue Ereigniskategorien umfassen:

- **Überwachen der Gruppenmitgliedschaften.** Ermöglicht Ihnen die Informationen zur Gruppenmitgliedschaft in Anmeldetoken eines Benutzers zu überwachen. Ereignisse werden generiert, wenn Mitgliedschaften aufgelistet sind, oder abgefragt werden, auf dem PC, in der anmeldesitzung erstellt wurde. 
 
- **Überwachen Sie Plug & Play-Aktivität.** Können Sie überwachen, wenn Plug & Play ein externes Geräts – erkennt, das Malware enthalten können. Plug & Play-Ereignisse können verwendet werden, um Änderungen in der Systemhardware aufzuspüren. Eine Liste von IDs-Hardwareanbieter ist im Ereignis enthalten.

Windows Server 2016 integriert einfach Security Incident (SIEM) ereignisverwaltungssysteme, z. B. Microsoft Operations Management Suite (OMS), das die Informationen in Intelligence-Berichten auf potenziellen sicherheitsverletzungen integrieren können. Die Tiefe der Informationen durch die Verbesserte Überwachung ermöglicht Sicherheitsteams zu identifizieren und zu potenziellen sicherheitsverletzungen zu reagieren, schnell und effektiv.

### <a name="secure-virtualization"></a>Sichern der Visualisierung
Unternehmen virtualisieren heute und alles, von SQL Server, SharePoint, Active Directory-Domänencontroller kann. Virtuelle Computer (VMs) erleichtern einfach bereitstellen, verwalten, Dienst und Ihrer Infrastruktur automatisieren. Aber wenn es um Sicherheit geht, geworden gefährdeten virtualisierungsfabrics eine neue Angriffsmethode, das zur Verteidigung gegen – schwer ist bis jetzt. Hinsichtlich der DSGVO sollten Sie vorstellen, zum Schützen von VMs, wie Sie physische Server, einschließlich der Verwendung von VM-TPM-Technologie geschützt würden.

Windows Server 2016 ändert sich im Grunde wie Unternehmen schützen können Virtualisierung, mit mehreren Technologien, mit denen Sie virtuelle Computer zu erstellen, die nur auf Ihren eigenen Fabric ausgeführt wird. dabei, um zu verhindern, die Speicher-, Netzwerk- und Hostgeräte, die sie ausgeführt werden.

#### <a name="shielded-virtual-machines"></a>Abgeschirmte virtuelle Computer
Die gleichen Dinge, die virtuelle Computer migrieren so leicht machen, Sicherung und Replikation, auch sie leichter zu ändern und zu kopieren. Ein virtueller Computer ist nur eine Datei, sodass es nicht im Speicher, Sicherungen oder an anderer Stelle im Netzwerk geschützt ist. Ein weiteres Problem ist, dass Fabric-Administratoren – gibt an, ob sie ein Speicheradministrator oder Netzwerkadministrator sind – den Zugriff auf alle virtuellen Computer.

Ein kompromittierte Fabric-Administrator kann auf virtuellen Computern problemlos kompromittierten Daten führen. Alles, was der Angreifer tun muss, ist die kompromittierte Anmeldeinformationen verwenden, kopieren alle VM-Dateien, die sie auf einem USB-Laufwerk wie, und führen es aus der Organisation, in dem diese VM-Dateien können über ein anderes System zugegriffen werden. Würde eine gestohlene dieser virtuellen Computer einer Active Directory-Domänencontroller, z. B. der Angreifer einfach den Inhalt anzeigen und verwenden verfügbar brute-Force-Techniken, um die Kennwörter in Active Directory-Datenbank, zu knacken letztlich ihnen Zugriff gewähren um alles in Ihrer Infrastruktur.

Windows Server 2016 führt abgeschirmte virtuelle Computer (abgeschirmte VMs) als Schutz gegen Szenarien, wie gerade beschrieben. Abgeschirmte VMs enthalten ein virtuelles TPM-Gerät, dadurch können Unternehmen BitLocker-Verschlüsselung auf den virtuellen Computern anwenden, und stellen Sie sicher, dass sie nur auf vertrauenswürdigen Hosts zum Schutz vor gefährdeten Speicher-, Netzwerk- und Host-Administratoren ausgeführt werden. Abgeschirmte VMs werden mit VMs der 2. Generation, die Firmware für Unified Extensible Firmware Interface (UEFI) unterstützt und virtuelles TPM erstellt.

#### <a name="host-guardian-service"></a>Host-Überwachungsdienst
Zusammen mit abgeschirmten VMs ist der Host-Überwachungsdienst eine wesentliche Komponente für die Erstellung einer sicheren Virtualisierungs-Fabric. Seine Aufgabe besteht darin, feststellen, die Integrität eines Hyper-V-Hosts, bevor er eine abgeschirmte VM starten oder zu diesem Host migrieren kann. Es enthält die Schlüssel für abgeschirmte VMs und wird nicht aufgehoben werden, bis die Sicherheitsintegrität gewährleistet werden kann. Es gibt zwei Möglichkeiten, die Hyper-V-Hosts, Host-Überwachungsdienst bestätigen erforderlich machen können.

Das erste und am sichersten, ist die Hardware-vertrauenswürdiger Nachweis. Diese Lösung erfordert, dass es sich bei Ihrem mit abgeschirmten VMs auf Hosts ausgeführt werden, die 2.0 der TPM-Chips und UEFI 2.3.1 erforderlich. Diese Hardware ist erforderlich, um die kontrollierter Start bereitstellen und Integritätsinformationen für Betriebssystem-Kernel von Host-Überwachungsdienst erforderlich, um sicherzustellen, dass den Hyper-V-Host nicht manipuliert wurde.

IT-Organisationen haben die Alternative der Verwendung von Admin-vertrauenswürdiger Nachweis, die möglicherweise wünschenswert, wenn TPM 2.0-Hardware nicht in Ihrer Organisation verwendet wird. Dieses Modell Nachweis ist einfach, die bereitgestellt werden, weil es sich bei Hosts werden einfach in eine Sicherheitsgruppe platziert und Host-Überwachungsdienst ist so konfiguriert, dass auf Hosts ausgeführt werden, die Mitglieder der Sicherheitsgruppe sind die abgeschirmte VMs zulassen. Mit dieser Methode ist keine komplexe Messung, um sicherzustellen, dass der Hostcomputer nicht manipuliert wurde. Es entfällt jedoch die Möglichkeit, nicht verschlüsselten virtuellen Computer aus die Tür auf USB-Laufwerke oder, dass der virtuelle Computer auf einem nicht autorisierten-Host ausgeführt wird. Dies ist, da die VM-Dateien nicht auf jedem Computer als die in der festgelegten Gruppe ausgeführt werden. Wenn Sie noch nicht über TPM 2.0-Hardware verfügen, können Sie mit Admin-vertrauenswürdiger Nachweis beginnen und auf Hardware-vertrauenswürdiger Nachweis wechseln, wenn die Hardware aktualisiert wird.

#### <a name="virtual-machine-trusted-platform-module"></a>VM Trusted Platform Module
Windows Server 2016 unterstützt TPM für virtuelle Computer, die Ihnen ermöglicht, erweiterter Sicherheit-Technologien wie BitLocker®-laufwerksverschlüsselung auf virtuellen Computern zu unterstützen. Sie können die TPM-Unterstützung für jede Generation 2 Hyper-V-VM aktivieren, mit Hyper-V-Manager oder das Enable-VMTPM Windows PowerShell-Cmdlet.

Sie können virtual TPM (vTPM) schützen, indem Sie mithilfe der lokalen kryptografischen Schlüssel auf dem Host oder im Host-Überwachungsdienst gespeichert. Während der Host-Überwachungsdienst mehr Infrastruktur erforderlich ist, bietet es also auch mehr Schutz.

#### <a name="distributed-network-firewall-using-software-defined-networking"></a>Softwaredefinierte Netzwerke mit verteilten Netzwerk-firewall
Eine Möglichkeit, den Schutz in virtualisierten Umgebungen zu verbessern, ist das Netzwerk auf eine Weise zu segmentieren, die VMs für die Kommunikation nur für den bestimmten Systemen erforderlich, um die Funktion ermöglicht. Beispielsweise wenn Ihre Anwendung nicht mit dem Internet eine Verbindung herstellen muss, können Sie es partitionieren beseitigen diese Systeme als Ziele aus externe Angreifer abzuwehren. Die Software defined Networking (SDN) in Windows Server 2016 enthält eine verteiltes Netzwerk-Firewall mit dem Sie die Sicherheitsrichtlinien, die Ihre Anwendungen vor Angriffen aus innerhalb oder außerhalb eines Netzwerks schützen können, dynamisch zu erstellen. Diese verteilten Netzwerk-Firewall fügt Ebenen für Ihre Sicherheit ermöglicht es Ihnen, Ihre Anwendungen im Netzwerk zu isolieren. Richtlinien können an einer beliebigen Stelle angewendet werden, über die Infrastruktur Ihres virtuellen Netzwerks, VM-zu-VM-Datenverkehr, Datenverkehr für virtuelle Computer-zu-Host oder virtuellen Computer mit dem Internet-Datenverkehr zu isolieren, bei Bedarf – entweder für einzelne Systeme, die möglicherweise gefährdet ist oder programmgesteuert über mehrere Subnetze. Windows Server 2016-Software-defined networking-Funktionen ermöglichen auch, weitergeleitet oder widerspiegeln eingehenden Datenverkehr an virtuelle Geräte nicht von Microsoft. Sie können z. B. alle Ihre e-Mail-Verkehr über eines virtuellen Barracuda-Geräts für zusätzliche spamfilterungs-Schutz gesendet. Dadurch können Sie problemlos Ebene in der Erhöhung der Sicherheit sowohl lokal oder in der Cloud.

### <a name="other-gdpr-considerations-for-servers"></a>Weitere Überlegungen DSGVO für Server
Die DSGVO enthält explizite Anforderungen für Breach Notification, in denen eine Verletzung der personenbezogenen Daten bedeutet, dass "_eine Verletzung der Sicherheit, was die versehentliche oder nicht illegale Zerstörung, Verlust, Änderung, nicht autorisierter Offenlegung von oder den Zugriff auf, Personal Daten übertragen, gespeichert oder anderweitig verarbeitet._ "  Natürlich kann nicht Beginn vorwärts bewegen, um den strengen Anforderungen DSGVO-Benachrichtigung an, wenn Sie die im vornherein Erkennung der sicherheitsverletzung können nicht innerhalb von 72 Stunden zu erfüllen.

Wie in der Windows-Security-Center-Whitepaper, erwähnt [nach einer Sicherheitsverletzung: Umgang mit komplexen Bedrohungen](http://wincom.blob.core.windows.net/documents/Post_Breach_Dealing_with_Advanced_Threats_Whitepaper.pdf)

> "_Im Gegensatz zur vor sicherheitsverletzung nach einer sicherheitsverletzung nimmt eine Verletzung bereits durchgeführt wurden – als Flight Recorder und Crime Szene Prüfer (CSI) fungiert. Nach einer sicherheitsverletzung Sicherheitsteams stellt die Informationen bereit und Toolset erforderlich zu erkennen, untersuchen und reagieren auf Angriffe, die andernfalls unentdeckt bleiben und unter dem Netz entfernt._ "

In diesem Abschnitt betrachten wir wie Windows Server die DSGVO Breach Notification Verpflichtungen erfüllen können. Dies beginnt mit Grundlegendes zu den zugrunde liegenden Threat-Daten an Microsoft, die gesammelt und analysiert, die für Ihr Angebot zur Verfügung und Informationen über Windows Defender Advanced Threat Protection (ATP), diese Daten für Sie wichtig sein können.

#### <a name="insightful-security-diagnostic-data"></a>Aufschlussreiche Sicherheitsdiagnosedaten
Seit fast zwei Jahrzehnten hat Microsoft Bedrohungen nützliche Informationen in aktiviert wurde, die helfen können, verstärken Sie ihre Plattform aus, und Kunden zu schützen. Dank der großen Computing-Vorteile von heute durch die Cloud, finden wir neue Verwendungsmöglichkeiten für unsere umfangreiche Analysemodule, die von der Bedrohungserkennung verursacht und zum Schutz unserer Kunden sind.

Durch das Anwenden einer Kombination von automatisierten und manuellen Prozessen, Machine Learning und menschlichen Experten, können wir ein intelligentes Security-Diagramm erstellen, das von sich selbst lernt und sich in Echtzeit weiter entwickelt, um neue Bedrohungen für unsere Produkte zu erkennen und darauf zu reagieren.

![Microsoft Intelligence Security Graph](../media/GDPR-Windows-Server-Overview/gdpr-intelligent-security-graph.png)

Im Rahmen von Microsoft Threat Intelligence umfasst buchstäblich Milliarden von Datenpunkten an: 35 Milliarden Nachrichten überprüft monatlich, 1 Milliarde Kunden in Unternehmens- und endbenutzeranwendungen Segmente, die Zugriff auf 200 Clouddienste und 14 Milliarden Authentifizierungen täglich ausgeführt. Alle diese Daten ist zusammengestellt in Ihrem Auftrag von Microsoft Intelligent Security Graph zu erstellen, mit denen Sie Ihr Zugriff auf dynamische Weise sorgen Sie für Sicherheit, produktiv bleiben und erfüllen die Anforderungen der dsgvo werden geteilt zu schützen.

#### <a name="detecting-attacks-and-forensic-investigation"></a>Erkennen von Angriffen und forensische Untersuchung
Auch die besten Endpoint-Schutzmaßnahmen können irgendwann überwunden werden, da Cyberangriffe mehr ausgefeilt und zielgerichtet sind. Zwei Funktionen können verwendet werden, um potenzielle sicherheitsverletzung Erkennung – Windows Defender Advanced Threat Protection (ATP) und Microsoft Advanced Threat Analytics (ATA) zu unterstützen.

Windows Defender Advanced Threat Protection (ATP) hilft Ihnen, fortgeschrittene Angriffe zu erkennen und untersuchen und auf Datenschutzverletzungen im Netzwerk zu reagieren. Die Typen von datenschutzverletzungen erwartet, dass die DSGVO Sie über technische Sicherheitsmaßnahmen, um sicherzustellen, dass die laufende Vertraulichkeit, Integrität und Verfügbarkeit von persönlichen Daten und Systeme zur Verarbeitung von Schutz.

Sind Sie zu den Hauptvorteilen von Windows Defender ATP die folgenden Schritte aus:

- **Erkennen, der nicht erkennbaren.** Sensoren, die tief in die Betriebssystem-Kernel, Windows-Sicherheitsexperten und eindeutige Speicherverfahrens von über 1 Milliarde Computer und Signale für alle Microsoft-Dienste erstellt werden.

- **Integrierte, nicht angepasst.** Ohne Agents, mit hoher Leistung und die minimale Auswirkungen, die mithilfe der Cloud; einfache Verwaltung ohne Bereitstellung. 

- **Zentrale Konsole für die Windows-Sicherheit.** Untersuchen der letzten sechs Monate umfassender, Computer-Zeitachse Vereinheitlichung Sicherheitsereignisse von Windows Defender ATP, Windows Defender Antivirus und Windows Defender Device Guard.

- **Die Leistungsfähigkeit von Microsoft Graph.** Nutzt Microsoft Intelligence Security Graph zum Integrieren von Erkennung und Untersuchung in ATP für Office 365-Abonnement, das wieder nachverfolgen und reagieren auf Angriffe.

Weitere Informationen finden Sie unter [Neuigkeiten im Windows Defender ATP Creators Update – Vorschau](https://blogs.microsoft.com/microsoftsecure/2017/03/13/whats-new-in-the-windows-defender-atp-creators-update-preview/).

ATA ist ein lokales Produkt, das hilft bei der Erkennung von Identitätsdiebstahl in einer Organisation. ATA kann erfassen und Analysieren von Netzwerkdatenverkehr für die Authentifizierung, Autorisierung und zum Sammeln von Protokollen (z. B. Kerberos, DNS, RPC, NTLM und andere Protokolle). ATA verwendet diese Daten, um ein Verhaltensprofil zu Benutzern und anderen Personen in einem Netzwerk zu erstellen, sodass Anomalien und bekannten Angriffsmustern erkannt werden können. Die folgende Tabelle enthält die Angriffstypen, die von ATA erkannt werden.


|Angriffstyp |Beschreibung |
|---------|---------|
|Böswillige Angriffe |Diese Angriffe werden erkannt, durch Angriffe aus einer Liste bekannter Angriffstypen, einschließlich suchen:<ul><li>Pass-the-Ticket (PtT)</li><li>Pass-the-Hash (PtH)</li><li>Overpass-the-Hash</li><li>Gefälschte PAC (MS14-068)</li><li>Golden Ticket</li><li>Böswillige Replikationen</li><li>Erkundung</li><li>Brute-force</li><li>Remoteausführung</li></ul>Eine vollständige Liste der böswilligen Angriffen, die erkannt werden können und die entsprechenden Beschreibungen, finden Sie unter [was verdächtigen Aktivitäten kann ATA erkennen?](https://docs.microsoft.com/advanced-threat-analytics/understand-explore/ata-threats).|
|Ungewöhnliches Verhalten |Diese Angriffe werden von mithilfe der Verhaltensanalyse erkannt und anhand von Machine learning, um verdächtige Aktivitäten, einschließlich zu identifizieren:<ul><li>Anomale Anmeldungen</li><li>Unbekannte Gefahren</li><li>Kennwortfreigabe</li><li>Lateral-movement</li></ul>|
|Sicherheitsprobleme und-Risiken |Diese Angriffe werden erkannt, durch Betrachten der aktuellen Netzwerk- und Systemkonfiguration, einschließlich:<ul><li>Fehlerhafte Vertrauensstellung</li><li>Schwacher Protokolle</li><li>Bekannter protokollschwachstellen.</li></ul>|

Sie können ATA verwenden, um privilegierte Identitäten Gefährdung von Angreifern zu erkennen. Weitere Informationen zum Bereitstellen von ATA finden Sie unter den Themen Planung und Bereitstellung, in der [Advanced Threat Analytics-Dokumentation](https://docs.microsoft.com/advanced-threat-analytics/).

## <a name="related-content-for-associated-windows-server-2016-solutions"></a>Verwandte Inhalte für die zugehörigen Windows Server 2016-Lösungen

- **Windows Defender Antivirus:** https://www.youtube.com/watch?v=P1aNEy09NaI und https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10

- **Windows Defender Advanced Threat Protection:** https://www.youtube.com/watch?v=qxeGa3pxIwg und https://docs.microsoft.com/windows/threat-protection/windows-defender-atp/configure-server-endpoints-windows-defender-advanced-threat-protection

- **Windows Defender Device Guard:** https://www.youtube.com/watch?v=F-pTkesjkhI und https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide

- **Windows Defender Credential Guard:** https://www.youtube.com/watch?v=F-pTkesjkhI und https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard

- **Ablaufsteuerungsschutz:** https://msdn.microsoft.com/library/windows/desktop/mt637065(v=vs.85).aspx

- **Sicherheit und Zusicherungen:** https://docs.microsoft.com/windows-server/security/security-and-assurance

## <a name="disclaimer"></a>Haftungsausschluss
Dieser Artikel enthält einen Kommentar über die GDPR wie Microsoft ihn ab dem Datum der Veröffentlichung interpretiert. Wir haben sehr viel Zeit mit der GDPR verbracht und wir glauben, dass wir über ihre Absicht und Bedeutung im Klaren sind und diese so dargestellt haben. Die Anwendung der GDPR ist jedoch äußerst tatsachenspezifisch, und die Aspekte und Interpretationen der GDPR sind nicht definitiv beigelegt.

Daher dient dieser Artikel nur zu Informationszwecken und sollte nicht zuverlässig als rechtlicher Hinweise angesehen werden oder um zu bestimmen, wie die GDPR für Sie und Ihr Unternehmen angewendet wird. Wir empfehlen Ihnen, die mit einem gesetzlich qualifizierten Experten zusammen zu arbeiten, um die GDPR zu besprechen, wie sie speziell für Ihre Organisation angewendet wird und wie sie am besten funktioniert, um Kompatibilität zu gewährleisten.

MICROSOFT GIBT IN BEZUG AUF DIE INFORMATIONEN IN DIESEM ARTIKEL KEINERLEI GEWÄHRLEISTUNG, WEDER AUSDRÜCKLICH NOCH KONKLUDENT. Dieser Artikel wird auf "as-is"-Basis bereitgestellt. Die in diesem Artikel gegebenen Informationen und Ansichten, darunter URLs und andere Verweise auf Internetseiten, können ohne vorherige Ankündigung geändert werden.

Dieser Artikel stellt Ihnen keinerlei Rechte am geistigen Eigentum eines beliebigen Microsoft-Produkts zur Verfügung.  Dieser Artikel darf nur für interne Zwecke kopiert und verwendet werden.  

Veröffentlicht: September 2017<br>
Version 1.0<br>
© 2017 Microsoft. Alle Rechte vorbehalten.


