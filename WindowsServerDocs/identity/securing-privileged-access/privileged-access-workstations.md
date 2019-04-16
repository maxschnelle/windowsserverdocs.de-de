---
title: Arbeitsstationen mit privilegiertem Zugriff
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93589778-3907-4410-8ed5-e7b6db406513
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/09/2016
ms.openlocfilehash: ce64974d771a11ef11257bceef1c3fde1797a7da
ms.sourcegitcommit: 3bf47cf4e25896725137d983d63b8041a53cb9a2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="privileged-access-workstations"></a>Arbeitsstationen mit privilegiertem Zugriff

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Arbeitsstationen mit privilegiertem Zugriff (PAWs) Geben Sie ein dediziertes Betriebssystem für sensible Aufgaben, die gegen Angriffe aus dem Internet und Übertragung von Bedrohungen geschützt ist. Verwenden Sie Trennung dieser sensiblen Aufgaben und Konten aus den täglichen Arbeitsstationen und Geräte bietet sehr starken Schutz vor Phishing-Angriffe, Anwendung und Betriebssystem Sicherheitslücken, Angriffen durch identitätsvortäuschung und Methoden des Anmeldeinformationsdiebstahls z.B. Protokollierung von Tastatureingaben, [Pass-the-Hash](https://www.microsoft.com/en-us/download/details.aspx?id=36036), und [Pass-The-Ticket](https://download.microsoft.com/download/7/7/A/77ABC5BD-8320-41AF-863C-6ECFB10CB4B9/Mitigating%20Pass-the-Hash%20(PtH)%20Attacks%20and%20Other%20Credential%20Theft%20Techniques_English.pdf).

## <a name="architecture-overview"></a>Architektur (Übersicht)
Das folgende Diagramm zeigt einen separaten "Kanal" für die Verwaltung (eine höchst sensible Aufgabe), die durch Einrichten getrennter dedizierter Konten und Arbeitsstationen.

![Das Diagramm zeigt einen separaten "Kanal" für die Verwaltung (eine höchst sensible Aufgabe), die durch Einrichten getrennter dedizierter Konten und Arbeitsstationen](../media/privileged-access-workstations/PAWFig1.JPG)

Diese Architektur basiert auf den Schutzmaßnahmen in Windows10 [Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx) und [Device Guard](https://technet.microsoft.com/en-us/library/dn986865(v=vs.85).aspx) verfügt und diese Schutzmaßnahmen für sensible Konten und Aufgaben weit.

Diese Methode eignet sich für Konten mit Zugriff auf hochwertige Ressourcen:

-   **Administratorrechte** die PAWs bieten erhöhte Sicherheit für weitreichenden IT-Rollen und Aufgaben. Diese Architektur kann auf viele Arten von Systemen, einschließlich Active Directory-Domänen und Gesamtstrukturen, angewendet werden Microsoft Azure Active Directory-Mandanten, Office365-Mandanten, Prozess Steuerelement Netzwerke (PCN), Pcns Kontrolle und Data Acquisition SCADA-Systeme, Geldautomaten (Geldautomaten) und Point of Sale (PoS)-Geräte.

-   **Hohe Empfindlichkeit Information-Worker** der Ansatz paws bieten auch Schutz für vertrauliche Informationen und Mitarbeiter vor Ankündigung Unternehmensfusion Aktivität, pre-Release-Finanzberichte, Organisationseinheit in sozialen Medien, Kommunikation der Geschäftsleitung, noch nicht patentierte Geschäftsgeheimnisse, vertrauliche Recherchen oder andere vertrauliche oder sensiblen Daten in Zusammenhang mit. Diese Anleitung erläutert die Konfiguration der diese Information-Worker-Szenarien im Detail oder auch wird das Szenario in den technischen Anweisungen nicht.

    > [!NOTE]
    > Microsoft-IT-Abteilung verwendet PAWs (intern als "sichere Arbeitsstationen für Administratoren" oder SAWs bezeichnet) zum Verwalten von sicheren Zugriffs auf interne wichtigen Systemen in Microsoft. Dieser Leitfaden wurde zusätzliche Detail unten auf der PAW-Nutzung bei Microsoft im Abschnitt "Wie Microsoft Arbeitsstationen für Administratoren verwendet". Ausführlichere Informationen zu diesem Ansatz für hochwertige Element-Umgebung finden Sie im Artikel [Schützen von wertvollen Assets mit sicheren Arbeitsstationen](https://msdn.microsoft.com/en-us/library/mt186538.aspx).

In diesem Dokument wird beschrieben, warum diese Vorgehensweise für den Schutz von Konten mit weitreichenden Berechtigungen empfohlen wird, wie diese PAW-Lösungen aussehen, für den Schutz von Administratorrechten, und wie Sie schnell eine PAW-Lösung für die Verwaltung von Domänen- und Cloud-Dienste bereitstellen.

Dieses Dokument bietet eine detaillierte Anleitung für die Implementierung von mehreren PAW-Konfigurationen und bietet detaillierte implementierungsanweisungen, um Ihnen den Einstieg für den Schutz von Konten mit weitreichenden:

-   **Phase 1: sofortige Bereitstellung für Active Directory-Administratoren** Dies bietet eine PAW schnell, die auf lokalen Domänen- und Verwaltungsfunktionen schützen kann

-   **Phase 2: Erweitern des PAW auf alle Administratoren** dadurch Schutz für Administratoren von Cloud-Diensten wie Office365 und Azure, Unternehmensservern, unternehmensanwendungen und Arbeitsstationen

-   **Phase 3: Erweiterte PAW-Sicherheit** dies zusätzliche Schutzmaßnahmen und Überlegungen zur Sicherheit von PAWS erläutert

### <a name="why-a-dedicated-workstation"></a>Warum eine dedizierte Arbeitsstation?
Die aktuelle Umgebung der Bedrohung für Organisationen ist voller ausgefeilte und andere Angriffe aus dem Internet, die fortlaufende Sicherheitsrisiko für das Internet verfügbar gemacht werden Konten und Arbeitsstationen zu erstellen.

Dieser Bedrohungen müssen Organisationen eine Sicherheitsniveau "sicherheitsverletzungen" beim Entwerfen von Schutzmaßnahmen für wertvolle Assets wie Administratorkonten und sensible Unternehmensressourcen übernehmen. Diese wertvollen Assets mit sowohl direkten Bedrohungen aus dem Internet als auch vor Angriffen geschützt werden müssen über andere Arbeitsstationen, Servern und Geräten in der Umgebung bereitgestellt.

![Diese Abbildungzeigt das Risiko für verwaltete Assets, wenn ein Angreifer die Kontrolle über eine Benutzerarbeitsstation erhält, in denen vertrauliche Anmeldeinformationen verwendet werden](../media/privileged-access-workstations/PAWFig2.JPG)

Diese Abbildungzeigt das Risiko für verwaltete Assets, wenn ein Angreifer die Kontrolle über eine Benutzerarbeitsstation erhält, in denen vertrauliche Anmeldeinformationen verwendet werden.

Eine Angreifer Kontrolle über ein Betriebssystem verfügt über zahlreiche Möglichkeiten offen, unerlaubt Zugriff auf alle Aktivitäten auf der Arbeitsstation und die Identität des legitimen Kontos. Eine Vielzahl von bekannten und unbekannten Angriffstechniken kann verwendet werden, um diese Zugriffsebene zu erhalten. Die und ausgefeilter von Cyberangriffe haben Konzept der Trennung Clientbetriebssysteme für sensible Konten vollständig getrennten erweitern vorgenommen. Weitere Informationen zu diesen Arten von Angriffen finden Sie auf der [Pass The Hash Website](https://www.microsoft.com/pth) Whitepapers, Videos und vieles mehr.

Der PAW-Ansatz ist eine Erweiterung der etablierten empfohlen für Administratoren getrennte Administrator- und Benutzerkonten verwenden. Hier kommt ein individuell zugewiesenes Administratorkonto an, das vollständig vom Standardbenutzerkonto des Benutzers getrennt ist. PAW baut auf dieser Praxis für solche sensiblen Konten eine vertrauenswürdige Arbeitsstation bereitstellen.

> [!NOTE]
> Microsoft-IT-Abteilung verwendet PAWs (intern als "sichere Arbeitsstationen für Administratoren" oder SAWs bezeichnet) zum Verwalten von sicheren Zugriffs auf interne wichtigen Systemen in Microsoft.  Dieser Leitfaden wurde zusätzliche Detail auf der PAW-Nutzung bei Microsoft im Abschnitt "Wie Microsoft Arbeitsstationen für Administratoren verwendet"
>
> Ausführlichere Informationen zu diesem Ansatz für hochwertige Element-Umgebung finden Sie in Artikel [Schützen von wertvollen Assets mit sicheren Arbeitsstationen](https://msdn.microsoft.com/en-us/library/mt186538.aspx).

Dieser PAW-Leitfaden soll diese Funktion für den Schutz von wertvolle Konten wie z.B. hoher Berechtigung IT-Administratoren und hochsensible Geschäftskonten implementieren. Der Leitfaden unterstützt Sie:

-   Einschränken der Offenlegung von Anmeldeinformationen auf vertrauenswürdige Hosts.

-   Bereitstellen einer Arbeitsstation mit hoher Sicherheit für Administratoren, damit sie leicht administrative Aufgaben ausführen können.

Beschränken sensiblen Konten ausschließlich auf gesicherten PAWs mit ist eine einfache Schutz für diese Konten, der für Administratoren sicherstellen und eine solide, bezwingen sehr schwierig ist.

#### <a name="alternate-approaches---limitations-considerations-and-integration"></a>Alternative Ansätze: Einschränkungen, Überlegungen und Integration
Dieser Abschnittenthält Informationen wie die Sicherheit alternativer Ansätze im Vergleich zu PAWS und wie diese Ansätze innerhalb einer PAW-Architektur ordnungsgemäß integriert. All diese Ansätze erhebliches Risiko dar, wenn Sie isoliert implementiert haben, jedoch können Wert zu einer PAW-Implementierung in einigen Szenarien hinzufügen.

**Credential Guard und Microsoft Passport**

Windows10 eingeführte [Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx) Hardware- und virtualisierungsbasierte Sicherheit verwendet, um häufige Methoden des Anmeldeinformationsdiebstahls, wie z.B. Pass-the-Hash, durch Schützen der abgeleiteten Anmeldeinformationen zu verringern. Der private Schlüssel für Anmeldeinformationen durch [Microsoft Passport](http://aka.ms/passport) kann auch von der Hardware für Trusted Platform Module (TPM) geschützt werden.

Dies sind leistungsstarke Schutzmaßnahmen, aber Arbeitsstationen können immer noch anfällig für bestimmte Angriffe sein, auch wenn die Anmeldeinformationen durch Credential Guard oder Passport geschützt sind. Angriffen zählen der Missbrauch von Berechtigungen und die Verwendung von Anmeldeinformationen direkt von einem manipulierten Gerät, vor der Aktivierung von Credential Guard gestohlene Anmeldeinformationen sowie der Missbrauch von Management Verwaltungstools und schwachen Anwendungskonfigurationen auf der Arbeitsstation.

Anleitungen für PAWS in diesem Abschnittenthält die Verwendung einer Vielzahl dieser Technologien für hochsensible Konten und Aufgaben.

**Verwaltung virtueller Computer**

Ein administrativer virtuellen Computer (VM) ist ein dediziertes Betriebssystem für administrative Aufgaben auf einem standardbenutzerdesktop gehostet. Während dieser Ansatz bei der Bereitstellung ein dediziertes Betriebssystem für administrative Aufgaben PAW vergleichbar ist, hat es einen schwerwiegenden Fehler, da die virtuellen vom standardbenutzerdesktop für ihre Sicherheit abhängig ist.

Das folgende Diagramm zeigt die Fähigkeit von Angreifern, die auf das Zielobjekt Orte mit einer Admin-VM auf einer Benutzerarbeitsstation folgen und dass er schwierig, einen Pfad in der umgekehrten Konfiguration zu erstellen.

Die PAW-Architektur ist nicht zulässig, für das Hosten von auf der Arbeitsstation eines Benutzers, jedoch kann ein virtueller Benutzercomputer mit einem standardmäßigen Unternehmensimage gehostet werden, auf einer PAW-Host, um Mitarbeitern einen einzigen PC für alle Aufgaben bereitzustellen.

![Diagramm der PAW-Architektur](../media/privileged-access-workstations/PAWFig9.JPG)

**Sprungbrettserver**

Administrative "springen" zielserverarchitektur richten Sie eine kleine Anzahl Verwaltungskonsole Server und nur von bestimmten Mitarbeitern für Verwaltungsaufgaben verwendet werden. Dies basiert üblicherweise auf Remotedesktopdiensten, einer Präsentation 3rd Party-Virtualisierungslösung oder eine Virtual Desktop Infrastructure (VDI)-Technologie.

Dieser Ansatz wird häufig zum verwaltungsrisiken vorgeschlagen und bietet einige Sicherheitsmaßnahmen, aber der Sprungliste Server Ansatz selbst ist anfällig für bestimmte Angriffe, da es gegen die [Prinzip der "vertrauenswürdigen Quelle"](http://aka.ms/cleansource). Das Prinzip der vertrauenswürdigen Quelle muss alle sicherheitsabhängigkeiten weniger vertrauenswürdig als das Objekt, das gesichert werden.

![Diese Abbildungzeigt eine einfache kontrollbeziehung](../media/privileged-access-workstations/PAWFig3.JPG)

Diese Abbildungzeigt eine einfache kontrollbeziehung. Jedes Subjekt, das in ein Objekt ist eine sicherheitsabhängigkeit dieses Objekts. Wenn ein Angreifer eine sicherheitsabhängigkeit eines Zielobjekts (ein Subjekt) steuern kann, können sie dieses Objekt steuern.

Die verwaltungssitzung auf dem sprungbrettserver stützt sich auf die Integrität des lokalen Computers darauf zugreifen kann. Wenn dieser Computer eine Arbeitsstation Phishing-Angriffen und anderen internetbasierten Angriffsmethoden ist, wird die verwaltungssitzung auch verwaltungssitzung diesen Risiken ausgesetzt.

![Diese Abbildungzeigt, wie Angreifer einer eingerichteten auf das Zielobjekt folgen können](../media/privileged-access-workstations/PAWFig4.JPG)

Die obige Abbildungzeigt, wie Angreifer einer eingerichteten auf das Zielobjekt folgen können.

Während einige erweiterte Sicherheitsmaßnahmen wie mehrstufige Authentifizierung ist schwierig, ein Angreifer, der Übernahme dieser administrativen Sitzung von der Arbeitsstation des Benutzers, keine Sicherheitsfunktion erhöhen kann vollständig vor technischen Angriffen, wenn ein Angreifer schützen können, verfügt über Verwaltungszugriff auf dem Quell-PC (z.B. durch Eingabe unerlaubter Befehle in einer genehmigten Sitzung, durch Übernahme legitimer Prozesse usw..)

Die Standardkonfiguration in diesem PAW-Leitfaden installiert Verwaltungstools auf der PAW, jedoch kann bei Bedarf auch eine sprungbrettserverarchitektur hinzugefügt.

![Diese Abbildungzeigt, wie Umkehren der kontrollbeziehung und Zugreifen auf Benutzer-Apps auf einer Administratorarbeitsstation dem Angreifer das Zielobjekt erreichen können](../media/privileged-access-workstations/PAWFig5.JPG)

Die folgende Abbildungzeigt, wie Umkehren der kontrollbeziehung und Zugreifen auf Benutzer-Apps auf einer Administratorarbeitsstation dem Angreifer das Zielobjekt erreichen können. Der Benutzer sprungbrettserver wird weiterhin Risiken verfügbar gemacht, damit geeignete Kontrollmechanismen, sprungserver und Antwort-Prozessen für diesen Computer dem Internet verbundene weiterhin angewendet werden soll.

Diese Konfiguration muss Administratoren festgelegte Vorgehensweisen genau, um sicherzustellen, dass sie versehentlich Administratoranmeldeinformationen in die Benutzersitzung auf dem Desktop nicht eingeben.

![Diese Abbildungzeigt, wie den Zugriff auf einen administrativen sprungbrettserver über eine paw erfolgt keine der Angreifer an die verwaltungsassets zu](../media/privileged-access-workstations/PAWFig6.JPG)

Die folgende Abbildungzeigt, wie den Zugriff auf einen administrativen sprungbrettserver über eine paw erfolgt keine der Angreifer an die verwaltungsassets zu. Ein sprungbrettserver mit einer PAW kann in diesem Fall die Anzahl von Speicherorten für die Überwachung von Verwaltungsaktivitäten und Verteilung von Verwaltungsanwendungen und -Tools konsolidieren. Dieser Entwurf erhöht die Komplexität, jedoch kann Sicherheitsupdates Überwachung und Software vereinfachen, wenn eine große Anzahl von Konten und Arbeitsstationen in Ihre PAW-Implementierung verwendet werden. Der sprungbrettserver müssten erstellt und an den gleichen Sicherheitsstandards wie die PAW konfiguriert werden.

**Die Berechtigungsverwaltung**

Für die berechtigungsverwaltung sind Anwendungen, die bei Bedarf temporären Zugriff auf einzelne Berechtigungen oder privilegierte Konten bereitstellen. Die berechtigungsverwaltung sind eine sehr wertvolle Komponente einer umfassenden Strategie zur Sicherung des privilegierten Zugriffs und Transparenz und Verantwortlichkeit für administrative Aktivität.

Diese Lösungen nutzen üblicherweise einen flexiblen Workflow zum Gewähren von Zugriff und verfügen über zahlreiche weitere Sicherheitsfeatures und -Funktionen wie die kennwortverwaltung für Dienstkonten und die Integration mit administrativen sprungbrettservern. Es gibt viele Lösungen auf dem Markt, die Berechtigung Verwaltungsfunktionen bereitstellen, von denen Microsoft Identity Manager (MIM) privileged Access Management (PAM) ist.

Microsoft empfiehlt die Verwendung einer PAWS für den Zugriff für die berechtigungsverwaltung. Zugriff auf solche Lösungen sollte nur für PAWs gewährt werden. Microsoft empfiehlt nicht, diese Lösungen als Ersatz für eine PAW verwenden, da der Zugriff auf Berechtigungen von einem potenziell gefährdeten Benutzerdesktop gegen die [Quelle](http://aka.ms/cleansource) Grundsatz wie im folgenden Diagramm dargestellt:

![Das Diagramm zeigt, wie Microsoft nicht empfiehlt diese Lösungen als Ersatz für eine PAW verwenden, da das Prinzip der vertrauenswürdigen Quelle Zugriff auf Berechtigungen von einem potenziell gefährdeten Benutzerdesktop verletzt werden.](../media/privileged-access-workstations/PAWFig7.JPG)

Bereitstellung einer PAW für den Zugriff auf diese Lösungen können Sie die Sicherheitsvorteile der PAW und der Lösung für die berechtigungsverwaltung, zu erhalten, wie in diesem Diagramm dargestellt:

![Das Diagramm zeigt, wie Sie die Sicherheit der PAW und der Lösung für die berechtigungsverwaltung profitieren kann Bereitstellung einer PAW für den Zugriff auf diese Lösungen](../media/privileged-access-workstations/PAWFig8.JPG)

> [!NOTE]
> Diese Systeme sollten auf die höchste Ebene der Berechtigung eingestuft werden, die Sie verwalten, und mindestens auf dieser Ebene geschützt werden. Diese werden häufig zum Verwalten von Ebene-0-Lösungen und Assets der Ebene 0 konfiguriert und auf Ebene 0 klassifiziert werden soll.
> Weitere Informationen auf das Ebenenmodell finden Sie unter [http://aka.ms/tiermodel](http://aka.ms/tiermodel) finden Sie weitere Informationen zu Gruppen auf Ebene 0, Äquivalenz zur Ebene 0 in [Schützen des privilegierten Zugriffs – Referenzmaterial](../securing-privileged-access/securing-privileged-access-reference-material.md).

Weitere Informationen zum Bereitstellen von Microsoft Identity Manager (MIM) privileged Access Management (PAM) finden Sie unter [http://aka.ms/mimpamdeploy](http://aka.ms/mimpamdeploy)

#### <a name="how-microsoft-is-using-admin-workstations"></a>Wie verwendet Microsoft Arbeitsstationen für Administratoren
Microsoft verwendet die PAW-Architektur-Ansatz, sowohl intern auf unserer Systeme und unserer Kunden. Microsoft verwendet Arbeitsstationen für Administratoren intern in einer Reihe von Kapazität, einschließlich der Verwaltung von Microsoft-IT-Infrastruktur, Microsoft Entwicklung und den Betrieb und weitere wertvolle Assets.

Dieser Leitfaden basiert direkt auf der Privileged Access Workstation PAW-Referenzarchitektur bereitgestellt, die von unseren Expertenteams für cybersicherheit um Kunden vor Cyberangriffen zu schützen. Die Arbeitsstationen für Administratoren sind auch ein wichtiges Element der stärksten Schutzfunktion für Verwaltungsaufgaben bei Domäne und der administrativen Gesamtstruktur-Referenzarchitektur Enhanced Security Administrative Environment (ESAE).

Weitere Informationen auf der ESAE-verwaltungsgesamtstruktur finden Sie unter [Administrative ESAE-Gesamtstruktur Entwurfsansatz](http://aka.ms/ESAE) im Abschnitt [Schützen des privilegierten Zugriffs – Referenzmaterial](../securing-privileged-access/securing-privileged-access-reference-material.md).

Weitere Informationen zum beauftragen von Microsoft-Dienste für die Bereitstellung einer PAW- oder ESAE für Ihre Umgebung erhalten Sie von Ihrem Microsoft-Vertriebsmitarbeiter oder [auf dieser Seite](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

### <a name="what-is-a-privileged-access-workstation-paw"></a>Was ist eine Privileged Access Workstation (PAW)?
Vereinfacht ausgedrückt ist eine PAW eine gesicherte und gesperrte Arbeitsstation, die für die Verwendung mit hoher Sicherheit Garantien für sensible Konten und Aufgaben.  PAWs werden für die Verwaltung von Identitätssystemen, Cloud-Diensten und privaten cloudfabrics sowie vertrauliche Geschäftsfunktionen empfohlen.

> [!NOTE]
> Die PAW-Architektur ist eine 1:1-Zuordnung von Konten zu Arbeitsstation, obwohl dies eine häufige Konfiguration ist nicht erforderlich. PAW erstellt eine vertrauenswürdige arbeitsstationsumgebung, die von einem oder mehreren Konten verwendet werden kann.

Um die höchstmögliche Sicherheit zu bieten, PAWs sollten immer optimal auf dem neuesten Stand und sicher Betriebssystem ausgeführt verfügbar: empfiehlt Microsoft, Windows10 Enterprise, enthält zahlreiche weitere Sicherheitsfeatures, die in anderen Editionen nicht verfügbar (insbesondere [Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx) und [Device Guard](https://technet.microsoft.com/en-us/library/dn986865(v=vs.85).aspx)).

> [!NOTE]
> Organisationen ohne Zugriff auf Windows10 Enterprise können Windows10 Pro verwenden, die viele der wichtigen grundlegenden Technologien für PAWs, einschließlich der vertrauenswürdige Start, BitLocker und Remotedesktop enthält.  Kunden im Bildungsbereich können Windows10 Education verwenden.  Windows10 Home sollte nicht für eine PAW verwendet werden.
>
> Eine Vergleichsmatrix der verschiedenen Versionen von Windows10, finden Sie unter [in diesem Artikel](https://www.microsoft.com/en-us/WindowsForBusiness/Compare).

Die Sicherheitsmechanismen in PAW sind Eindämmen von den größten Auswirkungen zu wahrscheinlich Risiko der Gefährdung konzentriert. Dazu gehören Eindämmen von Angriffen auf die Umgebung und Eindämmen von Risiken, die die PAW-Steuerelemente mit der Zeit beeinträchtigt werden können:

-   **Angriffe aus dem Internet** -die meisten Angriffe stammen direkt oder indirekt aus Internetquellen und nutzen Sie das Internet zum Datendiebstahl und Befehl und Steuerelement (C2). Die Isolierung der PAW vom Internet ist ein wichtiges Element, um sicherzustellen, dass die PAW nicht gefährdet ist.

-   **Einsatzfähigkeit** -ist eine PAW zu schwierig für tägliche Aufgaben verwenden, Administratoren werden daran interessiert, die zum Erstellen von Problemumgehungen, um ihre Arbeit zu erleichtern. Diese Problemumgehungen Öffnen häufig die Arbeitsstationen für Administratoren und Konten zu erheblichen Sicherheitsrisiken ausgesetzt, damit es wichtig ist, und zu schulen, die PAW-Benutzer, um diese Probleme hinsichtlich der Verwendbarkeit sicher zu minimieren. Dies geschieht häufig durch Analysieren deren Feedback, das Installieren der Tools und Skripts, die zum Ausführen ihrer Aufgaben und sicherstellen, dass allen Administratoren erforderlichen kennen warum sie eine PAW, was eine PAW zu verwenden müssen ist, und wie Sie diese richtig und erfolgreich verwenden.

-   **Risiken durch die Umgebung** -da viele andere Computer und Konten in der Umgebung zu Internet Risiko Verzeichnis oder indirekt verfügbar gemacht werden, muss eine PAW vor Angriffen von kompromittierte Assets in der Produktionsumgebung geschützt werden. Dies ist erforderlich, begrenzen die Verwaltungstools und Konten, die Zugriff auf den PAWs auf das absolute Minimum zum Sichern und Überwachen dieser speziellen Arbeitsstationen erforderlich.

-   **Lieferkette** : Es ist unmöglich, entfernen alle mögliche Risiken der Manipulation der Lieferkette für Hardware und Software, einige wichtige Aktionen kritische Angriffsvektoren ergeben können, die Angreifer zugänglich sind. Hierzu gehört die Überprüfung der Integrität der sämtlicher Installationsmedien ([Prinzip der vertrauenswürdigen Quelle](http://aka.ms/cleansource)) und mit einem vertrauenswürdigen und seriösen Lieferanten für Hardware und Software.

-   **Physische Angriffe** -PAWs physisch mobile und außerhalb der physisch gesicherten Umgebung verwendet werden können, die sie vor Angriffen, die Nutzung von nicht autorisierten physischen Zugriff auf den Computer geschützt werden müssen.

> [!NOTE]
> Eine PAW wird eine Umgebung nicht vor einem Angreifer schützen, der bereits administrativen Zugriff über ein Active Directory-Gesamtstruktur erlangt hat.
> Da viele vorhandene Implementierungen der Active Directory Domain Services seit Jahren mit dem Risiko des Diebstahls von Anmeldeinformationen betrieben werden, sollten Organisationen ausgehen und die Möglichkeit, dass sie eine unerkannte Gefährdung der Domäne oder Organisationsadministrator möglicherweise berücksichtigen. Eine Organisation, die Gefährdung der Domäne vermutet, sollten die Verwendung von professionellen Incidents.
>
> Weitere Informationen zur Reaktion auf und Wiederherstellung finden Sie unter "Reaktion auf verdächtige Aktivitäten" und "Wiederherstellung nach einem Sicherheitsvorfall"-Abschnitte [Mitigating Pass-the-Hash and Other Credential Theft](https://www.microsoft.com/pth), Version 2.
>
> Besuchen Sie [Microsoft Vorfällen und Recovery Services](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx) um weitere Informationen zu erhalten.

### <a name="paw-hardware-profiles"></a>PAW-Hardwareprofile
Administratoren sind auch Standardbenutzer zu – sie benötigen also nicht nur eine PAW, sondern auch eine standardmäßige Benutzerarbeitsstation, E-Mails, Durchsuchen des Webs und Zugriff auf Unternehmensdaten Branchenanwendungen.  Um sicherzustellen, dass Administratoren produktive und sichere bleiben können ist für den Erfolg einer PAW-Bereitstellung unerlässlich.  Eine sichere Lösung, die Produktivität wird von den Benutzern durch einen abgebrochen werden die Produktivität verbessert (auch wenn es auf unsichere Weise erfolgt).

Um die Notwendigkeit der Sicherheit und Produktivität zu verteilen, empfiehlt Microsoft die Verwendung eines der folgenden PAW-Hardwareprofile:

-   **Dedizierte Hardware** -separate, dedizierte Geräte für Benutzeraufgaben und Verwaltungsaufgaben

-   **gleichzeitige Verwendung** -einzelne Geräte, die Benutzer und Verwaltungsaufgaben gleichzeitig ausführen können, durch die Nutzung des Betriebssystems oder einer Präsentation Virtualisierung.

Organisationen können nur eines der Profile oder beide verwenden. Es bestehen keine Interoperabilitätsprobleme zwischen den Hardwareprofilen, und Organisationen können die Flexibilität, das Hardwareprofil die besonderen Anforderungen und der Situation eines bestimmten Administrators entsprechen.

> [!NOTE]
> Es ist wichtig, dass in all diesen Szenarien administrative Mitarbeiter dürfen ein Standardbenutzerkonto ausgestellt werden, die getrennt von Administratorkonten festgelegt. Administratorkonten sollten nur unter dem administrativen Betriebssystem der PAW verwendet werden.

Diese Tabelle enthält eine Zusammenfassung der relativen Vorteile und Nachteile der einzelnen Hardwareprofile aus der Perspektive des operative erleichterte Bedienung und Produktivität und Sicherheit.  Beide Ansätze bieten eine hohe Sicherheit für Administratorkonten vor Diebstahl und Wiederverwendung.

|**Szenario**|**Vorteile**|**Nachteile**|
|--------|---------|-----------|
|Dedizierter Hardware|– Starkes Signal für die Vertraulichkeit von Aufgaben<br />– Strikteste Trennung zur Sicherheit|– Zusätzlicher Platzbedarf<br />– Höheres Gewicht (bei Remotearbeit)<br />-Hardware Kosten|
|Gleichzeitige Verwendung|– Geringere Hardwarekosten<br />– Nur Gerätefunktion|-Risiko unbeabsichtigter Fehler und Risiken erstellt Freigabe einzigen Tastatur und Maus|

Dieser Leitfaden enthält detaillierten Anweisungen für die PAW-Konfiguration für den Ansatz mit dedizierter Hardware. Besitzen Sie Anforderungen für die gleichzeitige Verwendung Hardwareprofile, können Sie passen Sie die Anweisungen auf der Grundlage dieser Leitfaden selbst oder einen professionellen Dienstleister wie Microsoft zur Unterstützung bei der es einstellen.

**Dedizierter Hardware**

In diesem Szenario wird eine PAW für die Verwaltung verwendet, die unabhängig von den PC für tägliche Aktivitäten wie E-Mail, dokumentbearbeitung und Entwicklung verwendet wird. Alle Verwaltungstools und -Anwendungen werden auf der PAW installiert, und alle produktivitätsanwendungen auf der standardarbeitsstation des Benutzers installiert sind. Die Schritt-für-Schritt-Anweisungen in diesem Leitfaden basieren auf diesem Hardwareprofil.

**Gleichzeitige Verwendung: Hinzufügen eines lokalen Benutzers VM**

In diesem Szenario der gleichzeitigen Verwendung wird ein einziger PC für sowohl für Verwaltungsaufgaben als auch für tägliche Aktivitäten wie E-Mail, dokumentbearbeitung und Entwicklung verwendet. In dieser Konfiguration Betriebssystem des Benutzers auch offline verfügbar (zum Bearbeiten von Dokumenten von und Arbeiten mit lokal zwischengespeicherten E-Mails), was allerdings Hardware und supportprozesse, die diese den Offlinezustand unterstützen können.

![Das Diagramm zeigt einzigen PC in einem Szenario der gleichzeitigen Verwendung sowohl für Verwaltungsaufgaben als auch für tägliche Aktivitäten zum wie E-Mail, dokumentbearbeitung und Entwicklung](../media/privileged-access-workstations/PAWFig10.JPG)

Die physische Hardware werden lokal zwei Betriebssysteme ausgeführt:

-   **Administratorbetriebssystem** -der physische Host führt Windows10 auf der PAW-Host für Verwaltungsaufgaben

-   **Benutzerbetriebssystem** -ein Windows10 Client Hyper-V-VM-Gast wird ein Unternehmensimage ausgeführt.

Mit Windows 10Hyper-V kann ein virtueller Gastcomputer (auch unter Windows10) eine umfassenden Benutzeroberfläche einschließlich Audio-, Video- und kommunikationsanwendungen z.B. Skype for Business Internet haben.

In dieser Konfiguration erfolgt tägliche Aufgaben, die keine Administratorrechte erfordert in der virtuellen Computer ein regulären Windows10-Unternehmensimage und unterliegen den PAW-Host zugewiesen ist. Alle administrativen Arbeit wird im administratorbetriebssystem ausgeführt.

Um dies zu konfigurieren, folgen Sie den Anweisungen in dieser Anleitung für den PAW-Host, fügen Sie Client Hyper-V-Features hinzu, erstellen Sie einen virtuellen Benutzercomputer und installieren Sie ein Windows10-Unternehmensimage auf dem virtuellen Benutzercomputer.

Lesen [Hyper-V für Clients](https://technet.microsoft.com/en-us/library/hh857623.aspx) Artikel Weitere Informationen zu dieser Funktion. Bitte beachten Sie, dass das Betriebssystem auf virtuellen Gastcomputern für die Lizenzierung pro müssen [Microsoft-Produktlizenzierung](https://www.microsoft.com/en-us/Licensing/product-licensing/products.aspx)auch beschriebenen [hier](https://www.microsoft.com/en-us/Licensing/learn-more/brief-windows-virtual-machine.aspx).

**Gleichzeitige Verwendung: Hinzufügen von RemoteApp, RDP oder einer VDI**

In diesem Szenario der gleichzeitigen Verwendung wird ein einziger PC für beide Verwaltungsaufgaben verwendet und tägliche Aktivitäten wie E-Mail, dokumentbearbeitung und Entwicklung eingesetzt. In dieser Konfiguration werden die Benutzer-Betriebssysteme werden zentral bereitgestellt und verwaltet (in der Cloud oder in Ihrem Rechenzentrum), jedoch nicht verfügbar, während die Verbindung getrennt.

![Die Abbildungzeigt einen einzigen PC in einem Szenario der gleichzeitigen Verwendung für beide Verwaltungsaufgaben verwendet und tägliche Aktivitäten wie E-Mail, dokumentbearbeitung und Entwicklung eingesetzt](../media/privileged-access-workstations/PAWFig11.JPG)

Die physische Hardware wird ein einzelnes PAW-Betriebssystem für administrative Aufgaben lokal ausgeführt und eine Verbindung mit einem Microsoft bzw. 3rd Party Remotedesktopdienst für benutzeranwendungen wie E-Mail, dokumentbearbeitung und Branchenanwendungen.

In dieser Konfiguration erfolgt tägliche Aufgaben, die keine Administratorrechte in den Remotebetriebssystemen und Anwendungen, die nicht unterliegen den PAW-Host zugewiesen werden. Alle administrativen Arbeit wird im administratorbetriebssystem ausgeführt.

Um dies zu konfigurieren, befolgen Sie die Anweisungen in dieser Anleitung für den PAW-Host, Netzwerkkonnektivität mit den Remotedesktopdiensten zulassen und dann Verknüpfungen zum Benutzerdesktop der PAW den Zugriff auf die Anwendungen hinzufügen. Die Remotedesktopdienste konnte in vielen u. a. gehostet werden:

-   Ein vorhandener Remotedesktop- oder VDI-Dienst (lokal oder in der Cloud)

-   Einen neuen Dienst, die Installation von lokalen oder in der Cloud

-   Azure RemoteApp unter Verwendung vorkonfigurierter Office365-Vorlagen oder Ihrer eigenen Installationsimages

Weitere Informationen zu Azure RemoteApp finden Sie auf [auf dieser Seite](https://www.remoteapp.windowsazure.com).

### <a name="paw-scenarios"></a>PAW-Szenarien
Dieser Abschnittenthält Richtlinien, die auf welche Szenarien dieser PAW-Leitfaden angewendet werden soll. In allen Szenarien sollten Administratoren Sie nur die PAWs für Supportaufgaben für Remotesysteme geschult werden. Um die erfolgreiche und sichere Nutzung zu unterstützen, sollte alle PAW-Benutzer werden ebenfalls gefördert werden anbieten, um Feedback für die PAWS zu verbessern und das Feedback für die Integration in Ihr PAW-Programm sorgfältig geprüft werden müssen.

In allen Szenarien können in späteren Phasen zusätzliche Sicherheitsmaßnahmen sowie verschiedene Hardwareprofile in dieser Anleitung verwendet werden, um die verwendbarkeits- oder Sicherheitsanforderungen der Rollen zu erfüllen.

> [!NOTE]
> Beachten Sie, dass diese Anleitung unterschieden zwischen dem erforderlichen Zugriff auf bestimmte Dienste im Internet (z.B. Azure und Office365-Verwaltungsportale) und dem "offenen Internet" für alle Hosts und -Dienste.

Weitere Informationen finden Sie unter der [Ebenenmodell](http://aka.ms/tiermodel) Weitere Informationen über die ebenenbezeichnungen.

|**Szenarien**|**Verwenden Sie die PAW?**|**Umfang und Überlegungen zur Sicherheit**|
|---------|--------|---------------------|
|Active Directory-Administratoren – Ebene 0|Ja|Eine Anleitung für Phase 1 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– Eine verwaltungsgesamtstruktur kann hinzugefügt werden, um den stärksten Schutz für dieses Szenario bereitzustellen. Weitere Informationen auf der ESAE-verwaltungsgesamtstruktur finden Sie unter [Administrative ESAE-Gesamtstruktur Entwurfsansatz](http://aka.ms/esae)<br />– Eine PAW kann für die Verwaltung von mehreren Domänen oder über mehrere Gesamtstrukturen verwendet werden.<br />– Wenn Domänencontroller in einer Infrastruktur als Service (IaaS) oder lokalen Virtualisierungslösung gehostet werden, sollten Sie priorisieren, Implementierung der PAWs für die Administratoren dieser Lösungen|
|Der Administrator des Azure IaaS und PaaS-Services - Ebene 0 oder Ebene 1 (Siehe Bereich und Überlegungen zum Entwurf)|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– PAWs sollten für mindestens verwendet werden der globale Administrator und Abonnementabrechnung Administrator. Sie sollten auch PAWs für delegierte Administratoren kritischer oder vertraulicher Server verwenden.<br />– PAWs sollten für die Verwaltung des Betriebssystems verwendet werden, und Anwendungen, die Verzeichnissynchronisierung sowie Identitätsverbund für Cloud-Dienste wie z.B. [Azure AD Connect](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect/) und Active Directory Federation Services (AD FS).<br />– Die Einschränkungen für ausgehenden Netzwerkdatenverkehr dürfen Verbindungen nur mit autorisierten Clouddiensten, gemäß Anleitung für Phase 2 zulassen. Kein offener Internetzugang sollten auf PAWs zugelassen werden.<br />– EMET sollte für alle auf der Arbeitsstation verwendeten Browser konfiguriert werden **Hinweis:** ein Abonnement wird als Ebene 0 für eine Gesamtstruktur sein, wenn sich Domänencontroller oder andere Hosts auf Ebene 0 im Abonnement befinden. Ein Abonnement ist Ebene 1, wenn keine Server der Ebene 0 in Azure gehostet werden|
|Verwalten von Office365-Mandanten <br />-Ebene 1|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– PAWs sollten für mindestens verwendet werden die Abonnementabrechnung Administrator, globaler Administrator, Exchange-Administrator, SharePoint-Administrator und Benutzer Management-Administratorrollen. Sie sollten auch unbedingt die Verwendung von PAWs für delegierte Administratoren höchst kritischer oder sensibler Daten erwägen.<br />– EMET sollte für alle auf der Arbeitsstation verwendeten Browser konfiguriert werden<br />– Die Einschränkungen für ausgehenden Netzwerkdatenverkehr dürfen Verbindungen nur mit Microsoft-Diensten, gemäß Anleitung für Phase 2 zulassen. Kein offener Internetzugang sollten auf PAWs zugelassen werden.|
|Anderer IaaS-der PaaS-Clouddienste<br />– Ebene 0 oder Ebene 1 (Siehe Bereich und Überlegungen zum Entwurf)||Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– PAWs sollten für alle Rollen verwendet werden, die über Administratorrechte verfügen über Cloud gehostete virtuelle Computer einschließlich der Möglichkeit Agents installieren, der Export von Festplattendateien oder Zugriff auf Speichersysteme, in der Festplattenlaufwerke mit Betriebssystemen, sensiblen Daten oder geschäftskritischen Daten gespeichert.<br />– Die Einschränkungen für ausgehenden Netzwerkdatenverkehr dürfen Verbindungen nur mit Microsoft-Diensten, gemäß Anleitung für Phase 2 zulassen. Kein offener Internetzugang sollten auf PAWs zugelassen werden.<br />– EMET sollte für alle auf der Arbeitsstation verwendeten Browser konfiguriert werden. **Hinweis:** ein Abonnement Ebene 0 für eine Gesamtstruktur ist, wenn sich Domänencontroller oder andere Hosts auf Ebene 0 im Abonnement befinden. Ein Abonnement ist Ebene 1, wenn keine Server der Ebene 0 in Azure gehostet werden.|
|Virtualization-Administratoren<br />– Ebene 0 oder Ebene 1 (Siehe Bereich und Überlegungen zum Entwurf)|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– PAWs sollten für alle Rollen verwendet werden, die über Administratorrechte verfügen über VMs einschließlich der Möglichkeit zum Installieren von Agents, der Export von virtuellen Festplattendateien oder Zugriff auf Speichersysteme, in der Festplattenlaufwerke mit Informationen zu Gastbetriebssystemen, sensiblen Daten oder geschäftskritischen Daten gespeichert. **Hinweis:** ein Virtualisierungssystem (und die zugehörigen Administratoren) gelten Ebene 0 für eine Gesamtstruktur, wenn sich Domänencontroller oder andere Hosts auf Ebene 0 im Abonnement befinden. Ein Abonnement ist Ebene 1, wenn keine Server der Ebene 0 im Virtualisierungssystem gehostet werden.|
|Die Serverwartung<br />-Ebene 1|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– Eine PAW sollte für Administratoren verwendet werden, die Aktualisierung, Patching und Problembehandlung von Unternehmensservern und -Apps unter Windows Server, Linux und anderen Betriebssystemen.<br />-Dedizierte Verwaltungstools müssen auf PAWs, um den größeren dieser Administratoren abzudecken.|
|Für Benutzerarbeitsstationen <br />-Ebene 2|Ja|Eine Anleitung für Phase 2 erstellte PAW ist für Rollen, die über Administratorrechte für den Endbenutzer-Geräte (z.B. Helpdesk und Deskside Rollen unterstützen) ausreichend.<br /><br />-Zusätzliche Anwendungen müssen möglicherweise auf den PAWs ticketmanagement und andere Supportfunktionen aktivieren installiert werden.<br />– EMET sollte für alle auf der Arbeitsstation verwendeten Browser konfiguriert werden.<br />    Möglicherweise müssen dedizierte Verwaltungstools auf PAWs, um den größeren dieser Administratoren abzudecken.|
|SQL-, SharePoint- oder Zeile der Branchen-Administrator<br />-Ebene 1||Eine Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />-Zusätzliche Verwaltungstools müssen auf den PAWs können Administratoren Anwendungen verwalten, ohne Verbindung mit Servern, die mithilfe von Remotedesktop installiert werden.|
|Benutzer in sozialen Medien verwalten|Teilweise|Eine gemäß der Anleitung für Phase 2 erstellte PAW kann als Ausgangspunkt zur Bereitstellung von Sicherheit für diese Rollen verwendet werden.<br /><br />– Schützen und Verwalten von Social-Media-Konten, die mithilfe von Azure Active Directory (AAD) für freigeben, schützen und Tracking-Zugriff auf Konten in sozialen.<br />    Weitere Informationen zu dieser Funktion finden Sie unter [in diesem Blogbeitrag](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx).<br />– Die Einschränkungen für ausgehenden Netzwerkdatenverkehr dürfen Verbindungen mit diesen Diensten zulassen. Dies kann erfolgen, indem Sie offene Internetverbindungen (sehr viel höheres Sicherheitsrisiko, das viele PAWS aushebelt) oder nur erforderliche DNS-Adressen für den Dienst (es kann schwierig sein, um zu erhalten) ermöglicht.|
|Standardbenutzer|Nein|Während viele Sicherheitsschritte für Standardbenutzer verwendet werden können, soll PAW Konten vom offenen Internetzugriff zu isolieren, die meisten Benutzer für Ihre täglichen Aufgaben benötigen.|
|Gast VDI/Kiosk|Nein|Während viele Sicherheitsschritte für ein kiosksystem für Gäste verwendet werden können, dient die PAW-Architektur zum Erhöhen der Sicherheit für hochsensible Konten, nicht erhöhen der Sicherheit für weniger vertrauliche Konten bereitzustellen.|
|VIP-Benutzer (Executive, Forschungsmitarbeiter usw.).|Teilweise|Eine Anleitung für Phase 2 erstellte PAW kann als Ausgangspunkt verwendet werden, zur Bereitstellung von Sicherheit für diese Rollen<br /><br />– Dieses Szenario ist vergleichbar mit einem standardmäßigen Benutzerdesktop, aber in der Regel ist ein kleiner, einfacher und bekanntes Anwendungsprofil. Dieses Szenario erfordert in der Regel erkennen und schützen sensible Daten, Dienste und Anwendungen (die möglicherweise nicht auf den Desktops installiert).<br />– Diese Rollen erfordern üblicherweise ein hohes Maß an Sicherheit und sehr hohes Maß an Benutzerfreundlichkeit, die erfordern Designänderungen vor, um die benutzeranforderungen zu erfüllen.|
|Industrielle Steuerungssysteme (z.B. SCADA, PCN und DCS)|Teilweise|Eine Anleitung für Phase 2 erstellte PAW kann verwendet werden als Ausgangspunkt zur Bereitstellung von Sicherheit für diese Rollen als die meisten ICS keine Konsolen (einschließlich solcher allgemeinen Standards wie SCADA und PCN) das offene Internet oder E-Mails erfordern.<br /><br />– Anwendungen für die Steuerung physischer Computer integriert und ihre Kompatibilität getestet und angemessen geschützt werden müssen|
|Embedded-Betriebssystem|Nein|Während viele Sicherheitsschritte für PAWS für integrierte Betriebssysteme verwendet werden können, muss eine benutzerdefinierte Lösung für die Härtung in diesem Szenario entwickelt werden.|

> [!NOTE]
> **kombinierte Szenarien** einige Mitarbeiter sind möglicherweise Verwaltungsaufgaben, die mehrere Szenarien umfassen.
> In diesen Fällen sind wichtigen Regeln zu beachten, dass jederzeit die Regeln befolgt werden müssen. Finden Sie weitere Informationen im Ebenenmodell.

> [!NOTE]
> **Skalieren des PAW-Programms** Ihr PAW-Programm skaliert, um weitere Administratoren und Rollen abzudecken, müssen Sie weiterhin sicherstellen, dass Sie zur Einhaltung der Sicherheits- und verwalten. Dies erfordert möglicherweise zum Aktualisieren Ihrer IT Strukturen unterstützen oder neue erstellen, um PAW-spezifische Herausforderungen wie etwa den onboardingprozess, Incident Management, Verwaltung, zu beheben und Sammeln von Feedback an Adresse Verwendbarkeit bewältigen.  Ein Beispiel hierfür ist möglicherweise, dass Ihre Organisation entscheidet, arbeiten von zu Hause um Szenarien zu ermöglichen Administratoren, die eine Verschiebung von Desktop-PAWs Laptop-paws eingesetzt werden – eine Schicht, die zusätzliche Sicherheitsaspekte zu bedenken sind zur Folge haben.  Ein weiteres häufiges Beispiel ist zum Erstellen oder Aktualisieren von Schulungen für neue Administratoren. solche Schulungen jetzt Inhalte zur ordnungsgemäßen Verwendung einer paw enthalten muss (warum ihr Einsatz so wichtig ist und was eine PAW ist und nicht).  Weitere Aspekte, die beim berücksichtigt werden müssen, wie Sie Ihr PAW-Programm skaliert werden, finden Sie in Phase 2 der Anweisungen.

Dieser Leitfaden enthält detaillierten Anweisungen für die PAW-Konfiguration für die Szenarien, wie oben bereits erwähnt. Wenn Sie für andere Szenarien benötigen, können Sie passen Sie die Anweisungen auf der Grundlage dieser Leitfaden selbst oder einen professionellen Dienstleister wie Microsoft zur Unterstützung bei der es einstellen.

Weitere Informationen zum beauftragen von Microsoft-Dienste für eine PAW, die speziell für Ihre Umgebung entwerfen, wenden Sie sich an Ihrem Microsoft-Vertriebsmitarbeiter oder besuchen Sie [auf dieser Seite](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

### <a name="paw-installation-instructions"></a>Installationsanweisungen für PAWS
Da die PAW eine sichere und vertrauenswürdige Quelle für die Verwaltung bereitstellen muss, ist es wichtig, dass der Buildprozess sicher und vertrauenswürdig ist.  In diesem Abschnitterhalten Sie detaillierte Anweisungen, mit die Sie Ihre eigene PAW verwenden allgemeine Prinzipien erstellen können und Konzepte, die sehr ähnlich denen von Microsoft-IT und Microsoft cloudentwicklungs- und Dienstverwaltungsorganisationen.

Die Anweisungen sind der Schwerpunkt liegt auf Bereitstellen der wichtigsten Maßnahmen schnell nach und nach erhöhen und erweitern die Nutzung der PAWS für das Unternehmen in drei Phasen unterteilt.

-   Phase 1: sofortige Bereitstellung für Active Directory-Administratoren

-   Phase 2: Erweitern des PAW auf alle Administratoren

-   Phase 3: Erweiterte PAW-Sicherheit

Es ist wichtig zu beachten, dass die Phasen immer in der Reihenfolge ausgeführt werden soll, auch wenn sie geplant und im Rahmen desselben Gesamtprojekts implementiert.

#### <a name="phase-1---immediate-deployment-for-active-directory-administrators"></a>Phase 1: sofortige Bereitstellung für Active Directory-Administratoren
Zweck: Bietet eine PAW schnell, die lokalen Domänen- und Verwaltungsfunktionen schützen kann.

Einsatzbereich: Administratoren der Ebene 0 einschließlich Organisations-Admins, Domänen-Admins (für alle Domänen) und Administratoren von anderen autorisierenden Identitätssystemen.

Phase 1 konzentriert sich auf die Administratoren, die Ihre lokalen Active Directory-Domäne zu verwalten und die extrem wichtige Rollen, die häufig Ziel von Angreifern sind. Diese Identitätssysteme funktionieren effektiv schützen diese Administratoren, ob Ihre Active Directory-Domänencontroller (DCs) in lokalen Rechenzentren, in Azure Infrastructure-as-a-Service (IaaS) oder einem anderen IaaS-Anbieter gehostet werden.

In dieser Phase erstellen Sie sichere administrative Organisationseinheit (OU) Struktur von Active Directory zum Hosten der Arbeitsstation mit privilegiertem Zugriff (PAW) als auch die PAWs selbst bereitstellen.  Diese Struktur umfasst auch die Gruppenrichtlinien und Gruppen, um die Unterstützung der PAWS erforderlich sind.  Erstellen Sie die meisten der Struktur mithilfe von PowerShell-Skripts, die in verfügbaren [TechNet Gallery](http://aka.ms/pawmedia).

Die Skripts werden die folgenden Organisationseinheiten und Sicherheitsgruppen erstellen:

-   Organisationseinheiten (OE)

    -   Organisationseinheiten mit sechs neue auf oberster Ebene: Admin; Gruppen; Ebene-1-Servern. Arbeitsstationen; Benutzerkonten; und Computer Quarantine.  Jede OE auf oberster Ebene enthält eine Reihe von untergeordneten Organisationseinheiten.

-   Gruppen

    -   Sechs neue sicherheitsaktivierte globale Gruppen: Tier 0 Replication Maintenance; Tier 1 Server Maintenance; Service Desk Operators; Workstation Maintenance; PAW-Benutzer; PAW Maintenance.

Außerdem erstellen Sie eine Anzahl der Gruppenrichtlinienobjekte: PAW-Konfiguration – Computer. PAW-Konfiguration – Benutzer; RestrictedAdmin erforderlich – Computer; PAW Outbound Restrictions; Beschränken Sie die Anmeldung an der Arbeitsstation. Beschränken Sie Server-Anmeldung.

Phase 1 umfasst die folgenden Schritteaus:

1.  Führen Sie die erforderlichen Komponenten

    1.  **Stellen Sie sicher, dass alle Administratoren getrennte Konten für Verwaltung und Endbenutzeraktivitäten verwenden** (einschließlich E-Mail, das Browsen im Internet, Line-of-Business-Anwendungen und andere nicht administrativer Aktivitäten).  Zuweisen von einem Administratorkonto an jedem autorisierten Mitarbeiter getrennt vom Standardbenutzerkonto ist für das PAW-Modell, da nur bestimmte Konten PAW anmelden dürfen.

        > [!NOTE]
        > Jeder Administrator sollte sein eigenes Konto für die Verwaltung verwenden.  Freigeben Sie ein Administratorkonto nicht.

    2.  **Minimieren Sie die Anzahl der Administratoren mit Berechtigungen auf Ebene 0**.  Da jeder Administrator eine PAW verwenden muss, reduziert das Reduzieren der Anzahl der Administratoren die Anzahl der PAWs erforderlich, um sie und die damit verbundenen Kosten zu unterstützen. Eine geringere Anzahl von Administratoren senkt zudem eine potenzielle Gefährdung der Administratorrechte und die damit verbundenen Risiken. Es ist, zwar möglich, Administratoren an einem Ort eine PAW gemeinsam nutzen werden Administratoren in separaten physischen Standorten dagegen benötigen getrennte PAWs.

    3.  **Erwerben Sie die Hardware bei einem vertrauenswürdigen Lieferanten, die alle technischen Anforderungen erfüllt**. Microsoft empfiehlt, Erwerb von Hardware, die erfüllt die technischen Anforderungen im Artikel [Schützen von Domänenanmeldeinformationen mit Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx).

        > [!NOTE]
        > PAW installiert auf Hardware ohne diese Funktionen kann erhebliche Schutzmaßnahmen, aber erweiterte Sicherheitsfunktionen wie Credential Guard und Device Guard werden nicht verfügbar sein.  Credential Guard und Device Guard sind für die Bereitstellung in Phase 1 nicht erforderlich, aber wird dringend empfohlen, im Rahmen von Phase 3 (Erweiterte Sicherung).

        Stellen Sie sicher, dass die für die PAW verwendete Hardware bezogen ist ein Hersteller und Lieferanten, deren Sicherheitsmethoden von der Organisation als vertrauenswürdig eingestuft werden. Dies ist eine Anwendung des Prinzips der vertrauenswürdigen Quelle auf die Sicherheit in der Lieferkette.

        > [!NOTE]
        > Weitere Hintergrundinformationen zur Bedeutung der Sicherheit geben, finden Sie unter [dieser Website](https://www.microsoft.com/security/cybersecurity/).

    4.  Erwerben Sie, und überprüfen Sie die erforderlichen Windows10 Enterprise Edition und der Anwendungssoftware. Die für die PAWS erforderliche Software beziehen, und überprüfen sie anhand der Anleitung in [vertrauenswürdige Quelle für Installationsmedien](http://aka.ms/cleansource).

        -   Windows10 Enterprise Edition

        -   [Remoteserver-Verwaltungstools](https://www.microsoft.com/en-us/download/details.aspx?id=45520.) für Windows10

        -   Windows10 [-Sicherheitsgrundwerte](http://aka.ms/win10baselines)

        -   [Erweiterte Mitigation Experience Toolkit (EMET)](https://www.microsoft.com/en-us/download/details.aspx?id=49166)

            > [!NOTE]
            > Microsoft veröffentlicht MD5-Hashes für alle Betriebssysteme und Anwendungen auf MSDN, aber nicht alle Softwarehersteller eine ähnliche Dokumentation bereitzustellen.  In diesen Fällen sind andere Strategien erforderlich sein.  Weitere Informationen zur Überprüfung von Software finden Sie unter [Quelle](http://aka.ms/cleansource) für Installationsmedien.

    5.  **Sicherstellen, dass Sie WSUS-Server verfügbar im Intranet**. Sie benötigen einen WSUS-Server im Intranet zum Herunterladen und Installieren von Updates für die PAW. Dieser WSUS-Server sollten konfiguriert werden, dass alle Sicherheitsupdates für Windows10 automatisch genehmigt, oder eine administrative Mitarbeiter verfügen Verantwortung und Verantwortlichkeit schnell Softwareupdates genehmigen.

        > [!NOTE]
        > Weitere Informationen finden Sie im Abschnitt "Automatisches genehmigen Sie Updates für die Installation" in der [Genehmigen von Updates](https://technet.microsoft.com/en-us/library/cc708458(v=ws.10).aspx).

2.  Bereitstellen der Admin-OE-Frameworks zum Hosten der PAWs

    1.  Laden Sie die PAW-Skriptbibliothek aus [TechNet Gallery](http://aka.ms/PAWmedia)

        > [!NOTE]
        > Herunterladen Sie aller Dateien und speichern Sie sie in das Verzeichnis, und führen Sie sie in der unten angegebenen Reihenfolge.  Create-PAWGroups hängt vom Create-PAWOUs OU-Struktur, und Set-PAWOUDelegation auf die Gruppen von Create-PAWGroups erstellt.
        > Ändern Sie die Skripts oder die Datei durch Trennzeichen getrennte (CSV) nicht.

    2.  **Führen Sie das Create-PAWOUs. ps1-Skript**.  Dieses Skript wird die neue Organisationseinheit (OU)-Struktur in Active Directory erstellen und in den neuen Organisationseinheiten nach Bedarf die GPO-Vererbung blockieren.

    3.  **Führen Sie das Create-PAWGroups. ps1-Skript**.  Dieses Skript erstellt die neuen globalen Sicherheitsgruppen in den entsprechenden Organisationseinheiten.

        > [!NOTE]
        > Während dieses Skript die neuen Sicherheitsgruppen erstellen, wird es ihnen nicht automatisch aufgefüllt.

    4.  **Führen Sie das Set-PAWOUDelegation. ps1-Skript**.  Mit diesem Skript werden die neuen Organisationseinheiten zu den entsprechenden Gruppen Berechtigungen erteilen.

3.  **Ebene-0-Konten der Admin\Tier 0\Accounts Organisationseinheit verschieben**. Verschieben Sie jedes Konto, das Mitglied der Domänen-Admins, Organisations-Admins ist, oder der Ebene 0 entsprechende Gruppen (einschließlich geschachtelten Mitgliedschaften) in diese OE. Wenn Ihre Organisation eigene Gruppen verfügt, die diesen Gruppen hinzugefügt werden, sollten Sie diese mit der Admin\Tier 0\Groups Organisationseinheit verschieben.

    > [!NOTE]
    > Weitere Informationen auf dem Gruppen der Ebene 0 sind, finden Sie unter "Äquivalenz zur Ebene-0" in [Schützen des privilegierten Zugriffs – Referenzmaterial](../securing-privileged-access/securing-privileged-access-reference-material.md).

4.  Hinzufügen der geeigneten Mitglieder zu den jeweiligen Gruppen

    1.  **PAW-Benutzer** : Fügen Sie die Administratoren der Ebene 0 mit der Domäne oder Organisations-Admins Benutzergruppen, die Sie in Schritt1 von Phase 1 identifiziert.

    2.  **PAW Maintenance** – fügen Sie mindestens ein Konto, das für die PAW-Wartung verwendet wird, und Behandeln von Problemen. Die PAW Maintenance-Konten werden nur selten verwendet werden.

        > [!NOTE]
        > Fügen Sie das Benutzerkonto oder die Gruppe nicht sowohl "PAW Users" und "PAW Maintenance.  Das PAW-Sicherheitsmodell basiert teilweise auf der Annahme, dass die PAW-Benutzerkonto Rechte für die verwalteten Systeme oder über die PAW selbst, aber nicht beides privilegierten hat.
        >
        > -   Dies ist wichtig für die Entwicklung sorgfältiger Verwaltungsmethoden und -Gewohnheiten in Phase 1.
        > -   Dies ist entscheidend für Phase 2 und darüber hinaus Ausweitung von rechten, wenn PAWs werden zu verhindern.
        >
        > Im Idealfall keine Mitarbeiter Aufgaben auf mehreren Ebenen auf das Prinzip der Aufgabentrennung durchzusetzen zugewiesen sind, aber Microsoft ist sich bewusst, dass viele Organisationen können Personal (oder andere organisationsbezogene Anforderungen) begrenzt ist, die nicht für die Trennung von diesem vollständigen zulassen. In diesen Fällen die gleichen Mitarbeiter können beide Rollen zugewiesen werden, verwenden jedoch nicht das gleiche Konto für diese Funktionen.

5.  **Erstellen Sie Gruppenrichtlinienobjekt (GPO) "PAW-Konfiguration – Computer" und Verknüpfen mit der Organisationseinheit der Ebene 0 Geräte** ("Devices" unter Tier 0\Admin).  In diesem Abschnitterstellen Sie eine neue "PAW-Konfiguration – Computer" Gruppenrichtlinienobjekt, das bestimmte Schutzmaßnahmen für diese PAWs bereitstellt.

    > [!NOTE]
    > **Fügen Sie diese Einstellungen nicht der Standarddomänenrichtlinie hinzu**.  Auf diese Weise wirkt sich potenziell auf Vorgänge in der gesamten Active Directory-Umgebung.  Konfigurieren Sie diese Einstellungen nur in den neu erstellten Gruppenrichtlinienobjekten, die hier beschriebenen, und wenden Sie sie nur auf die Organisationseinheit "PAW".

    1.  **PAW-Wartungszugriff** : Diese Einstellung legt die Mitgliedschaft in bestimmten privilegierten Gruppen auf den PAWs auf eine bestimmte Gruppe von Benutzern. Wechseln Sie zu *Computer computerkonfiguration\einstellungen\systemsteuerungseinstellungen\lokale Benutzer* und Gruppen, und führen Sie die folgenden Schritteaus:

        1.  Klicken Sie auf **neu**, und klicken Sie auf **lokale Gruppe**

        2.  Wählen Sie die **Update** Aktion und wählen Sie "Administratoren (integriert)" (verwenden Sie nicht die Schaltfläche "Durchsuchen" zum Auswählen der Gruppe Administratoren).

        3.  Wählen Sie die **alle mitgliederbenutzer löschen** und **alle Mitgliedergruppen löschen** Kontrollkästchen

        4.  PAW Maintenance (Pawmaint) und Administrator hinzufügen (in diesem Fall verwenden Sie nicht die Schaltfläche "Durchsuchen" zum Auswählen des Administrators).

            > [!NOTE]
            > Fügen Sie der Gruppe "PAW Users" nicht zur Mitgliederliste für die lokale Gruppe "Administratoren".  Um sicherzustellen, dass die PAW Benutzer versehentlich oder absichtlich die Sicherheitseinstellungen der PAW nicht ändern können, sollten sie nicht Mitglied der lokalen Administratorgruppe sein.

            Weitere Informationen zur Verwendung von Voreinstellungen für Gruppenrichtlinien Gruppenmitgliedschaft ändern, finden Sie im TechNet-Artikel [Konfigurieren eines Elements für lokale Gruppenrichtlinien](https://technet.microsoft.com/en-us/library/cc732525.aspx).

    2.  **Beschränken Sie lokale Gruppenmitgliedschaft** -mit dieser Einstellung wird sichergestellt, dass die Mitgliedschaft lokaler Administratorengruppen auf der Arbeitsstation immer leer ist.

        1.  Wechseln Sie zu dem Computer computerkonfiguration\einstellungen\systemsteuerungseinstellungen\lokale Benutzer und Gruppen, und führen Sie die folgenden Schritteaus:

            1.  Klicken Sie auf **neu**, und klicken Sie auf **lokale Gruppe**

            2.  Wählen Sie die **Update** Aktion und wählen Sie "Sicherungs-Operatoren (integriert)" (verwenden Sie nicht die Schaltfläche "Durchsuchen", wählen Sie die Gruppe der Domäne Sicherungsoperatoren).

            3.  Wählen Sie die **alle mitgliederbenutzer löschen** und **alle Mitgliedergruppen löschen** Kontrollkästchen.

            4.  Fügen Sie keine Mitglieder der Gruppe.  Klicken Sie einfach auf **OK**.  Gruppenrichtlinien werden durch Zuweisen einer leeren Liste, entfernen Sie alle Mitglieder und Sicherstellen einer leeren Mitgliedschaftsliste, die jedes Mal die Gruppenrichtlinien aktualisiert werden.

        2.  Führen Sie die oben genannten Schrittefür die folgenden zusätzlichen Gruppen:

            -   Kryptografische Operatoren

            -   Hyper-V-Administratoren

            -   Netzwerkkonfigurations-Operatoren

            -   Erfahrene Benutzer

            -   Remote Desktop Users

            -   Replikatoren

        3.  PAW Logon Restrictions: wird diese Einstellung die Konten einschränken, die bei der PAW anmelden können. Gehen Sie folgendermaßen vor, um diese Einstellung zu konfigurieren:

            1.  Wechseln Sie lokal auf dem Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten\Lokal anmelden.

            2.  Wählen Sie diese Richtlinieneinstellungen definieren, und fügen Sie "PAW Users" und Administratoren (in diesem Fall verwenden Sie nicht die Schaltfläche "Durchsuchen" Administratoren auswählen).

        4.  **Eingehenden Netzwerkdatenverkehr blockieren** -mit dieser Einstellung wird sichergestellt, dass kein unangeforderter eingehender Netzwerkdatenverkehr zur PAW zugelassen wird. Gehen Sie folgendermaßen vor, um diese Einstellung zu konfigurieren:

            1.  Wechseln Sie zu Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Windows-Firewall mit erweiterter Sicherheit\windows-Firewall mit erweiterter Sicherheit, und führen Sie die folgenden Schritteaus:

                1.  Klicken Sie mit der rechten Maustaste auf die Windows-Firewall mit erweiterter Sicherheit, und wählen Sie **Richtlinie importieren**.

                2.  Klicken Sie auf **Ja** annehmen, dass dadurch alle vorhandenen Firewallrichtlinien überschrieben werden.

                3.  Navigieren Sie zu PAWFirewall.wfw, und wählen Sie **öffnen**.

                4.  Klicken Sie auf **OK**.

                    > [!NOTE]
                    > Sie können Adressen oder Subnetzen die PAW mit unerwünschten Datenverkehr an diesem Punkt (z.B. Sicherheitsüberprüfungs- oder Verwaltungssoftware Sicherheitssoftware. erreichen müssen hinzufügen
                    > Die Einstellungen in der WFW-Datei aktivieren die Firewall im Modus "Blockieren (Standard)", für alle Firewallprofile, deaktivieren die regelzusammenführung und aktivieren die Protokollierung sowohl für gelöschte als auch für erfolgreiche Pakete. Diese Einstellungen blockieren unangeforderten Datenverkehr und dennoch bidirektionale Kommunikation in Verbindungen, die von der PAW initiiert, verhindern, dass Benutzer mit lokalem Administratorzugriff lokale Firewallregeln, die die GPO-Einstellungen überschreiben würden, und stellen Sie sicher, dass Datenverkehr zur und aus der PAW protokolliert wird erstellen.
                    > **Durch Öffnen dieser Firewall wird die Angriffsfläche für die PAW erweitern und Sicherheitsrisiken erhöhen. Bevor Sie Adressen hinzufügen, finden Sie in AbschnittVerwaltung und Betrieb einer PAW in diesem Leitfaden**.

        5.  **Konfigurieren von Windows Update für WSUS** -führen Sie die folgenden Schritteaus, um die Einstellungen zum Konfigurieren von Windows Update für die PAWs zu ändern:

            1.  Wechseln Sie zu Computer Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\Windows-Updates, und führen Sie die folgenden Schritteaus:

                1.  Aktivieren der **Richtlinie automatische Updates konfigurieren**.

                2.  Wählen Sie Option **4 – Autom. herunterladen und laut Zeitplan installieren**.

                3.  Ändern Sie die Option **geplanter Installationstag** auf **0 – täglich** und die Option **Geplante Installationszeit** nach Belieben Organisationseinheit.

                4.  Aktivieren Sie die Option **internen Pfad für den Microsoft Updatedienst angeben** Richtlinie, und geben Sie in beiden Optionen die URL des ESAE WSUS-Servers.

        6.  Verknüpfen Sie die "PAW-Konfiguration – Computer" GPO wie folgt:

            |Richtlinie|Speicherort|
            |-----|---------|
            |PAW-Konfiguration – Computer |Admin\Tier 0\Devices|

6.  **Erstellen Sie Gruppenrichtlinienobjekt (GPO) "PAW-Konfiguration – Benutzer" und Verknüpfen mit der Organisationseinheit für Ebene-0-Konten ("Konten" unter Tier 0\Admin)**.  In diesem Abschnitterstellen Sie eine neue "PAW-Konfiguration – Benutzer" Gruppenrichtlinienobjekt, das bestimmte Schutzmaßnahmen für diese PAWs bereitstellt.

    > [!NOTE]
    > Fügen Sie diese Einstellungen nicht der Standarddomänenrichtlinie hinzu

    1.  **Internetbrowsen blockieren** - Internetbrowsen, dadurch wird eine Proxyadresse einer Loopbackadresse (127.0.0.1 festgelegt).

        1.  Wechseln Sie zu Benutzer Configuration\Preferences\Windows Settings\Registry. Maustaste auf die Registrierung, und wählen Sie **neu** \> **Registrierungselement** und konfigurieren Sie die folgenden Einstellungen:

            1.  Aktion: Ersetzen

            2.  Struktur: HKEY_CURRENT_USER

            3.  Schlüsselpfad: Software\Microsoft\Windows\CurrentVersion\Internet Settings

            4.  Wertname: ProxyEnable

                > [!NOTE]
                > Wählen Sie das standardmäßig links neben dem Namen der Wert nicht.

            5.  Werttyp: REG_DWORD

            6.  Wertdaten: 1

                1.  ein.  Klicken Sie auf der Registerkarte Allgemein, und wählen Sie **dieses Element entfernen, wenn es nicht mehr angewendet wird**.

                2.  Wählen Sie auf der Registerkarte Allgemein **Zielgruppenadressierung auf Elementebene**, und klicken Sie auf **Zielgruppenadressierung**.

                3.  Klicken Sie auf **neues Element**, und wählen Sie **Sicherheitsgruppe**.

                4.  Wählen Sie die Schaltfläche "..." und suchen Sie nach der Gruppe "PAW Users".

                5.  Klicken Sie auf **neues Element**, und wählen Sie **Sicherheitsgruppe**.

                6.  Wählen Sie die Schaltfläche "...", und suchen Sie nach der **Clouddienstadministratoren** Gruppe.

                7.  Klicken Sie auf die **Clouddienstadministratoren** Element, und klicken Sie auf **Elementoptionen**.

                8.  Wählen Sie **ist nicht**.

                9. Klicken Sie auf **OK** im Fenster vorgesehen sind.

            7.  Klicken Sie auf **OK** um die ProxyServer-Gruppenrichtlinieneinstellung abzuschließen.

        2.  Wechseln Sie zu Benutzer Configuration\Preferences\Windows Settings\Registry. Maustaste auf die Registrierung, und wählen Sie **neu** \> **Registrierungselement** und konfigurieren Sie die folgenden Einstellungen:

            -   Aktion: Ersetzen

            -   Struktur: HKEY_CURRENT_USER

            -   Schlüsselpfad: Software\Microsoft\Windows\CurrentVersion\Internet Settings

            -   Wertname: ProxyServer

                > [!NOTE]
                > Wählen Sie das standardmäßig links neben dem Namen der Wert nicht.

            -   Werttyp: REG_SZ

            -   Wertdaten: 127.0.0.1: 80

                1.  Klicken Sie auf die **allgemeine** Registerkarte, und wählen Sie **dieses Element entfernen, wenn es nicht mehr angewendet wird**.

                2.  Auf der **allgemeine** wählen Registerkarte **Zielgruppenadressierung auf Elementebene**, und klicken Sie auf **Zielgruppenadressierung**.

                3.  Klicken Sie auf **neues Element** und select-Sicherheitsgruppe.

                4.  Wählen Sie die Schaltfläche "...", und fügen Sie der Gruppe "PAW Users" hinzu.

                5.  Klicken Sie auf **neues Element** und select-Sicherheitsgruppe.

                6.  Wählen Sie die Schaltfläche "...", und suchen Sie nach der **Clouddienstadministratoren** Gruppe.

                7.  Klicken Sie auf die **Clouddienstadministratoren** Element, und klicken Sie auf **Elementoptionen**.

                8.  Wählen Sie **ist nicht**.

                9. Klicken Sie auf **OK** im Fenster vorgesehen sind.

        3.  Klicken Sie auf **OK** um die ProxyServer-Gruppenrichtlinieneinstellung abzuschließen.

    2.  Rufen Sie Benutzer Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\Internet Explorer, und aktivieren Sie die unten aufgeführten Optionen. Diese Einstellung werden verhindert, dass die Administratoren die Proxyeinstellungen manuell überschreiben.

        1.  Aktivieren der **deaktivieren, ändern die automatische Konfiguration** Einstellungen.

        2.  Aktivieren der **Änderung der Proxyeinstellungen verhindern**.

7.  **Beschränken Sie Administratoren Hosts auf niedrigerer Ebene anmelden**.  In diesem Abschnittwird Gruppenrichtlinien, um zu verhindern, dass Administratorkonten mit hohen Berechtigungen Protokollierung Hosts auf niedrigerer Ebene konfiguriert.

    1.  Erstellen Sie das neue **Restrict Workstation Logon** GPO - diese Einstellung verhindert, dass auf Ebene 0 und Ebene 1 Administratorkonten standardarbeitsstationen anmelden.  Dieses Gruppenrichtlinienobjekt mit der Organisationseinheit "Arbeitsstationen" auf oberster Ebene verknüpft werden soll, und weisen folgende Einstellungen:

        - (i) Wählen Sie im Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Rechte benutzerrechten\anmelden als Batchauftrag, **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 und Ebene 1 hinzu:

            **Gruppen Einstellungen hinzu:**

            Organisations-Admins

            Domänen-Admins

            Schema-Admins

            "DOMAIN\Administrators"

            Konten-Operatoren

            Sicherungs-Operatoren

            Druck-Operatoren

            Server-Operatoren

            Domänencontroller

            Read-Only Domänencontroller

            Richtlinien-Ersteller-Besitzer

            Kryptografische Operatoren

            > [!NOTE]
            > Hinweis: Integrierten Gruppen auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

            Andere delegierte Gruppen

            > [!NOTE]
            > Hinweis: Erstellten benutzerdefinierten Gruppen mit effektiven Zugriff auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

            Administratoren der Ebene 1

            > [!NOTE]
            > Hinweis: Diese Gruppe wurde zuvor in Phase 1 erstellt.

        - (Ii) Wählen Sie im Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Rechte benutzerrechten\anmelden als Dienst, **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 und Ebene 1 hinzu:

            **Gruppen Einstellungen hinzu:**

            Organisations-Admins

            Domänen-Admins

            Schema-Admins

            "DOMAIN\Administrators"

            Konten-Operatoren

            Sicherungs-Operatoren

            Druck-Operatoren

            Server-Operatoren

            Domänencontroller

            Read-Only Domänencontroller

            Richtlinien-Ersteller-Besitzer

            Kryptografische Operatoren

            > [!NOTE]
            > Hinweis: Integrierten Gruppen auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

            Andere delegierte Gruppen

            > [!NOTE]
            > Hinweis: Erstellten benutzerdefinierten Gruppen mit effektiven Zugriff auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

            Administratoren auf Ebene 1

            > [!NOTE]
            > Hinweis: Diese Gruppe wurde zuvor in Phase 1 erstellt.

    2.  Erstellen Sie das neue **Server einschränken** GPO - diese Einstellung verhindert, dass Administratorkonten der Ebene 0 Anmelden an Server der Ebene 1.  Dieses Gruppenrichtlinienobjekt mit der Organisationseinheit "Server der Ebene 1" auf oberster Ebene verknüpft werden soll, und weisen folgende Einstellungen:

        -   (i) Wählen Sie im Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Rechte benutzerrechten\anmelden als Batchauftrag, **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 hinzu:

            **Gruppen Einstellungen hinzu:**

            Organisations-Admins

            Domänen-Admins

            Schema-Admins

            "DOMAIN\Administrators"

            Konten-Operatoren

            Sicherungs-Operatoren

            Druck-Operatoren

            Server-Operatoren

            Domänencontroller

            Read-Only Domänencontroller

            Richtlinien-Ersteller-Besitzer

            Kryptografische Operatoren

            > [!NOTE]
            > Hinweis: Integrierten Gruppen auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

            Andere delegierte Gruppen

            > [!NOTE]
            > Hinweis: Erstellten benutzerdefinierten Gruppen mit effektiven Zugriff auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

        -   (Ii) Wählen Sie im Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Rechte benutzerrechten\anmelden als Dienst, **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 hinzu:

            **Gruppen Einstellungen hinzu:**

            Organisations-Admins

            Domänen-Admins

            Schema-Admins

            "DOMAIN\Administrators"

            Konten-Operatoren

            Sicherungs-Operatoren

            Druck-Operatoren

            Server-Operatoren

            Domänencontroller

            Read-Only Domänencontroller

            Richtlinien-Ersteller-Besitzer

            Kryptografische Operatoren

            > [!NOTE]
            > Hinweis: Integrierten Gruppen auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

            Andere delegierte Gruppen

            > [!NOTE]
            > Hinweis: Erstellten benutzerdefinierten Gruppen mit effektiven Zugriff auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

        -   (Iii) Wählen Sie lokal, im Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Rechte benutzerrechten\anmelden **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 hinzu:

            **Gruppen Einstellungen hinzu:**

            Organisations-Admins

            Domänen-Admins

            Schema-Admins

            Konten-Operatoren

            Sicherungs-Operatoren

            Druck-Operatoren

            Server-Operatoren

            Domänencontroller

            Read-Only Domänencontroller

            Richtlinien-Ersteller-Besitzer

            Kryptografische Operatoren

            > [!NOTE]
            > Hinweis: Integrierten Gruppen auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

            Andere delegierte Gruppen

            > [!NOTE]
            > Hinweis: Erstellten benutzerdefinierten Gruppen mit effektiven Zugriff auf Ebene 0 finden Sie unter Äquivalenz zur Ebene 0 Weitere Detail.

8.  Bereitstellen der PAWs

    > [!NOTE]
    > Stellen Sie sicher, dass die PAW über das Netzwerk während des Buildprozesses des Betriebssystems getrennt ist.

    1.  Installieren Sie Windows10 mithilfe der Installationsmedien aus vertrauenswürdiger Quelle, die Sie zuvor erhalten haben.

        > [!NOTE]
        > Sie können Microsoft Deployment Toolkit (MDT) oder ein anderes Bild automatisierte Bereitstellungssystem verwenden, um PAW-Bereitstellung zu automatisieren, jedoch müssen Sie sicherstellen, dass der Buildprozess so vertrauenswürdig ist wie die PAW ist. Angreifer suchen sich gezielt Unternehmensimages und -Bereitstellungssysteme (z.B. ISOs, Bereitstellungspakete usw.) als persistenzmechanismus bereits vorhandenen oder Images sollte nicht verwendet werden.
        >
        > Wenn Sie die Bereitstellung der PAW automatisieren, müssen Sie folgende Schritteausführen:
        >
        > -   Erstellen Sie das System mithilfe eines Installationsmediums überprüft mithilfe der Anleitungen im [vertrauenswürdige Quelle für Installationsmedien](http://aka.ms/cleansource).
        > -   Stellen Sie sicher, dass das System für die automatisierte Bereitstellung über das Netzwerk während des Buildprozesses des Betriebssystems getrennt ist.

    2.  Legen Sie ein eindeutiges komplexes Kennwort für das lokale Administratorkonto an.  Verwenden Sie ein Kennwort, das für ein anderes Konto in der Umgebung verwendet wurde.

        > [!NOTE]
        > Microsoft empfiehlt die Verwendung [lokalen Administrator Kennwort Solution (LAPS)](https://www.microsoft.com/en-us/download/details.aspx?id=46899) das lokale Administratorkennwort für alle Arbeitsstationen einschließlich PAWs zu verwalten.  Wenn Sie LAPS verwenden, stellen Sie sicher, dass Sie nur der Gruppe "PAW Maintenance" das Recht zum Lesen von über LAPS verwalteten Kennwörter für die PAWs erteilen.

    3.  Installieren Sie Remote Server Administration Tools für Windows10 mithilfe der Installationsmedien aus vertrauenswürdiger Quelle.

    4.  Installieren Sie Enhanced Mitigation Experience Toolkit (EMET) mithilfe der Installationsmedien aus vertrauenswürdiger Quelle.

        > [!NOTE]
        > Bitte beachten Sie, dass zum Zeitpunkt der letzten Aktualisierung dieses Leitfadens befand sich EMET 5.5 noch in der beta-Tests wurde.  Da dies die erste Version von Windows10 unterstützt wird, wird sie hier trotzdem trotz der Beta-Zustand.  Wenn die Installation von Betasoftware auf der PAW Ihren risikorichtlinien zuwiderläuft, überspringen Sie diesen Schrittfür den Moment.

    5.  Verbinden Sie die PAW mit dem Netzwerk.  Stellen Sie sicher, dass die PAW auf mindestens einen Domänencontroller (DC) eine Verbindung herstellen kann.

    6.  Verwenden ein Konto, das Mitglied der Gruppe "PAW Maintenance" ist, führen Sie den folgenden PowerShell-Befehl von der neu erstellten PAW das Beitreten zur Domäne in der entsprechenden Organisationseinheit:

        `Add-Computer -DomainName Fabrikam -OUPath "OU=Devices,OU=Tier 0,OU=Admin,DC=fabrikam,DC=com"`

        Ersetzen Sie die Verweise auf *Fabrikam* mit Ihrem Domänennamen entsprechend den Anforderungen.  Wenn Ihr Domänenname mehrere Ebenen (z.B. child.fabrikam.com) erweitert, fügen Sie die zusätzlichen Namen mit dem "DC =" Bezeichner in der Reihenfolge, in dem sie in der Domäne vollständig qualifizierten Domänennamen angezeigt werden.

        > [!NOTE]
        > Wenn Sie bereitgestellt haben eine [Administrative ESAE-Gesamtstruktur](http://aka.ms/esae) (für Administratoren auf Ebene 0 in Phase 1) oder eine [Microsoft Identity Manager (MIM) privilegierte zugriffsverwaltung (PAM)](http://aka.ms/mimpamdeploy) (für Ebene 1 und 2 Administratoren in Phase 2), fügen Sie in diesem Fall die PAW zur Domäne in dieser Umgebung anstatt zur Produktionsdomäne.

    7.  Wenden Sie alle wichtigen Windows-Updates vor der Installation andere Software (einschließlich Verwaltungstools, Agents usw..).

    8.  Anwendung der Gruppenrichtlinie zu erzwingen.

        1.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und geben Sie den folgenden Befehl aus:

            `Gpupdate /force /sync`

        2.  Starten Sie den Computer neu

    9. **(Optional) **Installieren Sie weitere erforderliche Tools für Active Directory-Administratoren. Installieren Sie weitere Tools oder Skripts, die zum Ausführen von Aufgaben erforderlich. Sicherstellen, dass das Risiko einer Offenlegung von Anmeldeinformationen auf den Zielcomputern mit einem beliebigen Tool einhergeht, bevor auf einer paw installieren. Zugriff [auf dieser Seite](http://aka.ms/logontypes) erhalten Sie weitere Informationen zur Bewertung von Verwaltungstools und Verbindungsmethoden Risikos für Anmeldeinformationen durch. Sicherstellen, dass alle Installationsmedien die in erhalten [vertrauenswürdige Quelle für Installationsmedien](http://aka.ms/cleansource).

        > [!NOTE]
        > Verwendung eines sprungbrettservers als zentralen Speicherort für diese Tools kann die Komplexität reduzieren, auch wenn es als eine Sicherheitsgrenze dienen nicht.

    10. **(Optional) **Erforderlichen RAS-Software herunterladen und installieren. Wenn Administratoren die PAW Remote für die Verwaltung verwenden, installieren Sie die Remotezugriffssoftware Sicherheitsinformationen vom Hersteller RAS-Lösung. Sicherstellen, dass um alle Installationsmedien die in der vertrauenswürdigen Quelle für Installationsmedien zu erhalten.

        > [!NOTE]
        > Sorgfältig alle Risiken bei der Remote-Zugriff über eine paw EINHERGEHEN.  Während eine mobile PAW, viele wichtige Szenarien ermöglicht, einschließlich arbeiten von zu Hause, RAS-Software kann potenziell anfällig für Angriffe sein, und Sie werden verwendet, um eine PAW gefährden.

    11. Überprüfen Sie die Integrität des PAW-Systems, indem Sie prüfen und zu bestätigen, dass alle entsprechenden Einstellungen mithilfe der folgenden Schrittesind:

        1.  Stellen Sie sicher, dass nur die PAW-spezifischen Gruppenrichtlinien auf die PAW angewendet werden

            1.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und geben Sie den folgenden Befehl aus:

                `Gpresult /scope computer /r`

            2.  Überprüfen Sie die resultierende Liste, und stellen Sie sicher, dass die einzige Gruppe angezeigt werden diejenigen, die Sie soeben erstellt haben.

        2.  Stellen Sie sicher, dass keine weiteren Benutzerkonten Mitglied von privilegierten Gruppen auf der PAW mithilfe der folgenden Schrittesind:

            1.  Öffnen **lokale Benutzer und Gruppen bearbeiten** (lusrmgr.msc) wählen **Gruppen**, und stellen Sie sicher, dass die einzigen Mitglieder der Gruppe der lokalen Administratoren das lokale Administratorkonto und die globale Sicherheitsgruppe PAW Maintenance sind.

                > [!NOTE]
                > Die Gruppe "PAW Users" sollten nicht Mitglied der lokalen Gruppe Administratoren sein.  Die einzigen Mitglieder sollte das lokale Administratorkonto und die globale Sicherheitsgruppe PAW Maintenance (und PAW Users sollten nicht Mitglied dieser globalen Gruppe entweder).

            2.  Zudem **lokale Benutzer und Gruppen bearbeiten**, stellen Sie sicher, dass die folgenden Gruppen keine Mitglieder enthalten:

                -   Sicherungs-Operatoren

                -   Kryptografische Operatoren

                -   Hyper-V-Administratoren

                -   Netzwerkkonfigurations-Operatoren

                -   Erfahrene Benutzer

                -   Remote Desktop Users

                -   Replikatoren

    12. **(Optional) **Wenn Ihre Organisation eine Sicherheitsinformations- und Ereignis-Management (SIEM)-Lösung verwendet, stellen Sie sicher, dass die PAW [zum Weiterleiten von Ereignissen an das System über Windows Ereignis Ereignisweiterleitung konfiguriert](http://blogs.technet.com/b/jepayne/archive/2015/11/24/monitoring-what-matters-windows-event-forwarding-for-everyone-even-if-you-already-have-a-siem.aspx) oder anderweitig mit der Lösung registriert, damit die SIEM-Lösung aktiv Ereignisse und Informationen von der PAW empfängt.  Die Detail dieses Vorgangs variieren basierend auf Ihrer SIEM-Lösung.

        > [!NOTE]
        > Wenn Ihre SIEM einen Agent, die als System oder ein lokales Administratorkonto auf den PAWs ausgeführt wird erfordert, stellen Sie sicher, dass die SIEM mit der gleichen Grad an vertrauen, als Domänencontroller und Identitätssysteme verwaltet werden.

    13. **(Optional) **Wenn Sie LAPS zur Verwaltung des Kennworts für das lokale Administratorkonto auf Ihrer PAW bereitstellen möchten, stellen Sie sicher, dass das Kennwort erfolgreich registriert ist.

        -   Öffnen Sie mit einem Konto mit Berechtigungen zum Lesen von über LAPS verwalteten Kennwörter **Active Directory-Benutzer und -Computer** (dsa.msc).  Stellen Sie sicher, dass erweiterte Funktionen aktiviert ist, und klicken Sie dann das entsprechende Computerobjekt Maustaste.  Klicken Sie auf der Registerkarte Attribut-Editor, und stellen Sie sicher, dass der Wert für MsSVSadmPwd mit einem gültigen Kennwort aufgefüllt wird.

#### <a name="phase-2---extend-paw-to-all-administrators"></a>Phase 2: Erweitern des PAW auf alle Administratoren
Einsatzbereich: Alle Benutzer mit administrativen Rechten für unternehmenskritische Anwendungen und Abhängigkeiten.  Dazu zählen u. a. mindestens Administratoren von Anwendungsservern, betrieblichen Stabilität und Sicherheit, die Überwachung von Lösungen, Virtualisierungslösungen, Speichersystemen und Netzwerkgeräten.

> [!NOTE]
> Die Anweisungen in dieser Phase wird davon ausgegangen, dass Phase 1 vollständig abgeschlossen wurde.  Phase 2 kann nicht gestartet werden, bis Sie alle Schrittein Phase 1 abgeschlossen haben.

Wenn Sie bestätigen, dass alle Schrittedurchgeführt wurden, führen Sie die folgenden Schrittezum Abschließen der Phase 2:

1.  **(Empfohlen) **Aktivieren **RestrictedAdmin** -Modus – aktivieren Sie dieses Feature auf Ihren vorhandenen Servern und Arbeitsstationen, und erzwingen Sie dann die Verwendung dieses Features. Diese Funktion muss auf die Zielservern Windows Server2008 R2 ausgeführt werden oder höher und auf den Zielarbeitsstationen Windows7 oder höher ausgeführt werden.

    1.  Aktivieren Sie **RestrictedAdmin** Modus auf Ihren Servern und Arbeitsstationen mithilfe der Anweisungen in diesem verfügbaren [Seite](http://aka.ms/rdpra).

        > [!NOTE]
        > Bevor Sie die Aktivierung dieser Funktion für den Internetzugang, sollten Sie das Risiko, dass Angreifer sich mit diesen Servern mit einem zuvor gestohlenen Kennworthash authentifizieren.

    2.  "RestrictedAdmin erforderlich – Computer" Gruppenrichtlinienobjekt (GPO) zu erstellen. In diesem Abschnitterstellt ein Gruppenrichtlinienobjekt die Verwendung erzwingt der /RestrictedAdmin für ausgehende Remotedesktopverbindungen, Schutz von Konten vor Diebstahl von Anmeldeinformationen auf den Zielsystemen wechseln

        -   Wechseln Sie zu Computer Computerkonfiguration\Richtlinien\Administrative vorlagen\System\delegierung von Anmeldeinformationen\delegierung von Anmeldeinformationen an Remoteserver, und legen Sie auf **aktiviert**.

    3.  Verknüpfen der **RestrictedAdmin** erforderlich – Computer mit der entsprechenden Ebene 1 und/oder Ebene-2-Geräte mithilfe der folgenden Optionen:

        PAW-Konfiguration – Computer

        -> Speicherort für Verknüpfung: Admin\Tier 0\Devices (vorhanden)

        PAW-Konfiguration – Benutzer

        -> Speicherort für Verknüpfung: Admin\Tier 0\Accounts

        RestrictedAdmin erforderlich – Computer

        -> Admin\Tier1\Devices oder -> Admin\Tier2\Devices (beide sind optional)

        > [!NOTE]
        > Dies ist nicht für Systeme auf Ebene 0 erforderlich, da diese Systeme bereits Vollzugriff auf alle Assets in der Umgebung befinden.

2.  Verschieben Sie Objekte der Ebene 1 in den entsprechenden Organisationseinheiten.

    1.  Verschieben Sie Gruppen auf Ebene 1, Admin\Tier 1\Groups Organisationseinheit. Suchen Sie alle Gruppen, die die folgenden administrativen Berechtigungen gewähren, und verschieben Sie sie in diese OE.

        -   Lokaler Administrator auf mehreren Servern

        -   Administratorzugriff auf Clouddienste

        -   Administratorzugriff auf unternehmensanwendungen

    2.  Ebene-1-Konten der Admin\Tier 1\Accounts Organisationseinheit zu verschieben. Verschieben Sie jedes Konto, ein Mitglied dieser Gruppen auf Ebene 1 (einschließlich geschachtelten Mitgliedschaften) in diese OE.

3.  Hinzufügen der geeigneten Mitglieder zu den jeweiligen Gruppen

    -   **Tier 1 Admins** -diese Gruppe enthält die Administratoren auf Ebene 1, die sich auf Ebene-2-Hosts von beschränkt wird. Fügen Sie all Ihre Verwaltungsgruppen auf Ebene 1, die über Administratorrechte für Server oder Internetdienste verfügen.

        > [!NOTE]
        > Wenn Administratoren Aufgaben zum Verwalten von Ressourcen auf mehreren Ebenen verfügen, müssen Sie jede Ebene ein separates Administratorkonto erstellen.

4.  Aktivieren Sie Credential Guard, um das Risiko des Diebstahls von Anmeldeinformationen zu reduzieren und wiederverwenden.  Credential Guard ist ein neues Feature von Windows10, die Zugriff auf Anmeldeinformationen einschränkt Methoden des Anmeldeinformationsdiebstahls (einschließlich Pass-the-Hash) zu verhindern.  Credential Guard ist für den Endbenutzer vollständig transparent und erfordert minimale Einrichtungszeit und Mühe.  Weitere Informationen zu Credential Guard einschließlich der Bereitstellungsschritte und hardwarevoraussetzungen finden Sie im Artikel [Schützen von Domänenanmeldeinformationen mit Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx).

    > [!NOTE]
    > Deviceguard muss aktiviert sein, um die Konfiguration und Verwendung von Credential Guard.  Sie sind jedoch nicht erforderlich, um andere Device Guard-Schutzfunktionen konfigurieren, um Credential Guard verwenden.

5.  **(Optional) **Verbindungen mit Clouddiensten zu aktivieren. Dieser Schrittermöglicht die Verwaltung von Clouddiensten wie Azure und Office365 mit geeigneten Sicherheitsmaßnahmen. Dieser Schrittist auch für Microsoft Intune zum Verwalten der PAWs erforderlich.

    > [!NOTE]
    > Überspringen Sie diesen Schritt, wenn keine cloudkonnektivität für die Verwaltung von Clouddiensten oder die Verwaltung von Intune erforderlich ist.

    Diese Schrittewerden beschränken die Kommunikation über das Internet nur autorisierte Clouddienste (jedoch nicht dem offenen Internet) und fügen Schutzmaßnahmen für die Browser und andere Anwendungen, die Inhalte aus dem Internet verarbeiten. Diese PAWs für die Verwaltung sollten niemals für standardbenutzeraufgaben wie Internetkommunikation und produktivitätsanwendungen verwendet werden.

    Zum Aktivieren von Verbindungen mit PAW führen Sie die Dienste die folgenden Schritteaus:

    1.  Konfigurieren Sie die PAW, um nur autorisierte Internetziele zugelassen.  Wie Sie Ihre PAW-Bereitstellung zum Aktivieren der Verwaltung in der Cloud erweitern, müssen Sie ermöglichen den Zugriff auf autorisierte Dienste und gleichzeitig den Zugriff aus dem Internet öffnen, in dem können Angriffe leichter Ihre Administratorkonten bereitgestellt werden.

        1.  Erstellen Sie **Clouddienstadministratoren** Gruppe, und fügen Sie alle Konten hinzu, die Zugriff auf Clouddienste im Internet erforderlich ist.

        2.  Laden Sie die PAW *proxy.pac* aus der Datei [TechNet Gallery](http://aka.ms/pawmedia) und veröffentlichen Sie es auf einer internen Website.

            > [!NOTE]
            > Sie benötigen zum Aktualisieren der *proxy.pac* Datei nach dem Herunterladen, um sicherzustellen, dass sie auf dem neuesten Stand und abgeschlossen ist.  
            > Microsoft veröffentlicht alle aktuellen Office365 und Azure-URLs im Büro [Supportcenter](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
            >
            > Sie müssen möglicherweise weitere gültige Internetziele für andere IaaS-Anbieter zu dieser Liste hinzufügen, aber nicht hinzufügen, Produktivität, Unterhaltung, Nachrichten, oder suchwebsites zu dieser Liste hinzufügen.
            >
            > Sie müssen auch die PAC-Datei um eine gültige Proxyadresse für diese Adressen verwenden aufzunehmen anpassen.

            > [!NOTE]
            > Sie können auch den Zugriff von der PAW auch über einen Webproxy umfassendem Schutz beschränken. Es wird nicht empfohlen dies selbst ohne PAC-Datei wie es nur den Zugriff für PAWs, während Sie mit dem Unternehmensnetzwerk verbunden sind eingeschränkt wird.

            Diese Anweisungen wird davon ausgegangen, dass Sie Internet Explorer (oder Microsoft Edge) verwenden für die Verwaltung von Office365, Azure und andere Cloud-Dienste. Microsoft empfiehlt, ähnliche Einschränkungen für 3rd Party Browsern, die Sie, für die Verwaltung benötigen konfigurieren. Web-Browser auf den PAWs sollte nur für die Verwaltung von Cloud-Diensten und niemals zum allgemeinen Webbrowsen verwendet werden.

        3.  Nach der Konfiguration der *proxy.pac* Datei, aktualisieren Sie die PAW-Konfiguration – Benutzer Gruppenrichtlinienobjekt.

            1.  Wechseln Sie zu Benutzer Configuration\Preferences\Windows Settings\Registry. Maustaste auf die Registrierung, und wählen Sie **neu** \> **Registrierungselement** und konfigurieren Sie die folgenden Einstellungen:

                1.  Aktion: Ersetzen

                2.  Struktur: Die HKEY_ CURRENT_USER

                3.  Schlüsselpfad: Software\Microsoft\Windows\CurrentVersion\Internet Settings

                4.  Wertname: AutoConfigUrl

                    > [!NOTE]
                    > Wählen Sie nicht die **Standard** auf der linken Seite der Wertname.

                5.  Werttyp: REG_SZ

                6.  Wertdaten: Geben Sie die vollständige URL in die *proxy.pac* Datei, z.B. http:// und den Namen der Datei – z.B. http://proxy.fabrikam.com/proxy.pac.  Die URL kann auch mit einer einzelnen Bezeichnung URL - z.B. http://proxy/proxy.pac sein.

                    > [!NOTE]
                    > Die PAC-Datei kann auch auf eine Dateifreigabe, mit der Syntax des file://server.fabrikan.com/share/proxy.pac gehostet werden, aber dies erfordert, sodass das file://-Protokoll dar. Finden Sie im Abschnitt "Hinweis: File://-based veralteten" dieses [Understanding Web Proxy Configuration](http://blogs.msdn.com/b/ieinternals/archive/2013/10/11/web-proxy-configuration-and-ie11-changes.aspx) Blog für Weitere Informationen zum Konfigurieren des erforderlichen Registrierungswerts.

                7.  Klicken Sie auf die **allgemeine** Registerkarte, und wählen Sie **dieses Element entfernen, wenn es nicht mehr angewendet wird**.

                8.  Auf der **allgemeine** wählen Registerkarte **Zielgruppenadressierung auf Elementebene**, und klicken Sie auf **Zielgruppenadressierung**.

                9. Klicken Sie auf **neues Element**, und wählen Sie **Sicherheitsgruppe**.

                10. Wählen Sie die Schaltfläche "...", und suchen Sie nach der **Clouddienstadministratoren** Gruppe.

                11. Klicken Sie auf **neues Element**, und wählen Sie **Sicherheitsgruppe**.

                12. Wählen Sie die Schaltfläche "...", und suchen Sie nach der **PAW Users** Gruppe.

                13. Klicken Sie auf die **PAW Users** Element, und klicken Sie auf **Elementoptionen**.

                14. Wählen Sie **ist nicht**.

                15. Klicken Sie auf **OK** im Fenster vorgesehen sind.

                16. Klicken Sie auf **OK** zum Abschließen der **AutoConfigUrl** Gruppenrichtlinieneinstellung.

    2.  Wenden Sie Windows10-Sicherheitsbaselines und Cloud-Dienst den Zugriff Link die sicherheitsgrundwerte für Windows und Cloud-Dienst zugreifen können (falls erforderlich) mit den richtigen Organisationseinheiten mithilfe der folgenden Schritteaus:

        1.  Extrahieren Sie den Inhalt der Windows10 Security Baselines ZIP-Datei.

        2.  Erstellen Sie diese Gruppenrichtlinienobjekte [Importieren der Richtlinie](https://technet.microsoft.com/en-us/library/cc753786.aspx) -Einstellungen und [Link](https://technet.microsoft.com/en-us/library/cc732979.aspx) gemäß der folgenden Tabelle. Verknüpfen Sie jede Richtlinie mit jedem Speicherort und stellen Sie sicher, die Reihenfolge der Tabelle entspricht (spätere Einträge in der Tabelle sollten später angewendet und mit höherer Priorität werden):

            **Richtlinien:**

            |||
            |-|-|
            |CM Windows10 – Domänensicherheit|N/v – jetzt nicht verknüpfen|
            |SCM Windows10 TH2 – Computer|Admin\Tier 0\Devices|
            ||Admin\Tier 1\Devices|
            ||Admin\Tier 2\Devices|
            |SCM Windows10 TH2 – BitLocker|Admin\Tier 0\Devices|
            ||Admin\Tier 1\Devices|
            ||Admin\Tier 2\Devices|
            |SCM Windows10 – Credential Guard|Admin\Tier 0\Devices|
            ||Admin\Tier 1\Devices|
            ||Admin\Tier 2\Devices|
            |SCM Internet Explorer – Computer|Admin\Tier 0\Devices|
            ||Admin\Tier 1\Devices|
            ||Admin\Tier 2\Devices|
            |PAW-Konfiguration – Computer|Admin\Tier 0\Devices (vorhanden)|
            ||Admin\Tier 1\Devices (neue Verknüpfung)|
            ||Admin\Tier 2\Devices (neue Verknüpfung)|
            |RestrictedAdmin erforderlich – Computer|Admin\Tier 0\Devices|
            ||Admin\Tier 1\Devices|
            ||Admin\Tier 2\Devices|
            |SCM Windows10 - Benutzer|Admin\Tier 0\Devices|
            ||Admin\Tier 1\Devices|
            ||Admin\Tier 2\Devices|
            |SCM Internet Explorer – Benutzer|Admin\Tier 0\Devices|
            ||Admin\Tier 1\Devices|
            ||Admin\Tier 2\Devices|
            |PAW-Konfiguration – Benutzer|Admin\Tier 0\Devices (vorhanden)|
            ||Admin\Tier 1\Devices (neue Verknüpfung)|
            ||Admin\Tier 2\Devices (neue Verknüpfung)|

            > [!NOTE]
            > Die "SCM Windows10 – Domäne Security" Gruppenrichtlinienobjekt mit der Domäne unabhängig von der PAW verknüpft werden kann, aber Sie wirkt sich auf die gesamte Domäne.

6.  **(Optional) **Weitere erforderliche Tools für Administratoren auf Ebene 1 installieren. Installieren Sie weitere Tools oder Skripts, die zum Ausführen von Aufgaben erforderlich. Sicherstellen, dass das Risiko einer Offenlegung von Anmeldeinformationen auf den Zielcomputern mit einem beliebigen Tool einhergeht, bevor auf einer paw installieren. Weitere Informationen zur Bewertung von Verwaltungstools und Risikos für Anmeldeinformationen durch Methoden finden Sie unter [auf dieser Seite](http://aka.ms/logontypes). Sicherstellen, dass um alle Installationsmedien die in der vertrauenswürdigen Quelle für Installationsmedien zu erhalten.

7.  Identifizieren Sie und erhalten Sie sicher zu, Software und Anwendungen, die für die Verwaltung benötigt.  Dies ähnelt den entsprechenden Aufgaben in Phase 1, aber einen umfassenderen Bereich aufgrund der größeren Anzahl von Anwendungen, Dienste und Systeme gesichert werden müssen.

    > [!NOTE]
    > Stellen Sie sicher, dass Sie diese neuen Anwendungen (einschließlich Webbrowsern) schützen, indem Sie zustimmen Schutzmaßnahmen von EMET darauf.

    Beispiele für zusätzliche Software und Anwendungen:

    -   Microsoft Azure PowerShell

    -   Office365 PowerShell (auch bekannt als Microsoft Online Services-Modul)

    -   Anwendung oder Dienst-Verwaltungssoftware basierend auf der Microsoft Management Console

    -   Proprietäre (nicht MMC-basierte) Anwendung oder Service Management-Software

        > [!NOTE]
        > Viele Anwendungen werden jetzt ausschließlich über Webbrowser, einschließlich viele Clouddienste verwaltet.  Obwohl dadurch die Anzahl der Anwendungen, die auf einer PAW installiert werden müssen, wird auch das Risiko von Interoperabilitätsproblemen der Browser eingeführt.  Sie müssen einen Nicht-Microsoft-Webbrowser auf bestimmten PAW-Instanzen, aktivieren Sie die Verwaltung bestimmter Dienste bereitstellen.  Wenn Sie einen zusätzlichen Webbrowser bereitstellen, stellen Sie sicher, dass Sie alle vertrauenswürdigen Quelle Prinzipien folgen und sichern den Browser gemäß den Sicherheitsinformationen des Herstellers.

8.  **(Optional) **Herunterladen und installieren Sie alle erforderlichen Verwaltungs-Agents.

    > [!NOTE]
    > Wenn Sie zusätzliche Verwaltungs-Agents (Überwachung, Sicherheit, konfigurationsverwaltung usw.) installieren möchten, ist es wichtig, sicherzustellen, dass die Verwaltungssystemen auf der gleichen Ebene als Domänencontroller und Identitätssysteme vertrauenswürdig sind. Weitere Informationen finden Sie im verwalten und Aktualisieren von PAWs.

9. Bewerten Sie Ihre Infrastruktur, um Systeme zu identifizieren, die zusätzliche Sicherheit Schutzmaßnahmen durch eine PAW erfordern.  Stellen Sie sicher, dass Sie wissen genau, welche Systeme geschützt werden müssen.  Stellen Sie kritische Fragen zu den Ressourcen selbst, wie z.B.:

    -   Wo befinden sich die Zielsysteme, die verwaltet werden müssen?  Sind sie in einem einzigen physischen Ort erfasst oder mit einem klar definierten Subnetz verbunden?

    -   Wie viele Systeme sind vorhanden?

    -   Führen Sie diese Systeme anderen Systemen abhängig (Virtualisierung, Speicher usw.), und wenn dies der Fall ist, wie werden diese Systeme verwaltet?  Wie werden die kritischen Systeme verfügbar gemacht werden, um diese Abhängigkeiten, und welche zusätzlichen Risiken durch diese Abhängigkeiten verbunden?

    -   Wie kritisch sind die verwalteten Dienste, und was ist Verlusten, wenn diese Dienste gefährdet sind?

        > [!NOTE]
        > Fügen Sie Ihre Clouddienste in dieser Bewertung - Angreifer Zielen immer häufiger auf unsichere cloudbereitstellungen und ist es besonders wichtig, dass Sie diese Dienste verwalten, wie Sie Ihre unternehmenskritischen lokalen Anwendungen sicher.

        Verwenden Sie diese Bewertung, um Systeme zu identifizieren, die zusätzlichen Schutz benötigen, und erweitern Sie Ihr PAW-Programm an den Administratoren dieser Systeme.  Beispiele für Systeme, die erheblich von der PAW-basierte Verwaltung profitieren enthalten SQL Server (lokal und SQL Azure), Personalabteilung Anwendungen und Finanzsoftware.

        > [!NOTE]
        > Wenn eine Ressource aus einem Windows-System verwaltet wird, kann mit einer PAW verwaltet werden, auch wenn die Anwendung selbst unter einem Betriebssystem als Windows oder auf einer Nicht-Microsoft-Cloud-Plattform ausgeführt wird.  Beispielsweise sollte der Besitzer eines Amazon Web Services-Abonnements nur eine PAW verwenden, dieses Konto zu verwalten.

10. Entwickeln Sie eine Anforderungs- und Verteilungsmethode Methode für die Bereitstellung von PAWs in großem Umfang in Ihrer Organisation.  Abhängig von der Anzahl der PAWs, die Sie in Phase 2 bereitstellen möchten, müssen Sie möglicherweise den Prozess automatisieren.

    -   Erwägen Sie die Entwicklung, einen formellen Anforderungs- und Genehmigungsprozess für Administratoren, mit denen eine PAW zu erhalten.  Dieser Prozess können Sie den Bereitstellungsprozess standardisieren, Verantwortlichkeit für PAW-Geräte sicherstellen und Lücken in der PAW-Bereitstellung zu identifizieren.

    -   Wie bereits erwähnt, sollte diese Lösung für die Bereitstellung unabhängig von vorhandenen Automatisierungsmethoden (die bereits gefährdet sind möglicherweise) und in Phase 1 beschriebenen Prinzipien befolgen.

        > [!NOTE]
        > Jedes System, das Ressourcen verwaltet, sollten sich auf der gleichen oder einer höheren Vertrauensebene verwaltet.

11. Überprüfen und ggf. zusätzliche Profile bereitstellen.  Das Hardwareprofil, die, das Sie für Phase 1 ausgewählt haben, möglicherweise nicht für alle Administratoren geeignet.  Überprüfen Sie die Hardwareprofile, und wählen Sie ggf. zusätzliche Profile aus, um die Anforderungen der Administratoren zu erfüllen.  Z.B. das dedizierte Hardware-Profil (Trennung von PAWS und täglich verwenden Arbeitsstationen) ist möglicherweise nicht für einen Administrator, der viel unterwegs – in diesem Fall können Sie die gleichzeitige Verwendung Profil (PAW mit Benutzer-VM) für diesen Administrator bereitstellen.

12. Berücksichtigen Sie die Kultur, Betrieb, Kommunikation und die mit einer erweiterte PAW-Bereitstellung einhergehen.   Eine so wesentliche Änderung an einem Verwaltungsmodell erfordert naturgemäß auch Änderungsmanagement zu einem gewissen Grad, und es ist wichtig, die in das Bereitstellungsprojekt selbst zu erstellen.  Mindestens die folgenden Punkte:

    -   Wie kommunizieren Sie die Änderungen an die Führungsebene, um sicherzustellen, dass ihre Unterstützung?  Ein Projekt, das ohne Führungskräften unterstützt wahrscheinlich Fehler auf, oder die zumindest kämpfen Finanzierung und allgemeine Akzeptanz.

    -   Wie werden Sie den neuen Prozess für Administratoren dokumentieren?  Diese Änderungen müssen dokumentiert und mitgeteilt werden, nicht nur den vorhandenen Administratoren (die müssen ihre Gewohnheiten ändern und Verwalten von Ressourcen auf andere Weise), sondern auch neuen Administratoren (die die Organisation befördert oder innerhalb).  Es ist wichtig, dass die Dokumentation klar ist und die Bedeutung von Bedrohungen, die Rolle von PAWS zum Schutz der Administratoren und wie Sie die richtige Verwendung vollständig paws.

        > [!NOTE]
        > Dies ist besonders wichtig bei Rollen mit hoher Umsatz, einschließlich, aber nicht beschränkt auf Helpdeskmitarbeitern.

    -   Wie stellen sicher Sie die Kompatibilität mit den neuen Prozess?  Während das PAW-Modell eine Reihe von technischen Kontrollmechanismen, um zu verhindern, dass die Offenlegung privilegierter Anmeldeinformationen enthält, ist es unmöglich, alle möglichen gefährdungen allein mit technischen Mitteln vollständig zu verhindern.  Obwohl es möglich, um zu verhindern, dass einen Administrator an einem Benutzerdesktop mit privilegierten Anmeldeinformationen erfolgreich angemeldet ist, kann z.B. allein der Versuch der Anmeldung die Anmeldeinformationen für eine Schadsoftware auf diesem Computer verfügbar machen.  Daher ist es wichtig, dass Sie nicht nur die Vorteile des PAW-Modells, sondern auch die Risiken der Nichtkompatibilität zu gliedern.  Dies sollte ergänzt werden, durch Überwachungs- und Warnungsfunktionen, sodass Offenlegung von Anmeldeinformationen schnell erkannt und behoben werden kann.

#### <a name="phase-3-extend-and-enhance-protection"></a>Phase 3: Erweitern Sie und verbessern Sie des Schutzes
Einsatzbereich: Diese Schutzmaßnahmen erweitern die Systeme in Phase 1, dadurch unterstützt den grundlegenden Schutz mit erweiterten Features, einschließlich mehrstufige Authentifizierung und Netzwerkzugriffsregeln.

> [!NOTE]
> In dieser Phase kann jederzeit nach Abschluss der Phase 1 ausgeführt werden.  Es ist nicht Beendigung von Phase 2 abhängig und kann daher vor dem durchgeführt, gleichzeitig mit oder nach Phase 2.

Gehen Sie folgendermaßen vor, um diese Phase zu konfigurieren:

1.  Aktivieren Sie die mehrstufige Authentifizierung für privilegierte Konten.  Mehrstufige Authentifizierung verstärkt die kontosicherheit dem Benutzer ein physisches Token neben Anmeldeinformationen bereitstellen.  Multi-Factor Authentication ergänzt Authentifizierungsrichtlinien sehr gut, aber es hängt nicht Authentifizierungsrichtlinien für die Bereitstellung (und, Authentifizierungsrichtlinien erfordern auch keine Multi-Factor Authentication).  Microsoft empfiehlt die Verwendung einer der folgenden Formen der mehrstufigen Authentifizierung:

    -   **Smart Card**: eine Smartcard ist ein Manipulationssicheres, tragbares physisches Gerät und dadurch eine zweite Überprüfung während des Anmeldevorgangs für Windows.  Dass ein Benutzer für die Anmeldung eine Karte besitzen, können Sie das Risiko von gestohlenen Anmeldeinformationen Remote wiederverwendet werden reduzieren.  Ausführliche Informationen zu Smartcard-Anmeldung in Windows finden Sie im Artikel [Smart Card Overview](https://technet.microsoft.com/en-us/library/hh831433.aspx).

    -   **Virtuelle Smartcard**: eine virtuelle Smartcard bietet die gleichen Sicherheitsvorteile wie physische Smartcards mit den zusätzlichen Vorteil auf bestimmte Hardware verknüpft wird.  Ausführliche Informationen zu Bereitstellung und Hardwareanforderungen finden Sie in den Artikeln [Virtual Smart Card Overview](https://technet.microsoft.com/en-us/library/dn593708.aspx) und [erste Schrittemit virtuellen Smartcards: Handbuch mit exemplarischer Vorgehensweise](https://technet.microsoft.com/en-us/library/dn579260.aspx).

    -   **Microsoft Passport**: Microsoft Passport können Benutzer, die für die Authentifizierung bei einem Microsoft-Konto, ein Active Directory-Konto, Microsoft Azure Active Directory (Azure AD)-Konto oder Nicht-Microsoft-Dienst, der Fast ID Online (FIDO)-Authentifizierung unterstützt. Nach einer anfänglichen zweistufigen Überprüfung bei der Microsoft Passport-Registrierung ein Microsoft Passport auf dem Gerät des Benutzers eingerichtet wird, und der Benutzer legt eine Geste, die Windows Hello oder eine PIN sein kann. Microsoft Passport-Anmeldeinformationen handelt es sich um ein asymmetrisches Schlüsselpaar, die innerhalb der isolierten Umgebungen von Trusted Platform Modules (TPMs) generiert werden kann.
        Weitere Informationen zu Microsoft Passport [Microsoft Passport – Überblick](https://technet.microsoft.com/en-us/library/dn985839%28v=vs.85%29.aspx) Artikel.

    -   **Azure Multi-Factor Authentication**: Azure Multi-Factor Authentication (MFA) bietet die Sicherheit von einem zweiten überprüfungsfaktors sowie die erweiterten Schutz durch Überwachung und Machine Learning-basierte Analysen.  Azure MFA kann nicht nur Azure-Administratoren, sondern auch viele andere Lösungen schützen, z.B. Webanwendungen, Azure Active Directory und lokale Lösungen wie Remotezugriff und Remotedesktop.  Weitere Informationen zu Azure Multi-Factor Authentication, finden Sie im Artikel [Multi-Factor Authentication](https://azure.microsoft.com/en-us/services/multi-factor-authentication).

2.  **Positivliste vertrauenswürdige Anwendungen über Device Guard und/oder AppLocker**.  Durch die Möglichkeit einschränken von nicht vertrauenswürdigen oder nicht signierter Code auf einer PAW ausgeführt, können Sie außerdem die Wahrscheinlichkeit schädlicher Aktivitäten und gefährdungen verringern.  Windows enthält zwei primäre Optionen für die anwendungssteuerung:

    -   **AppLocker**: mit AppLocker können Administratoren steuern, welche Anwendungen auf einem bestimmten System ausgeführt werden können.  AppLocker kann werden zentral durch eine Gruppenrichtlinie gesteuert und auf bestimmte Benutzer oder Gruppen (für die Zielanwendung für Benutzer von PAWs) angewendet.  Weitere Informationen zu AppLocker finden Sie im TechNet-Artikel [AppLocker: Übersicht](https://technet.microsoft.com/library/hh831440.aspx).

    -   **Deviceguard**: das neue Device Guard-Feature bietet erweiterte hardwarebasierte anwendungssteuerung, die im Gegensatz zu AppLocker nicht überschrieben werden kann, auf dem betroffenen Gerät.  Ebenso wie AppLocker kann Device Guard über eine Gruppenrichtlinie gesteuert und auf bestimmte Benutzer ausgerichtet werden.  Weitere Informationen zum Einschränken der anwendungsnutzung mit Device Guard finden Sie im TechNet-Artikel [Device Guard-Bereitstellungshandbuch](https://technet.microsoft.com/en-us/library/mt463091(v=vs.85).aspx).

3.  **Mit der geschützten Benutzer, Authentifizierungsrichtlinien und Authentifizierungssilos weiteren Schutz von privilegierten Konten**.  Die Member der geschützten Benutzer gelten zusätzliche Sicherheitsrichtlinien, die die Anmeldeinformationen schützen befinden sich in der lokalen Sicherheits-Agent (LSA) und erheblich Minimieren des Risikos der Diebstahl und Wiederverwendung.  Authentifizierungsrichtlinien und Silos steuern, wie Benutzer Zugriff auf Ressourcen in der Domäne.  Gemeinsamem Einsatz Stärken diese Schutzmaßnahmen erheblich die kontosicherheit dieser Benutzer.  Weitere Informationen zu diesen Features finden Sie unter Webartikel [How to Configure Protected Accounts](https://technet.microsoft.com/en-us/library/dn518179.aspx).

    > [!NOTE]
    > Diese Schutzmaßnahmen zu ergänzen, nicht ersetzen, vorhandenen Sicherheitsmaßnahmen in Phase 1.  Administratoren sollten weiterhin getrennte Konten für Verwaltung und allgemeine Nutzung verwenden.

### <a name="managing-and-updating-paws"></a>Verwalten und Aktualisieren von PAWs
PAWs müssen Anti-Malware-Funktionen und Softwareupdates müssen schnell angewendet werden, um die Integrität dieser Arbeitsstationen zu erhalten.

Zusätzliche Konfigurationsschritte, operative Überwachung und Verwaltung der Sicherheit können auch auf den paws verwendet werden, aber die Integration dieser muss sorgfältig berücksichtigt werden, da jede Verwaltungsfunktion Risiko einer Gefährdung der PAW über dieses Tool eingeführt. Ob es sinnvoll, erweiterte Verwaltungsfunktionen einzuführen, hängt von einer Reihe von Faktoren ab:

-   Der Sicherheitsstatus und -Verfahren des Verwaltungstools (einschließlich Softwareupdateverfahren für das Tool, Administratorrollen und Konten in diesen Rollen, Betriebssysteme, die das Tool gehostet oder verwaltet und anderen Hardware oder Software Abhängigkeiten des Tools)

-   Die Häufigkeit und Umfang von softwarebereitstellungen und -Updates auf den PAWs

-   Anforderungen an detaillierte Bestands- und Konfigurationsinformationen Informationen

-   Anforderungen an die Sicherheitsüberwachung

-   Organisationsinterne Standards und weitere organisationsspezifische Faktoren

Das Prinzip der vertrauenswürdigen Quelle müssen allen Tools zum Verwalten und Überwachen der PAWs verwendet vertrauenswürdigen mindestens die Ebene der paws vertraut sein. Dies erfordert in der Regel diese Tools über eine paw erfolgt, um sicherzustellen, dass keine sicherheitsabhängigkeiten von Arbeitsstationen der unteren Rechte verwaltet werden.

Diese Tabelle erläutert die verschiedene Vorgehensweisen, die zum Verwalten und Überwachen der PAWs verwendet werden können:

|Vorgehensweise|Überlegungen|
|------|---------|
|Standardmäßig in PAW<br /><br />– Windows Server Update Services<br />-Windows Defender|– Keine Zusatzkosten<br />– Führt erforderliche grundlegende Sicherheitsfunktionen<br />– Anweisungen in diesem Leitfaden enthalten|
|Verwalten mit [Intune](https://technet.microsoft.com/en-us/library/jj676587.aspx)|<ul><li>Bietet cloudbasierte Transparenz und Kontrolle<br /><br /><ul><li>Bereitstellung von Software</li><li>Verwaltung von Softwareupdates</li><li>Windows-Firewall-Gruppenrichtlinien-Verwaltungskonsole</li><li>Schutz vor malware</li><li>Remoteunterstützung</li><li>Softwarelizenzverwaltung.</li></ul></li><li>Keine Serverinfrastruktur erforderlich</li><li>Erfordert "Konnektivität zum Cloud-Dienste aktivieren", die Schrittein Phase 2</li><li>Wenn der PAW-Computer einer Domäne angehört, dies ist erforderlich, die lokalen Images mithilfe der im Download Sicherheitsbaseline bereitgestellten Tools die SCM-Baselines zuweisen.</li></ul>|
|Neue Instanzen von System Center zum Verwalten der PAWs|– Bietet Transparenz und Kontrolle für Konfiguration, softwarebereitstellung und Sicherheitsupdates<br />– Erfordert separate Serverinfrastruktur, Sichern es auf Ebene der PAWs und diese sehr privilegierten Mitarbeiter gesichert|
|Verwalten von PAWs mit vorhandenen Verwaltungstools|– Erhöht das Risiko einer Gefährdung der PAWs, sofern die vorhandene Verwaltungsinfrastruktur Sicherheitsstufe von PAWs hochgestuft wird erstellt **Hinweis:** Microsoft würde in der Regel davon abgeraten, diese Vorgehensweise, wenn Ihre Organisation einen bestimmten Grund dafür ist. Nach unserer Erfahrung ist in der Regel eine sehr hohe kostspielig, all diese Tools (und ihre sicherheitsabhängigkeiten) bis auf die gleiche Sicherheitsebene der PAWs zu.<br />– Die meisten dieser Tools bieten Transparenz und Kontrolle für Konfiguration, softwarebereitstellung und Sicherheitsupdates|
|Für Sicherheitsüberprüfung und Überwachungstools, die Administratorzugriff erfordern|Enthält alle Tools, die einen Agent installieren oder ein Konto mit lokalem Administratorzugriff erforderlich.<br /><br />– Erfordert Tool Sicherheitsgarantie bis Ebene der PAWs zu portieren.<br />– Möglicherweise muss die Sicherheitsebene der PAWs Tool-Funktionalität unterstützen (Öffnen Sie die Ports, installieren Sie Java oder anderer Middleware usw.), erstellen einen Kompromiss sicherheitsentscheidung|
|Sicherheit und Ereignis-Management (SIEM-Lösung)|<ul><li>Wenn SIEM-Lösung ohne Agents wird<br /><br /><ul><li>Zugriff auf Ereignisse auf PAWs ohne Administratorrechte können mit einem Konto in der **Ereignisprotokollleser** Gruppe</li><li>Erfordert das Öffnen von Netzwerkports zum Zulassen von eingehendem Datenverkehr von den SIEM-Servern</li></ul></li><li>Wenn SIEM einen Agent erfordert, finden Sie unter anderen Zeile **Security Scanning or Monitoring Tools, die Administratorzugriff erfordern**.</li></ul>|
|Windows-Ereignisweiterleitung|– Stellt eine Methode ohne Agents zum Weiterleiten von Sicherheitsereignissen von den PAWs an einen externen Datensammler oder eine SIEM-Lösung<br />-Ereignisse auf PAWs ohne Administratorrechte möglich<br />– Erfordert keinen Öffnen von Netzwerkports zum Zulassen von eingehendem Datenverkehr von den SIEM-Servern|

#### <a name="operating-paws"></a>Betriebssystem von PAWs
Die PAW-Lösung sollte den Standards unter betrieben werden [betriebliche Standards](http://aka.ms/securitystandards) basierend auf dem Prinzip der vertrauenswürdigen Quelle.

## <a name="related-topics"></a>Verwandte Themen
[Interessante Cybersicherheit Microsoft](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)

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

[Trusted Platform Module](C:\sd\docs\p_ent_keep_secure\p_ent_keep_secure\trusted_platform_module_technology_overview.xml)
