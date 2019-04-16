---
title: "Schützen des privilegierten Zugriffs – Referenzmaterial"
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22ee9a77-4872-4c54-82d9-98fc73a378c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: ee5769a3ed0225ebdd31645027bace38f0bff1b9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="securing-privileged-access-reference-material"></a>Schützen des privilegierten Zugriffs – Referenzmaterial

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


Dieser Abschnittenthält Referenzinformationen zum Schützen des privilegierten Zugriffs einschließlich:

-   [Active Directory-verwaltungsebenenmodell](#ADATM_BM)

-   [Prinzip der vertrauenswürdigen Quelle](#CSP_BM)

-   [ESAE-Verwaltungsgesamtstruktur Entwurfsansatz](#ESAE_BM)

-   [Äquivalenz zur Ebene 0](#T0E_BM)

-   [Verwaltungstools und Anmeldetypen](#ATLT_BM)

## <a name="ADATM_BM"></a>Active Directory-verwaltungsebenenmodell
Der Zweck dieses Ebenenmodell wird mithilfe einer Reihe von Pufferzonen zwischen der vollständige Kontrolle über die Umgebung (Ebene 0) und die mit hohem Risiko Arbeitsstation-Ressourcen, die Angreifer häufig gefährden Identitätssysteme zu schützen.

![Das Diagramm zeigt die drei Ebenen des Tier-Modells](../media/securing-privileged-access-reference-material/PAW_RM_Fig1.JPG)

Dieses Modell besteht aus drei Ebenen und enthält nur Administratorkonten, keine standardmäßigen Benutzerkonten:

-   **Ebene 0** -unmittelbaren Kontrolle des Unternehmens Identitäten in der Umgebung. Ebene 0 umfasst Konten, Gruppen und andere Ressourcen, die direkte oder indirekte administrative Kontrolle über die Active Directory-Gesamtstruktur, Domänen oder Domänencontrollern verfügen und alle Ressourcen darin. Die Vertraulichkeit aller Assets der Ebene 0 entspricht alle effektiv gegenseitig steuern werden.

-   **Ebene 1** -Kontrolle von Unternehmensservern und Anwendungen. Assets der Ebene 1 umfassen Serverbetriebssysteme, Clouddienste und unternehmensanwendungen. Administratorkonten der Ebene 1 haben administrative Kontrolle für eine signifikante Menge von gehostet wird, auf diese Ressourcen. Ein gängiges Beispiel sind Serveradministratoren, die diese Betriebssysteme, die Möglichkeit beizubehalten, alle Unternehmensdienste auswirken.

-   **Ebene 2** -Kontrolle von Benutzerarbeitsstationen und Geräte. Administratorkonten der Ebene 2 verfügen auf Benutzerarbeitsstationen und -Geräten administrative Kontrolle für eine signifikante Menge von gehostet wird. Beispiele sind Helpdesk- und computersupportadministratoren sie die Integrität von praktisch sämtlichen Benutzerdaten auswirken können.

> [!NOTE]
> Die Ebenen dienen zudem als grundlegender priorisierungsmechanismus zum Schutz von administrativen Assets, aber es ist wichtig zu beachten, dass ein Angreifer mit Kontrolle aller Assets einer beliebigen Ebene die meisten oder alle unternehmensassets zugreifen kann. Der Grund ist es hilfreich, als grundlegender priorisierungsmechanismus ist Angreifer Probleme/Kosten. Es ist einfacher, ein Angreifer mit vollständiger Kontrolle aller Identitäten (Ebene 0) oder Servern ausgeführt werden und Clouddienste (Ebene 1) als ist, wenn sie auf jedem einzelnen Arbeitsstationen oder Benutzergeräte (Ebene 2) zum Abrufen der Daten Ihrer Organisation zugreifen müssen.

### <a name="containment-and-security-zones"></a>Eindämmung und Sicherheitszonen
Die Ebenen werden relativ zu einer bestimmten Sicherheitszone. Während sie viele Namen überschritten haben, sind Sicherheitszonen einen bewährten Ansatz, die Kapselung von Sicherheitsrisiken durch eine Isolierung zwischen ihnen zu ermöglichen. Das Ebenenmodell ergänzt die Isolierung durch Eindämmen von Angriffsversuchen innerhalb einer Sicherheitszone, in denen die Netzwerkisolation nicht wirksam ist. Sicherheitszonen können umfassen sowohl lokal und Cloud-Infrastruktur, wie im Beispiel, in denen Domänencontroller und Domänenmitglieder innerhalb derselben Domäne lokal sind, und in Azure.

![Das Diagramm zeigt, wie Sicherheitszonen umfassen sowohl lokal als auch Cloud-Infrastruktur](../media/securing-privileged-access-reference-material/PAW_RM_Fig2.JPG)

Das Ebenenmodell verhindert eine Ausweitung von rechten beschränken, welche Administratoren steuern und, in dem sie sich anmelden können (da es sich um eine Anmeldung an einem Computer Kontrolle über diese Anmeldeinformationen und allen Assets, die über diese Anmeldeinformationen verwaltet gewährt).

### <a name="control-restrictions"></a>Eingeschränkten Kontrolle
Eingeschränkten Kontrolle sind in der folgenden Abbildungdargestellt:

![Diagramm der eingeschränkten Kontrolle](../media/securing-privileged-access-reference-material/PAW_RM_Fig3.JPG)

### <a name="primary-responsibilities-and-critical-restrictions"></a>Primäre Aufgaben und wichtige Einschränkungen
**Administrator der Ebene 0** -Identitätsspeicher und eine kleine Anzahl von Systemen, die effektive steuern, verwalten und:

-   Verwalten und Steuern von Assets auf sämtlichen Ebenen nach Bedarf

-   Interaktives anmelden oder Zugriff auf Assets, die auf der Ebene 0 als vertrauenswürdig eingestuft werden können

**Administrator der Ebene 1** -Unternehmensservern, Dienste und Anwendungen verwalten und:

-   Ausschließlich Verwaltung und Steuerung von Assets auf Ebene 1 oder Ebene 2

-   Ausschließlich Zugriff auf Assets (über den Anmeldetyp "Netzwerk"), die auf Ebene 1 oder Ebene 0 als vertrauenswürdig gelten

-   Können nur interaktiv anmelden bei Assets auf Ebene 1 als vertrauenswürdig eingestuft

**Administrator der Ebene 2** -Enterprise-Desktops, Laptops, Drucker und andere Benutzergeräte verwalten und:

-   Ausschließlich Verwaltung und Steuerung von Assets auf Ebene 2

-   Assets (über Anmeldetyp "Netzwerk") auf jeder Ebene bei Bedarf können zugreifen werden.

-   Können nur interaktiv anmelden bei Assets auf Ebene 2 als vertrauenswürdig eingestuft

### <a name="logon-restrictions"></a>Anmeldeeinschränkungen
Anmeldebeschränkungen sind in der folgenden Abbildungdargestellt:

![Diagramm der anmeldeeinschränkungen](../media/securing-privileged-access-reference-material/PAW_RM_Fig4.JPG)

> [!NOTE]
> Beachten Sie, dass einige Ressourcen können Auswirkungen auf Ebene 0 für die Verfügbarkeit der Umgebung, aber nicht direkt beeinträchtigt die Vertraulichkeit oder Integrität der Assets. Dazu gehören der DNS-Serverdienst sowie wichtige Netzwerkgeräte wie internetproxys.

## <a name="CSP_BM"></a>Prinzip der vertrauenswürdigen Quelle
Das Prinzip der vertrauenswürdigen Quelle muss alle sicherheitsabhängigkeiten weniger vertrauenswürdig als das Objekt, das gesichert werden.

![Das Diagramm zeigt, wie jedes Subjekt, das ein Objekt eine sicherheitsabhängigkeit dieses Objekts ist](../media/securing-privileged-access-reference-material/PAW_RM_Fig5.JPG)

Jedes Subjekt, das in ein Objekt ist eine sicherheitsabhängigkeit dieses Objekts. Wenn ein Angreifer effektiver Kontrolle über ein Zielobjekt steuern kann, können sie dieses Zielobjekt kontrollieren. Aus diesem Grund müssen Sie sicherstellen, dass die Zusicherungen für alle sicherheitsabhängigkeiten mindestens über die gewünschte Sicherheitsstufe des Objekts selbst.

Beim einfach ist erfordert dies Umsetzung die kontrollbeziehungen eines Element (Objekt) und eine Abhängigkeitsanalyse davon ermittelt alle sicherheitsabhängigkeiten (Subjekte) durchführen.

Da eine transitive Kontrolle handelt, muss dieses Prinzip rekursiv wiederholt werden. Für Beispiel, wenn ein Steuerelemente B und B, C Steuerelemente, steuert dann A indirekt auch C.

![Das Diagramm zeigt, wie wenn eine Steuerelemente B, und B steuert C, dann A indirekt auch C-Steuerelemente](../media/securing-privileged-access-reference-material/PAW_RM_Fig6.JPG)

Ein Angreifer Zugriff gefährdet, erhält auf Alles, was eine steuert (einschließlich B) und alles B steuert (einschließlich C). Verwenden die Sprache des sicherheitsabhängigkeiten dieses Beispiels, B und A sicherheitsabhängigkeiten von C und müssen auf die gewünschte Sicherheitsstufe von C nacheinander für C, um die Sicherheitsstufe müssen gesichert werden.

Für IT-Infrastrukturen und Identitätssystemen Systeme sollte dieses Prinzip zu den am häufigsten verwendeten Steuerelement auch die Hardware, auf dem Systeme installiert sind, die Installationsmedien für Systeme, die Architektur und die Konfiguration des Systems sowie tägliche Vorgänge angewendet werden.

### <a name="clean-source-for-installation-media"></a>Vertrauenswürdige Quelle für Installationsmedien
![Das Diagramm zeigt eine vertrauenswürdige Quelle für Installationsmedien](../media/securing-privileged-access-reference-material/PAW_RM_CSIM.JPG)

Das Prinzip der vertrauenswürdigen Quelle auf Installationsmedien anwenden, müssen Sie sicherstellen, dass das Installationsmedium nicht manipuliert wurde seit der Freigabe durch den Hersteller (so gut wie bestimmt werden kann). Diese Abbildungzeigt einen Angreifer diesen Weg auf um einen Computer zu gefährden:

![Diese Abbildungzeigt einen Angreifer mit einem Pfad, einen Computer zu gefährden](../media/securing-privileged-access-reference-material/PAW_RM_Fig8.JPG)

Das Prinzip der vertrauenswürdigen Quelle auf Installationsmedien anzuwenden, müssen Überprüfen der Integrität der Software des gesamten Zyklus verfügen, während der Übernahme, Speicher, einschließlich zu übertragen, bis es verwendet wird.

#### <a name="software-acquisition"></a>Erwerb von Software
Die Quelle der Software sollte über eine der folgenden Methoden überprüft werden:

-   Software wird auf einem physischen Medium abgerufen, die bekannt ist, das vom Hersteller oder einer seriösen Quelle, in der Regel werden diese Medien von einem Anbieter stammen.

-   Software wird aus dem Internet bezogen und mit Hersteller bereitgestellten Dateihashes überprüft.

-   Software wird aus dem Internet bezogen und durch den Download und Vergleich von zwei unabhängigen Kopien überprüft:

    -   Laden Sie auf zwei Hosts ohne sicherheitsbeziehung herunter (nicht in derselben Domäne befindet und nicht von dieselben Tools verwaltet werden), vorzugsweise über getrennte Internetverbindungen.

    -   Vergleichen Sie die heruntergeladenen Dateien über ein Hilfsprogramm wie Certutil:

        `certutil -hashfile <filename>`

Wenn möglich, alle Anwendungssoftware wie Anwendungsinstallationsprogramme und -Tools digital signiert und überprüft mithilfe von Windows Authenticode mit der [Windows Sysinternals](https://www.microsoft.com/sysinternals)s-Tool *sigcheck.exe*, mit sperrüberprüfung. Bestimmte Software kann erforderlich sein, in denen der Anbieter kann diese Art von digitaler Signatur nicht bereitstellen.

#### <a name="software-storage-and-transfer"></a>Software-Speicherung und Übertragung
Wenn die Software erhalten haben, sollte es an einem Ort gespeichert werden, der nicht geändert werden, insbesondere durch das Internet verbundene Hosts oder Mitarbeiter, deren auf einer niedrigeren Ebene als die Systeme, die Software oder ein Betriebssystem installiert werden. Bei diesem Speicher kann es sich um physische Medien oder einen sicheren elektronischen Speicherort handeln.

#### <a name="software-usage"></a>Der Softwareverwendung
Im Idealfall sollte die Software zum Zeitpunkt überprüft werden, die sie verwendet wird, z.B. wenn es manuell installiert, für ein Konfigurationsverwaltungstool verpackt oder in ein Konfigurationsverwaltungstool importiert.

### <a name="clean-source-for-architecture-and-design"></a>Vertrauenswürdige Quelle für Architektur und Entwurf
Das Prinzip der vertrauenswürdigen Quelle auf die Systemarchitektur anzuwenden, müssen Sie sicherstellen, dass das System nicht auf Systemen mit niedrigerer Vertrauensebene abhängt. Ein System abhängige kann auf eine höhere Vertrauensstellung System, jedoch nicht auf einem System mit niedrigeren Sicherheitsstandards Vertrauensebene.

Beispielsweise ist die akzeptabel für Active Directory zum Steuern von einem standardmäßigen Benutzerdesktop, sondern eine erhebliche Ausweitung von Berechtigungen Risiko für einen standardbenutzerdesktop Kontrolle von Active Directory.

![Das Diagramm zeigt, wie ein System auf einem System mit höherer Vertrauensstellung abhängig sein kann, aber nicht auf einem System mit niedrigeren Sicherheitsstandards Vertrauensebene](../media/securing-privileged-access-reference-material/PAW_RM_Fig09.JPG)

Die kontrollbeziehung kann über verschiedene Methoden, einschließlich der Sicherheits-Zugriffssteuerungslisten (ACLs) für Objekte wie Dateisysteme, über die Mitgliedschaft in der lokalen Administratorgruppe auf einem Computer oder auf einem Computer (mit der Möglichkeit, beliebigen Code und Skripts auszuführen) als System ausgeführten installierten Agents verwendet werden.

Ein häufig übersehenes Beispiel ist die Offenlegung Anmeldung, wodurch eine kontrollbeziehung, entsteht indem die Administratoranmeldeinformationen eines Systems, um ein anderes System. Dies ist die zugrunde liegende Ursache, warum den Diebstahl von Angriffen wie den Hashwert zu übergeben sind so gefährlich. Wenn ein Administrator mit Anmeldeinformationen der Ebene 0 Benutzerdesktop anmeldet, werden sie die Anmeldeinformationen für den Desktop, platzieren es in der AD-Steuerelement, und erstellen eine Erhöhung der Rechte in Active Directory verfügbar machen. Weitere Informationen zu diesen Angriffen finden Sie unter [auf dieser Seite](https://technet.microsoft.com/en-us/security/dn785092).

Aufgrund der großen Anzahl von Objekten, die von Identitätssystemen wie Active Directory abhängen, sollten Sie die Anzahl der Systeme minimieren, denen Ihre Active Directory und Domänencontroller abhängig sind.

![Das Diagramm zeigt, dass Sie Ihre Active Directory, der Anzahl der Systeme minimieren sollten und hängen von Domänencontrollern](../media/securing-privileged-access-reference-material/PAW_RM_Fig010.JPG)

Weitere Informationen zum Minimieren der wichtigsten Risiken von active Directory finden Sie unter [auf dieser Seite](http://aka.ms/hardenAD).

### <a name="OSBCS_BM"></a>Prinzip der vertrauenswürdigen Quelle für betriebliche Standards
In diesem Abschnittwird beschrieben, die betriebliche Standards und die Ziele für die administrative Mitarbeiter dürfen. Diese Standards soll die administrative Kontrolle über eine Organisation IT-Systeme gegen Risiken zu sichern, die durch betriebliche Verfahren und Prozesse entstehen könnten.

![Das Diagramm zeigt, wie Standards entworfen werden, um administrative Kontrolle über Unternehmensdaten IT-Systeme gegen Risiken abzusichern, die durch betriebliche Verfahren und Prozesse entstehen könnten](../media/securing-privileged-access-reference-material/PAW_RM_Fig11.JPG)

#### <a name="integrating-the-standards"></a>Integrieren der Standards
Sie können diese Standards in allgemeinen Standards und Verfahren Ihrer Organisation integrieren. Sie können anpassen, um die spezifischen Anforderungen, die verfügbaren Tools und die Risikobereitschaft Ihrer Organisation, aber nur minimale Änderungen an das Risiko zu reduzieren, wird empfohlen. Es wird empfohlen, dass Sie die Standardeinstellungen in diesem Leitfaden als Benchmark für Ihren idealen Endzustand verwenden und Verwalten von Deltas als Ausnahmen in der Reihenfolge ihrer Priorität behandelt werden.

Der Leitfaden zu Standards gliedert ist in die folgenden Abschnitte unterteilt:

-   Annahmen

-   Change Advisory Board

-   Betriebliche Verfahren

    -   Zusammenfassung

    -   Standards-Detail

#### <a name="assumptions"></a>Annahmen
Die Standards in diesem Abschnittwird davon ausgegangen, dass die Organisation die folgenden Attribute:

-   Die meisten oder alle Server und Arbeitsstationen sind mit Active Directory verknüpft.

-   Alle zu verwaltenden Servern ausgeführt werden Windows Server2008 R2 oder höher und RDP-Modus RestrictedAdmin-Modus ist aktiviert.

-   Alle zu verwaltenden Arbeitsstationen Windows7 oder höher ausgeführt werden und RDP-Modus RestrictedAdmin-Modus ist aktiviert.

    > [!NOTE]
    > Zum Aktivieren des RDP-Modus RestrictedAdmin-Modus finden Sie unter [auf dieser Seite](http://aka.ms/RDPRA).

-   Smartcards sind verfügbar und werden für alle Administratorkonten bereitgestellt.

-   Die *Builtin\Administrator* für jede Domäne als ein Konto Notfallzugriff festgelegt wurde

-   Eine Lösung zur Verwaltung von Unternehmen bereitgestellt wird.

-   [LAPS](http://aka.ms/laps) für Server und Arbeitsstationen, verwalten Sie das Kennwort des lokalen Administratorkontos bereitgestellt wurde

-   Eine privileged Access Management-Lösung wie Microsoft Identity Manager an, oder es ist ein Plan für die eine verwenden möchten.

-   Mitarbeiter zugewiesen Sicherheitshinweise zu überwachen und reagieren Sie darauf.

-   Die technische Möglichkeit, schnell Microsoft-Sicherheitsupdates anzuwenden ist verfügbar.

-   Baseboard-Verwaltungscontroller auf Servern verwendet werden, oder die Sicherheitsmaßnahmen werden strikt eingehalten.

-   Administratorkonten und -Gruppen für Server (Administratoren der Ebene 1) und Arbeitsstationen (Administratoren der Ebene 2) werden von Domänenadministratoren (Ebene 0) verwaltet werden.

-   Es ist ein Change Advisory Board (CAB) oder einer anderen benannten Stelle genehmigt Änderungen an Active Directory.

#### <a name="change-advisory-board"></a>Change advisory Board
Ein Change Advisory Board (CAB) ist die Diskussion genehmigungsstelle für Änderungen, die das Sicherheitsprofil der Organisation auswirken kann. Ausnahmen bezüglich dieser Standards sollten auf die CAB-Datei mit einer Risikobewertung und Begründung übermittelt werden.

Die einzelnen Standards in diesem Dokument wird nach der Bedeutung des jeweiligen Standards für eine bestimmte Ebene aufgeteilt.

![Diagramm des Standards für angegebenen Ebenen](../media/securing-privileged-access-reference-material/PAW_RM_Fig12.JPG)

Alle Ausnahmen für erforderliche Elemente (mit einem roten Achteck oder orangefarbenen Dreieck in diesem Dokument gekennzeichnet) werden als vorübergehend betrachtet, und sie müssen vom CAB genehmigt werden. Folgende Richtlinien:

-   Die erste Anforderung Begründung und das Risiko muss vom unmittelbaren Vorgesetzten des Mitarbeiters abgezeichnet signiert, läuft nach sechs Monaten ab.

-   Verlängerung benötigen, ein Unternehmen abgezeichnet Begründung und das Risiko und Ablaufzeitraum von sechs Monaten.

Alle Ausnahmen für empfohlene Elemente (mit einem gelben Kreis in diesem Dokument gekennzeichnet) werden als vorübergehend betrachtet und müssen vom CAB genehmigt werden. Folgende Richtlinien:

-   Die erste Anforderung Begründung und das Risiko muss vom unmittelbaren Vorgesetzten des Mitarbeiters abgezeichnet signiert, läuft nach 12Monaten ab.

-   Verlängerung benötigen, ein Unternehmen abgezeichnet Begründung und das Risiko und Ablaufzeitraum von 12Monaten.

#### <a name="operational-practices-standards-summary"></a>Standards für Betriebsmethoden
Die Spalten für die Ebenen in dieser Tabelle finden Sie in der Ebene des Administratorkontos, die Kontrolle über die in der Regel alle Assets dieser Ebene auswirkt.

![Tabelle zeigt die Ebene des Administratorkontos](../media/securing-privileged-access-reference-material/PAW_RM_Fig13.JPG)

Entscheidungen bezüglich, die in regelmäßigen Abständen vorgenommen werden, sind wichtig, um den Sicherheitsstatus der Umgebung. Diese Standards für Prozesse und Verfahren können Sie sicherstellen, dass betriebliche Fehler nicht zu einer Betriebsvorgängen innerhalb der Umgebung führt.

##### <a name="administrator-enablement-and-accountability"></a>Befähigung und Verantwortlichkeit
Administratoren müssen darüber informiert, befugt sind, geschult und Handlungen Umgebung so sicher wie möglich werden.

###### <a name="administrative-personnel-standards"></a>Administrative Mitarbeiter dürfen Standards
Mitarbeiter mit administrativen müssen überprüft werden, um sicherzustellen, dass sie vertrauenswürdig sind und eine Administratorrechte benötigen:

-   Führen Sie hintergrundüberprüfung für Mitarbeiter durch, bevor Sie Administratorrechte zuweisen.

-   Überprüfen Sie Administratorrechte Quartal um zu bestimmen, welche Mitarbeiter weiterhin eine seriösen Administratorzugriff benötigen.

###### <a name="administrative-security-briefing-and-accountability"></a>Administrative Sicherheit Einweisung und Verantwortlichkeit
Administratoren müssen informiert und für die Risiken der Organisation sowie ihre Rolle beim Umgang mit diesen Risiken verantwortlich sein. Administratoren sollten jährlich in geschult werden:

-   Allgemeine Bedrohungslandschaft

    -   Entschlossene

    -   Angriffstechniken, einschließlich Pass-the-Hash und Diebstahl von Anmeldeinformationen

-   Organisationsspezifische Bedrohungen und incidents

-   Die Rolle des Administrators beim Schutz gegen Angriffe

    -   Verwalten der Offenlegung von Anmeldeinformationen mit dem Ebenenmodell

    -   Verwenden von administrativen Arbeitsstationen

    -   Verwenden von Remote Desktop Protocol RestrictedAdmin-Modus

-   Organisationsspezifische administrative Verfahren

    -   Überprüfen Sie aller betrieblichen Richtlinien in diesem Standard

    -   Implementieren Sie die folgenden wichtigen Regeln:

        -   Verwenden Sie keine Administratorkonten auf administrativen Arbeitsstationen

        -   Deaktivieren oder entfernen Sie keinesfalls Sicherheitskontrollen Ihrer Konten oder Arbeitsstationen (z.B. anmeldeeinschränkungen oder Attribute für Smartcards erforderlich)

        -   Melden Sie Probleme oder ungewöhnliche Aktivität

Um Verantwortlichkeit sicherzustellen, sollten alle Mitarbeiter mit Administratorkonten ein Dokument Administrative Verhaltensregeln signieren, die besagt, dass er organisationsspezifischen administratorichtlinien möchten.

###### <a name="provisioning-and-deprovisioning-processes-for-administrative-accounts"></a>Bereitstellung und Aufheben der Bereitstellung für Administratorkonten
Die folgenden Standards müssen eingehalten werden, um lebenszyklusanforderungen einzuhalten.

-   Alle Administratorkonten müssen von den in der folgenden Tabelle aufgeführten genehmigenden Stelle genehmigt werden.

    -   Genehmigung darf nur erteilt werden, wenn das Personal, dass einem vorliegen Unternehmen Administratorrechte benötigen.

    -   Genehmigung für Administratorrechte darf sechs Monate nicht überschreiten.

-   Zugriff auf Administratorrechte muss sofort hat beim:

    -   Mitarbeiter übernehmen eine neue Position.

    -   Mitarbeiter verlassen die Organisation.

-   Konten müssen sofort deaktiviert werden, wenn Mitarbeiter das Unternehmen verlässt.

-   Deaktivierte Konten müssen innerhalb von sechs Monaten gelöscht werden und der Datensatz ihrer Löschung in Change Approval Boards erfasst eingegeben werden muss.

-   Überprüfen Sie alle privilegierten Konto pro Monat die Mitgliedschaft, um sicherzustellen, dass keine nicht autorisierten Berechtigungen erteilt wurden. Dies kann durch ein automatisiertes Tool ersetzt werden, mit der Änderung benachrichtigt.

|Ebene der Kontoberechtigung|Genehmigen von Berechtigungen|Häufigkeit der Überprüfung von Mitgliedschaft|
|--------------|------------|----------------|
|Administrator der Ebene 0|Change Approval Board|Monatlich oder automatisiert|
|Administrator der Ebene 1|Administratoren der Ebene 0 oder Sicherheit|Monatlich oder automatisiert|
|Administrator der Ebene 2|Administratoren der Ebene 0 oder Sicherheit|Monatlich oder automatisiert|

##### <a name="operationalize-least-privilege"></a>Operationalisieren der geringsten Rechte
Diese Standards unterstützen jeweils geringsten Rechte implementiert, durch Reduzieren der Anzahl der Administratoren-Rolle und die Zeitdauer, über die Rechte verfügen.

> [!NOTE]
> Erreichen der geringsten Rechte in Ihrer Organisation benötigen Sie die Rollen, ihren Anforderungen und entwurfsmechanismen, um sicherzustellen, dass sie ihre Aufgaben ausführen können, mit der geringsten Rechte zu verstehen. Die jeweils geringsten Rechte in einem administrativen Modell häufig erfordert die Verwendung von mehrere Ansätze:
>
> -   Beschränken Sie die Anzahl von Administratoren oder Mitgliedern privilegierter Gruppen
> -   Delegieren Sie weniger Berechtigungen an Konten
> -   Geben Sie bei Bedarf zeitgebundene Berechtigungen
> -   Ermöglichen Sie anderen Mitarbeitern das Ausführen von Aufgaben (Concierge-Ansatz)
> -   Implementieren Sie Prozesse für den Notfallzugriff und seltene Szenarien

###### <a name="limit-count-of-administrators"></a>Einschränken der Anzahl von Administratoren
Mindestens zwei Mitarbeiter sollten jeder Administratorrolle zugewiesen werden, um Geschäftskontinuität sicherzustellen.

Wenn die Anzahl der Mitarbeiter zu einer Funktion zugewiesen zwei übersteigt, muss das Change Approval Board die spezifischen Gründe für das Zuweisen von Berechtigungen zu den einzelnen Mitgliedern (einschließlich der zwei ursprünglichen) genehmigen. Die Gründe für die Genehmigung muss Folgendes umfassen:

-   Die technischen Aufgaben, die von den Administratoren ausgeführt werden, die die Administratorrechte erforderlich sind

-   Wie oft werden die Aufgaben ausgeführt

-   Grund, warum die Aufgaben von einem anderen Administrator in ihrem Auftrag ausgeführt werden kann

-   Dokumentieren Sie alle anderen bekannten alternative Ansätze zum Erteilen der Berechtigung und warum nicht umsetzbar sind

###### <a name="dynamically-assign-privileges"></a>Dynamisches Zuweisen von Berechtigungen
Administratoren müssen abrufen "just-in-Time-Berechtigungen, deren Verwendung ihre Aufgaben auszuführen. Keine Berechtigungen werden Administratorkonten dauerhaft zugewiesen werden.

> [!NOTE]
> Dauerhaft zugewiesene Administratorrechten denken beim Erstellen einer Strategie für die "höchsten Rechte" da administrative Mitarbeiter dürfen den schnellen Zugriff auf Berechtigungen erfordern für betriebliche Verfügbarkeit aufrechterhalten, wenn ein Problem vorliegt. Just-in-Time-Berechtigungen ermöglichen:
>
> -   Weisen Sie Berechtigungen genauer gesagt, Abrufen der geringsten Rechte näher zu.
> -   Geringere Dauer der Offenlegung von rechten
> -   Tracking-Berechtigungen verwenden, um Missbrauch oder Angriffe zu erkennen.

##### <a name="manage-risk-of-credential-exposure"></a>Verwalten von Risiken einer Offenlegung von Anmeldeinformationen
Verwenden Sie die folgenden Methoden, um ordnungsgemäße Risiko einer Offenlegung von Anmeldeinformationen verwalten.

###### <a name="separate-administrative-accounts"></a>Separate Administratorkonten
Alle Mitarbeiter, die über Administratorrechte verfügen müssen separate Konten für administrative Funktionen verfügen, die Benutzerkonten sind.

-   **Standardbenutzerkonten** -gewährt Standardbenutzerrechte für standardmäßige Benutzeraufgaben, z.B. E-Mail, Surfen im Web, und Line-of-Business-Anwendungen. Diese Konten sollten keine Administratorrechte erteilt werden.

-   **Administratorkonten** -separate Konten für Mitarbeiter, die die entsprechenden Administratorrechte zugewiesen werden. Ein Administrator, der zur Verwaltung von Assets auf allen Ebenen erforderlich ist, sollte ein separates Konto für jede Ebene verfügen. Diese Konten sollten keinen Zugriff auf E-Mail-Adresse oder das öffentliche Internet verfügen.

###### <a name="administrator-logon-practices"></a>Die administratoranmeldung
Bevor ein Administrator auf einem Host interaktiv (lokal über Standard-RDP, unter Verwendung von RunAs oder über die Konsole Virtualization) anmelden kann, muss dem Host erfüllen und den Standard für die Ebene des Administratorkontos (oder einer höheren Ebene).

Administratoren können nur mit ihren Administratorkonten bei Administratorarbeitsstationen anmelden. Administratoren melden Sie sich nur auf verwaltete Ressourcen mithilfe der genehmigten supporttechnologie im nächsten Abschnittbeschrieben.

> [!NOTE]
> Dies ist erforderlich, da auf diesem Host interaktiv anmelden bei einem Host Kontrolle über die Anmeldeinformationen erteilt werden.
>
> Weitere Informationen finden Sie unter der [Verwaltungstools und Anmeldetypen](http://aka.ms/admintoolsecurity) Einzelheiten zu Anmeldetypen, allgemeinen Verwaltungstools und Offenlegung von Anmeldeinformationen.

###### <a name="use-of-approved-support-technology-and-methods"></a>Verwenden genehmigter supporttechnologien und -Methoden
Administratoren, die Remote-Systeme und Benutzer zu unterstützen, müssen diese Richtlinien, um zu verhindern, dass ein Angreifer die Steuerung des Remotecomputers Anmeldeinformationen des Administrators stiehlt folgen.

-   Die primären Supportoptionen sollte verwendet werden, sofern diese verfügbar sind.

-   Die sekundären Supportoptionen sollten nur verwendet werden, wenn die primäre Supportoption nicht verfügbar ist.

-   Zulässige Supportmethoden dürfen niemals verwendet werden.

-   Kein Browsen oder E-Mail-Zugriff auf das Internet kann ein Administratorkonto zu einem beliebigen Zeitpunkt ausgeführt werden.

###### <a name="tier-0-forest-domain-and-dc-administration"></a>Ebene-0-Gesamtstruktur, Domäne und DC-Verwaltung
Stellen Sie sicher, dass für dieses Szenario die folgenden Methoden angewendet werden:

-   **Remoteserversupport** -beim Remotezugriff auf einen Server müssen Administratoren der Ebene 0 folgenden Richtlinien befolgen:

    -   **Primär (Tool)** -Remotetools, die Netzwerkanmeldungen verwenden (Typ 3). Weitere Informationen finden Sie unter [Verwaltungstools und Anmeldetypen](http://aka.ms/admintoolsecurity).

    -   **Primär (interaktiv)** -RDP-Modus RestrictedAdmin verwenden oder eine Standard-RDP-Sitzung auf einer Administratorarbeitsstation mit Domänenkonto

    > [!NOTE]
    > Wenn Sie eine Ebene 0 verfügen, fügen Sie hinzu ", die Berechtigungen verwendet just-in-Time von einer privileged Access Management-Lösung erhalten."

-   **Unterstützung für physische Server** : Wenn physisch an der Serverkonsole darstellen oder VM-Konsole (Hyper-V oder VMWare Tools), haben diese Konten keine bestimmten Verwaltungstool nutzungseinschränkungen lediglich die allgemeinen Einschränkungen von standardmäßigen Benutzeraufgaben wie E-Mail und Durchsuchen des Internets.

    > [!NOTE]
    > Verwaltung der Ebene 0 unterscheidet sich von der Verwaltung von anderen Ebenen, da alle Assets der Ebene 0 bereits über direkte oder indirekte Kontrolle aller Assets verfügen. Beispielsweise verfügt eine Angreifer Kontrolle über Domänencontroller die Anmeldeinformationen von angemeldeten Administratoren stehlen, da diese bereits Zugriff auf alle Domänenanmeldeinformationen in der Datenbank haben.

###### <a name="tier-1-server-and-enterprise-application-support"></a>Ebene-1-Server und Application Supportseite für Unternehmen
Stellen Sie sicher, dass für dieses Szenario die folgenden Methoden angewendet werden:

-   **Remoteserversupport** -beim Remotezugriff auf einen Server müssen Administratoren der Ebene 1 diese Richtlinien befolgen:

    -   **Primär (Tool)** -Remotetools, die Netzwerkanmeldungen verwenden (Typ 3). Weitere Informationen finden Sie unter [Mitigating Pass-the-Hash and Other Credential Theft](https://www.microsoft.com/pth) v1 (Seite 42-47).

    -   **Primär (interaktiv)** -Verwendung RDP-Modus RestrictedAdmin auf einer Administratorarbeitsstation mit Domänenkonto, die Berechtigungen verwendet just-in-Time von einer privileged Access Management-Lösung abgerufen.

    -   **Sekundäre** – melden Sie sich bei dem Server mithilfe eines lokalen Kontokennworts, das von LAPS auf einer Administratorarbeitsstation festgelegt ist.

    -   **Verboten** -Standard-RDP darf nicht mit einem Domänenkonto verwendet werden.

    -   **Verboten** -mit dem Domänenkonto Anmeldeinformationen während der Sitzung (z.B. *RunAs* oder die Authentifizierung gegenüber einer Freigabe). Dies gibt an, der das Risiko des Diebstahls von Anmeldeinformationen.

-   **Unterstützung für physische Server** – wenn physisch an der Serverkonsole darstellen oder VM-Konsole (Hyper-V oder VMWare Tools) Administratoren der Ebene 1 müssen rufen Sie das Kennwort des lokalen aus LAPS vor dem Zugriff auf den Server.

    -   **Primäre** -das von LAPS auf einer Administratorarbeitsstation vor der Anmeldung beim Server festgelegte lokale Kontokennwort abzurufen.

    -   **Verboten** -mit einem Domänenkonto anmelden ist in diesem Szenario nicht zulässig.

    -   **Verboten** -mit dem Domänenkonto Anmeldeinformationen während der Sitzung (z.B. RunAs oder Authentifizierung gegenüber einer Freigabe). Dies gibt an, der das Risiko des Diebstahls von Anmeldeinformationen.

###### <a name="tier-2-help-desk-and-user-support"></a>Helpdesk- und Benutzersupport der Ebene 2-Hilfe
Helpdesk- und benutzersupportorganisationen bieten Support für Endbenutzer (die keine Administratorrechte erforderlich) und die Arbeitsstationen der Benutzer (die Administratorrechte erforderlich sind) ausführen.

**Benutzersupport** -Aufgaben gehören zur Unterstützung von Benutzern beim Durchführen von Aufgaben, die keine Änderungen an der Arbeitsstation erfordern häufig ihnen zeigen, wie ein Anwendungs- oder Betriebssystemfeature verwenden.

-   **Deskseitiger Benutzersupport** -Supportmitarbeiter der Ebene 2 sind physisch am Arbeitsplatz des Benutzers präsent.

    -   **Primäre** -"über die Schulter" Unterstützung bereitgestellt wird, keine Tools.

    -   **Verboten** -mit administrativen Anmeldeinformationen für Domänen-Konto anmeldet, ist in diesem Szenario nicht zulässig. Wechseln Sie zu deskseitigen Support, wenn Administratorrechte erforderlich sind.

-   **Remotebenutzersupport** -der Ebene 2 Supportmitarbeiter sind physisch an den Benutzer zu verbinden.

    -   **Primäre** -Remoteunterstützung, Skype for Business oder ähnliche Freigabe des Benutzerbildschirms können verwendet werden. Weitere Informationen finden Sie unter [Neuigkeiten von Windows-Remoteunterstützung?](https://windows.microsoft.com/en-us/windows/what-is-windows-remote-assistance)

    -   **Verboten** -mit administrativen Anmeldeinformationen für Domänen-Konto anmeldet, ist in diesem Szenario nicht zulässig. Wechseln Sie zu der Support für Arbeitsstationen, wenn Administratorrechte erforderlich sind.

-   **Support für Arbeitsstationen** - Aufgaben umfassen die Wartung von Arbeitsstationen oder Zugriff auf ein System zur Problembehandlung, die benötigt werden, für die Protokolle anzuzeigen, Installieren von Software, Treiber zu aktualisieren und So weiter.

    -   **Deskseitigen Support** -Supportmitarbeiter der Ebene 2 sind physisch am Computer des Benutzers.

        -   **Primäre** -die vor dem Herstellen einer Verbindung mit der Arbeitsstation des Benutzers auf einer Administratorarbeitsstation von LAPS festgelegte lokale Kontokennwort abzurufen.

        -   **Verboten** -mit administrativen Anmeldeinformationen für Domänen-Konto anmeldet, ist in diesem Szenario nicht zulässig.

    -   **Support für Arbeitsstationen** -der Ebene 2 Supportmitarbeiter sind physisch an der Arbeitsstation zu verbinden.

        -   **Primäre** -Verwendung RDP-Modus RestrictedAdmin auf einer Administratorarbeitsstation mit Domänenkonto, die Berechtigungen verwendet just-in-Time von einer privileged Access Management-Lösung abgerufen.

        -   **Sekundäre** -ein, das vor dem Herstellen einer Verbindung mit der Arbeitsstation des Benutzers auf einer Administratorarbeitsstation von LAPS festgelegte lokale Kontokennwort abzurufen.

        -   **Verboten** -Standard-RDP mit einem Domänenkonto verwenden.

###### <a name="no-browsing-the-public-internet-with-admin-accounts-or-from-admin-workstations"></a>Kein Browsen im öffentlichen Internet über Administratorkonten oder auf Administratorarbeitsstationen
Administrative Mitarbeiter können nicht Durchsuchen des Internets, während Sie mit einem Administratorkonto oder bei einer Administratorarbeitsstation angemeldet sind, auf. Die einzige Ausnahme ist die Verwendung eines Webbrowsers einen cloudbasierten Dienst, z.B. Microsoft Azure, Amazon Web Services, Microsoft Office365 oder Gmail für Unternehmen verwalten.

###### <a name="no-accessing-email-with-admin-accounts-or-from-admin-workstations"></a>Kein Zugriff auf E-Mails über Administratorkonten oder auf Administratorarbeitsstationen
Administrative Mitarbeiter dürfen nicht auf E-Mail, während Sie mit einem Administratorkonto oder bei einer Administratorarbeitsstation angemeldet sind, auf zugreifen.

###### <a name="store-service-and-application-account-passwords-in-a-secure-location"></a>Store-Dienst und die Anwendung an einem sicheren Ort Kontokennwörter
Die folgenden Richtlinien sollte verwendet werden, für die physische Sicherheit, Steuern des Zugriffs auf das Kennwort verarbeitet:

-   Sperren Sie Kennwörter für Dienstkonten in einem Safe.

-   Stellen Sie sicher, dass nur Mitarbeiter, oder über die Vertrauensebene des Kontos haben Sie Zugriff auf das Kontokennwort.

-   Die Anzahl der Personen, die auf die Kennwörter auf ein Minimum zu für nachvollziehbare Verantwortlichkeiten zugreifen.

-   Stellen Sie sicher, dass alle Zugriff auf das Kennwort angemeldet, nachverfolgt und von einer unbeteiligten Partei, z.B. ein Vorgesetzter, der nicht zum Ausführen von IT-Administration geschult wurde überwacht wird.

##### <a name="strong-authentication"></a>Strenge Authentifizierung
Verwenden Sie die folgenden Methoden, um die ordnungsgemäße Konfiguration der strengen Authentifizierung.

###### <a name="enforce-smartcard-multi-factor-authentication-mfa-for-all-admin-accounts"></a>Erzwingen der Smartcard Multi-Factor Authentication (MFA) für alle Administratorkonten
Kein Administratorkonto ist zulässig, ein Kennwort zur Authentifizierung verwendet. Die einzigen autorisierten Ausnahmen sind die notfallzugriffskonten, die über die geeigneten Prozesse geschützt sind.

Verknüpfen Sie alle Administratorkonten mit einer Smartcard, und aktivieren Sie das Attribut "**Smartcard für die interaktive Anmeldung erforderlich**."

Ein Skript sollte implementiert werden, um automatisch und in regelmäßigen Abständen den zufälligen Kennworthashwert zurücksetzen, indem Sie deaktivieren und umgehend erneut aktiviert das Attribut "**Smartcard für die interaktive Anmeldung erforderlich**."

Erlauben Sie keine Ausnahmen für Konten von Mitarbeitern die notfallzugriffskonten verwendet.

###### <a name="enforce-multi-factor-authentication-for-all-cloud-admin-accounts"></a>Erzwingen der mehrstufigen Authentifizierung für alle Cloudadministratorkonten
Alle Konten mit Administratorrechten in einem Cloud-Dienst, z.B. Microsoft Azure und Office365, müssen die mehrstufige Authentifizierung verwenden.

##### <a name="rare-use-emergency-procedures"></a>Selten erforderliche Notfallmaßnahmen
Betriebliche Verfahren müssen die folgenden Standards zu unterstützen:

-   Stellen Sie sicher, dass Ausfälle schnell behoben werden können.

-   Sicherstellen Sie, dass nur selten mit umfassenden rechten Aufgaben abgeschlossen werden können, je nach Bedarf.

-   Stellen Sie sicher, dass sichere Verfahren verwendet werden, um die Anmeldeinformationen und Berechtigungen zu schützen.

-   Stellen Sie sicher, dass die geeignete Verfahren für Nachverfolgung und Genehmigung implementiert sind.

###### <a name="correctly-follow-appropriate-processes-for-all-emergency-access-accounts"></a>Ordnungsgemäße Implementierung der geeignete Verfahren für alle notfallzugriffskonten
Stellen Sie sicher, dass jedes notfallzugriffskonto ein Tracking Blatt im Safe hinterlegt ist.

Das Verfahren für das Kennwort beispielsweise dokumentiert sollten für jedes Konto befolgt werden Ändern des Kennworts nach jeder Verwendung und Abmeldung bei Arbeitsstationen oder Servern, die nach Abschluss des Vorgangs verwendet.

Die Verwendung von Notfallzugriff, die Konten durch das Change Approval Board bzw. nach dem Ereignis als genehmigte Notfallverwendung genehmigt werden sollen.

###### <a name="restrict-and-monitor-usage-of-emergency-access-accounts"></a>Einschränken Sie und überwachen Sie der Verwendung von notfallzugriffskonten
Für jede Verwendung von notfallzugriffskonten:

-   Nur autorisierte Domänenadministratoren können die notfallzugriffskonten mit Domänenadministratorberechtigungen zugreifen.

-   Die notfallzugriffskonten können nur auf Domänencontrollern und anderen Hosts der Ebene 0 verwendet werden.

-   Dieses Konto sollte nur verwendet werden:

    -   Führen Sie die Problembehandlung und Behebung technischer Probleme, die die Verwendung der richtigen Administratorkonten verhindern.

    -   Durchführen Sie seltener Aufgaben, z.B. an:

        -   Schema-Verwaltung

        -   Gesamtstrukturweite Aufgaben, die Administratorrechte auf Unternehmensebene erforderlich ist. Beachten Sie, dass die topologieverwaltung, einschließlich der Verwaltung von Active Directory Standort- und Subnetzinformationen delegiert wird, um die Nutzung dieser Rechte einzuschränken.

-   Für jede Verwendung eines dieser Konten sollte Genehmigung vom Leiter Sicherheitsgruppe geschrieben haben

-   Das Verfahren auf dem Blatt Nachverfolgung für jedes notfallzugriffskonto erfordert das Kennwort nach jeder Verwendung geändert werden. Ein Mitglied des Sicherheitsteams sollte überprüfen, dass diese ordnungsgemäß ausgeführt wurde.

###### <a name="temporarily-assign-enterprise-admin-and-schema-admin-membership"></a>Vorübergehendes Zuweisen der Mitgliedschaft als Organisations-Admins und schema
Erforderliche und entfernt nach verwenden sollten Berechtigungen hinzugefügt werden. Notfallzugriffskonten sollten diese Berechtigungen nur die Dauer des Vorgangs ausgeführt werden und bis zu 10 Stunden zugewiesen haben. Alle Verwendung und die Dauer dieser Berechtigungen sollten in Change Approval Boards erfasst werden, nachdem der Vorgang abgeschlossen ist.

## <a name="ESAE_BM"></a>ESAE-Verwaltungsgesamtstruktur Entwurfsansatz
Dieser Abschnittenthält einen Ansatz für eine administrative Gesamtstruktur basierend auf der Enhanced Security Administrative Environment (ESAE)-Referenzarchitektur bereitgestellt, die von Microsoft dienstleistungsteams um Kunden vor Cyberangriffen zu schützen.

Dedizierten administrativen Gesamtstruktur können Organisationen Host Administratorkonten, Arbeitsstationen und Gruppen in einer Umgebung stärkere Sicherheitskontrollen auf als die Produktionsumgebung.

Diese Architektur ermöglicht eine Reihe von Sicherheitskontrollen, die nicht in einer einzelnen Gesamtstruktur-Architektur, auch ein Arbeitsstationen mit privilegiertem Zugriff (PAWs) verwaltet möglich oder nicht einfach zu konfigurieren sind. Dieser Ansatz ermöglicht die Bereitstellung von Konten als Standard nicht privilegierten Benutzern in der administrativen Gesamtstruktur, die in der Produktionsumgebung hohe Berechtigungen sind umfassende technische Erzwingung von Governance. Diese Architektur ermöglicht auch die Verwendung des Features ausgewählte Authentifizierung einer Vertrauensstellung als zum Einschränken Anmeldungen (und Offenlegung von Anmeldeinformationen) nur autorisierte Hosts. In Situationen, in denen größer ein gewisses Maß an Sicherheit für die Produktionsgesamtstruktur gewünscht ist ohne die Kosten und Komplexität einer vollständigen Wiederherstellung, kann eine administrative Gesamtstruktur eine Umgebung bereitstellen, die den Sicherheitsgrad der der Produktionsumgebung erhöht wird.

Während dieser Ansatz eine Gesamtstruktur zu einer Active Directory-Umgebung hinzufügt, sind die Kosten und Komplexität der festen Aufbaus kleine Hardware- und softwareanforderungen und geringe Anzahl von Benutzern beschränkt.

> [!NOTE]
> Dieser Ansatz funktioniert gut für die Verwaltung von Active Directory, aber viele Anwendungen sind mit nicht kompatibel, die von Konten aus einer externen Gesamtstruktur eine verwaltet wird.

Diese Abbildungzeigt eine ESAE-Gesamtstruktur verwendet für die Verwaltung von Assets der Ebene 0 sowie eine PRIV-Gesamtstruktur, die für die Verwendung mit Privileged Access Management-Funktion von Microsoft Identity Manager konfiguriert. Weitere Informationen zum Bereitstellen einer MIM PAM-Instanz finden Sie unter [Privileged Identity Management für Active Directory-Domänendienste (AD DS)](https://technet.microsoft.com/en-us/library/mt150258.aspx) Artikel.

![Diese Abbildungzeigt eine ESAE-Gesamtstruktur verwendet für die Verwaltung von Assets der Ebene 0 sowie eine PRIV-Gesamtstruktur, die für die Verwendung mit Privileged Access Management-Funktion von Microsoft Identity Manager konfiguriert](../media/securing-privileged-access-reference-material/PAW_RM_Fig14.JPG)

Eine dedizierte administrative Gesamtstruktur ist eine standardmäßige einzelne Domäne Active Directory-Gesamtstruktur für die Funktion des Active Directory-Verwaltung. Administrative Gesamtstrukturen und Domänen strikter abgesichert werden als Produktionsgesamtstrukturen aufgrund des begrenzten Anwendungsfälle Produktionsgesamtstrukturen.

Entwurf einer administrativen Gesamtstruktur sollte Folgendes berücksichtigt werden:

-   **Beschränkter Gültigkeitsbereich** -der primäre Nutzen einer administrativen Gesamtstruktur ist die hohes Maß an Sicherheit und der verringerten Angriffsfläche geringeren Restrisiko. Die Gesamtstruktur kann verwendet werden, um zusätzliche Verwaltungsfunktionen und -Anwendungen, aber jede Erweiterung des Bereichs wird die Angriffsfläche der Gesamtstruktur und seine Ressourcen zu erhöhen. Ziel ist es, die Funktionen der Gesamtstruktur und der Administrator Benutzer innerhalb beschränken, um die Angriffsfläche minimal zu halten, daher sollte jede Erweiterung des Bereichs sorgfältig überlegt werden.

-   **Konfiguration von Vertrauensstellungen** -Vertrauensstellung aus verwalteten Forestss oder Domänen zur administrativen Gesamtstruktur konfigurieren

    -   Eine unidirektionale Vertrauensstellung ist von der Produktionsumgebung zur administrativen Gesamtstruktur erforderlich. Dies kann eine Domänen- oder Gesamtstruktur-Vertrauensstellung. Der administrativen Gesamtstruktur bzw. der Domäne muss nicht die verwalteten Domänen/Gesamtstrukturen zum Verwalten von Active Directory zu vertrauen, jedoch möglicherweise zusätzliche Anwendungen sind, eine bidirektionale Vertrauensstellung, Sicherheitsüberprüfungen erforderlich und Tests.

    -   Die ausgewählte Authentifizierung sollte verwendet werden, um Konten in der administrativen Gesamtstruktur Protokollierung nur auf, um den richtigen produktionshosts zu beschränken. Für die Verwaltung von Domänencontrollern und Delegieren von rechten in Active Directory, dies in der Regel "Darf-Anmeldung" ist Berechtigung erforderlich von Domänencontrollern auf Ebene 0 Administratorkonten in der administrativen Gesamtstruktur. Weitere Informationen finden Sie in der Einstellungen für ausgewählte Authentifizierung konfigurieren.

-   **Berechtigungen und Härten von Domänen** -die administrative Gesamtstruktur geringsten Rechte, die anhand der Anforderungen für Active Directory-Verwaltung konfiguriert werden soll.

    -   Erteilen von Berechtigungen für die Verwaltung von Domänencontrollern und Delegieren von Berechtigungen muss der lokalen Domänengruppe "VORDEFINIERT\Administratoren" Administratorkonten für die Gesamtstruktur hinzugefügt. Dies ist, da der globalen Gruppe Domänen-Admins Mitglieder einer externen Domäne haben kann.

    -   Die Verwendung dieser Gruppe zum Erteilen von rechten spricht ist, dass sie Administratorzugriff auf neue Gruppenrichtlinienobjekte standardmäßig nicht. Dies kann geändert werden, mithilfe des folgenden Verfahrens in [diesem Knowledge Base-Artikel](https://support.microsoft.com/kb/321476) so ändern Sie die Standardberechtigungen für Schemas.

    -   Konten in der administrativen Gesamtstruktur, die verwendet werden, um die Verwaltung der Produktionsumgebung sollte nicht über Administratorrechte für die administrative Gesamtstruktur, Domänen oder Arbeitsstationen gewährt werden.

    -   Administratorrechte für die administrative Gesamtstruktur sollten von Offline-Vorgang, reduzieren Sie die Gelegenheit für Angreifer oder böswillige, Löschen von Überwachungsprotokollen eng kontrolliert werden. Dies hilft sicherzustellen, dass Mitarbeiter mit Administratorkonten für die Produktion die Einschränkungen ihrer Konten entspannen und das Risiko für die Organisation erhöhen können nicht.

    -   Die administrative Gesamtstruktur muss die Microsoft Security Compliance Basislinie (SCB)-Konfigurationen für die Domäne, einschließlich sicherer Konfigurationen für Authentifizierungsprotokolle.

    -   Alle Hosts in der administrativen Gesamtstruktur sollten automatisch mit Sicherheitsupdates aktualisiert werden. Während das Risiko einer Unterbrechung der Domänencontroller erstellen kann, bietet es eine erhebliche Verringerung von Sicherheitsrisiken nicht gepatchten Schwachstellen.

        > [!NOTE]
        > Eine dedizierte Instanz von Windows Server Update Services kann konfiguriert werden, dass Updates automatisch genehmigt. Weitere Informationen finden Sie im Abschnitt "Automatisches genehmigen Sie Updates für die Installation" Genehmigen von Updates.

-   **Härten von Arbeitsstationen** -Build der administrativen Arbeitsstationen mit dem [Privileged Access Workstations](../securing-privileged-access/privileged-access-workstations.md) (über Phase 3), ändern Sie jedoch die Domänenmitgliedschaft zur administrativen Gesamtstruktur anstelle der Produktionsumgebung.

-   **Server und Domänencontroller Hardening** – für alle Domänencontroller und Server in der administrativen Gesamtstruktur:

    -   Stellen Sie sicher, alle Medien wird überprüft mithilfe der Anleitungen im [vertrauenswürdige Quelle für Installationsmedien](http://aka.ms/cleansource)

    -   Stellen Sie sicher, dass die administrative Gesamtstruktur-Server den neuesten Betriebssystemen installiert ist, werden soll, auch wenn dies nicht in der Produktion möglich ist.

    -   Hosts in der administrativen Gesamtstruktur sollten automatisch mit Sicherheitsupdates aktualisiert werden.

        > [!NOTE]
        > Windows Server Update Services können konfiguriert werden, dass Updates automatisch genehmigt. Weitere Informationen finden Sie im Abschnitt "Automatisches genehmigen Sie Updates für die Installation" Genehmigen von Updates.

    -   Sicherheitsbaselines sollten als Ausgangskonfiguration verwendet werden.

        > [!NOTE]
        > Kunden können die Microsoft Security Compliance-Toolkit (SCT) zum Konfigurieren von Baselines auf den administrativen Hosts verwenden.

    -   Sicherer Start, um gegen Angreifer oder Malware, die beim Laden von nicht signierten Codes in den Startprozess zu verringern.

        > [!NOTE]
        > Dieses Feature wurde in Windows8 zu nutzen, die Unified Extensible Firmware Interface (UEFI) eingeführt.

    -   Verschlüsselung ganzer Volumes zur Verlust physischer Computer, z.B. administrativer Laptops verwendet Remote zu verringern.

        > [!NOTE]
        > Weitere Informationen finden Sie unter [BitLocker](https://technet.microsoft.com/en-us/library/dn641993.aspx) Weitere Informationen.

    -   USB-Einschränkungen zum Schutz vor physischen infektionsvektoren.

        > [!NOTE]
        > Weitere Informationen finden Sie unter [Steuerelement Lese- oder Write Access to Removable Devices or Media](https://technet.microsoft.com/en-us/library/cc730808(v=ws.10).aspx) Weitere Informationen.

    -   Die Netzwerkisolation zum Schutz vor Netzwerkangriffen und unbeabsichtigten. Hostfirewalls sollten alle eingehenden Verbindungen, mit Ausnahme der ausdrücklich erforderlichen, und sämtliche ausgehenden Internetzugriffe sperren.

    -   Antischadsoftware zum Schutz vor bekannten Risiken und Malware.

    -   Attack Surface Analyse, um die Einführung neuer Angriffsvektoren auf Windows während der Installation von neuer Software zu verhindern.

        > [!NOTE]
        > Verwendung von Tools wie z.B. die [Attack Surface Analyzer (ASA)](https://www.microsoft.com/en-us/download/details.aspx?id=24487) hilft Konfigurationseinstellungen auf einem Host und durch Software oder Konfigurationsänderungen eingeführt Angriffsvektoren zu identifizieren.

-   Härtung von Konto

    -   Multi-Factor Authentication sollte für alle Konten in der administrativen Gesamtstruktur, mit Ausnahme eines Kontos konfiguriert werden. Mindestens ein Administratorkonto sollte sein, dass die Kennwort-basiert, um sicherzustellen, dass Zugriff für den Fall, dass die mehrstufige Authentifizierung verarbeiten Pausen funktionieren. Dieses Konto sollte durch strikte physische Kontrollmechanismen geschützt werden.

    -   Für Multi-Factor Authentication konfigurierte Konten sollten eines neuen NTLM Hash für Konten regelmäßig festgelegt, konfiguriert werden. Dies erfolgt durch das Deaktivieren und Aktivieren des Kontoattributs Smartcard für die interaktive Anmeldung erforderlich ist.

        > [!NOTE]
        > Dadurch kann laufende Vorgänge unterbrochen, die dieses Konto verwenden, damit dieser Vorgang nur, wenn Administratoren das Konto, z.B. nachts oder am Wochenende verwenden, wird nicht gestartet werden sollen.

-   Der sprungserver

    -   Der sprungserver Steuerelemente für die administrative Gesamtstruktur sollten bei Anomalien in der administrativen Gesamtstruktur Warnungen ausgeben entworfen werden. Die begrenzte Anzahl von autorisierten Szenarios und Aktivitäten können diese Steuerelemente präziser als die Produktionsumgebung optimieren.

Weitere Informationen zu Microsoft-Diensten zum Entwerfen und Bereitstellen einer ESAE für Ihre Umgebung, finden Sie unter [auf dieser Seite](https://www.microsoft.com/services).

## <a name="T0E_BM"></a>Äquivalenz zur Ebene 0
Die meisten Organisationen kontrollieren die Mitgliedschaft leistungsstarke Gruppen auf Ebene 0 Active Directory wie Administratoren, Domänen-Admins und Organisations-Admins.  Viele Organisationen übersehen das Risiko anderer Gruppen, die Rechte in einer typischen active Directory-Umgebung effektiv entsprechen. Diese Gruppen bieten einen Recht problemlosen Eskalationspfad für Angreifer die gleichen expliziten Ebene-0-Berechtigungen, die über verschiedene Angriffsmethoden.

Beispiel: ein konnte Zugriff auf ein Sicherungsmedium eines Domänencontrollers erhalten und extrahieren alle Anmeldeinformationen aus den Dateien auf diesem Medium und verwenden, um Berechtigungen zu erweitern.

Organisationen sollten steuern und überwachen Sie die Mitgliedschaft in allen Gruppen der Ebene 0 (einschließlich geschachtelter Mitgliedschaften) einschließlich:

-   Organisations-Admins

-   Domänen-Admins

-   Schema-Admins

-   "VORDEFINIERT\Administratoren"

-   Konten-Operatoren

-   Sicherungs-Operatoren

-   Druck-Operatoren

-   Server-Operatoren

-   Domänencontroller

-   Read-only Domain Controller

-   Richtlinien-Ersteller-Besitzer

-   Kryptografische Operatoren

-   Distributed COM-Benutzer

-   Andere delegierte Gruppen

    > [!NOTE]
    > "Andere delegierten Gruppen" bezieht sich auf Gruppen, die von Ihrer Organisation zu verwalten, die ebenfalls über effektiven Zugriff der Ebene 0 möglicherweise erstellt werden können.

## <a name="ATLT_BM"></a>Verwaltungstools und Anmeldetypen
Dies ist die Referenzinformationen, um das Risiko einer Offenlegung von Anmeldeinformationen mit der Verwendung verschiedener Tools für die Remoteverwaltung zu identifizieren.

In einem Szenario mit Remote-Verwaltung werden Anmeldeinformationen immer auf dem Quellcomputer verfügbar gemacht, damit eine Arbeitsstation mit vertrauenswürdigen privilegiertem Zugriff (PAW) für sensible oder hoher Auswirkung Konten immer empfohlen wird. Gibt an, ob die Anmeldeinformationen und potenziell gestohlen, auf dem Zielcomputer (Remotecomputer) offengelegt werden, hängt in erster Linie auf der Windows-Anmeldetyp, der von der Verbindungsmethode verwendet.

Diese Tabelle enthält Richtlinien für die meisten gängigen Verwaltungstools und Verbindungsmethoden:

|Verbindung<br />Methode|Anmeldetyp|Wiederverwendbare Anmeldeinformationen auf dem Zielserver|Kommentare|
|-----------|-------|--------------------|------|
|Melden Sie sich an der Konsole|Interaktive|v|Umfasst Remotehardwarezugriff / Lights-out-Karten und Netzwerk-KVMs.|
|RUNAS|Interaktive|v||
|RUNAS//NETWORK|Neue Anmeldeinformationen|v|Klont die aktuelle LSA-Sitzung für den lokalen Zugriff, jedoch neue Anmeldeinformationen mit Netzwerkressourcen Herstellen einer Verbindung verwendet.|
|Remotedesktop (erfolgreich)|RemoteInteractive|v|Wenn die Remotedesktop-Client konfiguriert ist, um lokale Geräte und Ressourcen freizugeben, können diese auch gefährdet sein.|
|Remotedesktop (Fehler – Anmeldetyp verweigert)|RemoteInteractive|-|Standardmäßig werden nur sehr kurz gespeichert RDP-Anmeldeinformationen für ein Fehler auftritt. Dies kann nicht der Fall sein, wenn der Computer gefährdet ist.|
|NET verwenden * \\\SERVER|Netzwerk|-||
|NET verwenden * \\\SERVER /u: Benutzer|Netzwerk|-||
|MMC-Snap-Ins für Remotecomputer|Netzwerk|-|Beispiel: Computer Computerverwaltung, Ereignisanzeige, Geräte-Manager, Dienste|
|PowerShell WinRM|Netzwerk|-|Beispiel: Enter-PSSession Server|
|PowerShell WinRM mit CredSSP|NetworkClearText|v|New-PSSession Server<br />-Credssp Authentifizierung<br />-Cred credential|
|PsExec ohne explizite Anmeldeinformationen|Netzwerk|-|Beispiel: PsExec \\\server cmd|
|PsExec mit expliziten Anmeldeinformationen|Netzwerk und interaktive|v|PsExec \\\server u - Benutzer -p Pwd cmd<br />Erstellt mehrere anmeldesitzungen.|
|Remote-Registrierung|Netzwerk|-||
|Remotedesktop-Gatewayserver|Netzwerk|-|Authentifizierung gegenüber Remotedesktopgateway.|
|Geplante Aufgabe|Stapel|v|Kennwort wird auch als geheime LSA-Daten auf dem Datenträger gespeichert werden.|
|Führen Sie Tools als Dienst|Dienst|v|Kennwort wird auch als geheime LSA-Daten auf dem Datenträger gespeichert werden.|
|Sicherheitsrisiken überprüfen|Netzwerk|-|Die meisten Scanner standardmäßig die Netzwerkanmeldungen, obwohl einige Anbieter können nicht Netzwerkanmeldungen implementieren und weitere Anmeldeinformationen das Risiko eines Diebstahls einzuführen.|

Verwenden Sie Informationen zur Webauthentifizierung finden Sie in der folgenden Tabelle:

|Verbindung<br />Methode|Anmeldetyp|Wiederverwendbare Anmeldeinformationen auf dem Zielserver|Kommentare|
|-----------|-------|--------------------|------|
|IIS "Standardauthentifizierung"|NetworkCleartext<br />(IIS) 6.0 +<br /><br />Interaktive<br />(vor IIS 6.0)|v||
|IIS integrierte Windows-Authentifizierung"|Netzwerk|-|NTLM- und Kerberos-Anbieter.|

Definitionen:

-   **Anmeldetyp** identifiziert den Anmeldetyp, der von der Verbindung initiiert.

-   **Wiederverwendbare Anmeldeinformationen auf dem Ziel** gibt an, dass die folgenden Typen von Anmeldeinformationen im LSASS-Prozessspeicher auf dem Zielcomputer gespeichert werden, in denen das angegebene Konto lokal angemeldet wird:

    -   LM- und NT-hashes

    -   Kerberos-TGTs

    -   Nur-Text-Kennwort (falls zutreffend).

    -

Die Symbole in dieser Tabelle wie folgt definiert:

-   (-) zeigt an, dass Anmeldeinformationen nicht offengelegt werden.

-   (V) Zeigt an, dass Anmeldeinformationen verfügbar gemacht werden.

Bei Verwaltungsanwendungen, die nicht in dieser Tabelle enthalten sind, können Sie den Anmeldetyp anhand des entsprechenden Felds in den überwachten Anmeldeereignissen ermitteln. Weitere Informationen finden Sie unter [Anmeldeereignisse](https://technet.microsoft.com/en-us/library/cc787567(v=ws.10).aspx).

In Windows-basierten Computern werden alle Authentifizierungen als einer von mehreren Anmeldetypen verarbeitet, unabhängig davon, welches Authentifizierungsprotokoll oder welcher Authenticator verwendet wird. Diese Tabelle enthält die gängigsten Anmeldetypen sowie die zugehörigen Attribute relativ zum Diebstahl von Anmeldeinformationen:

|Anmeldetyp|#|Akzeptierte Authenticators|Wiederverwendbare Anmeldeinformationen in LSA-Sitzung|Beispiele für|
|-------|---|--------------|--------------------|------|
|Interaktiv (lokale Anmeldung)|2|Kennwort, Smartcard,<br />andere|Ja|Konsolenanmeldung;<br />RUNAS;<br />Lösungen zur Remotesteuerung Hardware (z.B. Netzwerk-KVM oder Remotezugriff / Lights-Out-Karte in Servern)<br />IIS-Standardauthentifizierung (vor IIS 6.0)|
|Netzwerk|3|Kennwort<br />NT-Hash<br />Kerberos-Tickets|Nein (Ausnahme: Wenn Delegierung und Kerberos-vorhanden Tickets und aktiviert)|NET USE;<br />RPC-Aufrufe;<br />Remotezugriff auf die Registrierung;<br />IIS integrierte Windows-Authentifizierung;<br />SQL-Windows-Authentifizierung,|
|Stapel|4|Kennwort (üblicherweise als geheime LSA-Daten gespeichert)|Ja|Geplante Aufgaben|
|Dienst|5|Kennwort (üblicherweise als geheime LSA-Daten gespeichert)|Ja|Windows-Dienste|
|NetworkCleartext|8|Kennwort|Ja|IIS-Standardauthentifizierung (IIS 6.0 und höher);<br />WindowsPowerShell mit CredSSP|
|Neue Anmeldeinformationen|9|Kennwort|Ja|RUNAS//NETWORK|
|RemoteInteractive|10|Kennwort, Smartcard,<br />andere|Ja|Remotedesktop (früher als "Terminal Services" bezeichnet)|

Definitionen:

-   **Anmeldetyp** ist der Typ der angeforderten Anmeldung.

-   **#**ist der numerische Bezeichner für den Anmeldetyp, der in Überwachungsereignissen des Sicherheitsereignisprotokolls gemeldet wird.

-   **Akzeptierte Authenticators** gibt an, welche Typen von Authenticators eine Anmeldung dieses Typs initiieren können.

-   **Wiederverwendbare Anmeldeinformationen** in LSA angibt, ob der Anmeldetyp zur Folge der LSA-Sitzung Anmeldeinformationen, z.B. Nur-Text-Kennwörter, NT-Hashes oder Kerberos-Tickets, die Authentifizierung gegenüber anderer Netzwerkressourcen verwendet werden können.

-   **Beispiele für** Liste allgemeine Szenarien, in denen der Anmeldetyp verwendet wird.

> [!NOTE]
> Weitere Informationen zu Anmeldetypen, finden Sie unter [SECURITY_LOGON_TYPE Enumeration](https://technet.microsoft.com/en-us/library/aa380129(VS.85).aspx).
