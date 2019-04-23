---
title: Warum können Privileged Access Workstations Schützen Ihrer Organisation
description: Wie kann PAW Sicherheitsstatus Ihrer Organisation steigern
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 93589778-3907-4410-8ed5-e7b6db406513
ms.date: 02/14/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: fd87ef674fcfefa8e2dc1d7122de64ed8f5510a0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891261"
---
# <a name="privileged-access-workstations"></a>Arbeitsstationen mit privilegiertem Zugriff

>Gilt für: Windows Server

Arbeitsstationen mit privilegiertem Zugriff (Privileged Access Workstations, PAWs) stellen ein dediziertes Betriebssystem für sensible Aufgaben bereit, das vor Angriffen aus dem Internet und der Übertragung von Bedrohungen geschützt ist. Die Trennung dieser sensiblen Aufgaben und Konten von den Arbeitsstationen und Geräten für den täglichen Gebrauch bietet ein sehr hohes Maß an Schutz vor Phishingangriffen, Sicherheitsrisiken bei Anwendungen und Betriebssystemen, Angriffen durch Identitätsvortäuschung und Diebstahl von Anmeldeinformationen, beispielsweise durch Aufzeichnung von Tastaturanschlägen sowie [Pass-the-Hash](https://www.microsoft.com/en-us/download/details.aspx?id=36036)- und [Pass-the-Ticket](https://download.microsoft.com/download/7/7/A/77ABC5BD-8320-41AF-863C-6ECFB10CB4B9/Mitigating%20Pass-the-Hash%20(PtH)%20Attacks%20and%20Other%20Credential%20Theft%20Techniques_English.pdf)-Mechanismen.

## <a name="what-is-a-privileged-access-workstation"></a>Was ist eine Arbeitsstation mit privilegiertem Zugriff?

Einfach gesagt ist eine Arbeitsstation mit privilegiertem Zugriff (Privileged Access Workstation, PAW) eine gesicherte und gesperrte Arbeitsstation, die ein Höchstmaß an Sicherheit für sensible Konten und Aufgaben bietet.  PAWs empfehlen sich für die Verwaltung von Identitätssystemen, Clouddiensten und privaten Cloudfabrics ebenso wie für vertrauliche Geschäftsfunktionen.

> [!NOTE]
> Die PAW-Architektur erfordert keine 1:1-Zuordnung von Konten zu Arbeitsstation, obwohl dies eine häufige Konfiguration ist. Mit einer PAW wird eine vertrauenswürdige Arbeitsstationsumgebung erstellt, die von einem oder mehreren Konten verwendet werden kann.

Um die größtmögliche Sicherheit zu gewährleisten, sollten PAWs immer die aktuellste und sichere Betriebssysteme ausführen: Microsoft empfiehlt dringend, Windows 10 Enterprise, enthält eine Anzahl von zusätzliche Sicherheitsfeatures, die in anderen Editionen nicht verfügbar (insbesondere [Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) und [Device Guard](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx)).

> [!NOTE]
> Organisationen, in denen Windows 10 nicht zur Verfügung steht, können Windows 10 Pro verwenden. Diese Edition enthält viele der wichtigen grundlegenden Technologien für PAWs, wie z.B. vertrauenswürdiger Start, BitLocker und Remotedesktop.  Kunden im Bildungswesen können Windows 10 Education verwenden.  Windows 10 Home sollte für eine PAW nicht verwendet werden.
>
> Eine Vergleichsmatrix der verschiedenen Editionen von Windows 10 finden Sie [in diesem Artikel](https://www.microsoft.com/en-us/WindowsForBusiness/Compare).

Die Sicherheitsmechanismen auf PAWs wurden dazu konzipiert, die wahrscheinlichsten Gefährdungsrisiken mit den größten Auswirkungen zu minimieren. Hierzu gehört die Minimierung von Angriffen auf die Umgebung und die Minimierung des Risikos, dass die Kontrollmechanismen auf den PAWs im Lauf der Zeit weniger greifen:

* **Angriffe aus dem Internet**: Die meisten Angriffe stammen direkt oder indirekt aus Internetquellen und nutzen das Internet zum Datendiebstahl und für C2-Angriffe (Command and Control). Die Isolierung der PAW vom Internet ist ein wesentliches Element, um sicherzustellen, dass die PAW nicht gefährdet wird.
* **Einsatzfähigkeit**: Wenn eine PAW zu kompliziert und schwierig zu verwenden ist, sind Administratoren wahrscheinlich geneigt, sich Problemumgehungen auszudenken, um ihre Arbeit zu erleichtern. Solche Problemumgehungen führen häufig dazu, dass die Arbeitsstationen für Administratoren und die Administratorkonten erheblichen Sicherheitsrisiken ausgesetzt werden. Daher ist es von entscheidender Bedeutung, die PAW-Benutzer einzubeziehen und zu schulen, um solche Probleme bei der Verwendung sicher zu minimieren. Oft genügt es schon, das Feedback der Benutzer zu beachten, die Tools und Skripts zu installieren, die sie für ihre Aufgaben benötigen, und sicherzustellen, dass allen Administratoren bewusst ist, was eine PAW ist, warum sie eine PAW verwenden müssen und wie sie diese richtig und erfolgreich verwenden.
* **Risiken durch die Umgebung**: Da viele andere Computer und Konten in einer Umgebung direkt oder indirekt Risiken durch das Internet ausgesetzt sind, muss eine PAW vor Angriffen von kompromittierte Assets in der Produktionsumgebung geschützt werden. Daher müssen die Verwaltungstools und -konten, die auf PAWs zugreifen können, auf das absolute Minimum reduziert werden, das für zum Sichern und Überwachen dieser speziellen Arbeitsstationen erforderlich ist.
* **Manipulationen aus der Lieferkette**: Es ist unmöglich, sämtliche möglichen Manipulationsrisiken aus der Lieferkette für Hardware und Software zu entfernen. Allerdings lassen sich kritische Angriffsvektoren, die potenziellen Angreifern problemlos zur Verfügung stehen, mit einigen entscheidenden Aktionen erheblich minimieren. Hierzu gehört die Überprüfung sämtlicher Installationsmedien ([Prinzip der vertrauenswürdigen Quelle](http://aka.ms/cleansource)) und die Zusammenarbeit mit einem vertrauenswürdigen und seriösen Lieferanten für Hardware und Software.
* **Physische Angriffe**: Das PAWs mobil sein und außerhalb der physisch gesicherten Umgebung verwendet werden können, müssen sie vor Angriffen geschützt werden, die sich einen nicht autorisierten physischen Zugriff auf den Computer zunutze machen.

> [!NOTE]
> Eine PAW kann eine Umgebung nicht vor einem Angreifer schützen, der bereits administrativen Zugriff über eine Active Directory-Gesamtstruktur erhalten hat.
> Da viele vorhandene Implementierungen der Active Directory Domain Services seit Jahren mit dem Risiko des Diebstahls von Anmeldeinformationen betrieben werden, müssen Organisationen von einer Sicherheitslücke ausgehen und die Möglichkeit in Betracht ziehen, dass die eine bisher unerkannte Gefährdung der Anmeldeinformationen eines Domänen- oder Unternehmensadministrators besteht. Eine Organisation, die eine Gefährdung ihrer Domäne vermutet, sollte den Einsatz von Expertendiensten zur Behebung von Incidents erwägen.
>
> Weitere Informationen zur Reaktion auf und Wiederherstellung nach Incidents finden Sie im Whitepaper [Mitigating Pass-the-Hash and Other Credential Theft](https://www.microsoft.com/pth), Version 2 (Minimieren von Pass-the-Hash-Vorfällen und anderen Methoden des Anmeldeinformationsdiebstahls), in den Abschnitten zur Reaktion auf verdächtige Aktivitäten und zur Wiederherstellung nach einem Sicherheitsvorfall.
>
> Weitere Informationen finden Sie auf der [Microsoft-Seite zur Reaktion auf und Wiederherstellung nach Incidents](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

### <a name="paw-hardware-profiles"></a>PAW-Hardwareprofile

Administratoren sind auch Standardbenutzer – sie benötigen also nicht nur eine PAW, sondern auch eine standardmäßige Benutzerarbeitsstation, um E-Mails zu lesen, im Internet zu suchen und auf Branchenanwendungen zuzugreifen.  Für den Erfolg einer PAW-Bereitstellung ist es entscheidend, dass Administratoren sowohl sicher als auch produktiv arbeiten können.  Eine sichere Lösung, die die Produktivität massiv einschränkt, wird von den Benutzern abgelehnt. Stattdessen werden die Benutzer eine Lösung nutzen, die ihre Produktivität erweitert – auch wenn dies auf Kosten der Sicherheit geht.

Um für ein optimales Verhältnis zwischen Sicherheit und Produktivität zu sorgen, empfiehlt Microsoft die Verwendung eines der folgenden PAW-Hardwareprofile:

* **Dedizierte Hardware**: Separate, dedizierte Geräte für Benutzeraufgaben und Verwaltungsaufgaben.
* **Gleichzeitige Verwendung**: Ein einziges Gerät, auf dem mithilfe der Virtualisierung per Betriebssystem oder per Präsentation Benutzer- und Verwaltungsaufgaben gleichzeitig ausgeführt werden können.

Organisationen können nur eines der Profile oder beide verwenden. Es bestehen keine Interoperabilitätsprobleme zwischen den Hardwareprofilen, und Organisationen können ein Hardwareprofil flexibel an die besonderen Anforderungen eines bestimmten Administrators anpassen.

> [!NOTE]
> In all diesen Szenarien ist es von entscheidender Bedeutung, dass Administratoren auch ein Standardbenutzerkonto erhalten, das von den designierten Administratorkonten getrennt ist. Ein Administratorkonto sollte nur unter dem administrativen Betriebssystem der PAW verwendet werden.

Die folgende Tabelle bietet eine Übersicht über die jeweiligen Vor- und Nachteile der Hardwareprofile hinsichtlich der operativen Benutzerfreundlichkeit sowie der Produktivität und Sicherheit.  Beide Ansätze bieten eine hohe Sicherheit und schützen Administratorkonten vor Diebstahl und Wiederverwendung von Anmeldeinformationen.

|**Szenario**|**Vorteile**|**Nachteile**|
|--------|---------|-----------|
|Dedizierte Hardware|– Starkes Signal für die Vertraulichkeit von Aufgaben<br />– Strikteste Trennung zur Sicherheit|– Zusätzlicher Platzbedarf<br />– Höheres Gewicht (bei Remotearbeit)<br />– Hardwarekosten|
|Gleichzeitige Verwendung|– Geringere Hardwarekosten<br />– Nur ein Gerät erforderlich|– Gemeinsame Nutzung einer einzigen Tastatur und Maus erhöht das Risiko unbeabsichtigter Fehler und Risiken|

Dieser Leitfaden enthält detaillierte Anweisungen für die PAW-Konfiguration für den Ansatz mit dedizierter Hardware. Wenn Sie Hardwareprofile für die gleichzeitige Verwendung benötigen, können Sie die Anweisungen in diesem Leitfaden selbst entsprechend anpassen oder einen professionellen Dienstleister wie z.B. Microsoft mit der Einrichtung beauftragen.

#### <a name="dedicated-hardware"></a>Dedizierte Hardware

In diesem Szenario wird eine PAW für die Verwaltung verwendet, die vollständig von dem PC für tägliche Aktivitäten wie E-Mail, Dokumentbearbeitung und Entwicklung getrennt ist. Alle Verwaltungstools und -anwendungen werden auf der PAW installiert, alle Produktivitätsanwendungen auf der Standardarbeitsstation des Benutzers. Die Schrittanweisungen in diesem Leitfaden basieren auf diesem Hardwareprofil.

#### <a name="simultaneous-use---adding-a-local-user-vm"></a>Gleichzeitige Verwendung: Hinzufügen eines lokalen Benutzers VM

In diesem Szenario der gleichzeitigen Verwendung wird ein einziger PC sowohl für Verwaltungsaufgaben als auch für tägliche Aktivitäten wie E-Mail, Dokumentbearbeitung und Entwicklung eingesetzt. In dieser Konfiguration ist das Betriebssystem des Benutzers auch offline verfügbar (zum Bearbeiten von Dokumenten und zum Arbeiten mit lokal zwischengespeicherten E-Mails), erfordert jedoch Hardware und Supportprozesse, die den Offlinezustand unterstützen.

![Diagramm das zeigt, dass ein einziger PC in einem Szenario der gleichzeitigen Verwendung sowohl für Verwaltungsaufgaben als auch für tägliche Aktivitäten wie E-Mail, Dokumentbearbeitung und Entwicklung eingesetzt wird](../media/privileged-access-workstations/PAWFig10.JPG)

Auf der physischen Hardware werden lokal zwei Betriebssysteme ausgeführt:

* **Administratorbetriebssystem:** Auf dem physischen PAW-Host wird Windows 10 für Verwaltungsaufgaben ausgeführt.
* **Benutzerbetriebssystem**: Auf einem virtuellen Hyper-V-Clientgastcomputer unter Windows 10 wird ein Unternehmensimage ausgeführt.

Mit Windows 10 Hyper-V, kann eine Gast-VM (auch unter Windows 10) eine umfassenden Benutzeroberfläche, einschließlich von Audio-, Video- und wie Skype for Business verfügen.

In dieser Konfiguration werden tägliche Aufgaben, für die keine Administratorrechte erforderlich sind, auf dem virtuellen Computer mit dem Benutzerbetriebssystem ausgeführt, auf dem ein standardmäßiges Windows 10-Unternehmensimage installiert ist und das nicht den Einschränkungen unterliegt, die für den PAW-Host gelten. Alle Verwaltungsaufgaben werden im Administratorbetriebssystem ausgeführt.

Um dieses Setup zu konfigurieren, führen Sie die Schritte in dieser Anleitung für den PAW-Host aus, fügen Sie Hyper-V-Funktionen für Clients hinzu, erstellen Sie einen virtuellen Benutzercomputer, und installieren Sie dann ein Windows 10-Unternehmensimage auf dem virtuellen Benutzercomputer.

Lesen Sie den Artikel [Hyper-V für Clients](https://technet.microsoft.com/library/hh857623.aspx), um weitere Informationen zu dieser Funktion zu erhalten. Beachten Sie, dass das Betriebssystem auf virtuellen Gastcomputern gemäß der [Microsoft-Produktlizenzierung](https://www.microsoft.com/en-us/Licensing/product-licensing/products.aspx) lizenziert werden muss, die auch [hier](https://www.microsoft.com/en-us/Licensing/learn-more/brief-windows-virtual-machine.aspx) beschrieben wird.

#### <a name="simultaneous-use---adding-remoteapp-rdp-or-a-vdi"></a>Gleichzeitige Verwendung: Hinzufügen von RemoteApp, RDP oder einer VDI

In diesem Szenario der gleichzeitigen Verwendung wird ein einziger PC sowohl für Verwaltungsaufgaben als auch für tägliche Aktivitäten wie E-Mail, Dokumentbearbeitung und Entwicklung eingesetzt. In dieser Konfiguration werden die Benutzerbetriebssysteme zentral bereitgestellt und verwaltet (in der Cloud oder im Rechenzentrum), sind aber offline nicht verfügbar.

![Abbildung die zeigt, dass ein einziger PC in einem Szenario der gleichzeitigen Verwendung sowohl für Verwaltungsaufgaben als auch für tägliche Aktivitäten wie E-Mail, Dokumentbearbeitung und Entwicklung eingesetzt wird](../media/privileged-access-workstations/PAWFig11.JPG)

Auf der physischen Hardware wird lokal ein einzelnes PAW-Betriebssystem für Verwaltungsaufgaben ausgeführt. Für Benutzeranwendungen wie E-Mail, Dokumentbearbeitung und Branchensoftware ist die Kontaktaufnahme mit einem Remotedesktopdienst von Microsoft oder einem Drittanbieter erforderlich.

In dieser Konfiguration werden tägliche Aufgaben, für die keine Administratorrechte erforderlich sind, in den Remotebetriebssystemen und -anwendungen ausgeführt, die nicht den Einschränkungen unterliegen, die für den PAW-Host gelten. Alle Verwaltungsaufgaben werden im Administratorbetriebssystem ausgeführt.

Befolgen Sie für diese Konfiguration die Anweisungen im vorliegenden Leitfaden für den PAW-Host, aktivieren Sie eine Netzwerkverbindung zu den Remotedesktopdiensten, und fügen Sie dann Verknüpfungen zum Benutzerdesktop der PAW hinzu, um den Zugriff auf die Anwendungen zu ermöglichen. Die Remotedesktopdienste können auf verschiedene Weise gehostet werden. Hier einige Beispiele:

* Als vorhandener Remotedesktop- oder VDI-Dienst (lokal oder in der Cloud)
* Als neuer Dienst, den Sie lokal oder in der Cloud installieren
* Azure RemoteApp unter Verwendung vorkonfigurierter Office 365-Vorlagen oder Ihrer eigenen Installationsimages

Weitere Informationen zu Azure RemoteApp finden Sie [auf dieser Seite](https://www.remoteapp.windowsazure.com).

## <a name="how-microsoft-is-using-administrative-workstations"></a>Wie Microsoft verwendet Arbeitsstationen für Administratoren

Microsoft verwendet PAW-Architekturen sowohl für die eigenen internen Systeme als auch für Kundensysteme. Microsoft verwendet Arbeitsstationen für Administratoren intern für eine Reihe von Funktionen, beispielsweise für die Verwaltung der Microsoft-IT-Infrastruktur, für die Entwicklung und den Betrieb der Microsoft-Cloudfabricinfrastruktur sowie für weitere wertvolle Assets.

Dieser Leitfaden basiert direkt auf der PAW-Referenzarchitektur, die von unseren Expertenteams für Cybersicherheit bereitgestellt wurde, um Kunden vor Cyberangriffen zu schützen. Die Arbeitsstationen für Administratoren sind auch ein wichtiges Element der stärksten Schutzfunktion für Aufgaben der Domänenverwaltung: der ESAE-Referenzarchitektur für Verwaltungsgesamtstrukturen (Enhanced Security Administrative Environment).

Informationen zur ESAE-Verwaltungsgesamtstruktur finden Sie unter [Schützen des privilegierten Zugriffs – Referenzmaterial](../securing-privileged-access/securing-privileged-access-reference-material.md) im Abschnitt [ESAE-basierter Ansatz für den Entwurf einer administrativen Gesamtstruktur](http://aka.ms/ESAE).

## <a name="architecture-overview"></a>Übersicht über die Architektur

Das Diagramm unten zeigt einen separaten „Kanal“ für die Verwaltung (eine höchst sensible Aufgabe), der durch Einrichten getrennter dedizierter Konten und Arbeitsstationen für die Verwaltung entsteht.

![Diagramm, das einen separaten „Kanal“ für die Verwaltung (eine höchst sensible Aufgabe) zeigt, der durch Einrichten getrennter dedizierter Konten und Arbeitsstationen für die Verwaltung entsteht](../media/privileged-access-workstations/PAWFig1.JPG)

Diese Architektur basiert auf den Schutzmaßnahmen der Windows 10-Funktionen [Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) und [Device Guard](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx) und geht für sensible Konten und Aufgaben weit über diese Maßnahmen hinaus.

Diese Methode eignet sich für Konten mit Zugriff auf hochwertige Assets:

* **Administratorrechte** -PAWs bieten erhöhte Sicherheit für weitreichenden administrative IT-Rollen und Aufgaben. Diese Architektur kann auf viele Arten von Systemen angewendet werden, wie z.B.: Active Directory-Domänen und -Gesamtstrukturen, Microsoft Azure Active Directory-Mandanten, Office 365-Mandanten, Prozesssteuerungsnetzwerke (Process Control Networks, PCNs), SCADA-Systeme (Supervisory Control and Data Acquisition), Geldautomaten und Verkaufsstellengeräte (Point of Sale, PoS).
* **Information Worker mit hoher** -Ansatz wird in eine PAW bieten auch Schutz für streng vertrauliche Information Worker-Aufgaben und Mitarbeiter, die im Zusammenhang mit vor Ankündigung Zusammenführungs- sowie Kaufszenarien Aktivität Vorabversion Finanzberichte, Präsenz der Organisation in sozialen Medien, Kommunikation der Geschäftsleitung, noch nicht patentierte Geschäftsgeheimnisse, vertrauliche Recherchen oder andere vertrauliche oder sensiblen Daten. Der vorliegende Leitfaden erläutert nicht die detaillierte Konfiguration solcher Information Worker-Szenarien, auch wird das Szenario nicht in den technischen Anweisungen behandelt.

    > [!NOTE]
    > Die Microsoft-IT-Abteilung verwendet PAWs (die intern als „Sichere Arbeitsstationen für Administratoren“ [Secure Admin Workstations, SAWs] bezeichnet werden), um den sicheren Zugriff auf diese wertvollen Microsoft-internen Systeme zu verwalten. Im Abschnitt „Verwendung von Arbeitsstationen für Administratoren bei Microsoft“ finden Sie weitere Informationen dazu, wie Microsoft PAWs einsetzt. Ausführlichere Informationen zu diesem Ansatz für eine Umgebung mit höchst wertvollen Assets finden Sie im Artikel [Schützen von wertvollen Assets mit sicheren Arbeitsstationen für Administratoren](https://msdn.microsoft.com/en-us/library/mt186538.aspx).

Das vorliegende Dokument erläutert, warum diese Vorgehensweise zum Schutz von privilegierten Konten mit weitreichenden Berechtigungen empfohlen wird, wie diese PAW-Lösungen zum Schutz von Administratorrechten aussehen und wie Sie schnell eine PAW-Lösung für die Verwaltung von Domänen- und Clouddiensten bereitstellen.

Dieses Dokument beschreibt zudem genau, wie verschiedene PAW-Konfigurationen implementiert werden, und bietet detaillierte Implementierungsanweisungen, damit Sie mit dem Schutz Ihrer Konten mit weitreichenden Berechtigungen beginnen können:

* [**Phase 1: sofortige Bereitstellung für Administratoren von Active Directory** ](#phase-1-immediate-deployment-for-active-directory-administrators) dadurch eine paw erfolgt schnell, die lokalen Administratorrollen für Domänen und Gesamtstrukturen schützen kann
* [**Phase 2: Erweitern der PAW auf alle Administratoren** ](#phase-2-extend-paw-to-all-administrators) dadurch Schutz für Administratoren von Clouddiensten wie Office 365 und Azure, Unternehmensservern, unternehmensanwendungen und Arbeitsstationen
* [**Phase 3: Erweiterte Sicherheit für PAWS** ](#phase-3-extend-and-enhance-protection) dies beschreibt zusätzliche Schutzmaßnahmen und Überlegungen zur Sicherheit von PAWS

### <a name="why-dedicated-workstations"></a>Warum dedizierte Arbeitsstationen?

In der heutigen Zeit sehen sich Organisationen immer mehr Bedrohungen durch ausgefeilte Phishingmethoden und andere Internetangriffe gegenüber, die ein kontinuierliches Sicherheitsrisiko für Konten und Arbeitsstationen mit Internetzugriff darstellen.

Aufgrund dieser Bedrohungen müssen Unternehmen Sicherheitsverletzungen sozusagen als „festen Bestandteil“ in ihre Überlegungen einbeziehen, wenn sie Schutzmaßnahmen für wertvolle Assets wie Administratorkonten und sensible Unternehmensressourcen einrichten. Diese wertvollen Assets müssen sowohl vor Bedrohungen aus dem Internet als auch vor Angriffen geschützt werden, die über andere Arbeitsstationen, Server und Geräte in der Umgebung erfolgen.

![Diese Abbildung zeigt das Risiko für verwaltete Assets, wenn ein Angreifer die Kontrolle über eine Benutzerarbeitsstation erhält, auf der vertrauliche Anmeldeinformationen verwendet werden](../media/privileged-access-workstations/PAWFig2.JPG)

Diese Abbildung zeigt das Risiko für verwaltete Assets, wenn ein Angreifer die Kontrolle über eine Benutzerarbeitsstation erhält, auf der vertrauliche Anmeldeinformationen verwendet werden.

Einem Angreifer, der die Kontrolle über ein Betriebssystem hat, stehen unzählige Möglichkeiten offen, unerlaubt Zugriff auf alle Aktivitäten auf der Arbeitsstation zu erhalten und die Identität des legitimen Kontos zu vorzutäuschen. Es gibt zahlreiche bekannte und noch nicht bekannte Angriffstechniken, mit denen ein Angreifer sich ein solches Maß an Zugriff verschaffen kann. Da Cyberangriffe immer zahlreicher und ausgefeilter werden, muss das Konzept der Trennung erweitert werden: Clientbetriebssysteme für sensible Konten müssen vollständig von der restlichen Umgebung getrennt werden. Weitere Details zu diesen Arten von Angriffen finden Sie auf der [Website zu Pass-the-Hash](https://www.microsoft.com/pth) mit Whitepapers, Videos und vielen weiteren Informationen.

Der PAW-Ansatz ist eine Erweiterung der empfohlenen und bereits gut etablierten Praxis, für Administratoren getrennte Administrator- und Benutzerkonten zu verwenden. Hier kommt ein individuell zugewiesenes Administratorkonto zum Einsatz, das vollständig vom Standardbenutzerkonto des Benutzers getrennt ist. PAWs bauen auf dieser Praxis auf, indem sie für solche sensiblen Konten eine vertrauenswürdige Arbeitsstation bereitstellen.

Der vorliegende Leitfaden zu Arbeitsstationen mit privilegiertem Zugriff unterstützt Sie dabei, diese Funktionalität zu implementieren, um wertvolle Konten wie z.B. IT-Administratorkonten mit hoher Berechtigungsstufe und hochsensible Geschäftskonten zu schützen. Der Leitfaden unterstützt Sie bei Folgendem:

* Einschränken der Offenlegung von Anmeldeinformationen auf vertrauenswürdige Hosts.
* Bereitstellen einer Arbeitsstation mit höchster Sicherheit für Administratoren, damit diese ihre Verwaltungsaufgaben problemlos und sicher ausführen können.

Indem Sie sicherstellen, dass sensible Konten ausschließlich auf gesicherten PAWs verwendet werden, bieten Sie diesen Konten eine solide Schutzmaßnahme, die sowohl die Nutzung durch Administratoren als auch die Verteidigung gegen Angriffe vereinfacht.

### <a name="alternate-approaches"></a>Alternative Ansätze

Dieser Abschnitt enthält Informationen zur Sicherheit alternativer Ansätze im Vergleich zu PAWs und beschreibt, wie solche Ansätze richtig in eine PAW-Architektur integriert werden. All diese Ansätze stellen ein erhebliches Risiko dar, wenn sie isoliert implementiert werden, können in einigen Szenarien aber einen wertvollen Beitrag zu einer PAW-Implementierung leisten.

#### <a name="credential-guard-and-windows-hello-for-business"></a>Credential Guard und Windows Hello for Business

[Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) wurde in Windows 10 eingeführt und verwendet hardware- und virtualisierungsbasierte Sicherheitsmechanismen, um häufige Methoden des Anmeldeinformationsdiebstahls, wie Pass-the-Hash, durch Schützen der abgeleiteten Anmeldeinformationen zu minimieren. Der private Schlüssel für die Anmeldeinformationen ein, die [Windows Hello for Business](http://aka.ms/passport) kann auch von Hardware, die Trusted Platform Module (TPM) geschützt werden.

Dies sind leistungsstarke Schutzmaßnahmen, aber Arbeitsstationen können immer noch anfällig für bestimmte Angriffe sein, auch wenn die Anmeldeinformationen durch Credential Guard oder Windows Hello for Business geschützt werden. Missbraucht, Berechtigungen und die Verwendung von Anmeldeinformationen direkt über ein kompromittiertes Gerät, zuvor gestohlene Anmeldeinformationen vor der Aktivierung von Credential Guard und den Missbrauch von Verwaltungstools und schwachen Anwendungskonfigurationen auf der Arbeitsstation Angriffen gehört.

Die Anleitungen für PAWs in diesem Abschnitt umfassen den Einsatz einer Vielzahl dieser Technologien für hochsensible Konten und Aufgaben.

#### <a name="administrative-vm"></a>Virtueller Verwaltungscomputer

Ein virtueller Verwaltungscomputer (Admin VM) ist ein dediziertes Betriebssystem für administrative Aufgaben auf einem standardbenutzerdesktop gehostet. Dieser Ansatz ähnelt der Verwendung einer PAW zwar in der Hinsicht, dass ein dediziertes Betriebssystem für administrative Aufgaben bereitgestellt wird, weist jedoch eine bedenkliche Schwachstelle auf: Die Sicherheit des virtuellen Verwaltungscomputers ist vom Standardbenutzerdesktop abhängig.

Das Diagramm unten veranschaulicht, wie ein Angreifer über einen virtuellen Verwaltungscomputer auf einer Benutzerarbeitsstation der Kontrollkette zum Zielobjekt folgen kann. Es zeigt auch, dass dies in der umgekehrten Konfiguration nahezu unmöglich ist.

Die PAW-Architektur sind nicht zulässig für das Hosten einer Admin-VM auf einer Benutzerarbeitsstation, allerdings kann eine Benutzer-VM mit einem standardmäßigen Unternehmensimage gehostet werden, auf die ein Administrator PAW, Mitarbeiter mit einem einzigen PC für alle Aufgaben bereitzustellen.

![Diagramm der PAW-Architektur](../media/privileged-access-workstations/PAWFig9.JPG)

#### <a name="jump-server"></a>Sprungbrettserver

In Verwaltungsarchitekturen mit Sprungbrettserver wird eine geringe Anzahl von Verwaltungskonsolenservern eingerichtet, die nur von bestimmten Mitarbeitern für Verwaltungsaufgaben verwendet werden dürfen. Eine solche Architektur basiert üblicherweise auf Remotedesktopdiensten, einer Drittanbieterlösung zur Virtualisierung per Präsentation oder einer VDI-Technologie (Virtual Desktop Infrastructure).

Dieser Ansatz wird häufig zur Minimierung von Verwaltungsrisiken vorgeschlagen und bietet einige Sicherheitsfunktionen. Allerdings ist das Sprungbrettserverkonzept selbst anfällig für bestimmte Angriffe, da es das [Prinzip der „vertrauenswürdigen Quelle“](http://aka.ms/cleansource) verletzt. Beim Prinzip der vertrauenswürdigen Quelle müssen alle Sicherheitsabhängigkeiten genauso vertrauenswürdig sein wie das zu sichernde Objekt.

![Abbildung, die eine einfache Kontrollbeziehung zeigt](../media/privileged-access-workstations/PAWFig3.JPG)

Diese Abbildung zeigt eine einfache Kontrollbeziehung. Jedes Subjekt, das ein Objekt kontrolliert, ist eine Sicherheitsabhängigkeit dieses Objekts. Wenn ein Angreifer sich Kontrolle über eine Sicherheitsabhängigkeit eines Zielobjekts (ein Subjekt) verschafft, erhält er damit auch die Kontrolle über dieses Objekt.

Die Verwaltungssitzung auf dem Sprungbrettserver ist von der Integrität des lokalen Computers abhängig, der auf die Sitzung zugreift. Wenn es sich bei diesem Computer um eine Arbeitsstation handelt, die Phishingangriffen oder anderen Angriffen aus dem Internet ausgesetzt sein kann, ist auch die Verwaltungssitzung diesen Risiken ausgesetzt.

![Abbildung die zeigt, wie Angreifer einer eingerichteten Kontrollkette folgen können, um zum gewünschten Zielobjekt zu gelangen](../media/privileged-access-workstations/PAWFig4.JPG)

Die obige Abbildung zeigt, wie Angreifer einer eingerichteten Kontrollkette folgen können, um zum gewünschten Zielobjekt zu gelangen.

Erweiterte Sicherheitsmaßnahmen wie die mehrstufige Authentifizierung können es einem Angreifer erschweren, von einer Benutzerarbeitsstation aus eine Verwaltungssitzung zu übernehmen. Es gibt allerdings keine Sicherheitsfunktion, die vollständig vor technischen Angriffen schützen kann, wenn ein Angreifer über Verwaltungszugriff auf dem Quellcomputer verfügt (z.B. durch Eingabe unerlaubter Befehle in einer genehmigten Sitzung, durch Übernahme legitimer Prozesse usw.).

Die Standardkonfiguration in diesem PAW-Leitfaden installiert Verwaltungstools auf der PAW, bei Bedarf kann jedoch auch eine Sprungbrettserverarchitektur hinzugefügt werden.

![Abbildung die zeigt, wie sich durch Umkehren der Kontrollbeziehung und Zugreifen auf Benutzer-Apps über eine Arbeitsstationen für Administratoren verhindern lässt, dass Angreifer ein Zielobjekt erreichen können](../media/privileged-access-workstations/PAWFig5.JPG)

Diese Abbildung zeigt, wie sich durch Umkehren der Kontrollbeziehung und Zugreifen auf Benutzer-Apps über eine Arbeitsstationen für Administratoren verhindern lässt, dass Angreifer ein Zielobjekt erreichen können. Der Sprungserver des Benutzers ist weiterhin Risiken ausgesetzt – für diesen Computer mit Internetzugriff sollten also geeignete Kontrollmechanismen und Prozesse implementiert werden, um Risiken zu erkennen, sich davor zu schützen und darauf zu reagieren.

In dieser Konfiguration müssen Administratoren sich sehr genau an festgelegte Vorgehensweisen halten, um sicherzustellen, dass sie auf ihrem Desktopcomputer nicht versehentlich Administratoranmeldeinformationen in die Benutzersitzung eingeben.

![Abbildung die zeigt, dass ein Angreifer keine Möglichkeit hat, an die Verwaltungsassets zu gelangen, wenn der Zugriff auf einen administrativen Sprungbrettserver über eine PAW erfolgt](../media/privileged-access-workstations/PAWFig6.JPG)

Diese Abbildung zeigt: Wenn der Zugriff auf einen administrativen Sprungbrettserver über eine PAW erfolgt, hat eine Angreifer keine Möglichkeit, an die Verwaltungsassets zu gelangen. In diesem Fall ermöglicht es ein Sprungbrettserver mit einer PAW Ihnen, die Anzahl von Speicherorten für die Überwachung von Verwaltungsaktivitäten und für die Verteilung von Verwaltungsanwendungen und -tools zu konsolidieren. Dies macht zwar das Design ein wenig komplexer, kann aber die Sicherheitsüberwachung und das Aufspielen von Softwareupdates vereinfachen, wenn Ihre PAW-Implementierung sehr viele Konten und Arbeitsstationen umfasst. Der Sprungbrettserver muss mit den gleichen Sicherheitsstandards erstellt und konfiguriert werden wie die PAW.

#### <a name="privilege-management-solutions"></a>Lösungen für die berechtigungsverwaltung

Lösungen für die Berechtigungsverwaltung sind Anwendungen, die bei Bedarf temporären Zugriff auf einzelne Berechtigungen oder privilegierte Konten bereitstellen. Lösungen für die Berechtigungsverwaltung sind eine sehr wertvolle Komponente einer umfassenden Strategie zur Sicherung des privilegierten Zugriffs und sorgen für die Transparenz und Zuverlässigkeit, die für Verwaltungsaktivitäten unabdingbar sind.

Diese Lösungen nutzen üblicherweise einen flexiblen Workflow zum Gewähren des Zugriffs und verfügen über zahlreiche weitere Sicherheitsfeatures und -methoden, wie z.B. die Kennwortverwaltung für Dienstkonten und die Integration mit administrativen Sprungbrettservern. Der Markt bietet eine Vielzahl solcher Lösungen mit Funktionen für die Berechtigungsverwaltung – z.B. die PAM-Lösung (Privileged Access Management) in Microsoft Identity Manager (MIM).

Microsoft empfiehlt die Verwendung einer PAW für den Zugriff auf Lösungen für die Berechtigungsverwaltung. Der Zugriff auf solche Lösungen sollte ausschließlich PAWs gewährt werden. Microsoft rät davon ab, diese Lösungen als Ersatz für eine PAW zu verwenden, da in diesem Fall der Zugriff auf Berechtigungen von einem potenziell gefährdeten Benutzerdesktop aus das Prinzip der [vertrauenswürdigen Quelle](http://aka.ms/cleansource) verletzt, wie im Diagramm unten gezeigt:

![Diagramm, das zeigt, wie Microsoft davon abrät, diese Lösungen als Ersatz für eine PAW zu verwenden, da in diesem Fall der Zugriff auf Berechtigungen von einem potenziell gefährdeten Benutzerdesktop aus das Prinzip der vertrauenswürdigen Quelle verletzt](../media/privileged-access-workstations/PAWFig7.JPG)

Durch Bereitstellen einer PAW für den Zugriff auf diese Lösungen können Sie von den Sicherheitsvorteilen sowohl der PAW als auch der Lösung für die Berechtigungsverwaltung profitieren, wie in diesem Diagramm gezeigt:

![Diagramm, das zeigt, wie Sie durch die Bereitstellung einer PAW für den Zugriff auf diese Lösungen von den Sicherheitsvorteilen aus der PAW und der Lösung für die Berechtigungsverwaltung profitieren](../media/privileged-access-workstations/PAWFig8.JPG)

> [!NOTE]
> Diese Systeme sollten auf die höchste Ebene der Berechtigung eingestuft werden, die sie verwalten, und mindestens auf dieser Ebene geschützt werden. Die Systeme werden im Allgemeinen für die Verwaltung von Lösungen und Assets auf Ebene 0 konfiguriert und sollten daher auf Ebene 0 eingestuft werden.
> Weitere Informationen zum Ebenenmodell, finden Sie unter [ http://aka.ms/tiermodel ](http://aka.ms/tiermodel) Weitere Informationen zu Gruppen auf Ebene 0, finden Sie unter "Äquivalenz in Ebene 0" [Schützen des privilegierten Zugriffs – Referenzmaterial](../securing-privileged-access/securing-privileged-access-reference-material.md).

Weitere Informationen zum Bereitstellen von Microsoft Identity Manager (MIM) privileged Access Management (PAM) finden Sie unter [http://aka.ms/mimpamdeploy](http://aka.ms/mimpamdeploy)

## <a name="paw-scenarios"></a>PAW-Szenarien

Dieser Abschnitt enthält Informationen dazu, auf welche Szenarien dieser PAW-Leitfaden angewendet werden sollte. In allen Szenarien sollten Administratoren entsprechend geschult werden, damit sie die PAWs nur für Supportaufgaben für Remotesysteme einsetzen. Um eine erfolgreiche und sichere Nutzung zu unterstützen, sollten alle PAW-Benutzer dazu angehalten werden, Feedback bereitstellen, um die Verwendung von PAWs zu verbessern. Das Feedback sollte sorgfältig geprüft und ggf. in unser PAW-Programm integriert werden.

In allen Szenarien können in späteren Phasen zusätzliche Sicherheitsmaßnahmen sowie verschiedene Hardwareprofile eingesetzt werden, um die Verwendbarkeits- oder Sicherheitsanforderungen der Rollen zu erfüllen.

> [!NOTE]
> Diese Anleitung unterscheidet explizit zwischen dem erforderlichen Zugriff auf bestimmte Dienste im Internet (z.B. Azure und Office 365-Verwaltungsportale) und dem "offenen Internet" für alle Hosts und -Dienste.

Weitere Informationen über die Ebenenbezeichnungen finden Sie im [Ebenenmodell](http://aka.ms/tiermodel).

|**Szenarien**|**Verwenden PAW?**|**Bereich und Überlegungen zur Sicherheit**|
|---------|--------|---------------------|
|Active Directory-Administratoren – Ebene 0|Ja|Eine gemäß der Anleitung für Phase 1 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– Eine Verwaltungsgesamtstruktur kann hinzugefügt werden, um in diesem Szenario höchstmöglichen Schutz zu bieten. Weitere Informationen zur ESAE-Verwaltungsgesamtstruktur finden Sie unter [ESAE-basierter Ansatz für den Entwurf einer administrativen Gesamtstruktur](http://aka.ms/esae).<br />– Eine PAW kann zur Verwaltung von mehreren Domänen oder mehreren Gesamtstrukturen verwendet werden.<br />– Wenn Domänencontroller in einer Infrastruktur als Service (IaaS) oder lokalen Virtualisierungslösung gehostet werden, sollten Sie die Implementierung der PAWs für die Administratoren dieser Lösungen priorisieren.|
|Verwalten von Azure IaaS- und PaaS-Diensten (Infrastructure-as-a-Service bzw. Platform-as-a-Service) – Ebene 0 oder Ebene 1 (siehe Überlegungen zu Einsatzbereich und Entwurf)|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– PAWs sollten zumindest für den globalen Administrator und für den für die Abonnementabrechnung zuständigen Administrator verwendet werden. Für delegierte Administratoren kritischer oder vertraulicher Server sollten Sie ebenfalls PAWs verwenden.<br />– PAWs sollten für die Verwaltung des Betriebssystems verwendet werden, und Anwendungen, Bereitstellen von Verzeichnissynchronisierung und den Identitätsverbund für, cloud-Dienste wie z. B. [Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) und Active Directory Federation Services (ADFS).<br />– Einschränkungen für den ausgehenden Netzwerkdatenverkehr dürfen Verbindungen nur mit autorisierten Clouddiensten zulassen, gemäß Anleitung für Phase 2. Auf PAWs darf kein offener Internetzugang zulässig sein.<br />– Windows Defender Exploit Guard müssen konfiguriert werden, auf der Arbeitsstation **beachten:**     Ein Abonnement gilt als Ebene 0 für eine Gesamtstruktur sein, wenn sich Domänencontroller oder andere Hosts auf Ebene 0 im Abonnement enthalten sind. Ein Abonnement befindet sich auf Ebene 1, wenn keine Server der Ebene 0 in Azure gehostet werden.|
|Verwalten von Office 365-Mandanten <br />– Ebene 1|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– PAWs sollten zumindest für den für die Abonnementabrechnung zuständigen Administrator, den globalen Administrator, den Exchange-Administrator, den SharePoint-Administrator und den Benutzerverwaltungsadministrator verwendet werden. Sie sollten auch unbedingt die Verwendung von PAWs für delegierte Administratoren höchst kritischer oder sensibler Daten erwägen.<br />– Windows Defender Exploit Guard sollte auf der Arbeitsstation konfiguriert werden.<br />– Einschränkungen für den ausgehenden Netzwerkdatenverkehr dürfen Verbindungen nur mit Microsoft-Diensten zulassen, gemäß Anleitung für Phase 2. Auf PAWs darf kein offener Internetzugang zulässig sein.|
|Verwalten anderer IaaS- der PaaS-Clouddienste<br />– Ebene 0 oder Ebene 1 (siehe Überlegungen zu Einsatzbereich und Entwurf)||Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– PAWs sollten für alle Rollen verwendet werden, die über Administratorrechte für in der Cloud gehostete virtuelle Computer verfügen. Zu den Aufgaben dieser Rollen gehören die Installation von Agents, der Export von Festplattendateien oder der Zugriff auf Speichersysteme, die Festplattenlaufwerke mit Betriebssystemen, sensiblen Daten oder geschäftskritischen Daten enthalten.<br />– Einschränkungen für den ausgehenden Netzwerkdatenverkehr dürfen Verbindungen nur mit Microsoft-Diensten zulassen, gemäß Anleitung für Phase 2. Auf PAWs darf kein offener Internetzugang zulässig sein.<br />– Windows Defender Exploit Guard sollte auf der Arbeitsstation konfiguriert werden. **Hinweis**: Ein Abonnement ist Ebene 0 für eine Gesamtstruktur aus, wenn sich Domänencontroller oder andere Hosts auf Ebene 0 im Abonnement enthalten sind. Ein Abonnement befindet sich auf Ebene 1, wenn keine Server der Ebene 0 in Azure gehostet werden.|
|Virtualisierungsadministratoren<br />– Ebene 0 oder Ebene 1 (siehe Überlegungen zu Einsatzbereich und Entwurf)|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– PAWs sollten für alle Rollen verwendet werden, die über Administratorrechte für virtuelle Computer verfügen. Zu den Aufgaben dieser Rollen gehören die Installation von Agents, der Export von virtuellen Festplattendateien oder der Zugriff auf Speichersysteme, die Festplattenlaufwerke mit Informationen zu Gastbetriebssystemen, sensiblen Daten oder geschäftskritischen Daten enthalten. **Hinweis**: Ein Virtualisierungssystem (und die zugehörigen Administratoren) gelten Ebene 0 für eine Gesamtstruktur, wenn sich Domänencontroller oder andere Hosts auf Ebene 0 im Abonnement enthalten sind. Ein Abonnement befindet sich auf Ebene 1, wenn keine Server der Ebene 0 im Virtualisierungssystem gehostet werden.|
|Administratoren für die Serverwartung<br />– Ebene 1|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– Eine PAW sollte für Administratoren verwendet werden, die für Aktualisierung, Patching und Problembehandlung von Unternehmensservern und -Apps unter Windows Server, Linux und anderen Betriebssystemen zuständig sind.<br />– Möglicherweise müssen dedizierte Verwaltungstools auf den PAWs installiert werden, um den größeren Aufgabenbereich dieser Administratoren abzudecken.|
|Administratoren für Benutzerarbeitsstationen <br />– Ebene 2|Ja|Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für Rollen ausreichend, die über Administratorrechte für Endbenutzergeräte verfügen (z.B. für Rollen im Helpdesk- und Vor-Ort-Support).<br /><br />– Möglicherweise müssen auf den PAWs zusätzliche Anwendungen installiert werden, um das Ticketmanagement und andere Supportfunktionen zu ermöglichen.<br />– Windows Defender Exploit Guard sollte auf der Arbeitsstation konfiguriert werden.<br />    Möglicherweise müssen dedizierte Verwaltungstools auf den PAWs installiert werden, um den größeren Aufgabenbereich dieser Administratoren abzudecken.|
|SQL-, SharePoint- oder LoB-Administrator (Line of Business)<br />– Ebene 1||Eine gemäß der Anleitung für Phase 2 erstellte PAW ist für diese Rolle ausreichend.<br /><br />– Möglicherweise müssen auf den PAWs zusätzliche Verwaltungstools installiert werden, damit Administratoren Anwendungen verwalten können, ohne über Remotedesktop eine Verbindung zu einem Server herstellen zu müssen.|
|Benutzer, die die Präsenz in sozialen Medien pflegen|Teilweise|Eine gemäß der Anleitung für Phase 2 erstellte PAW kann als Ausgangspunkt zur Bereitstellung von Sicherheit für diese Rollen verwendet werden.<br /><br />– Schützen und verwalten Sie Konten in sozialen Medien, und verwenden Sie Azure Active Directory (AAD), um den Zugriff auf diese Konten freigeben, schützen und nachverfolgen zu können.<br />    Weitere Informationen zu dieser Funktionalität finden Sie in [diesem Blogbeitrag](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx).<br />– Die Einschränkungen für ausgehenden Netzwerkdatenverkehr müssen die Verbindung mit diesen Diensten zulassen. Hierzu können Sie offene Internetverbindungen zulassen (sehr viel höheres Sicherheitsrisiko, das viele Sicherheitsmechanismen auf PAWs aushebelt) oder nur die für den Dienst erforderlichen DNS-Adressen zulassen (es kann schwierig sein, diese DNS-Adressen abzurufen).|
|Standardbenutzer|Nein|Viele der Sicherheitsschritte können auch für Standardbenutzer verwendet werden. Eine PAW dagegen ist speziell zur Isolierung von Konten vom offenen Internetzugriff entworfen, den viele Benutzer für ihre täglichen Aufgaben benötigen.|
|Gast-VDI/Kiosk|Nein|Während viele Sicherheitsschritte für ein Kiosksystem für Gäste verwendet werden können, wurde die PAW-Architektur speziell dafür konzipiert, hochsensiblen Konten ein höheres Maß an Sicherheit zu bieten, und nicht dafür, mehr Sicherheit für weniger vertrauliche Konten bereitzustellen.|
|VIP-Benutzer (Unternehmensleitung, Forschungsmitarbeiter usw.)|Teilweise|Eine gemäß der Anleitung für Phase 2 erstellte PAW kann als Ausgangspunkt verwendet werden, um die Sicherheit für diese Rollen bereitzustellen.<br /><br />– Dieses Szenario ähnelt einem Szenario für Standardbenutzerdesktops, weist aber in der Regel ein kleineres, einfacheres und bekanntes Anwendungsprofil auf. Das Szenario erfordert üblicherweise, dass sensible Daten, Dienste und Anwendungen erkannt und geschützt werden (die auf den Desktops installiert sein können, aber nicht müssen).<br />– Diese Rollen erfordern üblicherweise ein hohes Maß an Sicherheit und ein sehr hohes Maß an Benutzerfreundlichkeit, wodurch Entwurfsänderungen erforderlich sind, um die Benutzeranforderungen zu erfüllen.|
|Industrielle Steuerungssysteme (z.B. SCADA, PCN und DCS)|Teilweise|Eine gemäß der Anleitung für Phase 2 erstellte PAW kann als Ausgangspunkt zur Bereitstellung von Sicherheit für diese Rollen verwendet werden, da die meisten ICS-Konsolen (einschließlich solcher allgemeinen Standards wie SCADA und PCN) keinen Zugriff auf das offene Internet oder E-Mails erfordern.<br /><br />– Anwendungen für die Steuerung physischer Computer müsste integriert und für die Kompatibilität getestet und angemessen geschützt werden.|
|Integriertes Betriebssystem|Nein|Während viele der Sicherheitsschritte für PAWs für integrierte Betriebssysteme verwendet werden können, muss in diesem Szenario eine benutzerdefinierte Lösung für die Sicherung entwickelt werden.|

> [!NOTE]
> **Kombinierte Szenarien**: Einige Mitarbeiter sind möglicherweise für Verwaltungsaufgaben verantwortlich, die mehrere Szenarien umfassen.
> In diesen Fällen gilt als oberste Regel, dass jederzeit die Regeln des Ebenenmodells befolgt werden müssen. Weitere Informationen finden Sie im Ebenenmodell.

> [!NOTE]
> **Skalieren des PAW-Programms**: Wenn Ihr PAW-Programm skaliert werden muss, um weitere Administratoren und Rollen abzudecken, müssen Sie weiterhin sicherstellen, dass die Sicherheits- und Nutzbarkeitsstandards eingehalten werden. Dazu müssen Sie möglicherweise Ihre IT-Supportstrukturen aktualisieren oder neue einrichten, um PAW-spezifische Herausforderungen wie etwa den Onboardingprozess, das Incidentmanagement oder die Konfigurationsverwaltung zu bewältigen. Zudem müssen Sie das Feedback der Benutzer berücksichtigen, um eventuelle Probleme mit der Nutzbarkeit zu beheben.  Ein Beispiel: Ihre Organisation beschließt, Administratoren das Arbeiten von zu Hause aus zu ermöglichen. Daher müssen statt Desktop-PAWs jetzt Laptop-PAWs eingesetzt werden – eine Änderung, bei der zusätzliche Sicherheitsaspekte zu bedenken sind.  Ein weiteres häufiges Szenario ist die Erstellung oder Aktualisierung von Schulungen für neue Administratoren. Solche Schulungen müssen jetzt Inhalte zur ordnungsgemäßen Verwendung einer PAW enthalten (und darüber informieren, was eine PAW ist, was sie nicht ist und warum ihr Einsatz so wichtig ist).  Weitere Aspekte, die beim Skalieren Ihres PAW-Programms berücksichtigt werden müssen, finden Sie in Phase 2 der Anweisungen.

Dieser Leitfaden enthält detaillierte Anweisungen für die PAW-Konfiguration für die oben genannten Szenarien. Wenn Sie andere Szenarien implementieren, können Sie die Anweisungen in diesem Leitfaden selbst entsprechend anpassen oder einen professionellen Dienstleister wie z.B. Microsoft mit der Einrichtung beauftragen.

Informationen dazu, wie Sie Microsoft-Dienste für die Bereitstellung einer auf Ihre Umgebung zugeschnittenen PAW-Lösung in Anspruch nehmen können, erhalten Sie von Ihrem Microsoft-Vertriebsmitarbeiter oder [auf dieser Seite](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

## <a name="paw-phased-implementation"></a>Implementierung von PAWS in Phasen

Da eine PAW eine sichere und vertrauenswürdige Quelle für die Verwaltung bereitstellen muss, ist es von größter Bedeutung, dass der Buildprozess ebenfalls sicher und vertrauenswürdig ist.  Dieser Abschnitt enthält detaillierte Anweisungen, mit denen Sie selbst PAWs erstellen können. Dabei kommen allgemeine Prinzipien und Konzepte zum Einsatz, die den von der Microsoft-IT und den Cloudentwicklungs- und Dienstverwaltungsorganisationen von Microsoft verwendeten sehr ähneln.

Die Anweisungen sind in drei Phasen unterteilt, und der Schwerpunkt liegt darauf, die wichtigsten Risikominimierungen schnell einzurichten und die Nutzung der PAWs für das Unternehmen dann nach und nach zu steigern und zu erweitern.

* [Phase 1: sofortige Bereitstellung für Active Directory-Administratoren](#phase-1-immediate-deployment-for-active-directory-administrators)
* [Phase 2: Erweitern der PAW auf alle Administratoren](#phase-2-extend-paw-to-all-administrators)
* [Phase 3: Erweiterte PAW-Sicherheit](#phase-3-extend-and-enhance-protection)

Beachten Sie Folgendes: Die Phasen sollten immer in dieser Reihenfolge ausgeführt werden, auch wenn sie im Rahmen desselben Gesamtprojekts geplant und implementiert werden.

### <a name="phase-1-immediate-deployment-for-active-directory-administrators"></a>Phase 1: Sofortige Bereitstellung für Active Directory-Administratoren

Zweck: Bietet eine paw erfolgt schnell, die lokalen Domänen- und Gesamtstrukturfunktionsebenen Administratorrollen schützen kann.

Umfang: Administratoren der Ebene 0, einschließlich Unternehmensadministratoren, Domänenadministratoren (für alle Domänen) und Administratoren anderer maßgeblicher Identitätssysteme.

Phase 1 konzentriert sich auf die Administratoren, die Ihre lokale Active Directory-Domäne verwalten. Dies sind extrem wichtige Rollen, die häufig Ziel von Angreifern sind. Diese Identitätssysteme schützen diese Administratoren effektiv, unabhängig davon, ob Ihre Active Directory-Domänencontroller in lokalen Rechenzentren, in Azure IaaS oder von einem anderen IaaS-Anbieter gehostet werden.

Während dieser Phase erstellen Sie die sichere Verwaltungsstruktur für die Active Directory-Organisationseinheit (OE), um Ihre PAWs zu hosten. Des Weiteren stellen Sie die PAWs selbst bereit.  Diese Struktur umfasst auch die Gruppenrichtlinien und Gruppen, die für die Unterstützung der PAWs erforderlich sind.  Sie erstellen den größten Teil der Struktur mithilfe von PowerShell-Skripts, die in der [TechNet-Galerie](http://aka.ms/pawmedia) verfügbar sind.

Diese Skripts erstellen die folgenden Organisationseinheiten und Sicherheitsgruppen:

* Organisationseinheiten
   * Sechs neue Organisationseinheiten auf oberster Ebene:  Admin; Gruppen Server der Schicht 1; Arbeitsstationen; Benutzerkonten und -Computer unter Quarantäne gestellt.  Jede OE auf oberster Ebene enthält mehrere untergeordnete Organisationseinheiten.
* Gruppen
   * Sechs neue mit aktivierter Sicherheit globale Gruppen:  Tier 0 Replication Maintenance; Ebene 1 Server Maintenance; Service Desk Operators; Arbeitsstation-Wartung; PAW-Benutzer; PAW Maintenance.

Sie werden auch eine Reihe von Group Policy Objects erstellen: PAW-Konfiguration – Computer; PAW-Konfiguration – Benutzer; RestrictedAdmin erforderlich – Computer; PAW Outbound Restrictions; Beschränken Sie die Anmeldung an der Arbeitsstation. Beschränken Sie die Server-Anmeldung.

Phase 1 umfasst die folgenden Schritte:

#### <a name="complete-the-prerequisites"></a>Erfüllen der Voraussetzungen

1. **Stellen Sie sicher, dass alle Administratoren getrennte Konten für ihre Verwaltungs- und Endbenutzeraktivitäten verwenden** (einschließlich E-Mail, Internetrecherche, LoB-Anwendungen und weiterer nicht administrativer Aktivitäten).  Es ist von grundlegender Bedeutung für das PAW-Modell, dass jedem autorisierten Mitarbeiter ein spezifisches, vom Standardbenutzerkonto strikt getrenntes Verwaltungskonto zugewiesen wird, da sich nur bestimmte Konten bei einer PAW anmelden dürfen.

   > [!NOTE]
   > Jeder Administrator sollte sein eigenes Konto für die Verwaltung verwenden.  Administratorkonto sollten nicht gemeinsam genutzt werden.

2. **Minimieren Sie die Anzahl der Administratoren mit Berechtigungen auf Ebene 0**.  Da jeder Administrator eine eigene PAW verwenden muss, senken Sie durch Reduzieren der Anzahl von Administratoren die Anzahl von erforderlichen PAWs und entsprechend auch die damit verbundenen Kosten. Eine geringere Anzahl von Administratoren senkt zudem eine potenzielle Gefährdung der Administratorrechte und die damit zusammenhängenden Risiken. Administratoren an einem gemeinsamen Standort können eine PAW gemeinsam nutzen, Administratoren in separaten physischen Standorten dagegen benötigen getrennte PAWs.
3. **Erwerben Sie die Hardware bei einem vertrauenswürdigen Lieferanten, der alle technischen Anforderungen erfüllt**. Microsoft empfiehlt, Hardware zu erwerben, die die technischen Anforderungen im Artikel [Schützen von Domänenanmeldeinformationen mit Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) erfüllt.

   > [!NOTE]
   > Eine PAW, die auf einer Hardwarekomponente ohne diese Funktionen installiert wird, kann bereits ein hohes Maß an Schutz bieten, erweiterte Sicherheitsfunktionen wie Credential Guard und Device Guard stehen in diesem Fall allerdings nicht zur Verfügung.  Credential Guard und Device Guard sind für die Bereitstellung in Phase 1 nicht unbedingt erforderlich, werden im Rahmen von Phase 3 (erweiterte Sicherung) jedoch dringend empfohlen.
   >
   > Stellen Sie sicher, dass die für die PAW verwendete Hardware von einem Hersteller und einem Lieferanten stammt, deren Sicherheitsmethoden von der Organisation als vertrauenswürdig eingestuft werden. Dies ist eine Anwendung des Prinzips der vertrauenswürdigen Quelle auf die Sicherheit in der Lieferkette.
   >
   > Hintergrundinformationen zur Bedeutung der Sicherheit in der Lieferkette finden Sie [auf dieser Website](https://www.microsoft.com/security/cybersecurity/).

4. **Abrufen und überprüfen Sie die erforderlichen Windows 10 Enterprise Edition und die Anwendungssoftware**. Beziehen Sie die für die PAWs erforderliche Software, und überprüfen Sie sie anhand der Anleitung unter [Vertrauenswürdige Quelle für Installationsmedien](http://aka.ms/cleansource).

   * Windows 10 Enterprise Edition
   * [Remoteserver-Verwaltungstools](https://www.microsoft.com/en-us/download/details.aspx?id=45520.) für Windows 10
   * [Windows 10-Sicherheitsbaselines](http://aka.ms/win10baselines)

      > [!NOTE]
      > Microsoft veröffentlicht MD5-Hashes für alle Betriebssysteme und Anwendungen auf MSDN, allerdings bieten nicht alle Softwarehersteller eine ähnliche Dokumentation.  In solchen Fällen sind andere Strategien erforderlich.  Weitere Informationen zur Überprüfung von Software finden Sie unter [Vertrauenswürdige Quelle für Installationsmedien](http://aka.ms/cleansource).

5. **Stellen Sie sicher, dass im Intranet ein WSUS-Server verfügbar ist**. Sie benötigen einen WSUS-Server im Intranet, um Updates für PAWs herunterzuladen und zu installieren. Dieser WSUS-Server sollte so konfiguriert sein, dass alle Sicherheitsupdates für Windows 10 automatisch genehmigt werden, oder verantwortungsvolle Verwaltungsmitarbeiter müssen Softwareupdates schnell und zuverlässig genehmigen.

   > [!NOTE]
   > Weitere Informationen finden Sie im Dokument [Genehmigen von Updates](https://technet.microsoft.com/library/cc708458(v=ws.10).aspx) unter „Automatisches Genehmigen der Installation von Updates“.

#### <a name="deploy-the-admin-ou-framework-to-host-the-paws"></a>Bereitstellen des Administrator-OE-Frameworks zum Hosten der PAWs

1. Laden Sie die PAW-Skriptbibliothek aus der [TechNet-Galerie](http://aka.ms/PAWmedia) herunter.

   > [!NOTE]
   > Laden Sie alle Dateien herunter, speichern Sie sie im gleichen Verzeichnis, und führen Sie sie in der unten angegebenen Reihenfolge aus.  Create-PAWGroups hängt von der von Create-PAWOUs erstellten OE-Struktur ab, und Set-PAWOUDelegation hängt von den von Create-PAWGroups erstellten Gruppen ab.
   > Ändern Sie weder eines der Skripts noch die CSV-Datei.

2. **Führen Sie das Skript Create-PAWOUs.ps1 aus**.  Dieses Skript erstellt die neue OE-Struktur in Active Directory und blockiert nach Bedarf die GPO-Vererbung in den neuen Organisationseinheiten.
3. **Führen Sie das Skript Create-PAWGroups.ps1 aus**.  Dieses Skript erstellt die neuen globalen Sicherheitsgruppen in den entsprechenden Organisationseinheiten.

   > [!NOTE]
   > Das Skript erstellt zwar die neuen Sicherheitsgruppen, füllt sie aber nicht automatisch auf.

4. **Führen Sie das Skript Set-PAWOUDelegation.ps1 aus**.  Dieses Skript weist den entsprechenden Gruppen die Berechtigungen für die neuen Organisationseinheiten zu.

#### <a name="move-tier-0-accounts-to-the-admintier-0accounts-ou"></a>Verschieben von Ebene-0-Konten für die Organisationseinheit des Admin\Tier 0\Accounts

Verschieben Sie jedes Konto, das Mitglied der Gruppe „Domänenadministratoren“, „Unternehmensadministratoren“ oder einer Gruppe mit entsprechenden Berechtigungen auf Ebene 0 (einschließlich geschachtelter Mitgliedschaften) ist, in diese OE. Wenn Ihre Organisation diesen Gruppen eigene Gruppen hinzugefügt hat, sollten Sie diese in die OE „Admin\Tier 0\Groups“ verschieben.

   > [!NOTE]
   > Weitere Informationen dazu, welche Gruppen sich auf Ebene 0 befinden, finden Sie unter „Äquivalenz zur Ebene 0“ in [Schützen des privilegierten Zugriffs – Referenzmaterial](../securing-privileged-access/securing-privileged-access-reference-material.md).

#### <a name="add-the-appropriate-members-to-the-relevant-groups"></a>Hinzufügen der geeigneten Mitglieder zu den jeweiligen Gruppen

1. **PAW Users**: Fügen Sie die Administratoren auf Ebene 0 zu den Gruppen der Domänen- oder Unternehmensadministratoren hinzu, die Sie in Schritt 1 von Phase 1 identifiziert haben.
2. **PAW Maintenance**: Fügen Sie mindestens ein Konto hinzu, das für Aufgaben der Wartung und Problembehandlung für die PAWs verwendet wird. Das Konto bzw. die Konten „PAW Maintenance“ wird/werden nur selten verwendet.

   > [!NOTE]
   > Fügen Sie ein Benutzerkonto oder eine Benutzergruppe nicht sowohl zu „PAW Users“ als auch zu „PAW Maintenance“ hinzu.  Das PAW-Sicherheitsmodell basiert teilweise auf der Annahme, dass ein PAW-Benutzerkonto über privilegierte Zugriffsrechte für die verwalteten Systeme oder für die PAW selbst verfügt, nicht jedoch für beides.
   >
   > * Dies ist ein wichtiger Aspekt für die Entwicklung sorgfältiger Verwaltungsmethoden und -gewohnheiten in Phase 1.
   > * In Phase 2 und darüber hinaus ist dieser Aspekt von entscheidender Bedeutung, um eine Übertragung von Zugriffsrechten auf verschiedene PAWs zu vermeiden, wenn PAWs ebenenübergreifend eingesetzt werden.
   >
   > Idealerweise werden keinem Mitarbeiter Aufgaben auf mehreren Ebenen zugewiesen, um das Prinzip der Aufgabentrennung durchzusetzen. Microsoft ist jedoch bewusst, dass viele Organisationen nicht über genügend Mitarbeiter verfügen oder andere organisationsbezogene Anforderungen vorliegen, sodass eine vollständige Trennung nicht immer möglich ist. In diesen Fällen können beide Rollen dem gleichen Mitarbeiter zugewiesen werden, dieser sollte dann aber nicht das gleiche Konto für diese Funktionen verwenden.

#### <a name="create-paw-configuration---computer-group-policy-object-gpo"></a>Erstellen Sie "PAW-Konfiguration – Computer" des Gruppenrichtlinienobjekts (GPO)

In diesem Abschnitt erstellen Sie eine neue "PAW-Konfiguration – Computer" Gruppenrichtlinienobjekt, das bestimmte Schutzmaßnahmen für diese PAWs bieten, und verknüpfen Sie sie mit der Geräte-OE der Ebene 0 ("Devices" unter Tier 0\Admin).

   > [!NOTE]
   > **Fügen Sie diese Einstellungen nicht zur Standarddomänenrichtlinie hinzu**.  Dies könnte sich auf Vorgänge in Ihrer gesamten Active Directory-Umgebung auswirken.  Konfigurieren Sie diese Einstellungen nur in den hier beschriebenen, neu erstellten Gruppenrichtlinienobjekten, und wenden Sie sie nur auf die Organisationseinheit „PAW“ an.

1. **PAW-Wartungszugriff**: Diese Einstellung legt die Mitgliedschaft in bestimmten privilegierten Gruppen auf den PAWs auf eine bestimmte Benutzergruppe fest. Wechseln Sie zu *Computerkonfiguration\Einstellungen\Systemsteuerungseinstellungen\Lokale Benutzer und Gruppen*, und führen Sie folgende Schritte aus:
   1. Klicken Sie auf **Neu** und dann auf **Lokale Gruppe**.
   2. Wählen Sie die Aktion **Update**, und wählen Sie „Administratoren (integriert)“ (verwenden Sie nicht die Schaltfläche zum Durchsuchen, um die Gruppenadministratoren für die Domäne auszuwählen).
   3. Wählen Sie die Kontrollkästchen **Alle Mitgliederbenutzer löschen** und **Alle Mitgliedergruppen löschen** aus.
   4. Fügen Sie die Gruppe „PAW Maintenance“ (pawmaint) und „Administrator“ hinzu (verwenden Sie auch hier nicht die Durchsuchen-Schaltfläche zum Auswählen des Administrators).

      > [!NOTE]
      > Fügen Sie die Gruppe „PAW Users“ nicht zur Mitgliederliste für die lokale Administratorengruppe hinzu.  Um sicherzustellen, dass PAW-Benutzer die Sicherheitseinstellungen der PAW nicht versehentlich oder absichtlich ändern können, sollten sie kein Mitglied der lokalen Administratorengruppe sein.
      >
      > Weitere Informationen zur Verwendung von Einstellungen für Gruppenrichtlinien, um Gruppenmitgliedschaften zu ändern, finden Sie im TechNet-Artikel [Konfigurieren eines Elements für lokale Gruppen](https://technet.microsoft.com/library/cc732525.aspx).

2. **Einschränken der lokalen Gruppenmitgliedschaft**: Diese Einstellung stellt sicher, dass die Mitgliedschaft lokaler Administratorengruppen auf der Arbeitsstation immer leer ist.
   1. Wechseln Sie zu „Computerkonfiguration\Einstellungen\Systemsteuerungseinstellungen\Lokale Benutzer und Gruppen“, und führen Sie folgende Schritte aus:
      1. Klicken Sie auf **Neu** und dann auf **Lokale Gruppe**.
      2. Wählen Sie die Aktion **Update**, und wählen Sie „Sicherungs-Operatoren (integriert)“ (verwenden Sie nicht die Schaltfläche zum Durchsuchen, um die Sicherungsoperatoren für die Domänengruppe auszuwählen).
      3. Wählen Sie die Kontrollkästchen **Alle Mitgliederbenutzer löschen** und **Alle Mitgliedergruppen löschen** aus.
      4. Fügen Sie der Gruppe keine Mitglieder hinzu.  Klicken Sie einfach auf **OK**.  Durch Zuweisen einer leeren Liste entfernt die Gruppenrichtlinie automatisch alle Mitglieder und stellt bei jeder Aktualisierung der Gruppenrichtlinie sicher, dass die Mitgliedschaftsliste leer ist.
   2. Führen Sie die oben genannten Schritte für die folgenden zusätzlichen Gruppen aus:
      * Kryptografie-Operatoren
      * Hyper-V-Administratoren
      * Netzwerkkonfigurations-Operatoren
      * Powerusers
      * Remotedesktopbenutzer
      * Replikatoren
   3. **PAW Logon Restrictions** -diese Einstellung wird die Konten, die bei der PAW anmelden können, eingeschränkt. Führen Sie die folgenden Schritte aus, um diese Einstellung zu konfigurieren:
      1. Wechseln Sie zu „Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten\Lokal anmelden zulassen“.
      2. Wählen Sie diese Richtlinieneinstellungen definieren und Hinzufügen von "PAW Users" und der-Administratoren (in diesem Fall verwenden Sie nicht die Schaltfläche zum Durchsuchen auf Administratoren).
   4. **Eingehenden Netzwerkdatenverkehr blockieren**: Diese Einstellung stellt sicher, dass kein unangeforderter eingehender Netzwerkdatenverkehr zur PAW zugelassen wird. Führen Sie die folgenden Schritte aus, um diese Einstellung zu konfigurieren:
      1. Wechseln Sie zu „Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Windows-Firewall mit erweiterter Sicherheit\Windows-Firewall mit erweiterter Sicherheit“, und führen Sie folgende Schritte aus:
         1. Klicken Sie mit der rechten Maustaste auf „Windows-Firewall mit erweiterter Sicherheit“, und wählen Sie **Richtlinie importieren** aus.
         2. Klicken Sie auf **Ja**, um zu bestätigen, dass dadurch alle vorhandenen Firewallrichtlinien überschrieben werden.
         3. Navigieren Sie zu „PAWFirewall.wfw“, und wählen Sie **Öffnen**.
         4. Klicken Sie auf **OK**.

            > [!NOTE]
            > An dieser Stelle können Sie Adressen oder Subnetze hinzufügen, deren Datenverkehr zur PAW auch unangefordert zugelassen wird (z.B. Sicherheitsüberprüfungs- oder Verwaltungssoftware).
            > Die Einstellungen in der WFW-Datei aktivieren die Firewall im Modus „Blockieren (Standard)“ für alle Firewallprofile, deaktivieren die Regelzusammenführung und aktivieren die Protokollierung sowohl für gelöschte als auch für erfolgreiche Pakete. Diese Einstellungen blockieren unangeforderten Datenverkehr, lassen aber bidirektionale Kommunikation in Verbindungen zu, die von der PAW initiiert wurden. Sie verhindern zudem, dass Benutzer mit lokalem Administratorzugriff lokale Firewallregeln erstellen, die die GPO-Einstellungen überschreiben würden, und sie stellen sicher, dass Datenverkehr zur und aus der PAW protokolliert wird.
            > **Durch Öffnen dieser Firewall wird die Angriffsfläche für die PAW vergrößert, und das Sicherheitsrisiko steigt. Bevor Sie Adressen hinzufügen, lesen Sie den Abschnitt zu Verwaltung und Betrieb einer PAW in diesem Leitfaden**.

   5. **Konfigurieren von Windows Update für WSUS**: Führen Sie die unten stehenden Schritte durch, um die Einstellungen zur Konfiguration von Windows Update für die PAWs zu ändern:
      1. Wechseln Sie zu Computer Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\Windows-Updates aus, und führen Sie die folgenden Schritte aus:
         1. Aktivieren Sie die Richtlinie **Automatische Updates konfigurieren**.
         2. Wählen Sie die Option **4 – Autom. Herunterladen und laut Zeitplan installieren**.
         3. Ändern Sie die Option **Geplanter Installationstag** zu **0 – Täglich** und die Option **Geplante Installationszeit** zu der Uhrzeit, die für den Betrieb Ihrer Organisation am besten passt.
         4. Aktivieren Sie Option **Intranet-Microsoft-Updatedienst angeben** Richtlinie, und geben Sie bei beiden Optionen die URL des ESAE WSUS-Servers.
   6. Verknüpfen Sie die "PAW-Konfiguration – Computer" GPO wie folgt:

         |Richtlinie|Speicherort|
         |-----|---------|
         |PAW-Konfiguration – Computer |Admin\Tier 0\Devices|

#### <a name="create-paw-configuration---user-group-policy-object-gpo"></a>Erstellen Sie die Gruppenrichtlinienobjekt (GPO) "PAW-Konfiguration – Benutzer"

In diesem Abschnitt erstellen Sie eine neue "PAW-Konfiguration – Benutzer" Gruppenrichtlinienobjekt, das bestimmte Schutzmaßnahmen für diese PAWs und einen Link zu den Konten-OE der Ebene 0 ("Konten" unter Tier 0\Admin) bereitstellt.

   > [!NOTE]
   > Fügen Sie diese Einstellungen nicht zur Standarddomänenrichtlinie hinzu.

1. **Internetbrowsen blockieren**: Um unbeabsichtigtes Internetbrowsen zu verhindern, legt diese Einstellung die Proxyadresse einer Loopbackadresse fest (127.0.0.1).
   1. Wechseln Sie zum Benutzer Configuration\Preferences\Windows Settings\Registry. Mit der rechten Maustaste Registrierung, wählen Sie **neu** > **Registrierungselement** und konfigurieren Sie die folgenden Einstellungen:
      1. Aktion:  Ersetzen
      2. Struktur: HKEY_CURRENT_USER
      3. Schlüsselpfad:  Software\Microsoft\Windows\CurrentVersion\Internet Settings
      4. Wertname: ProxyEnable

         > [!NOTE]
         > Aktivieren Sie nicht das Feld „Standard“ links neben dem Namen des Werts.

      5. Werttyp: REG_DWORD
      6. Wert: 1
         1. Klicken Sie auf die Registerkarte „Allgemein“, und wählen Sie **Element entfernen, wenn es nicht mehr angewendet wird** aus.
         2. Wählen Sie auf der Registerkarte „Allgemein“ die Option **Zielgruppenadressierung auf Elementebene**, und klicken Sie dann auf **Zielgruppenadressierung**.
         3. Klicken Sie auf **Neues Element**, und wählen Sie die Option **Sicherheitsgruppe** aus.
         4. Wählen Sie die Schaltfläche „...“ aus, und suchen Sie nach der Gruppe „PAW Users“.
         5. Klicken Sie auf **Neues Element**, und wählen Sie die Option **Sicherheitsgruppe** aus.
         6. Wählen Sie die Schaltfläche „...“ aus, und suchen Sie nach der Gruppe **Cloud Services-Administratoren**.
         7. Klicken Sie auf das Element **Cloud Services-Administratoren**, und klicken Sie auf **Elementoptionen**.
         8. Wählen Sie **Ist nicht** aus.
         9. Klicken Sie im Fenster für die Zielgruppenadressierung auf **OK**.
      7. Klicken Sie auf **OK**, um die ProxyServer-Gruppenrichtlinieneinstellung abzuschließen.
   2. Wechseln Sie zum Benutzer Configuration\Preferences\Windows Settings\Registry. Mit der rechten Maustaste Registrierung, wählen Sie **neu** > **Registrierungselement** und konfigurieren Sie die folgenden Einstellungen:

      * Aktion: Ersetzen
      * Struktur: HKEY_CURRENT_USER
      * Schlüsselpfad: Software\Microsoft\Windows\CurrentVersion\Internet Settings
         * Wertname: ProxyServer

            > [!NOTE]
            > Aktivieren Sie nicht das Feld „Standard“ links neben dem Namen des Werts.

         * Werttyp: REG_SZ
         * Wert: 127.0.0.1:80
            1. Klicken Sie auf die Registerkarte **Allgemein**, und wählen Sie **Element entfernen, wenn es nicht mehr angewendet wird** aus.
            2. Wählen Sie auf der Registerkarte **Allgemein** die Option **Zielgruppenadressierung auf Elementebene**, und klicken Sie dann auf **Zielgruppenadressierung**.
            3. Klicken Sie auf **Neues Element**, und wählen Sie die Sicherheitsgruppe aus.
            4. Wählen Sie die Schaltfläche „...“ aus, und fügen Sie die Gruppe „PAW Users“ hinzu.
            5. Klicken Sie auf **Neues Element**, und wählen Sie die Sicherheitsgruppe aus.
            6. Wählen Sie die Schaltfläche „...“ aus, und suchen Sie nach der Gruppe **Cloud Services-Administratoren**.
            7. Klicken Sie auf das Element **Cloud Services-Administratoren**, und klicken Sie auf **Elementoptionen**.
            8. Wählen Sie **Ist nicht** aus.
            9. Klicken Sie im Fenster für die Zielgruppenadressierung auf **OK**.

   3. Klicken Sie auf **OK**, um die ProxyServer-Gruppenrichtlinieneinstellung abzuschließen.
2. Wechseln Sie zum Benutzer Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\Internet Explorer, und aktivieren Sie die unten aufgeführten Optionen. Diese Einstellungen verhindern, dass Administratoren die Proxyeinstellungen manuell überschreiben können.
   1. Aktivieren Sie die Option **Änderung der Einstellungen für automatische Konfiguration deaktivieren**.
   2. Aktivieren Sie die Option **Änderung der Proxyeinstellungen verhindern**.

#### <a name="restrict-administrators-from-logging-onto-lower-tier-hosts"></a>Administratoren von Protokollierung Hosts auf niedrigerer Ebene zu beschränken.

In diesem Abschnitt konfigurieren Sie Gruppenrichtlinien, um zu verhindern, dass Administratorkonten mit hohen Berechtigungen sich bei Hosts auf niedrigerer Ebene anmelden können.

1. Erstellen Sie das neue Gruppenrichtlinienobjekt **Anmelden bei Arbeitsstation einschränken**. Diese Einstellung verhindert, dass sich Administratorkonten der Ebenen 0 und 1 bei Standardarbeitsstationen anmelden können.  Dieses Gruppenrichtlinienobjekt "Arbeitsstationen" der obersten Ebene Organisationseinheit verknüpft werden soll, und weisen folgende Einstellungen:
   * Wählen Sie im Computer Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von benutzerrechten\anmelden als Batchauftrag, **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 und Ebene 1 hinzu:     Enterprise Admins Domänen-Admins, Schema Administratoren domäne\administratoren Konto Operatoren Sicherungs-Operatoren drucken Operatoren Server Operatoren Domain Controller nur-Lese Directory-Domänencontrollergruppe Richtlinie Creators Besitzer kryptografischen Operator verglichen

         > [!NOTE]
         > Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

         Tier 1 Admins

         > [!NOTE]
         > This Group was created earlier in Phase 1.

   * Wählen Sie im Computer Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten\Lokal Anmelden als Dienst, **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 und Ebene 1 hinzu:     Enterprise Admins Domänen-Admins, Schema Administratoren domäne\administratoren Konto Operatoren Sicherungs-Operatoren drucken Operatoren Server Operatoren Domain Controller nur-Lese Directory-Domänencontrollergruppe Richtlinie Creators Besitzer kryptografischen Operator verglichen

         > [!NOTE]
         > Note: Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Note: Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

         Tier 1 Admins

         > [!NOTE]
         > Note: This Group was created earlier in Phase 1

2. Erstellen Sie das neue **Anmelden bei Server einschränken** GPO - diese Einstellung verhindert, dass Administratorkonten der Ebene 0 Protokollierung auf dem Server der Ebene 1.  Dieses Gruppenrichtlinienobjekt "Tier 1 Servers" der obersten Ebene Organisationseinheit verknüpft werden soll, und weisen folgende Einstellungen:
   * Wählen Sie im Computer Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von benutzerrechten\anmelden als Batchauftrag, **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 hinzu:     Enterprise Admins Domänen-Admins, Schema Administratoren domäne\administratoren Konto Operatoren Sicherungs-Operatoren drucken Operatoren Server Operatoren Domain Controller nur-Lese Directory-Domänencontrollergruppe Richtlinie Creators Besitzer kryptografischen Operator verglichen

         > [!NOTE]
         > Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

   * Wählen Sie im Computer Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten\Lokal Anmelden als Dienst, **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 hinzu:     Enterprise Admins Domänen-Admins, Schema Administratoren domäne\administratoren Konto Operatoren Sicherungs-Operatoren drucken Operatoren Server Operatoren Domain Controller nur-Lese Directory-Domänencontrollergruppe Richtlinie Creators Besitzer kryptografischen Operator verglichen

         > [!NOTE]
         > Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

   * Wählen Sie lokal in Computer Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten\Lokal anmelden **diese Richtlinieneinstellungen definieren** und fügen Sie die Gruppen auf Ebene 0 hinzu:     Enterprise Admins Domänen-Admins, Schema-Admins-Konto Operatoren Sicherungs-Operatoren Druck-Operatoren Server Operatoren Domain Controller nur-Lese Directory-Domänencontrollergruppe Richtlinie Creators Besitzer kryptografischen Operatoren

         > [!NOTE]
         > Note: Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Note: Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

#### <a name="deploy-your-paws"></a>Bereitstellen der PAW(s)

   > [!NOTE]
   > Stellen Sie sicher, dass die Verbindung zwischen PAW und Netzwerk während des Buildprozesses des Betriebssystems getrennt ist.

1. Installieren Sie Windows 10 von den Installationsmedien aus vertrauenswürdiger Quelle, die Sie zuvor bezogen haben.

   > [!NOTE]
   > Sie können das Microsoft Deployment Toolkit (MDT) oder ein anderes System zur automatisierten Bereitstellung von Images verwenden, um die PAW-Bereitstellung zu automatisieren. Sie müssen allerdings sicherstellen, dass der Buildprozess so vertrauenswürdig ist wie die PAW. Angreifer suchen sich gezielt Unternehmensimages und -bereitstellungssysteme (z.B. ISOs, Bereitstellungspakete usw.) als Persistenzmechanismus aus , daher sollten keine bereits vorhandenen Bereitstellungssysteme oder Images verwendet werden.
   >
   > Wenn Sie die Bereitstellung der PAW automatisieren, müssen Sie Folgendes ausführen:
   >
   > * Erstellen Sie das System über Installationsmedien, die mithilfe der in [Vertrauenswürdige Quelle für Installationsmedien](http://aka.ms/cleansource) beschriebenen Verfahren überprüft wurden.
   > * Stellen Sie sicher, dass die Verbindung zwischen dem automatisierten Bereitstellungssystem und dem Netzwerk während des Buildprozesses des Betriebssystems getrennt ist.

2. Legen Sie ein eindeutiges komplexes Kennwort für das lokale Administratorkonto fest.  Verwenden Sie kein Kennwort, das bereits für ein anderes Konto in der Umgebung verwendet wurde.

   > [!NOTE]
   > Microsoft empfiehlt die Verwendung der [Local Administrator Password Solution (LAPS)](https://www.microsoft.com/en-us/download/details.aspx?id=46899), um lokale Administratorkennwörter für alle Arbeitsstationen einschließlich PAWs zu verwalten.  Wenn Sie LAPS verwenden, stellen Sie sicher, dass Sie nur der Gruppe „PAW Maintenance“ die Berechtigung zum Lesen der über LAPS verwalteten Kennwörter für die PAWs erteilen.

3. Installieren Sie die Remoteserver-Verwaltungstools für Windows 10 mithilfe der Installationsmedien aus vertrauenswürdiger Quelle.
4. Konfigurieren von Windows Defender Exploit Guard

   > [!NOTE]
   > Konfigurationsrichtlinien folgen

5. Verbinden Sie die PAW mit dem Netzwerk.  Stellen Sie sicher, dass die PAW mit mindestens einem Domänencontroller eine Verbindung herstellen kann.
6. Verwenden Sie ein Konto, das Mitglied der Gruppe „PAW Maintenance“ ist, und führen Sie auf der neu erstellten PAW folgenden PowerShell-Befehl aus, um die PAW in der entsprechenden Organisationseinheit zur Domäne hinzuzufügen:

   `Add-Computer -DomainName Fabrikam -OUPath "OU=Devices,OU=Tier 0,OU=Admin,DC=fabrikam,DC=com"`

   Ersetzen Sie die Verweise auf *Fabrikam* durch Ihren Domänennamen.  Wenn Ihr Domänenname mehrere Ebenen umfasst (z.B. child.fabrikam.com), fügen Sie die zusätzlichen Namen mit dem Bezeichner „DC=“ in der Reihenfolge hinzu, in der sie im vollqualifizierten Domänennamen der Domäne angezeigt werden.

   > [!NOTE]
   > Wenn Sie eine [Administrative ESAE-Gesamtstruktur](http://aka.ms/esae) (für Administratoren auf Ebene 0 in Phase 1) oder eine [PAM-Lösung (Privileged Access Management) in Microsoft Identity Manager (MIM)](http://aka.ms/mimpamdeploy) (für Administratoren der Ebenen 1 und 2 in Phase 2) bereitgestellt haben, fügen Sie die PAW zur Domäne in dieser Umgebung anstatt zur Produktionsdomäne hinzu.

7. Wenden Sie alle kritischen und wichtigen Windows-Updates an, bevor Sie andere Softwareanwendungen (z.B. Verwaltungstools, Agents usw.) installieren.
8. Erzwingen Sie die Anwendung der Gruppenrichtlinie.
   1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten aus, und geben Sie den folgenden Befehl aus: `Gpupdate /force /sync`
   2. Starten Sie den Computer neu.

9. (Optional) Installieren Sie weitere erforderliche Tools für Active Directory-Administratoren. Installieren Sie weitere Tools oder Skripts, die zur Ausführung von beruflichen Aufgaben benötigt werden. Stellen Sie sicher, dass Sie das Risiko bewerten, das mit dem Verfügbarmachen von Anmeldeinformationen auf den Zielcomputern mit einem beliebigen Tool einhergeht, bevor Sie das Tool auf einer PAW installieren. Auf [dieser Seite](http://aka.ms/logontypes) erhalten Sie weitere Informationen zur Bewertung des Risikos für Anmeldeinformationen durch Verwaltungstools und Verbindungsmethoden. Stellen Sie sicher, dass beim Beziehen sämtlicher Installationsmedien die in [Vertrauenswürdige Quelle für Installationsmedien](http://aka.ms/cleansource) beschriebenen Verfahren angewendet werden.

   > [!NOTE]
   > Die Verwendung eines Sprungbrettservers als zentralen Speicherort für diese Tools kann die Komplexität reduzieren, auch wenn der Server nicht als Sicherheitsgrenze dient.

10. (Optional) Herunterladen Sie und installieren Sie erforderliche Remotezugriffssoftware. Wenn Administratoren die PAW zur Remoteverwaltung verwenden, installieren Sie die Remotezugriffssoftware, und beachten Sie die entsprechenden Sicherheitsinformationen Ihres Anbieters der Remotezugriffssoftware. Stellen Sie sicher, dass beim Beziehen sämtlicher Installationsmedien die in „Vertrauenswürdige Quelle für Installationsmedien“ beschriebenen Verfahren angewendet werden.

   > [!NOTE]
   > Wägen Sie sorgfältig alle Risiken ab, die mit dem Gewähren des Remotezugriffs über eine PAW einhergehen.  Eine mobile PAW ermöglicht zwar viele wichtige Szenarien, beispielsweise das Arbeiten von zu Hause, allerdings ist Remotezugriffssoftware potenziell anfällig für Angriffe und kann eine PAW gefährden.

11. Überprüfen Sie die Integrität des PAW-Systems, indem Sie folgende Schritte durchführen, um die Einstellungen zu prüfen und zu bestätigen, dass alle Einstellungen ordnungsgemäß eingerichtet sind:
   1. Vergewissern Sie sich, dass nur die PAW-spezifischen Gruppenrichtlinien auf die PAW angewendet wurden.
      1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten aus, und geben Sie den folgenden Befehl aus: `Gpresult /scope computer /r`
      2. Überprüfen Sie die ausgegebene Liste, und stellen Sie sicher, dass nur diejenigen Gruppenrichtlinien angezeigt werden, die Sie weiter oben selbst erstellt haben.
   2. Vergewissern Sie sich mithilfe der folgenden Schritte, dass keine anderen Benutzerkonten Mitglied von privilegierten Gruppen auf der PAW sind:
      1. Öffnen Sie **Lokale Benutzer und Gruppen bearbeiten** (lusrmgr.msc), wählen Sie **Gruppen** aus, und vergewissern Sie sich, dass das lokale Administratorkonto und die globale Sicherheitsgruppe „PAW Maintenance“ die einzigen Mitglieder der lokalen Administratorengruppe sind.

         > [!NOTE]
         > Die Gruppe „PAW Users“ darf kein Mitglied der lokalen Administratorengruppe sein.  Als einzige Mitglieder zulässig sind das lokale Administratorkonto und die globale Sicherheitsgruppe „PAW Maintenance“ (und die Gruppe „PAW Users“ darf auch kein Mitglied dieser globalen Gruppe sein).

      2. Stellen Sie, ebenfalls mithilfe von **Lokale Benutzer und Gruppen bearbeiten**, sicher, dass die folgenden Gruppen keine Mitglieder enthalten: Sicherungs-Operatoren-Kryptografie-Operatoren-Hyper-V-Administratoren Network Configuration Operatoren Power Benutzer Remotedesktopbenutzer Replikatoren

12. (Optional) Wenn Ihre Organisation eine Sicherheitsinformationen und Ereignis-verwaltungslösung (SIEM) verwendet, stellen Sie sicher, dass die PAW [so konfiguriert, dass Ereignisse an das System über (Windows Event Forwarding, WEF) weiterleiten](http://blogs.technet.com/b/jepayne/archive/2015/11/24/monitoring-what-matters-windows-event-forwarding-for-everyone-even-if-you-already-have-a-siem.aspx) oder andernfalls registriert ist, mit der Lösung, damit dem SIEM-Server aktiv Ereignisse und Informationen von der PAW empfängt.  Die Details dieses Vorgangs variieren basierend auf Ihrer SIEM-Lösung.

   > [!NOTE]
   > Wenn Ihre SIEM-Lösung einen Agent erfordert, der auf den PAWs mit einem Systemadministratorkonto oder einem lokalen Administratorkonto ausgeführt wird, stellen Sie sicher, dass die SIEM-Lösung auf der gleichen Vertrauensebene verwaltet wird wie Ihre Domänencontroller und Identitätssysteme.

13. (Optional) Wenn Sie LAPS zur Verwaltung des Kennworts für das lokale Administratorkonto auf Ihrer PAW bereitstellen möchten, stellen Sie sicher, dass das Kennwort erfolgreich registriert wurde.

   * Verwenden Sie ein Konto, das über Berechtigungen zum Lesen von über LAPS verwalteten Kennwörtern verfügt, und öffnen Sie **Active Directory-Benutzer und -Computer** (dsa.msc).  Stellen Sie sicher, dass die erweiterten Funktionen aktiviert sind, und klicken Sie mit der rechten Maustaste auf das entsprechende Computerobjekt.  Wählen Sie die Registerkarte „Attribut-Editor“ aus, und vergewissern Sie sich, dass der Wert für msSVSadmPwd mit einem gültigen Kennwort aufgefüllt ist.

### <a name="phase-2-extend-paw-to-all-administrators"></a>Phase 2: Erweitern der PAW auf alle Administratoren

Umfang: Alle Benutzer mit administrativen Rechten für unternehmenskritische Anwendungen und Abhängigkeiten.  Hierzu sollten mindestens die Administratoren von Anwendungsservern, Lösungen zur Überwachung der betrieblichen Stabilität und Sicherheit, Virtualisierungslösungen, Speichersystemen und Netzwerkgeräten gehören.

> [!NOTE]
> Bei den Anweisungen in dieser Phase wird vorausgesetzt, dass Phase 1 vollständig abgeschlossen ist.  Beginnen Sie nicht mit Phase 2, wenn noch nicht alle Schritte in Phase 1 abgeschlossen sind.

Sobald Sie sich vergewissert haben, dass alle Schritte vollständig abgeschlossen wurden, führen Sie die unten stehenden Schritte für Phase 2 durch:

#### <a name="recommended-enable-restrictedadmin-mode"></a>(Empfohlen) Aktivieren Sie **RestrictedAdmin** Modus

Aktivieren Sie dieses Feature auf Ihren vorhandenen Servern und Arbeitsstationen, und erzwingen Sie die Verwendung dieses Features zu. Diese Funktion muss auf die Zielservern Windows Server 2008 R2 ausgeführt werden oder höher und auf den Zielarbeitsstationen Windows 7 oder höher ausgeführt werden.

1. Aktivieren Sie den Modus **RestrictedAdmin** auf Ihren Servern und Arbeitsstationen, indem Sie die Anweisungen auf [dieser Seite](http://aka.ms/rdpra) befolgen.

   > [!NOTE]
   > Bevor Sie diese Funktion für Server mit Internetzugang aktivieren, erwägen Sie das Risiko, dass Angreifer sich mit einem zuvor gestohlenen Kennworthash auf diesen Servern authentifizieren können.

2. Erstellen Sie das Gruppenrichtlinienobjekt „RestrictedAdmin erforderlich – Computer“. In diesem Abschnitt wird ein Gruppenrichtlinienobjekt erstellt, das die Verwendung der Option „/RestrictedAdmin“ für ausgehende Remotedesktopverbindungen erzwingt, um die Konten vor dem Risiko durch gestohlene Anmeldeinformationen auf den Zielsystemen zu schützen.
   * Wechseln Sie zu „Computerkonfiguration\Richtlinien\Administrative Vorlagen\System\Delegierung von Anmeldeinformationen\Delegierung von Anmeldeinformationen an Remoteserver einschränken“, und legen Sie die Einstellung auf **Aktiviert** fest.
3. Verknüpfen Sie **RestrictedAdmin erforderlich – Computer** mit den jeweiligen Geräten auf Ebene 1 und/oder Ebene 2, und verwenden Sie dabei die folgenden Richtlinienoptionen:
   * PAW-Konfiguration – Computer
      * -> Speicherort aus: Admin\Tier 0\Devices (vorhanden)
   * PAW-Konfiguration – Benutzer
      * -> Speicherort aus: Admin\Tier 0\Accounts
   * RestrictedAdmin erforderlich – Computer
      * -> Admin\Tier1\Devices oder der-> Admin\Tier2\Devices (beide sind optional.)

   > [!NOTE]
   > Dies ist für Systeme auf Ebene 0 nicht erforderlich, da diese Systeme bereits über Vollzugriff auf alle Assets in der Umgebung verfügen.

#### <a name="move-tier-1-objects-to-the-appropriate-ous"></a>Verschieben Sie Objekte der Ebene 1 mit den entsprechenden Organisationseinheiten

1. Verschieben Sie Gruppen der Ebene 1 in die OE „Admin\Tier 1\Groups“. Suchen Sie alle Gruppen, die die folgenden administrativen Berechtigungen gewähren, und verschieben Sie sie in diese OE.
   * Lokaler Administrator auf mehreren Servern
      * Administratorzugriff auf Clouddienste
      * Administratorzugriff auf Unternehmensanwendungen
2. Verschieben Sie Konten auf Ebene 1 in die OE „Admin\Tier 1\Accounts“. Verschieben Sie jedes Konto, das Mitglied dieser Gruppen auf Ebene 1 ist (einschließlich geschachtelter Mitgliedschaften), in diese OE.
3. Hinzufügen der geeigneten Mitglieder zu den jeweiligen Gruppen
   * **Tier 1 Admins**: Diese Gruppe enthält die Administratoren auf Ebene 1, die sich nicht bei Hosts auf Ebene 2 anmelden dürfen. Fügen Sie all Ihre Verwaltungsgruppen auf Ebene 1 hinzu, die über Administratorrechte für Server oder Internetdienste verfügen.

      > [!NOTE]
      > Wenn es zu den Aufgaben eines Verwaltungsmitarbeiters gehört, Assets auf mehreren Ebenen zu verwalten, müssen Sie für jede Ebene ein separates Administratorkonto erstellen.

4. Aktivieren Sie Credential Guard, um das Risiko zu senken, dass Anmeldeinformationen gestohlen und wiederverwendet werden.  Credential Guard ist ein neues Feature von Windows 10, das den Zugriff von Anwendungen auf Anmeldeinformationen einschränkt, um Angriffe durch Diebstahl von Anmeldeinformationen (z.B. Pass-the-Hash) zu verhindern.  Credential Guard ist für den Endbenutzer vollständig transparent, und die Einrichtung erfordert nur wenig Zeit und Aufwand.  Weitere Informationen zu Credential Guard einschließlich der Bereitstellungsschritte und Hardwarevoraussetzungen finden Sie im Artikel [Schützen von Domänenanmeldeinformationen mit Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx).

   > [!NOTE]
   > Um Credential Guard konfigurieren und verwenden zu können, muss Device Guard aktiviert sein.  Sie müssen aber keine weiteren Device Guard-Schutzfunktionen konfigurieren, um Credential Guard verwenden zu können.

5. (Optional) Aktivieren Sie Verbindungen mit Clouddiensten. Dieser Schritt ermöglicht die Verwaltung von Clouddiensten wie Azure und Office 365 mit geeigneten Sicherheitsmaßnahmen. Dieser Schritt ist auch erforderlich, damit die PAWs über Microsoft Intune verwaltet werden können.

   > [!NOTE]
   > Überspringen Sie diesen Schritt, wenn Sie für die Verwaltung von Clouddiensten oder die Verwaltung über Intune keine Cloudkonnektivität benötigen.

   * Diese Schritte beschränken die Kommunikation über das Internet ausschließlich auf autorisierte Clouddienste (Kommunikation mit dem offenen Internet ist nicht möglich) und fügen Schutzmaßnahmen für die Browser und andere Anwendungen hinzu, die Inhalte aus dem Internet verarbeiten. Diese PAWs für die Verwaltung sollten niemals für Standardbenutzeraufgaben wie Internetkommunikation und Produktivitätsanwendungen verwendet werden.
   * Um Verbindungen mit PAW-Diensten zu aktivieren, führen Sie die folgenden Schritte aus:

   1. Konfigurieren Sie die PAW so, dass nur autorisierte Internetziele zugelassen werden.  Wenn Sie Ihre PAW-Bereitstellung auf die Verwaltung in der Cloud erweitern, müssen Sie den Zugang zu autorisierten Diensten zulassen und gleichzeitig den Zugriff aus dem offenen Internet unterbinden, da ein solcher Zugriff potenzielle Angriffe auf Ihre Administratorkonten vereinfacht.

      1. Erstellen Sie die Gruppe **Clouddienstadministratoren**, und fügen Sie der Gruppe alle Konten hinzu, die Zugriff auf Clouddienste im Internet benötigen.
      2. Laden Sie die PAW-Datei *proxy.pac* aus der [TechNet-Galerie](http://aka.ms/pawmedia) herunter, und veröffentlichen Sie sie auf einer internen Website.

         > [!NOTE]
         > Sie müssen die Datei *proxy.pac* nach dem Herunterladen aktualisieren, um sicherzustellen, dass sie aktuell und vollständig ist.  
         > Microsoft veröffentlicht alle aktuellen Office 365- und Azure-URLs im [Supportcenter](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US) für Office. Bei dieser Anleitung wird davon ausgegangen, dass Sie Internet Explorer (oder Microsoft Edge) für die Verwaltung von Office 365, Azure und anderen Clouddiensten verwenden. Microsoft empfiehlt, ähnliche Einschränkungen für Drittanbieterbrowser zu konfigurieren, die Sie für die Verwaltung benötigen. Webbrowser sollten auf PAWs nur zur Verwaltung von Clouddiensten verwendet werden, niemals zum allgemeinen Webbrowsen.
         >
         > Möglicherweise müssen Sie der Liste weitere gültige Internetziele für andere IaaS-Anbieter hinzufügen. Fügen Sie jedoch keine Produktivitäts-, Unterhaltungs-, Nachrichten- oder Suchwebsites zu dieser Liste hinzu.
         >
         > Möglicherweise müssen Sie auch die PAC-Datei um eine gültige Proxyadresse zur Verwendung mit diesen Adressen ergänzen.
         >
         > Sie können den Zugriff von der PAW auch einschränken, indem Sie zur umfassenden Verteidung außerdem einen Webproxy einsetzen. Es wird nicht empfohlen, diese Vorgehensweise ohne PAC-Datei zu verwenden, da hierbei der Zugriff für PAWs nur beschränkt wird, wenn eine Verbindung mit dem Unternehmensnetzwerk besteht.

      3. Sobald Sie die Datei *proxy.pac* konfiguriert haben, aktualisieren Sie das Gruppenrichtlinienobjekt „PAW-Konfiguration – Benutzer“.
         1. Wechseln Sie zum Benutzer Configuration\Preferences\Windows Settings\Registry. Mit der rechten Maustaste Registrierung, wählen Sie **neu** > **Registrierungselement** und konfigurieren Sie die folgenden Einstellungen:
            1. Aktion: Ersetzen
            2. Struktur: HKEY_ CURRENT_USER
            3. Schlüsselpfad: Software\Microsoft\Windows\CurrentVersion\Internet Settings
            4. Wertname: AutoConfigUrl

               > [!NOTE]
               > Aktivieren Sie nicht das Feld **Standard** links neben dem Namen des Werts.

            5. Werttyp: REG_SZ
            6. Wertdaten: Geben Sie die vollständige URL in die *proxy.pac* -Datei, einschließlich http:// und die File-Name – z. B. http://proxy.fabrikam.com/proxy.pac.  Die URL kann einer einzelnen Bezeichnung-URL - auch zum Beispiel sein, http://proxy/proxy.pac

               > [!NOTE]
               > Die PAC-Datei kann auch auf einer Dateifreigabe gehostet werden, die Syntax lautet: file://server.fabrikan.com/share/proxy.pac. Hierfür muss aber das file://-Protokoll zugelassen werden. Finden Sie unter der "Hinweis: File://-Based Proxy Skripts veraltet"im Abschnitt dieses [Understanding Web Proxy Configuration](http://blogs.msdn.com/b/ieinternals/archive/2013/10/11/web-proxy-configuration-and-ie11-changes.aspx) Blog, um weitere Informationen zum Konfigurieren des erforderlichen Registrierungswerts.

            7. Klicken Sie auf die Registerkarte **Allgemein**, und wählen Sie **Element entfernen, wenn es nicht mehr angewendet wird** aus.
            8. Wählen Sie auf der Registerkarte **Allgemein** die Option **Zielgruppenadressierung auf Elementebene**, und klicken Sie dann auf **Zielgruppenadressierung**.
            9. Klicken Sie auf **Neues Element**, und wählen Sie die Option **Sicherheitsgruppe** aus.
            10. Wählen Sie die Schaltfläche „...“ aus, und suchen Sie nach der Gruppe **Cloud Services-Administratoren**.
            11. Klicken Sie auf **Neues Element**, und wählen Sie die Option **Sicherheitsgruppe** aus.
            12. Wählen Sie die Schaltfläche „...“ aus, und suchen Sie nach der Gruppe **PAW Users**.
            13. Klicken Sie auf das Element **PAW Users** und dann auf **Elementoptionen**.
            14. Wählen Sie **Ist nicht** aus.
            15. Klicken Sie im Fenster für die Zielgruppenadressierung auf **OK**.
            16. Klicken Sie auf **OK**, um die **AutoConfigUrl**-Gruppenrichtlinieneinstellung abzuschließen.
   2. Wenden Sie Windows 10-Sicherheitsbaselines und den Clouddienstzugriff an. Verknüpfen Sie die Sicherheitsbaselines für Windows und den Clouddienstzugriff (sofern erforderlich) mit den richtigen Organisationseinheiten. Führen Sie dazu folgende Schritte aus:
      1. Extrahieren Sie den Inhalt der ZIP-Datei mit den Windows 10-Sicherheitsbaselines.
      2. Erstellen Sie die entsprechenden Gruppenrichtlinienobjekte, [importieren Sie die Richtlinieneinstellungen](https://technet.microsoft.com/library/cc753786.aspx), und erstellen Sie die [Verknüpfungen](https://technet.microsoft.com/library/cc732979.aspx) gemäß der folgenden Tabelle. Verknüpfen Sie jede Richtlinie mit jedem Speicherort, und stellen Sie sicher, dass die Reihenfolge der Tabelle entspricht (spätere Einträge in der Tabelle sollten später und mit höherer Priorität angewendet werden):

         **Richtlinien:**

         |||
         |-|-|
         |CM Windows 10 – Domänensicherheit|N/V – zum jetzigen Zeitpunkt nicht verknüpfen|
         |SCM Windows 10 TH2 – Computer|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Windows 10 TH2 – BitLocker|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Windows 10 – Credential Guard|Admin\Tier 0\Devices|
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
         |SCM Windows 10 – User|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Internet Explorer – Benutzer|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |PAW-Konfiguration – Benutzer|Admin\Tier 0\Devices (vorhanden)|
         ||Admin\Tier 1\Devices (neue Verknüpfung)|
         ||Admin\Tier 2\Devices (neue Verknüpfung)|

         > [!NOTE]
         > Das Gruppenrichtlinienobjekt „CM Windows 10 – Domänensicherheit“ kann unabhängig von der PAW mit der Domäne verknüpft werden, wirkt sich jedoch auf die gesamte Domäne aus.

6. (Optional) Installieren Sie weitere erforderliche Tools für Administratoren auf Ebene 1 an. Installieren Sie weitere Tools oder Skripts, die zur Ausführung von beruflichen Aufgaben benötigt werden. Stellen Sie sicher, dass Sie das Risiko bewerten, das mit dem Verfügbarmachen von Anmeldeinformationen auf den Zielcomputern mit einem beliebigen Tool einhergeht, bevor Sie das Tool auf einer PAW installieren. Auf [dieser Seite](http://aka.ms/logontypes) erhalten Sie weitere Informationen zur Bewertung des Risikos für Anmeldeinformationen durch Verwaltungstools und Verbindungsmethoden. Stellen Sie sicher, dass beim Beziehen sämtlicher Installationsmedien die in „Vertrauenswürdige Quelle für Installationsmedien“ beschriebenen Verfahren angewendet werden.
7. Identifizieren Sie die Software und Anwendungen, die für die Verwaltung benötigt werden, und beziehen Sie diese auf sichere Weise.  Dieser Schritt ähnelt den entsprechenden Aufgaben in Phase 1, deckt aber einen umfassenderen Bereich ab, da mehr Anwendungen, Dienste und Systeme gesichert werden müssen.

   > [!NOTE]
   > Stellen Sie sicher, dass Sie diese neuen Anwendungen (einschließlich Webbrowsern) geschützt durch Entscheidung für in die Schutzmaßnahmen, die von Windows Defender Exploit Guard.

   Beispiele für zusätzliche Software und Anwendungen:

      * Microsoft Azure PowerShell
      * Office 365 PowerShell (auch bekannt als Microsoft Online Services-Modul)
      * Auf der Microsoft Management Console (MMC) basierende Software für die Anwendungs- oder Dienstverwaltung
      * Proprietäre (nicht MMC-basierte) Software für die Anwendungs- oder Dienstverwaltung

         > [!NOTE]
         > Viele Anwendungen, einschließlich einer Vielzahl von Clouddiensten, werden heute ausschließlich über Webbrowser verwaltet.  Dadurch sinkt zwar die Anzahl der Anwendungen, die auf einer PAW installiert werden müssen, gleichzeitig steigt aber auch das Risiko von Interoperabilitätsproblemen der Browser.  Möglicherweise müssen Sie auf bestimmten PAW-Instanzen einen nicht von Microsoft stammenden Webbrowser bereitstellen, um die Verwaltung bestimmter Dienste zu ermöglichen.  Wenn Sie einen zusätzlichen Webbrowser bereitstellen, stellen Sie sicher, dass Sie das Prinzip der vertrauenswürdigen Quelle befolgen und den Browser gemäß den Sicherheitsinformationen des Herstellers sichern.

8. (Optional) Herunterladen Sie und installieren Sie alle erforderlichen Verwaltungs-Agents.

   > [!NOTE]
   > Wenn Sie zusätzliche Verwaltungs-Agents installieren (für Überwachung, Sicherheit, Konfigurationsverwaltung usw.), müssen Sie unbedingt sicherstellen, dass den Verwaltungssystemen auf der gleichen Stufe vertraut wird wie den Domänencontrollern und Identitätssystemen. Weitere Informationen hierzu finden Sie unter „Verwalten und Aktualisieren von PAWs“.

9. Bewerten Sie Ihre Infrastruktur, um Systeme zu ermitteln, in denen die zusätzlichen Sicherheitsmaßnahmen erforderlich sind, die durch eine PAW bereitgestellt werden.  Stellen Sie sicher, dass Sie genau wissen, welche Systeme geschützt werden müssen.  Stellen Sie kritische Fragen zu den Ressourcen selbst:

   * Wo befinden sich die Zielsysteme, die verwaltet werden müssen?  Befinden sie sich an einem einzigen physischen Ort, oder sind sie mit einem klar definierten Subnetz verbunden?
   * Wie viele Systeme sind vorhanden?
   * Sind diese Systeme von anderen Systemen abhängig (z.B. Virtualisierungs- oder Speichersystemen usw.)? Falls ja, wie werden diese Systeme verwaltet?  Wie werden die kritischen Systeme für diese Abhängigkeiten verfügbar gemacht, und welche zusätzlichen Risiken bestehen durch diese Abhängigkeiten?
   * Wie kritisch sind die verwalteten Dienste, und mit welchen Verlusten ist zu rechnen, falls diese Dienste gefährdet sind?

      > [!NOTE]
      > Beziehen Sie Ihre Clouddienste in diese Bewertung ein. Angreifer zielen immer häufiger auf unsichere Cloudbereitstellungen ab, daher müssen Sie diese Dienste mit den gleichen Sicherheitsstandards verwalten wie Ihre unternehmenskritischen lokalen Anwendungen.

        Verwenden Sie diese Bewertung, um Systeme zu identifizieren, die zusätzlichen Schutz benötigen, und erweitern Sie Ihr PAW-Programm auf die Administratoren dieser Systeme.  SQL Server (sowohl lokal also auch SQL Azure), Anwendungen für Personalabteilungen und Finanzsoftware sind Beispiele für Systeme, denen die PAW-basierte Verwaltung erhebliche Vorteile bietet.

        > [!NOTE]
        > Wenn eine Ressource über ein Windows-System verwaltet wird, kann sie auch mit einer PAW verwaltet werden, auch wenn die Anwendung selbst unter einem anderen Betriebssystem als Windows oder auf einer nicht von Microsoft stammenden Cloudplattform ausgeführt wird.  Beispielsweise sollte der Besitzer eines Amazon Web Services-Abonnements eine PAW nur für die Verwaltung dieses Kontos verwenden.

10. Entwickeln Sie eine Anforderungs- und Verteilungsmethode zur Bereitstellung von PAWs in großem Umfang in Ihrer Organisation.  Je nachdem, wie viele PAWs Sie in Phase 2 bereitstellen möchten, müssen Sie den Prozess möglicherweise automatisieren.

   * Ziehen Sie in Betracht, einen formellen Anforderungs- und Genehmigungsprozess für Administratoren zu entwickeln, den diese zum Erhalten einer PAW durchlaufen müssen.  Mit einem solchen Prozess können Sie den Bereitstellungsprozess standardisieren, die Verantwortlichkeit für PAW-Geräte sicherstellen und Lücken bei der PAW-Bereitstellung identifizieren.
   * Wie bereits erläutert, sollte diese Bereitstellungslösung von vorhandenen Automatisierungsmethoden (die möglicherweise bereits gefährdet sind) getrennt werden und den in Phase 1 beschriebenen Prinzipien folgen.

        > [!NOTE]
        > Jedes System, das zur Verwaltung von Ressourcen verwendet wird, sollte selbst auf der gleichen oder einer höheren Vertrauensebene verwaltet werden.

11. Überprüfen Sie die vorhandenen PAW-Hardwareprofile, und stellen Sie bei Bedarf zusätzliche bereit.  Ein Hardwareprofil, das Sie für Phase 1 ausgewählt haben, eignet sich möglicherweise nicht für alle Administratoren.  Überprüfen Sie die Hardwareprofile, und wählen Sie ggf. zusätzliche Profile aus, um die Anforderungen der Administratoren zu erfüllen.  Das Profil „Dedizierte Hardware“ (Trennung von PAWs und Arbeitsstationen für tägliche Aufgaben) eignet sich möglicherweise nicht für einen Administrator, der viel unterwegs ist. In diesem Fall sollten Sie für diesen Administrator das Profil „Gleichzeitige Verwendung“ bereitstellen (PAW mit Benutzer-VM).
12. Berücksichtigen Sie die Anforderungen hinsichtlich Kultur, Betrieb, Kommunikation und Schulungsbedarf, die mit einer erweiterten PAW-Bereitstellung einhergehen.   Eine so wesentliche Änderung an einem Verwaltungsmodell erfordert naturgemäß auch ein gewisses Maß an Change Management, und es ist wichtig, dieses in das Bereitstellungsprojekt selbst zu integrieren.  Beziehen Sie mindestens die folgenden Punkte in Ihre Planung ein:

   * Wie kommunizieren Sie die Änderungen an die Führungsebene, um sich deren Unterstützung zu sichern?  Ein Projekt, das nicht von den Führungskräften unterstützt wird, wird wahrscheinlich scheitern bzw. es wird zumindest schwierig, die notwendige Finanzierung und allgemeine Akzeptanz zu erhalten.
   * Wie dokumentieren Sie den neuen Prozess für Administratoren?  Diese Änderungen müssen dokumentiert und mitgeteilt werden, und zwar nicht nur den vorhandenen Administratoren (die ihre Gewohnheiten ändern und Ressource auf andere Weise verwalten müssen), sondern auch neuen Administratoren (die innerhalb der Organisation befördert oder neu eingestellt wurden).  Die Dokumentation muss klar verständlich sein und die Bedeutung von Bedrohungen, die Rolle von PAWs für den Schutz der Administratoren und die richtige Verwendung der PAWs vollständig und ausführlich erläutern.

      > [!NOTE]
      > Dies ist insbesondere bei Rollen mit hoher Fluktuation sehr wichtig, z.B. bei Helpdeskmitarbeitern.

   * Wie stellen Sie die Kompatibilität mit dem neuen Prozess sicher?  Das PAW-Modell bietet zwar eine Reihe von technischen Kontrollmechanismen, um die Offenlegung privilegierter Anmeldeinformationen zu verhindern, allerdings ist es unmöglich, alle möglichen Gefährdungen allein mit technischen Mitteln zu vermeiden.  Ein Beispiel: Es lässt sich zwar verhindern, dass ein Administrator sich erfolgreich mit privilegierten Anmeldeinformationen an einem Benutzerdesktop anmeldet, aber schon der einfache Versuch einer solchen Anmeldung kann die Anmeldeinformationen für eine Schadsoftware verfügbar machen, die sich auf diesem Computer befindet.  Von daher ist es von essenzieller Bedeutung, dass Sie nicht nur die Vorteile des PAW-Modells aufzeigen, sondern auch die Risiken klar herausstellen, die durch Nichteinhaltung von Regeln und Anweisungen entstehen können.  Ergänzen Sie dieses Konzept durch Überwachungs- und Warnungsfunktionen, sodass eine Offenlegung von Anmeldeinformationen schnell erkannt und behoben werden kann.

### <a name="phase-3-extend-and-enhance-protection"></a>Phase 3: Erweitern und Verbessern des Schutzes

Umfang: Diese Schutzmaßnahmen erweitern die Systeme, die in Phase 1 ergänzen den grundlegenden Schutz mit erweiterten Features, einschließlich Multi-Factor-Authentifizierung und Netzwerkzugriffsregeln erstellt.

> [!NOTE]
> Diese Phase kann jederzeit nach Abschluss von Phase 1 ausgeführt werden.  Sie ist nicht von der Beendigung von Phase 2 abhängig, kann also vor, gleichzeitig mit oder nach Phase 2 erfolgen.

Führen Sie die folgenden Schritte aus, um diese Phase zu konfigurieren:

1. **Aktivieren von Multi-Factor Authentication für privilegierte Konten**.  Die mehrstufige Authentifizierung verstärkt die Kontosicherheit, da der Benutzer zusätzlich zu den Anmeldeinformationen auch ein physisches Token bereitstellen muss.  Die mehrstufige Authentifizierung ist eine hervorragende Ergänzung zu Authentifizierungsrichtlinien, ihre Bereitstellung hängt aber nicht von Authentifizierungsrichtlinien ab (und umgekehrt ist für Authentifizierungsrichtlinien keine mehrstufige Authentifizierung erforderlich).  Microsoft empfiehlt die Verwendung einer der folgenden Formen der mehrstufigen Authentifizierung:

   * **Smartcard**: Eine Smartcard ist ein Manipulationssicheres, tragbares physisches Gerät eine zweite Überprüfung während des Anmeldevorgangs für Windows bietet.  Indem Sie voraussetzen, dass ein Benutzer für die Anmeldung eine Karte besitzen und bereitstellen muss, können Sie das Risiko senken, dann gestohlene Anmeldeinformationen remote wiederverwendet werden.  Einzelheiten zur Anmeldung an Windows mithilfe einer Smartcard finden Sie im Artikel [Smartcard: Übersicht](https://technet.microsoft.com/library/hh831433.aspx).
   * **Virtuelle Smartcard**:  Eine virtuelle Smartcard bietet die gleichen Sicherheitsvorteile wie physische Smartcards und mit den zusätzlichen Vorteil, die an bestimmte Hardwarekomponenten gekoppelt verknüpft wird.  Weitere Informationen zur Bereitstellung und hardwareanforderungen finden Sie in den Artikeln [Virtual Smart Card Overview](https://technet.microsoft.com/library/dn593708.aspx) und [erste Schritte mit virtuellen Smartcards: Handbuch mit exemplarischer Vorgehensweise](https://technet.microsoft.com/library/dn579260.aspx).
   * **Windows Hello for Business**: Windows Hello for Business können Benutzer, authentifizieren Sie sich bei einem Microsoft-Konto, Active Directory-Konto, ein Konto für Microsoft Azure Active Directory (Azure AD) oder nicht-Microsoft-Dienst, der ID Online FIDO Authentifizierung (Fast) unterstützt. Nach einer anfänglichen zweistufigen Überprüfung während der Windows Hello for Business-Registrierung einer Windows Hello for Business ist richten Sie auf dem Gerät des Benutzers und der Benutzer legt eine Geste fest, die Windows Hello oder eine PIN sein kann. Windows Hello for Business-Anmeldeinformationen sind ein asymmetrisches Schlüsselpaar, die in isolierten Umgebungen Trusted Platform Module (TPM) generiert werden kann.
      Weitere Informationen zu Windows Hello für Business-Lesevorgang [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification) Artikel.
   * **Azure Multi-Factor Authentication**:  Azure Multi-Factor-Authentication (MFA) bietet die Sicherheit eines zweiten überprüfungsfaktors sowie die erweiterten Schutz durch Überwachung und Machine Learning-basierte Analyse.  Die Azure MFA bietet nicht nur Sicherheit und Schutz für Azure-Administratoren, sondern auch für viele weitere Lösungen, wie z.B. Webanwendungen, Azure Active Directory und lokale Lösungen wie Remotezugriff und Remotedesktop.  Weitere Informationen zur Azure Multi-Factor Authentication finden Sie im Artikel [Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication).

2. **Whitelist vertrauenswürdige Anwendungen, die mithilfe von Windows Defender Application Control "bzw." AppLocker**.  Indem Sie die Möglichkeit einschränken, dass nicht vertrauenswürdiger oder nicht signierter Code auf einer PAW ausgeführt wird, können Sie die Wahrscheinlichkeit schädlicher Aktivitäten und Gefährdungen weiter verringern.  Windows bietet zwei primäre Optionen für die Anwendungssteuerung:

   * **AppLocker**:  Mit AppLocker können Administratoren steuern, welche Anwendungen auf einem bestimmten System ausgeführt werden können.  AppLocker kann über Gruppenrichtlinien zentral gesteuert und auf bestimmte Benutzer oder Gruppen angewendet werden (beispielsweise für eine bestimmte Zielanwendung auf die Benutzer einer PAW).  Weitere Informationen zu AppLocker finden Sie im TechNet-Artikel [Technische Übersicht über AppLocker](https://technet.microsoft.com/library/hh831440.aspx).
   * **Windows Defender Application Control**: die neue Windows Defender Application Control-Funktion bietet erweiterte hardwarebasierte anwendungssteuerung, die im Gegensatz zu AppLocker nicht überschrieben werden kann, auf dem betroffenen Gerät.  Windows Defender Application Control können, ebenso wie AppLocker kann über die Gruppenrichtlinie gesteuert und auf bestimmte Benutzer ausgerichtet werden.  Weitere Informationen zum Einschränken der anwendungsnutzung mit Windows Defender Application Control finden Sie in [Windows Defender Application Control-Bereitstellungshandbuch](https://docs.microsoft.com/en-gb/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

3. **Verwenden Sie die Gruppe „Geschützte Benutzer“, Authentifizierungsrichtlinien und Authentifizierungssilos, um privilegierte Konten zusätzlich zu schützen**.  Für die Mitglieder der Gruppe „Geschützte Benutzer“ gelten zusätzliche Sicherheitsrichtlinien, welche die im lokalen Sicherheits-Agent (LSA) gespeicherten Anmeldeinformationen schützen und das Risiko des Diebstahls und der Wiederverwendung von Anmeldeinformationen deutlich senken.  Authentifizierungsrichtlinien und -silos steuern die Art und Weise, in der Benutzer mit bestimmten Berechtigungen auf Ressourcen in der Domäne zugreifen können.  Bei gemeinsamem Einsatz stärken diese Schutzmaßnahmen die Kontosicherheit dieser Benutzer ganz erheblich.  Weitere Informationen zu diesen Funktionen finden Sie im Webartikel [Konfigurieren geschützter Konten](https://technet.microsoft.com/library/dn518179.aspx).

   > [!NOTE]
   > Diese Schutzmaßnahmen sollen die vorhandenen Sicherheitsmaßnahmen in Phase 1 ergänzen, nicht ersetzen.  Administratoren sollten weiterhin getrennte Konten für Verwaltung und allgemeine Nutzung verwenden.

## <a name="managing-and-updating"></a>Verwalten und aktualisieren

PAWs müssen über Funktionen zum Schutz vor Schadsoftware verfügen, und Softwareupdates müssen schnell aufgespielt werden, um die Integrität dieser Arbeitsstationen zu erhalten.

Auf den PAWs können zusätzliche Tools für Konfigurationsverwaltung, Betriebsüberwachung und Sicherheitsverwaltung verwendet werden. Die Integration dieser Tools muss jedoch sorgfältig erwogen werden, da jede Verwaltungsfunktion das Risiko einer Gefährdung der PAW durch das verwendete Tool birgt. Ob es sinnvoll ist, erweiterte Verwaltungsfunktionen einzuführen, hängt von verschiedenen Faktoren wie z.B. den folgenden ab:

* Sicherheitsstatus und -verfahren des Verwaltungstools (z.B. Softwareupdateverfahren für das Tool, Administratorrollen und Konten in diesen Rollen, Betriebssysteme, unter denen das Tool gehostet oder verwaltet wird, sowie weitere Hardware- und Softwareabhängigkeiten des Tools)
* Häufigkeit und Umfang von Softwarebereitstellungen und -updates auf den PAWs
* Anforderungen an detaillierte Bestands- und Konfigurationsinformationen
* Anforderungen an die Sicherheitsüberwachung
* Organisationsinterne Standards und weitere organisationsspezifische Faktoren

Dem Prinzip der vertrauenswürdigen Quelle zufolge muss allen Tools, die zur Verwaltung oder Überwachung der PAWs verwendet werden, mindestens auf der Ebene der PAWs vertraut werden. Das erfordert im Allgemeinen, dass diese Tools über eine PAW verwaltet werden, um sicherzustellen, dass keine Sicherheitsabhängigkeiten von Arbeitsstationen mit niedrigeren Berechtigungen vorhanden sind.

Diese Tabelle erläutert die verschiedenen Vorgehensweisen, die zum Verwalten und Überwachen der PAWs verwendet werden können:

|Vorgehensweise|Überlegungen|
|------|---------|
|Standardmäßig in PAW<br /><br />– Windows Server Update Services<br />– Windows Defender|– Keine Zusatzkosten<br />– Führt erforderliche grundlegende Sicherheitsfunktionen aus<br />– Anweisungen in diesem Leitfaden enthalten|
|Verwalten mit [Intune](https://technet.microsoft.com/library/jj676587.aspx)|<ul><li>Bietet cloudbasierte Transparenz und Kontrolle<br /><br /><ul><li>Softwarebereitstellung</li><li>Verwaltung von Softwareupdates</li><li>Verwaltung von Windows-Firewall-Richtlinien</li><li>Malwareschutz</li><li>Remoteunterstützung</li><li>Softwarelizenzverwaltung.</li></ul></li><li>Keine Serverinfrastruktur erforderlich</li><li>Erfordert das Ausführen der Schritte zum Aktivieren von Verbindungen mit Clouddiensten in Phase 2</li><li>Wenn der PAW-Computer keiner Domäne beigetreten ist, müssen mithilfe der im Download der Sicherheitsbaseline bereitgestellten Tools die SCM-Baselines auf die lokalen Images angewendet werden.</li></ul>|
|Neue System Center-Instanz(en) zum Verwalten der PAWs|– Bietet Transparenz und Kontrolle für Konfiguration, Softwarebereitstellung und Sicherheitsupdates<br />– Erfordert eine separate Serverinfrastruktur, die auf Ebene der PAWs gesichert werden muss, sowie die notwendigen Qualifikationen der Mitarbeiter mit diesen weit reichenden Berechtigungen|
|Verwalten von PAWs mit vorhandenen Verwaltungstools|: Erhöht das Risiko einer Gefährdung der PAWs, sofern die vorhandene Verwaltungsinfrastruktur auf Sicherheitsebene der PAWs hochgefahren wird, wird erstellt **beachten:**     Microsoft würde in der Regel dadurch davon abhalten, es sei denn, Ihre Organisation kein zwingender Grund es verwenden. Nach unserer Erfahrung ist es in der Regel sehr kostspielig, all diese Tools (und ihre Sicherheitsabhängigkeiten) auf die gleiche Sicherheitsebene heraufzustufen wie die PAWs.<br />– Die meisten dieser Tools bieten Transparenz und Kontrolle für Konfiguration, Softwarebereitstellung und Sicherheitsupdates|
|Tools für Sicherheitsüberprüfung und -überwachung, die Administratorzugriff erfordern|Hierzu gehören alle Tools, die einen Agent installieren oder ein Konto mit lokalem Administratorzugriff erfordern.<br /><br />– Tools müssen die gleiche Sicherheitsebene aufweisen wie die PAWs<br />– Möglicherweise muss die Sicherheitsebene der PAWs heruntergestuft werden, um die Funktionsweise der Tools zu unterstützen (Öffnen von Ports, Installieren von Java oder anderer Middleware usw.), wodurch über einen Kompromiss hinsichtlich der Sicherheit entschieden werden muss|
|SIEM-Lösung (Security Information and Event Management)|<ul><li>Wenn die SIEM-Lösung keinen Agent erfordert:<br /><br /><ul><li>Zugriff auf Ereignisse auf PAWs ist durch Verwenden eines Kontos in der Gruppe **Ereignisprotokollleser** auch ohne Administratorrechte möglich</li><li>Erfordert das Öffnen von Netzwerkports zum Zulassen von eingehendem Datenverkehr von den SIEM-Servern</li></ul></li><li>Wenn SIEM einen Agent erfordert: **Security Scanning or monitoring tools requiring admin access**</li></ul>|
|Windows-Ereignisweiterleitung|– Stellt eine Methode ohne Agents zum Weiterleiten von Sicherheitsereignissen von den PAWs an einen externen Datensammler oder eine SIEM-Lösung bereit<br />– Zugriff auf Ereignisse auf den PAWs auch ohne Administratorrechte möglich<br />– Öffnen von Netzwerkports zum Zulassen von eingehendem Datenverkehr von den SIEM-Servern nicht erforderlich|

## <a name="operating-paws"></a>Betrieb der PAWs

Die PAW-Lösung sollte gemäß den Standards unter [Prinzip der vertrauenswürdigen Quelle für betriebliche Standards](http://aka.ms/securitystandards) betrieben werden.

## <a name="related-topics"></a>Verwandte Themen

[Benutzerfreundliche Microsoft Cybersecurity-Dienste](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)

[Premier Vorgeschmack: Gewusst wie: Pass-the-Hash und anderen Formen der Diebstahl von Anmeldeinformationen zu verringern](https://channel9.msdn.com/Blogs/Taste-of-Premier/Taste-of-Premier-How-to-Mitigate-Pass-the-Hash-and-Other-Forms-of-Credential-Theft)

[Microsoft Advanced Threat Analytics](http://aka.ms/ata)

[Schützen Sie abgeleiteter Domänenanmeldeinformationen mit Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx)

[Device Guard – Überblick](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx)

[Schützen von wertvollen Assets mit sicheren Arbeitsstationen für Administratoren](https://msdn.microsoft.com/en-us/library/mt186538.aspx)

[Isolierter Benutzermodus in Windows 10 mit Dave Probert (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-in-Windows-10-with-Dave-Probert)

[Isolierte Prozesse im Benutzermodus und Features in Windows 10 mit Logan Gabriel (Channel 9)](http://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-Processes-and-Features-in-Windows-10-with-Logan-Gabriel)

[Mehr auf Prozesse und Features in Windows 10 Isolated User Mode mit Dave Probert (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/More-on-Processes-and-Features-in-Windows-10-Isolated-User-Mode-with-Dave-Probert)

[Beheben von Diebstahl von Anmeldeinformationen mithilfe der Windows 10 isolierten Benutzermodus (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Mitigating-Credential-Theft-using-the-Windows-10-Isolated-User-Mode)

[Aktivieren der strengen KDC-Überprüfung in Windows Kerberos](https://www.microsoft.com/en-us/download/details.aspx?id=6382)

[Neuerungen bei der Kerberosauthentifizierung für WindowsServer 2012](https://technet.microsoft.com/library/hh831747.aspx)

[Authentifizierungssicherung für AD DS in schrittweise Anleitung für Windows Server 2008 R2](https://technet.microsoft.com/library/dd378897(v=ws.10).aspx)

[Trusted Platform Module](C:\sd\docs\p_ent_keep_secure\p_ent_keep_secure\trusted_platform_module_technology_overview.xml)
