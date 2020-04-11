---
title: Schützen des privilegierten Zugriffs – Referenzmaterial
description: Funktionale Sicherheitskontrollen für Windows Server Active Directory-Domänen
ms.prod: windows-server
ms.topic: article
ms.assetid: 22ee9a77-4872-4c54-82d9-98fc73a378c0
ms.date: 02/14/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 00335fb2ca7a54031430c6c606fb6ffa23a8f7a2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855133"
---
# <a name="active-directory-administrative-tier-model"></a>Active Directory-Verwaltungsebenenmodell

>Gilt für: Windows Server

Dieses Ebenenmodell wird eingesetzt, um Identitätssysteme zu schützen. Zu diesem Zweck werden Pufferzonen zwischen der vollständigen Kontrolle der Umgebung (Ebene 0) und den Arbeitsstationsassets implementiert, die ein häufiges Ziel von Angreifern sind.

![Diagramm, das die drei Ebenen des Tier-Modells zeigt](../media/securing-privileged-access-reference-material/PAW_RM_Fig1.JPG)

Dieses Modell beinhaltet drei Ebenen sowie ausschließlich Administratorkonten (keine standardmäßigen Benutzerkonten):

- **Ebene 0**: Direkte Kontrolle von Unternehmensidentitäten innerhalb der Umgebung. Die Ebene 0 umfasst Konten, Gruppen und andere Assets mit direkter oder indirekter Administratorkontrolle der Active Directory-Gesamtstruktur, -Domänen oder -Domänencontroller sowie aller zugehörigen Assets. Da die Assets der Ebene 0 sich effektiv gegenseitig steuern und kontrollieren, ist die Vertraulichkeit dieser Assets äquivalent.
- **Ebene 1**: Kontrolle von Unternehmensservern und -anwendungen. Assets der Ebene 1 umfassen Serverbetriebssysteme, Clouddienste und Unternehmensanwendungen. Administratorkonten der Ebene 1 verfügen über administrative Berechtigungen für eine signifikante Menge von Unternehmensressourcen, die auf diesen Assets gehostet werden. Ein gängiges Beispiel sind Serveradministratoren, die die zugehörigen Betriebssysteme verwalten und damit Aufgaben ausführen, die sich auf alle Unternehmensdienste auswirken können.
- **Ebene 2**: Kontrolle von Benutzerarbeitsstationen und -geräten. Administratorkonten der Ebene 2 verfügen über administrative Berechtigungen für eine signifikante Menge von Unternehmensressourcen, die auf Benutzerarbeitsstationen und -geräten gehostet werden. Beispiele sind Helpdesk- und Computersupportadministratoren, deren Aufgaben sich auf die Integrität von praktisch sämtlichen Benutzerdaten auswirken können.

> [!NOTE]
> Die Ebenen dienen zudem als grundlegender Priorisierungsmechanismus zum Schutz von administrativen Assets. Bedenken Sie jedoch stets, dass ein Angreifer mit Kontrolle aller Assets einer beliebigen Ebene auf die meisten oder alle Unternehmensassets zugreifen kann. Das Ebenenmodell ist ein nützlicher grundlegender Priorisierungsmechanismus, weil es eine zusätzliche Hürde für Angreifer darstellt. Angreifer können ihre Pläne bei vollständiger Kontrolle aller Identitäten (Ebene 0) oder Server und Clouddienste (Ebene 1) einfacher umsetzen als in einem Szenario, in dem sie auf die einzelnen Arbeitsstationen oder Benutzergeräte (Ebene 2) zugreifen müssen, um Zugang zu den Daten Ihrer Organisation zu erhalten.

## <a name="containment-and-security-zones"></a>Eindämmung und Sicherheitszonen

Die Ebenen werden relativ zu einer bestimmten Sicherheitszone implementiert. Bei Sicherheitszonen handelt es sich um einen bewährten Ansatz, mit dem Sicherheitsbedrohungen durch eine Isolierung auf der Vermittlungsschicht eingedämmt werden können. Das Ebenenmodell ergänzt dieses Verfahren durch das Eindämmen von Angriffsversuchen innerhalb einer Sicherheitszone, in der die Netzwerkisolation nicht greift. Sicherheitszonen können sich sowohl über lokale als auch über cloudbasierte Infrastrukturen erstrecken, beispielsweise in einem Szenario, in dem Domänencontroller und Domänenmitglieder innerhalb derselben Domäne sowohl lokal als auch in Azure gehostet werden.

![Diagramm, das zeigt, wie Sicherheitszonen jeweils die lokale als auch die Cloudinfrastruktur umfassen können](../media/securing-privileged-access-reference-material/PAW_RM_Fig2.JPG)

Das Ebenenmodell verhindert eine Ausweitung von Rechten, indem die Bereiche eingeschränkt werden, die Administratoren steuern und in denen sich Administratoren anmelden können (durch die Anmeldung an einem Computer erhält der Benutzer Zugang zu diesen Anmeldeinformationen und allen Assets, die über diese Anmeldeinformationen verwaltet werden).

### <a name="control-restrictions"></a>Eingeschränkte Kontrolle

In der Abbildung unten sind die Kontrollbereiche eingeschränkt:

![Diagramm der eingeschränkten Kontrolle](../media/securing-privileged-access-reference-material/PAW_RM_Fig3.JPG)

### <a name="primary-responsibilities-and-critical-restrictions"></a>Primäre Aufgaben und wichtige Einschränkungen

**Administrator der Ebene 0**: Verwalten des Identitätsspeichers und einer kleinen Anzahl von Systemen, die diesen Speicher effektiv kontrollieren und steuern: Außerdem:

- Bei Bedarf Verwalten und Steuern von Assets auf sämtlichen Ebenen
- Interaktives Anmelden oder Zugriff auf Assets, die auf der Ebene 0 als vertrauenswürdig eingestuft werden

**Administrator der Ebene 1**: Verwalten von Unternehmensservern, -diensten und -anwendungen. Außerdem:

- Ausschließlich Verwaltung und Steuerung von Assets auf Ebene 1 und Ebene 2
- Ausschließlich Zugriff auf Assets (über den Anmeldetyp „Netzwerk“), die auf Ebene 1 und Ebene 0 als vertrauenswürdig eingestuft werden
- Interaktives Anmelden bei Assets, die auf der Ebene 1 als vertrauenswürdig eingestuft werden

**Administrator der Ebene 2**: Verwalten von Unternehmensdesktops, -laptops, -druckern und anderen Benutzergeräten. Außerdem:

- Ausschließlich Verwaltung und Steuerung von Assets auf Ebene 2
- Bei Bedarf Zugriff auf Assets auf allen Ebenen (über den Anmeldetyp „Netzwerk“)
- Ausschließlich interaktives Anmelden bei Assets, die auf der Ebene 2 als vertrauenswürdig eingestuft werden

### <a name="logon-restrictions"></a>Anmeldeeinschränkungen

Die Abbildung unten zeigt Anmeldeeinschränkungen:

![Diagramm der Anmeldeeinschränkungen](../media/securing-privileged-access-reference-material/PAW_RM_Fig4.JPG)

> [!NOTE]
> Beachten Sie, dass einige Assets sich im Umfang von Ebene 0 auf die Verfügbarkeit der Umgebung auswirken können. Die Vertraulichkeit oder Integrität der Assets wird jedoch nicht direkt beeinträchtigt. Dazu zählen der DNS-Serverdienst sowie wichtige Netzwerkgeräte wie Internetproxys.

## <a name="clean-source-principle"></a>Prinzip der vertrauenswürdigen Quelle

Beim Prinzip der vertrauenswürdigen Quelle müssen alle Sicherheitsabhängigkeiten genauso vertrauenswürdig sein wie das zu sichernde Objekt.

![Diagramm, das zeigt, dass jedes Subjekt, das ein Objekt kontrolliert, eine Sicherheitsabhängigkeit dieses Objekts ist](../media/securing-privileged-access-reference-material/PAW_RM_Fig5.JPG)

Jedes Subjekt, das ein Objekt kontrolliert, ist eine Sicherheitsabhängigkeit dieses Objekts. Wenn ein Angreifer ein Asset mit effektiver Kontrolle über ein Zielobjekt kontrollieren und steuern kann, so kann er auch dieses Zielobjekt kontrollieren. Daher müssen Sie sicherstellen, dass die Zusicherungen für alle Sicherheitsabhängigkeiten mindestens der Sicherheitsstufe des Objekts selbst entsprechen.

Wenngleich dies an sich einfach ist, müssen Sie zur Umsetzung die Kontrollbeziehungen eines Assets (Objekt) kennen und eine Abhängigkeitsanalyse durchführen, um alle Sicherheitsabhängigkeiten (Subjekte) zu ermitteln.

Da es sich um eine transitive Kontrolle handelt, muss dieses Prinzip rekursiv wiederholt werden. Beispiel: Wenn B von A und C von B gesteuert wird, dann steuert A indirekt auch C.

![Diagramm, das folgendes Beispiel zeigt: Wenn B von A und C von B gesteuert wird, dann steuert A indirekt auch C](../media/securing-privileged-access-reference-material/PAW_RM_Fig6.JPG)

Ein Angreifer, der A gefährdet, erhält Zugriff auf alle Elemente, die A steuert (einschließlich B) sowie alle Elemente, die B steuert (einschließlich C). Im Hinblick auf die Sicherheitsabhängigkeiten dieses Beispiels sind sowohl B als auch A Sicherheitsabhängigkeiten von C. Beide müssen folglich die gewünschte Sicherheitsstufe von C aufweisen, damit diese Stufe für C eingehalten wird.

Bei IT-Infrastrukturen und Identitätssystemen sollte dieses Prinzip auf die meisten gängigen Kontrollmechanismen angewendet werden. Dies umfasst auch die Hardware, auf der Systeme installiert sind, die Installationsmedien für die Systeme, die Architektur und die Konfiguration des Systems sowie tägliche Vorgänge.

## <a name="clean-source-for-installation-media"></a>Vertrauenswürdige Quelle für Installationsmedien

![Diagramm, das eine vertrauenswürdige Quelle für Installationsmedien zeigt](../media/securing-privileged-access-reference-material/PAW_RM_CSIM.JPG)

Um das Prinzip der vertrauenswürdigen Quelle auf Installationsmedien anzuwenden, müssen Sie (so gut wie möglich) sicherstellen, dass das Installationsmedium seit der Freigabe durch den Hersteller nicht manipuliert wurde. Nachfolgend wird gezeigt, wie ein Angreifer diesen Weg nutzt, um einen Computer zu gefährden:

![Die Abbildung zeigt, wie ein Angreifer diesen Weg nutzt, um einen Computer zu gefährden](../media/securing-privileged-access-reference-material/PAW_RM_Fig8.JPG)

Um das Prinzip der vertrauenswürdigen Quelle auf Installationsmedien anzuwenden, muss die Softwareintegrität während des gesamten Zyklus seit dem Erwerb überprüft werden (also vom Kauf über die Aufbewahrung und Übermittlung bis hin zur Verwendung).

### <a name="software-acquisition"></a>Erwerb der Software

Die Quelle der Software sollte über eine der folgenden Methoden überprüft werden:

- Software wird auf einem physischen Medium erworben, das vom Hersteller oder einer seriösen Quelle stammt (üblicherweise werden diese Medien von einem Anbieter ausgeliefert).
- Software wird aus dem Internet bezogen und mit Dateihashes überprüft, die vom Anbieter bereitgestellt werden.
- Software wird aus dem Internet bezogen und durch den Download und Vergleich von zwei unabhängigen Kopien überprüft:
   - Laden Sie die beiden Kopien auf zwei Hosts ohne Sicherheitsbeziehung herunter (die sich nicht innerhalb derselben Domäne befinden und nicht über dieselben Tools verwaltet werden), vorzugsweise über getrennte Internetverbindungen.
   - Vergleichen Sie die heruntergeladenen Dateien mithilfe eines Hilfsprogramms wie certutil: `certutil -hashfile <filename>`

Wenn möglich, sollte Anwendungssoftware wie Anwendungsinstallationsprogramme und -tools immer digital signiert und unter Verwendung von Windows Authenticode überprüft werden. Verwenden Sie dabei das Tool [Windows Sysinternals](https://www.microsoft.com/sysinternals), *sigcheck.exe*, mit Sperrüberprüfung. Möglicherweise sind auch Softwareprogramme erforderlich, bei denen der Anbieter diese Art von digitaler Signatur nicht bereitstellt.

### <a name="software-storage-and-transfer"></a>Speicherung und Übertragung von Software

Nach dem Kauf der Software sollte die Software an einem Speicherort gespeichert werden, der nicht bearbeitet oder geändert werden kann. Dies gilt insbesondere für mit dem Internet verbundene Hosts oder Mitarbeiter, deren Vertrauensebene niedriger ist als die der Systeme, auf denen die Software oder das Betriebssystem installiert wird. Bei diesem Speicher kann es sich um physische Medien oder einen sicheren elektronischen Speicherort handeln.

### <a name="software-usage"></a>Verwendung der Software

Die Software sollte idealerweise überprüft werden, wenn sie verwendet wird, also bei der manuellen Installation, beim Verpacken für ein Konfigurationsverwaltungstool oder beim Import in ein Konfigurationsverwaltungstool.

## <a name="clean-source-for-architecture-and-design"></a>Vertrauenswürdige Quelle für Architektur und Entwurf

Um das Prinzip der vertrauenswürdigen Quelle auf die Systemarchitektur anzuwenden, müssen Sie sicherstellen, dass das System nicht von Systemen mit niedrigerer Vertrauensebene abhängt. Ein System kann von einem System mit höherer Vertrauensebene abhängen, jedoch nicht von einem System mit niedrigerer Vertrauensebene und niedrigeren Sicherheitsstandards.

Beispiel: Active Directory kann einen standardmäßigen Benutzerdesktop steuern, wenn ein standardmäßiger Benutzerdesktop jedoch eine Active Directory-Implementierung steuern würde, wäre dies eine erhebliche Ausweitung von Berechtigungen, die ein erhöhtes Risiko nach sich ziehen würde.

![Diagramm, das zeigt, dass ein System von einem System mit höherer Vertrauensebene abhängen kann, jedoch nicht von einem System mit niedrigerer Vertrauensebene und niedrigeren Sicherheitsstandards](../media/securing-privileged-access-reference-material/PAW_RM_Fig09.JPG)

Die Kontrollbeziehung kann über verschiedene Methoden definiert werden, u. a. über Zugriffssteuerungslisten für Objekte wie Dateisysteme, über die Mitgliedschaft in der lokalen Administratorengruppe eines Computers oder über Agents, die auf einem als System ausgeführten Computer installiert werden (mit der Möglichkeit, beliebigen Code und beliebige Skripts auszuführen).

Ein häufig übersehenes Beispiel ist die Offenlegung von Informationen bei der Anmeldung. In diesem Fall entsteht eine Kontrollbeziehung, indem die Administratoranmeldeinformationen eines Systems für ein anderes System offengelegt werden. Aus diesem Grund sind Angriffe zum Diebstahl von Anmeldeinformationen (z. B. Pass-the-Hash) so gefährlich. Wenn ein Administrator sich mit Anmeldeinformationen der Ebene 0 bei einem standardmäßigen Benutzerdesktop anmeldet, werden diese Anmeldeinformationen für den Desktop offengelegt und können damit von AD kontrolliert und gesteuert werden. Die Berechtigungen können also auf AD ausgeweitet werden. Weitere Informationen zu diesen Angriffen finden Sie auf [dieser Seite](https://technet.microsoft.com/security/dn785092).

Aufgrund der großen Anzahl von Assets, die von Identitätssystemen wie Active Directory abhängen, sollten Sie die Anzahl von Systemen minimieren, von denen Ihre Active Directory-Bereitstellung und Ihre Domänencontroller abhängen.

![Diagramm, das zeigt, dass Sie die Anzahl der Systeme minimieren sollten, von denen Ihre Active Directory und Domänencontroller abhängig sind](../media/securing-privileged-access-reference-material/PAW_RM_Fig010.JPG)

Weitere Informationen zum Minimieren der wichtigsten Risiken im Zusammenhang mit Active Directory finden Sie auf [dieser Seite](https://aka.ms/hardenAD).

## <a name="operational-standards-based-on-clean-source-principle"></a>Prinzip der vertrauenswürdigen Quelle für betriebliche Standards

In diesem Abschnitt werden die betrieblichen Standards und Erwartungen für Mitarbeiter mit administrativen Berechtigungen beschrieben. Mithilfe dieser Standards soll die administrative Steuerung der IT-Systeme einer Organisation gegen Risiken geschützt werden, die durch betriebliche Verfahren und Prozesse entstehen könnten.

![Diagramm, das zeigt, dass mithilfe dieser Standards die administrative Steuerung der IT-Systeme einer Organisation gegen Risiken geschützt werden soll, die durch betriebliche Verfahren und Prozesse entstehen könnten](../media/securing-privileged-access-reference-material/PAW_RM_Fig11.JPG)

### <a name="integrating-the-standards"></a>Integrieren der Standards

Sie können diese Standards in die allgemeinen Standards und Verfahren Ihrer Organisation integrieren. Dabei können die Standards an die spezifischen Anforderungen, die verfügbaren Tools und die Risikobereitschaft Ihrer Organisation angepasst werden. Um Risiken zu minimieren, sollten diese Standards jedoch so wenig wie möglich geändert werden. Es wird empfohlen, die Standards in diesem Leitfaden als Benchmark für Ihren idealen Endzustand zu verwenden und Deltas als Ausnahmen zu verwalten, die nach Priorität behandelt werden.

Der Leitfaden zu Standards gliedert sich in die folgenden drei Abschnitte:

- Annahmen
- Change Advisory Board
- Betriebsmethoden
   - Zusammenfassung
   - Standards im Detail

### <a name="assumptions"></a>Annahmen

Bei den Standards in diesem Abschnitt wird davon ausgegangen, dass die Organisation über folgende Merkmale verfügt:

- Die meisten oder alle Server und Arbeitsstationen sind Teil der Active Directory-Implementierung.
- Auf allen zu verwaltenden Servern wird Windows Server 2008 R2 oder eine höhere Version ausgeführt, und der RDP-Modus RestrictedAdmin ist aktiviert.
- Auf allen zu verwaltenden Arbeitsstationen wird Windows 7 oder eine höhere Version ausgeführt, und der RDP-Modus RestrictedAdmin ist aktiviert.

   > [!NOTE]
   > Informationen zum Aktivieren des RDP-Modus RestrictedAdmin finden Sie auf [dieser Seite](https://aka.ms/RDPRA).

- Smartcards sind verfügbar und werden für alle Administratorkonten bereitgestellt.
- Für jede Domäne wurde *Builtin\Administrator* als Konto für den Notfallzugriff festgelegt.
- Es wurde eine Lösung zur Verwaltung von Unternehmensidentitäten bereitgestellt.
- Zur Verwaltung des Kennworts des lokalen Administratorkontos wurde [LAPS](https://aka.ms/laps) für Server und Arbeitsstationen bereitgestellt.
- Es wurde eine Privileged Access Management-Lösung wie Microsoft Identity Manager bereitgestellt, oder die Einführung einer solchen Lösung ist geplant.
- Es wurden Mitarbeiter zugewiesen, um Sicherheitshinweise zu überwachen und auf diese zu reagieren.
- Es ist technisch möglich, in kürzester Zeit Microsoft-Sicherheitsupdates anzuwenden.
- Es werden keine Baseboard-Verwaltungscontroller auf Servern verwendet, oder die Sicherheitsmaßnahmen werden strikt eingehalten.
- Administratorkonten und -gruppen für Server (Administratoren der Ebene 1) und Arbeitsstationen (Administratoren der Ebene 2) werden von Domänenadministratoren (Ebene 0) verwaltet.
- Änderungen an Active Directory werden von einem Change Advisory Board (CAB) oder einer anderen benannten Stelle genehmigt.

### <a name="change-advisory-board"></a>Change Advisory Board

Ein Change Advisory Board (CAB) ist das Diskussionsforum oder die Genehmigungsstelle für Änderungen, die sich auf das Sicherheitsprofil der Organisation auswirken können. Ausnahmen bezüglich dieser Standards sollten mit einer Risikobewertung und Begründung an das CAB übermittelt werden.

Die einzelnen Standards in diesem Dokument sind danach untergliedert, wie wichtig die Einhaltung des jeweiligen Standards für eine bestimmte Ebene ist.

![Diagramm des Standards für angegebenen Ebenen](../media/securing-privileged-access-reference-material/PAW_RM_Fig12.JPG)

Alle Ausnahmen für erforderliche Elemente (in diesem Dokument mit einem roten Achteck oder orangefarbenen Dreieck gekennzeichnet) werden als vorübergehend betrachtet und müssen vom CAB genehmigt werden. Die Richtlinien umfassen:

- Die Begründung und das Risiko der ersten Anforderung müssen vom unmittelbaren Vorgesetzten des Mitarbeiters abgezeichnet werden. Die Anforderung läuft nach sechs Monaten ab.
- Bei einer Erneuerung der Anforderung müssen die Begründung und das Risiko vom Leiter der Unternehmenseinheit abgezeichnet werden. Auch hier gilt ein Ablaufzeitraum von sechs Monaten.

Alle Ausnahmen für empfohlene Elemente (in diesem Dokument mit einem gelben Kreis gekennzeichnet) werden als vorübergehend betrachtet und müssen vom CAB genehmigt werden. Die Richtlinien umfassen:

- Die Begründung und das Risiko der ersten Anforderung müssen vom unmittelbaren Vorgesetzten des Mitarbeiters abgezeichnet werden. Die Anforderung läuft nach 12 Monaten ab.
- Bei einer Erneuerung der Anforderung müssen die Begründung und das Risiko vom Leiter der Unternehmenseinheit abgezeichnet werden. Auch hier gilt ein Ablaufzeitraum von 12 Monaten.

### <a name="operational-practices-standards-summary"></a>Zusammenfassung der Standards für Betriebsmethoden

Die Spalten für die Ebenen in dieser Tabelle beziehen sich auf die Ebene des Administratorkontos, dessen Kontroll- und Steuerungsvorgänge sich üblicherweise auf alle Assets dieser Ebene auswirken.

![Die Tabelle zeigt die Ebene des Administratorkontos](../media/securing-privileged-access-reference-material/PAW_RM_Fig13.JPG)

Entscheidungen bezüglich der Betriebsvorgänge, die regelmäßig getroffen werden, sind entscheidend, um den Sicherheitsstatus der Umgebung aufrechtzuerhalten. Diese Standards für Prozesse und Verfahren tragen dazu bei, dass betriebliche Fehler nicht zu einem Sicherheitsrisiko bei den Betriebsvorgängen innerhalb der Umgebung führen, das von einem Angreifer ausgenutzt werden kann.

#### <a name="administrator-enablement-and-accountability"></a>Befähigung und Verantwortlichkeit von Administratoren

Administratoren müssen für eine maximale Sicherheit innerhalb der Umgebung geschult und für ihre Handlungen verantwortlich sein.

##### <a name="administrative-personnel-standards"></a>Standards für Mitarbeiter mit administrativen Berechtigungen

Mitarbeiter mit administrativen Aufgaben müssen überprüft werden, um sicherzustellen, dass sie vertrauenswürdig sind und die Administratorrechte benötigen:

- Führen Sie eine Hintergrundüberprüfung für Mitarbeiter durch, bevor Sie Administratorrechte zuweisen.
- Überprüfen Sie die Administratorrechte einmal pro Quartal, um zu überprüfen, welche Mitarbeiter weiterhin Administratorzugriff benötigen.

##### <a name="administrative-security-briefing-and-accountability"></a>Einweisung und Verantwortlichkeit für administrative Sicherheit

Administratoren müssen über die Risiken der Organisation sowie ihre Rolle beim Umgang mit diesen Risiken informiert und für ihre Handlungen verantwortlich sein. Administratoren sollten jährlich in den folgenden Bereichen geschult werden:

- Allgemeine Bedrohungslandschaft
   - Bestimmte Angreifer
   - Angriffstechniken, einschließlich Pass-the-Hash und Diebstahl von Anmeldeinformationen
- Organisationsspezifische Bedrohungen und Incidents
- Die Rolle des Administrators beim Schutz gegen Angriffe
   - Verwalten der Offenlegung von Anmeldeinformationen mit dem Ebenenmodell
   - Verwenden von administrativen Arbeitsstationen
   - Verwenden des RDP-Modus RestrictedAdmin
- Organisationsspezifische administrative Verfahren
   - Überprüfen aller betrieblichen Richtlinien in diesem Standard
   - Befolgen Sie die folgenden wichtigen Regeln:
      - Verwenden Sie Administratorkonten ausschließlich auf administrativen Arbeitsstationen
      - Deaktivieren oder entfernen Sie keinesfalls Sicherheitskontrollen Ihrer Konten oder Arbeitsstationen (z. B. Anmeldeeinschränkungen oder Attribute, die für Smartcards erforderlich sind)
      - Melden Sie Probleme oder ungewöhnliche Aktivität

Um eine eindeutige Verantwortlichkeit sicherzustellen, sollten alle Mitarbeiter mit Administratorkonten ein Dokument mit Verhaltensregeln für Administratorrechte unterzeichnen, das besagt, dass die Mitarbeiter ihre Aufgaben in Übereinstimmung mit organisationsspezifischen Administratorichtlinien ausführen.

##### <a name="provisioning-and-deprovisioning-processes-for-administrative-accounts"></a>Verfahren zum Bereitstellen und Aufheben der Bereitstellung für Administratorkonten

Die folgenden Standards müssen eingehalten werden, um Lebenszyklusanforderungen einzuhalten.

- Alle Administratorkonten müssen von der in der folgenden Tabelle aufgeführten genehmigenden Stelle genehmigt werden.
   - Die Genehmigung darf nur erteilt werden, wenn geschäftliche Gründe dafür vorliegen, dass einem Mitarbeiter Administratorrechte zugewiesen werden.
   - Die Genehmigung für Administratorrechte darf für maximal sechs Monate erteilt werden.
- In den folgenden Fällen müssen die Administratorrechte umgehend entfernt werden:
   - Mitarbeiter übernehmen eine neue Position.
   - Mitarbeiter verlassen die Organisation.
- Wenn Mitarbeiter die Organisation verlassen, müssen die Konten umgehend deaktiviert werden.
- Deaktivierte Konten müssen innerhalb von sechs Monaten gelöscht werden, und der Nachweis über den Löschvorgang muss in den Daten des Change Approval Boards erfasst werden.
- Überprüfen Sie einmal pro Monat die Mitgliedschaft aller privilegierten Konten, um sicherzustellen, dass nicht autorisierten Benutzern keine Berechtigungen erteilt wurden. Stattdessen kann ein automatisiertes Tool eingesetzt werden, dass bei Änderungen eine Benachrichtigung sendet.

|Ebene der Kontoberechtigung|Genehmigende Stelle|Häufigkeit der Überprüfung von Mitgliedschaften|
|--------------|------------|----------------|
|Administrator der Ebene 0|Change Approval Board|Monatlich oder automatisiert|
|Administrator der Ebene 1|Administratoren der Ebene 0 oder Sicherheit|Monatlich oder automatisiert|
|Administrator der Ebene 2|Administratoren der Ebene 0 oder Sicherheit|Monatlich oder automatisiert|

#### <a name="operationalize-least-privilege"></a>Operationalisieren der geringsten Rechte

Mit diesen Standards werden die jeweils geringsten Rechte implementiert, sodass die Anzahl von Administratoren sowie die Zeitdauer reduziert wird, während der die Administratoren über die Rechte verfügen.

> [!NOTE]
> Um in Ihrer Organisation die jeweils geringsten Rechte zuzuweisen, müssen Sie mit Organisationsrollen, ihren Anforderungen und den Entwurfsmechanismen vertraut sein, um sicherzustellen, dass die Aufgaben dieser Rollen mit den jeweils geringsten Rechten ausgeführt werden. Um in einem administrativen Modell die jeweils geringsten Rechte zu nutzen, sind häufig mehrere Ansätze erforderlich:
>
> - Beschränken Sie die Anzahl von Administratoren oder Mitgliedern privilegierter Gruppen
> - Delegieren Sie weniger Berechtigungen an Konten
> - Stellen Sie nach Bedarf zeitgebundene Berechtigungen bereit
> - Ermöglichen Sie anderen Mitarbeitern das Ausführen von Aufgaben (Concierge-Ansatz)
> - Implementieren Sie Prozesse für den Notfallzugriff und seltene Szenarien

##### <a name="limit-count-of-administrators"></a>Einschränken der Anzahl von Administratoren

Um Geschäftskontinuität sicherzustellen, sollten jeder Administratorrolle mindestens zwei Mitarbeiter zugewiesen werden.

Wenn einer Rolle mehr als zwei Mitarbeiter zugewiesen werden, muss das Change Approval Board die spezifischen Gründe für das Zuweisen von Rechten zu den einzelnen Mitgliedern (einschließlich der zwei ursprünglichen Mitarbeiter) genehmigen. Die Gründe für die Genehmigung müssen Folgendes umfassen:

- Die technischen Aufgaben, die von den Administratoren ausgeführt werden und für die die Administratorrechte erforderlich sind
- Die Häufigkeit, mit der die Aufgaben ausgeführt werden
- Besondere Gründe, weshalb die Aufgaben nicht von einem anderen Administrator im Namen der Benutzer ausgeführt werden können
- Dokumentation aller bekannten Alternativen, um das Recht zu erteilen, sowie eine Erklärung, weshalb diese Alternativen nicht umsetzbar sind

##### <a name="dynamically-assign-privileges"></a>Dynamisches Zuweisen von Berechtigungen

Administratoren müssen Berechtigungen rechtzeitig („Just-In-Time“) erhalten, um ihre Aufgaben auszuführen. Berechtigungen werden Administratorkonten nie dauerhaft zugewiesen.

> [!NOTE]
> Mit dauerhaft zugewiesenen Administratorrechten wird eine Strategie der höchsten Rechte verfolgt, da administrative Mitarbeiter einen schnellen Zugriff auf Berechtigungen benötigen, um bei Problemen einen unterbrechungsfreien Betrieb sicherzustellen. Just-in-Time-Berechtigungen ermöglichen Folgendes:
>
> - Granulare Zuweisung von Berechtigungen, um dem Ansatz der geringsten Rechte näher zu kommen
> - Geringere Dauer der Offenlegung von Rechten
> - Nachverfolgen der Verwendung von Berechtigungen, um einen Missbrauch oder Angriffe zu ermitteln

#### <a name="manage-risk-of-credential-exposure"></a>Mindern des Risikos einer Offenlegung von Anmeldeinformationen

Wirken Sie dem Risiko einer Offenlegung von Anmeldeinformationen mithilfe der folgenden Maßnahmen entgegen.

##### <a name="separate-administrative-accounts"></a>Trennen von Administratorkonten

Alle Mitarbeiter, die über Administratorrechte verfügen dürfen, müssen über separate Konten für administrative Funktionen verfügen, die nicht mit ihren Benutzerkonten identisch sind.

- **Standardbenutzerkonten**: Erteilen Sie Standardbenutzerrechte für standardmäßige Benutzeraufgaben, z. B. für E-Mail-, Webbrowsing- und Branchenanwendungen. Diesen Konten sollten keine Administratorrechte erteilt werden.
- **Administratorkonten**: Separate Konten für Mitarbeiter, denen die entsprechenden Administratorrechte zugewiesen werden. Ein Administrator, der Assets auf allen Ebenen verwalten muss, sollte über ein separates Konto für jede Ebene verfügen. Diese Konten sollten nicht über Zugriff auf E-Mails oder das öffentliche Internet verfügen.

##### <a name="administrator-logon-practices"></a>Verfahren für die Administratoranmeldung

Bevor ein Administrator sich interaktiv bei einem Host anmelden kann (lokal über Standard-RDP, unter Verwendung von RunAs oder über die Virtualisierungskonsole), muss der Host mindestens den Standard für die Ebene des Administratorkontos (oder einer höheren Ebene) erfüllen.

Administratoren können sich nur mit ihren Administratorkonten bei Administratorarbeitsstationen anmelden. Administratoren können sich nur bei Verwendung der genehmigten Supporttechnologie (siehe nächster Abschnitt) bei verwalteten Ressourcen anmelden.

> [!NOTE]
> Der Grund für diese Anforderung ist, dass beim Anmelden an einem Host interaktiv Kontrolle über die Anmeldeinformationen für diesen Host gewährt wird.
>
> Einzelheiten zu Anmeldetypen, zu gängigen Verwaltungstools und zur Offenlegung von Anmeldeinformationen finden Sie unter [Verwaltungstools und Anmeldeinformationen](https://aka.ms/admintoolsecurity).

##### <a name="use-of-approved-support-technology-and-methods"></a>Verwenden genehmigter Supporttechnologien und -methoden

Administratoren, die Support für Remotesysteme und -benutzer bieten, müssen die folgenden Richtlinien befolgen, um zu verhindern, dass ein Angreifer, der die Kontrolle über den Remotecomputer hat, die Anmeldeinformationen des Administrators stiehlt.

- Sofern verfügbar, sollten die primären Supportoptionen verwendet werden.
- Die sekundären Supportoptionen sollten nur verwendet werden, wenn die primäre Supportoption nicht verfügbar ist.
- Nicht zulässige Supportmethoden dürfen niemals verwendet werden.
- Über ein Administratorkonto darf zu keinem Zeitpunkt das Internet durchsucht oder auf E-Mails zugegriffen werden.

###### <a name="tier-0-forest-domain-and-dc-administration"></a>Verwalten von Gesamtstrukturen, Domänen und Domänencontrollern der Ebene 0

Stellen Sie sicher, dass für dieses Szenario die folgenden Verfahren verwendet werden:

- **Remoteserversupport**: Beim Remotezugriff auf einen Server müssen Administratoren der Ebene 0 die folgenden Richtlinien befolgen:
  - **Primär (Tool)** : Remotetools, die Netzwerkanmeldungen verwenden (Typ 3). Weitere Informationen finden Sie unter [Verwaltungstools und Anmeldetypen](https://aka.ms/admintoolsecurity).
  - **Primär (interaktiv)** : Verwenden Sie den RDP-Modus RestrictedAdmin oder eine RDP-Standardsitzung auf einer Administratorarbeitsstation mit Domänenkonto

    > [!NOTE]
    > Wenn Sie über eine Rechteverwaltungslösung der Ebene 0 verfügen, fügen Sie Folgendes hinzu: Verwendung von Just-in-Time-Berechtigungen von einer Privileged Access Management-Lösung.

- **Physischer Serversupport**: Bei physischer Präsenz an einer Server- oder VM-Konsole (Hyper-V oder VMware Tools) gelten für diese Konten keine bestimmten Einschränkungen bezüglich der Nutzung von Verwaltungstools. Es gelten lediglich die allgemeinen Einschränkungen für standardmäßige Benutzeraufgaben wie der Zugriff auf E-Mails und das Durchsuchen des Internets.

   > [!NOTE]
   > Die Verwaltung der Ebene 0 unterscheidet sich von der Verwaltung der anderen Ebenen, da alle Assets der Ebene 0 bereits über direkte oder indirekte Kontrolle aller Assets verfügen. Beispiel: Ein Angreifer, der die Kontrolle über einen Domänencontroller hat, muss keine Anmeldeinformationen von angemeldeten Administratoren stehlen, da er bereits auf alle Domänenanmeldeinformationen in der Datenbank zugreifen kann.

###### <a name="tier-1-server-and-enterprise-application-support"></a>Support für Server und Unternehmensanwendungen der Ebene 1

Stellen Sie sicher, dass für dieses Szenario die folgenden Verfahren verwendet werden:

- **Remoteserversupport**: Beim Remotezugriff auf einen Server müssen Administratoren der Ebene 1 die folgenden Richtlinien befolgen:
   - **Primär (Tool)** : Remotetools, die Netzwerkanmeldungen verwenden (Typ 3). Weitere Informationen finden Sie auf Seite 42-47 unter [Mitigating Pass-the-Hash and Other Credential Theft](https://www.microsoft.com/pth) v1 (Verhindern von Pass-the-Hash-Angriffen und anderen Angriffen zum Diebstahl von Anmeldeinformationen).
   - **Primär (interaktiv)** : Verwenden Sie den RDP-Modus RestrictedAdmin auf einer Administratorarbeitsstation mit Domänenkonto, das Just-in-Time-Berechtigungen von einer Privileged Access Management-Lösung erhalten hat.
   - **Sekundär**: Melden Sie sich unter Verwendung eines lokalen Kontokennworts beim Server an, das von LAPS auf einer Administratorarbeitsstation festgelegt wird.
   - **Nicht zulässig**: Standard-RDP darf nicht mit einem Domänenkonto verwendet werden.
   - **Nicht zulässig**: Verwenden der Anmeldeinformationen des Domänenkontos während der Sitzung (z. B. die Verwendung von *RunAs* oder die Authentifizierung gegenüber einer Freigabe). Dabei besteht das Risiko eines Diebstahls der Anmeldeinformationen.
- **Physischer Serversupport**: Bei physischer Präsenz an einer Server- oder VM-Konsole (Hyper-V oder VMware Tools) müssen Administratoren der Ebene 1 das lokale Kontokennwort vor dem Zugriff auf den Server von LAPS abrufen.
   - **Primär**: Rufen Sie das von LAPS festgelegte lokale Kontokennwort von einer Administratorarbeitsstation ab, bevor Sie sich beim Server anmelden.
   - **Nicht zulässig**: Die Anmeldung über ein Domänenkonto ist in diesem Szenario nicht zulässig.
   - **Nicht zulässig**: Verwenden der Anmeldeinformationen des Domänenkontos während der Sitzung (z. B. die Verwendung von RunAs oder die Authentifizierung gegenüber einer Freigabe). Dabei besteht das Risiko eines Diebstahls der Anmeldeinformationen.

###### <a name="tier-2-help-desk-and-user-support"></a>Helpdesk- und Benutzersupport der Ebene 2

Helpdesk- und Benutzersupportorganisationen bieten Support für Endbenutzer (keine Administratorrechte erforderlich) und die Arbeitsstationen der Benutzer (Administratorrechte erforderlich).

**Benutzersupport**: Unterstützung der Benutzer beim Durchführen von Aufgaben, bei denen keine Änderungen an der Arbeitsstation erforderlich sind. Häufig wird den Benutzern dabei gezeigt, wie sie ein Anwendungs- oder Betriebssystemfeature verwenden.

- **Deskseitiger Benutzersupport**: Supportmitarbeiter der Ebene 2 sind physisch am Arbeitsplatz des Benutzers präsent.
   - **Primär**: Für Support, der vor Ort „über die Schulter“ bereitgestellt wird, sind möglicherweise keine Tools erforderlich.
   - **Nicht zulässig**: Die Anmeldung über die Administratoranmeldeinformationen eines Domänenkontos ist in diesem Szenario nicht zulässig. Wenn Administratorrechte erforderlich sind, wählen Sie den deskseitigen Support für Arbeitsstationen.
- **Remotebenutzersupport**: Supportmitarbeiter der Ebene 2 unterstützen den Benutzer von einem Remotestandort aus.
   - **Primär**: Remoteunterstützung, Skype for Business oder ähnliche Tools zur Freigabe des Benutzerbildschirms können verwendet werden. Weitere Informationen finden Sie unter [What is Windows Remote Assistance?](https://windows.microsoft.com/windows/what-is-windows-remote-assistance) (Was ist die Windows-Remoteunterstützung?)
   - **Nicht zulässig**: Die Anmeldung über die Administratoranmeldeinformationen eines Domänenkontos ist in diesem Szenario nicht zulässig. Wenn Administratorrechte erforderlich sind, wählen Sie den Support für Arbeitsstationen.
- **Support für Arbeitsstationen**: Die Aufgaben umfassen die Wartung von Arbeitsstationen oder eine Problembehandlung, für die Zugriff auf ein System erforderlich ist, um Protokolle anzuzeigen, Software zu installieren, Treiber zu aktualisieren usw.
   - **Deskseitiger Support für Arbeitsstationen**: Supportmitarbeiter der Ebene 2 sind physisch an der Arbeitsstation des Benutzers präsent.
      - **Primär**: Rufen Sie das von LAPS festgelegte lokale Kontokennwort von einer Administratorarbeitsstation ab, bevor Sie eine Verbindung mit der Arbeitsstation eines Benutzers herstellen.
      - **Nicht zulässig**: Die Anmeldung über die Administratoranmeldeinformationen eines Domänenkontos ist in diesem Szenario nicht zulässig.
   - **Remotesupport für Arbeitsstationen**: Supportmitarbeiter der Ebene 2 unterstützen den Benutzer von einem Remotestandort aus.
      - **Primär**: Verwenden Sie den RDP-Modus RestrictedAdmin auf einer Administratorarbeitsstation mit Domänenkonto, das Just-in-Time-Berechtigungen von einer Privileged Access Management-Lösung erhalten hat.
      - **Sekundär**: Rufen Sie ein von LAPS festgelegtes lokales Kontokennwort von einer Administratorarbeitsstation ab, bevor Sie eine Verbindung mit der Arbeitsstation eines Benutzers herstellen.
      - **Nicht zulässig**: Verwenden von Standard-RDP mit einem Domänenkonto.

###### <a name="no-browsing-the-public-internet-with-admin-accounts-or-from-admin-workstations"></a>Kein Browsen im öffentlichen Internet über Administratorkonten oder auf Administratorarbeitsstationen

Administrative Mitarbeiter dürfen nicht im öffentlichen Internet browsen, während sie mit einem Administratorkonto oder bei einer Administratorarbeitsstation angemeldet sind. Die einzige genehmigte Ausnahme ist die Verwendung eines Webbrowsers zum Verwalten eines cloudbasierten Diensts.

###### <a name="no-accessing-email-with-admin-accounts-or-from-admin-workstations"></a>Kein Zugriff auf E-Mails über Administratorkonten oder auf Administratorarbeitsstationen

Administrative Mitarbeiter dürfen nicht auf E-Mails zugreifen, während sie mit einem Administratorkonto oder bei einer Administratorarbeitsstation angemeldet sind.

###### <a name="store-service-and-application-account-passwords-in-a-secure-location"></a>Speichern von Kennwörtern für Dienst- oder Anwendungskonten an einem sicheren Speicherort

Die folgenden Richtlinien sollten für die physischen Sicherheitsverfahren befolgt werden, mit denen der Zugriff auf das Kennwort gesteuert wird:

- Bewahren Sie Kennwörter für Dienstkonten in einem Safe auf.
- Stellen Sie sicher, dass nur Mitarbeiter, die mindestens über die Vertrauensebene der Kontoebene verfügen, auf das Kontokennwort zugreifen können.
- Für nachvollziehbare Verantwortlichkeiten schränken Sie die Anzahl von Benutzern, die auf die Kennwörter zugreifen, auf ein Minimum ein.
- Stellen Sie sicher, dass jeder Zugriff auf das Kennwort von einer unbeteiligten Partei (z. B. ein Vorgesetzter, der nicht im Bereich der IT-Administration geschult wurde) protokolliert, nachverfolgt und überwacht wird.

##### <a name="strong-authentication"></a>Strenge Authentifizierung

Nutzen Sie die folgenden Verfahren für eine ordnungsgemäße Konfiguration der strengen Authentifizierung.

###### <a name="enforce-smartcard-multi-factor-authentication-mfa-for-all-admin-accounts"></a>Erzwingen Sie die mehrstufige Smartcard-Authentifizierung für alle Administratorkonten

Administratorkonten dürfen keine Kennwörter für die Authentifizierung verwenden. Die einzigen autorisierten Ausnahmen sind die Konten für den Notfallzugriff, die über die geeigneten Prozesse geschützt werden.

Verknüpfen Sie alle Administratorkonten mit einer Smartcard, und aktivieren Sie das Attribut **Benutzer muss sich mit einer Smartcard anmelden**.

Implementieren Sie ein Skript, um den zufälligen Kennworthashwert automatisch und regelmäßig zurückzusetzen. Dazu muss das Attribut **Benutzer muss sich mit einer Smartcard anmelden** deaktiviert und umgehend erneut aktiviert werden.

Lassen Sie mit Ausnahme der Konten für den Notfallzugriff keine weiteren Ausnahmen für Konten zu, die von Mitarbeitern verwendet werden.

###### <a name="enforce-multi-factor-authentication-for-all-cloud-admin-accounts"></a>Erzwingen der mehrstufigen Authentifizierung für alle Cloudadministratorkonten

Alle Konten mit Administratorrechten in einem Clouddienst (z. B. Microsoft Azure und Office 365) müssen die mehrstufige Authentifizierung verwenden.

##### <a name="rare-use-emergency-procedures"></a>Selten erforderliche Notfallmaßnahmen

Bei Betriebsmethoden müssen die folgenden Standards eingehalten werden:

- Stellen Sie sicher, dass Ausfälle schnell behoben werden können.
- Stellen Sie sicher, dass seltene Aufgaben, für die hohe Rechte erforderlich sind, abgeschlossen werden können.
- Stellen Sie sicher, dass sichere Verfahren verwendet werden, um die Anmeldeinformationen und Berechtigungen zu schützen.
- Stellen Sie sicher, dass geeignete Verfahren für Nachverfolgung und Genehmigung implementiert sind.

###### <a name="correctly-follow-appropriate-processes-for-all-emergency-access-accounts"></a>Ordnungsgemäße Implementierung der geeigneten Verfahren für alle Notfallzugriffskonten

Stellen Sie sicher, dass für jedes Notfallzugriffskonto ein Dokument zur Nachverfolgung im Safe hinterlegt ist.

Das in diesem Dokument aufgezeichnete Verfahren sollte für sämtliche Konten befolgt werden. Beispielsweise sollte das Kennwort nach jeder Verwendung und Abmeldung bei Arbeitsstationen oder Servern geändert werden.

Die Verwendung von Konten für den Notfallzugriff sollte immer vorab vom Change Approval Board genehmigt werden bzw. ggf. nachträglich als genehmigte Notfallverwendung.

###### <a name="restrict-and-monitor-usage-of-emergency-access-accounts"></a>Einschränken und Überwachen der Verwendung von Notfallzugriffskonten

Für jede Verwendung von Notfallzugriffskonten gilt Folgendes:

- Nur autorisierte Domänenadministratoren können auf die Notfallzugriffskonten mit Domänenadministratorberechtigungen zugreifen.
- Die Notfallzugriffskonten können nur auf Domänencontrollern und anderen Hosts der Ebene 0 verwendet werden.
- Dieses Konto sollte ausschließlich für folgende Zwecke verwendet werden:
  - Problembehandlung und Behebung technischer Probleme, die eine Verwendung der richtigen Administratorkonten verhindern.
  - Durchführen seltener Aufgaben, wie z. B.:
    - Schemaverwaltung
    - Aufgaben, die die Gesamtstruktur betreffen und Administratorrechte auf Unternehmensebene erfordern

      > [!NOTE]
      > Die Topologieverwaltung, einschließlich der Verwaltung von Active Directory-Standorten und -Subnetzen, wird delegiert, um die Nutzung dieser Rechte einzuschränken.

- Für jede Verwendung dieser Konten sollte eine schriftliche Genehmigung vom Leiter der Sicherheitsgruppe vorliegen
- Das im Dokument zur Nachverfolgung für jedes Notfallzugriffskonto festgelegte Verfahren sieht vor, dass das Kennwort nach jeder Verwendung geändert wird. Ein Mitglied des Sicherheitsteams sollte überprüfen, ob dieser Schritt ordnungsgemäß ausgeführt wurde.

###### <a name="temporarily-assign-enterprise-admin-and-schema-admin-membership"></a>Vorübergehendes Zuweisen der Mitgliedschaft als Unternehmens- oder Schemaadministrator

Die Berechtigungen sollten nach Bedarf hinzugefügt und nach der Verwendung entfernt werden. Diese Berechtigungen sollten Notfallzugriffskonten nur solange zugewiesen werden, bis die Aufgabe abgeschlossen ist. Die maximale Zeitdauer sollte 10 Stunden betragen. Die gesamte Verwendung dieser Berechtigungen sowie die Dauer sollten nach Abschluss der Aufgabe in den Aufzeichnungen des Change Approval Boards erfasst werden.

## <a name="esae-administrative-forest-design-approach"></a>ESAE-basierter Ansatz für den Entwurf einer administrativen Gesamtstruktur

In diesem Abschnitt wird ein Ansatz für den Entwurf einer administrativen Gesamtstruktur beschrieben, die auf der ESAE-Referenzarchitektur (Enhanced Security Administrative Environment) basiert. Diese wird von Microsoft-Dienstleistungsteams für Internetsicherheit bereitgestellt, um Kunden vor Angriffen im Internet zu schützen.

Mit einer dedizierten administrativen Gesamtstruktur sind Organisationen in der Lage, Administratorkonten, Arbeitsstationen und Gruppen zu hosten. Dabei weist die Umgebung stärkere Sicherheitskontrollen auf als die Produktionsumgebung.

Diese Architektur ermöglicht eine Reihe von Sicherheitskontrollen, die in einer Architektur mit einer einzelnen Gesamtstruktur nicht möglich oder nicht einfach zu konfigurieren sind. Dies gilt sogar für Gesamtstrukturen, die über Arbeitsstationen mit privilegiertem Zugriff verwaltet werden. Dieser Ansatz ermöglicht die Bereitstellung von Konten als Standardbenutzer ohne erweiterte Berechtigungen in der administrativen Gesamtstruktur, die in der Produktionsumgebung über weitgehende Berechtigungen verfügen, und somit eine umfassende technische Erzwingung von Governance. Zudem ermöglicht diese Architektur die Verwendung der ausgewählten Authentifizierung von Vertrauensstellungen zum Einschränken von Anmeldungen (und Offenlegen der Anmeldeinformationen) auf autorisierte Hosts. In Situationen, in denen eine umfassendere Sicherung für die Produktionsgesamtstruktur ohne die Kosten und Komplexität einer vollständigen Wiederherstellung erwünscht ist, kann eine administrative Gesamtstruktur eine Umgebung bereitstellen, in der für das Produktionsumfeld eine höhere Sicherheitsstufe gilt.

Wenngleich bei diesem Ansatz eine Gesamtstruktur zu einer Active Directory-Umgebung hinzugefügt wird, sind die Kosten und die Komplexität aufgrund des festen Aufbaus, der geringen Hardware- und Softwareanforderungen und der geringen Anzahl von Benutzern gering.

> [!NOTE]
> Dieser Ansatz eignet sich gut für die Verwaltung von Active Directory, viele Anwendungen können jedoch nicht über Konten aus einer externen Gesamtstruktur verwaltet werden, die eine Standardvertrauensstellung verwendet.

Diese Abbildung zeigt eine ESAE-Gesamtstruktur, die zur Verwaltung von Assets der Ebene 0 verwendet wird, sowie eine PRIV-Gesamtstruktur, die für die Verwendung mit der Privileged Access Management-Funktion von Microsoft Identity Manager konfiguriert ist. Weitere Informationen zur Bereitstellung einer Instanz von MIM PAM finden Sie im Artikel [Privileged Identity Management für Active Directory Domain Services (AD DS)](https://technet.microsoft.com/library/mt150258.aspx).

![Diese Abbildung zeigt eine ESAE-Gesamtstruktur, die zur Verwaltung von Assets der Ebene 0 verwendet wird, sowie eine PRIV-Gesamtstruktur, die für die Verwendung mit der Privileged Access Management-Funktion von Microsoft Identity Manager konfiguriert ist](../media/securing-privileged-access-reference-material/PAW_RM_Fig14.JPG)

Eine dedizierte administrative Gesamtstruktur ist eine Active Directory-Standardgesamtstruktur mit einer einzelnen Domäne, die ausschließlich der Active Directory-Verwaltung dient. Aufgrund des begrenzten Einsatzgebiets können administrative Gesamtstrukturen und Domänen strikter abgesichert werden als Produktionsgesamtstrukturen.

Beim Entwurf einer administrativen Gesamtstruktur sollte Folgendes berücksichtigt werden:

- **Beschränkter Gültigkeitsbereich**: Der primäre Nutzen einer administrativen Gesamtstruktur liegt in der hohen Sicherheitsstufe und der verringerten Angriffsfläche, die zu einem geringeren Restrisiko führen. Die Gesamtstruktur kann für zusätzliche Verwaltungsfunktionen und -anwendungen verwendet werden, jede Erweiterung des Bereichs vergrößert jedoch die Angriffsfläche der Gesamtstruktur und ihrer Ressourcen. Das Ziel ist die Einschränkung der Funktionen der Gesamtstruktur und ihrer Administratorbenutzer, um die Angriffsfläche minimal zu halten, daher sollte jede Erweiterung des Bereichs sorgfältig durchdacht werden.
- **Konfiguration von Vertrauensstellungen**: Die Konfiguration von Vertrauensstellungen wird von verwalteten Gesamtstrukturen oder Domänen zur administrativen Gesamtstruktur verlagert.
   - Von der Produktionsumgebung zur administrativen Gesamtstruktur ist eine unidirektionale Vertrauensstellung erforderlich. Dabei kann es sich um eine Domänen- oder Gesamtstruktur-Vertrauensstellung handeln. Die administrative Gesamtstruktur muss den verwalteten Domänen/Gesamtstrukturen nicht vertrauen, um Active Directory verwalten zu können. Zusätzliche Anwendungen können jedoch eine bidirektionale Vertrauensstellung, Sicherheitsüberprüfungen und Tests erfordern.
   - Um Konten in der administrativen Gesamtstruktur auf die Protokollierung auf den richtigen Produktionshosts zu beschränken, sollte die ausgewählte Authentifizierung verwendet werden. Zur Verwaltung von Domänencontrollern und Delegierung von Rechten in Active Directory ist hierbei in der Regel die Berechtigung für die Anmeldung auf Domänencontrollern für die jeweiligen Administratorkonten der Ebene 0 in der administrativen Gesamtstruktur erforderlich. Weitere Informationen finden Sie unter „Konfigurieren der Einstellungen für ausgewählte Authentifizierung“.
- **Berechtigungen und Härten von Domänen**: Die administrative Gesamtstruktur sollte anhand der geringsten erforderlichen Rechte für die Active Directory-Verwaltung konfiguriert werden.
   - Zum Erteilen von Rechten für die Verwaltung von Domänencontrollern und Delegieren von Berechtigungen müssen der lokalen Gruppe der Domäne „BUILTIN\Administrators“ Administratorkonten für die Gesamtstruktur hinzugefügt werden. Der Grund dafür ist, dass die globale Gruppe „Domänen-Admins“ nicht über Mitglieder einer externen Domäne verfügen darf.
   - Gegen die Verwendung dieser Gruppe zum Erteilen von Rechten spricht, dass standardmäßig kein Administratorzugriff auf neue Gruppenrichtlinienobjekte zugewiesen wird. Diese Standardberechtigungen für Schemas können über die in [diesem Knowledge Base-Artikel](https://support.microsoft.com/kb/321476) beschriebenen Schritte geändert werden.
   - Konten in der administrativen Gesamtstruktur, die für die Verwaltung der Produktionsumgebung verwendet werden, sollten keine Administratorberechtigungen für die administrative Gesamtstruktur oder die enthaltenen Domänen oder Arbeitsstationen erhalten.
   - Administratorrechte für die administrative Gesamtstruktur sollten über ein Offlineverfahren streng kontrolliert werden, um das Löschen von Überwachungsprotokollen durch Angreifer oder böswillige Mitarbeiter zu erschweren. Dies trägt auch dazu bei, dass Mitarbeiter mit Administratorkonten für die Produktion die Einschränkungen ihrer Konten nicht lockern und damit das Risiko für die Organisation steigern können.
   - Die administrative Gesamtstruktur sollte die Microsoft Security Compliance Baseline-Konfigurationen für die Domäne befolgen und sichere Konfigurationen für Authentifizierungsprotokolle aufweisen.
   - Alle Hosts in der administrativen Gesamtstruktur sollten automatisch mit Sicherheitsupdates aktualisiert werden. Dies birgt zwar das Risiko einer Unterbrechung des Domänencontroller-Wartungsbetriebs, bietet jedoch eine erhebliche Verringerung von Sicherheitsrisiken durch nicht behobene Schwachstellen.

      > [!NOTE]
      > Eine dedizierte Windows Server Update Services-Instanz kann so konfiguriert werden, dass Updates automatisch genehmigt werden. Weitere Informationen finden Sie im Abschnitt „Automatisches Genehmigen der Installation von Updates“ des Dokuments „Genehmigen von Updates“.

- **Härten von Arbeitsstationen**: Erstellen Sie die Administratorarbeitsstationen unter Verwendung der [Arbeitsstationen mit privilegiertem Zugriff](../securing-privileged-access/privileged-access-workstations.md) (über Phase 3), ändern Sie die Domänenmitgliedschaft jedoch so, dass anstelle der Produktionsumgebung die administrative Gesamtstruktur verwendet wird.
- **Härten von Servern und Domänencontrollern**: Für alle Domänencontroller und Server in der administrativen Gesamtstruktur gilt Folgendes:
   - Stellen Sie sicher, dass alle Medien über die in [Vertrauenswürdige Quelle für Installationsmedien](https://aka.ms/cleansource) beschriebenen Verfahren überprüft wurden.
   - Stellen Sie sicher, dass auf den Servern innerhalb der administrativen Gesamtstruktur aktuelle Betriebssysteme installiert sind (selbst wenn dies in der Produktionsumgebung nicht möglich ist).
   - Hosts in der administrativen Gesamtstruktur sollten automatisch mit Sicherheitsupdates aktualisiert werden.

      > [!NOTE]
      > Windows Server Update Services können so konfiguriert werden, dass Updates automatisch genehmigt werden. Weitere Informationen finden Sie im Abschnitt „Automatisches Genehmigen der Installation von Updates“ des Dokuments „Genehmigen von Updates“.

   - Sicherheitsbaselines sollten als Ausgangskonfiguration verwendet werden.

      > [!NOTE]
      > Kunden können das Microsoft Security Compliance Toolkit (SCT) zum Konfigurieren von Baselines auf den administrativen Hosts verwenden.

   - Sicherer Start zur Abhilfe gegen Angreifer oder Schadsoftware, die versuchen, während des Startvorgangs nicht signierten Code zu laden.

      > [!NOTE]
      > Diese Funktion wurde in Windows 8 eingeführt, um UEFI (Unified Extensible Firmware Interface) zu nutzen.

   - Verschlüsselung ganzer Volumes zur Verringerung des Risikos durch den Verlust physischer Computer, z. B. administrativer Laptops, die an Remotestandorten eingesetzt werden.

      > [!NOTE]
      > Weitere Informationen finden Sie unter [BitLocker](https://technet.microsoft.com/library/dn641993.aspx).

   - USB-Einschränkungen zum Schutz vor physischen Infektionsvektoren.

      > [!NOTE]
      > Weitere Informationen finden Sie unter [Control Read or Write Access to Removable Devices or Media](https://technet.microsoft.com/library/cc730808(v=ws.10).aspx) (Kontrollieren des Lese- oder Schreibzugriffs auf Wechselmedien).

   - Netzwerkisolation zum Schutz vor Netzwerkangriffen und unbeabsichtigten Administratoraktionen. Hostfirewalls sollten alle eingehenden Verbindungen, mit Ausnahme der ausdrücklich erforderlichen, und sämtliche ausgehenden Internetzugriffe sperren.

   - Antischadsoftware zum Schutz vor bekannten Risiken und Schadsoftware.

   - Analyse der Angriffsfläche zum Verhindern der Einführung neuer Angriffsvektoren auf Windows während der Installation von neuer Software.

      > [!NOTE]
      > Die Verwendung von Tools wie [Attack Surface Analyzer (ASA)](https://www.microsoft.com/download/details.aspx?id=24487) trägt dazu bei, die Konfigurationseinstellungen auf einem Host auszuwerten und Angriffsvektoren zu identifizieren, die durch Software oder Konfigurationsänderungen eingeführt werden.

- Härten von Konten
   - Mit Ausnahme eines Kontos sollte die mehrstufige Authentifizierung für alle Konten in der administrativen Gesamtstruktur konfiguriert werden. Mindestens ein Administratorkonto sollte kennwortbasiert sein, um bei einem Ausfall der mehrstufigen Authentifizierung die Möglichkeit des Zugriffs sicherzustellen. Dieses Konto sollte durch strikte physische Kontrollmechanismen geschützt werden.
   - Konten, die für die mehrstufige Authentifizierung konfiguriert sind, sollten für die regelmäßige Festlegung eines neuen NTLM-Hashs für Konten konfiguriert werden. Zu diesem Zweck können Sie das Attribut „Benutzer muss sich mit einer Smartcard anmelden“ deaktivieren und umgehend erneut aktivieren.

      > [!NOTE]
      > Durch diese Aktion können laufende Vorgänge unterbrochen werden, die dieses Konto nutzen. Daher sollte die Aktion nur initiiert werden, wenn das Konto nicht von Administratoren verwendet wird (z. B. nachts oder am Wochenende).

- Erkennungskontrollen
   - Erkennungskontrollen für die administrative Gesamtstruktur sollten bei Anomalien in der administrativen Gesamtstruktur Warnungen ausgeben. Die begrenzte Anzahl von autorisierten Szenarios und Aktivitäten trägt dazu bei, diese Kontrollen präziser als die Produktionsumgebung zu optimieren.

Weitere Informationen zu Microsoft-Diensten für den Entwurf und die Bereitstellung einer ESAE für Ihre Umgebung finden Sie auf [dieser Seite](https://www.microsoft.com/services).

## <a name="tier-0-equivalency"></a>Äquivalenz zur Ebene 0

Die meisten Organisationen kontrollieren die Mitgliedschaft wichtiger Active Directory-Gruppen der Ebene 0 (z. B. Administratoren, Domänen-Admins und Unternehmensadministratoren).  Dabei übersehen viele Organisationen jedoch das Risiko anderer Gruppen, die in einer typischen Active Directory-Umgebung effektiv über äquivalente Berechtigungen verfügen. Diese Gruppen bieten einen recht einfachen Eskalationspfad für Angreifer, um über verschiedene Angriffsmethoden auf dieselben expliziten Berechtigungen der Ebene 0 zuzugreifen.

Ein Serveroperator könnte z. B. Zugang zum Sicherungsmedium eines Domänencontrollers erhalten und alle Anmeldeinformationen aus den Dateien auf diesem Medium abrufen, um diese zur Ausweitung von Berechtigungen zu nutzen.

Organisationen sollten die Mitgliedschaft in allen Gruppen der Ebene 0 (einschließlich geschachtelter Mitgliedschaften) kontrollieren und überwachen. Dazu zählen u. a. die Folgenden:

- Organisations-Admins
- Domänen-Admins
- Schema-Admin
- BUILTIN\Administrators
- Konten-Operatoren
- Sicherungsoperatoren
- Druck-Operatoren
- Server-Operatoren
- Domänencontroller
- Read-only-Domänencontroller
- Gruppenrichtlinienersteller-Besitzer
- Kryptografie-Operatoren
- Distributed COM-Benutzer
- Andere delegierte Gruppen: benutzerdefinierte Gruppen, die von Ihrer Organisation zum Verwalten von Verzeichnisvorgängen erstellt werden und möglicherweise ebenfalls über effektiven Zugriff der Ebene 0 verfügen.

## <a name="administrative-tools-and-logon-types"></a>Verwaltungstools und Anmeldetypen

Anhand dieser Referenzinformationen können Sie das Risiko einer Offenlegung von Anmeldeinformationen ermitteln, das mit der Verwendung verschiedener Tools für die Remoteverwaltung einhergeht.

In einem Remoteverwaltungsszenario werden die Anmeldeinformationen auf dem Quellcomputer immer offengelegt. Daher wird für vertrauliche Konten oder Konten mit großen Auswirkungen eine vertrauenswürdige Arbeitsstation mit privilegiertem Zugriff empfohlen. Ob Anmeldeinformationen auf dem Zielcomputer (Remotecomputer) offengelegt werden und potenziell gestohlen werden können, hängt in erster Linie vom Windows-Anmeldetyp ab, der von der Verbindungsmethode verwendet wird.

Diese Tabelle umfasst Informationen zu den meisten gängigen Verwaltungstools und Verbindungsmethoden:

|Verbindungsmethode|Anmeldetyp|Wiederverwendbare Anmeldeinformationen auf dem Ziel|Kommentare|
|-----------|-------|--------------------|------|
|Anmeldung bei der Konsole|Interactive (Interaktiv)|v|Umfasst Remotehardwarezugriff/Lights-out-Karten und Netzwerk-KVMs.|
|RUNAS|Interactive (Interaktiv)|v||
|RUNAS/NETZWERK|NewCredentials|v|Klont die aktuelle LSA-Sitzung für den lokalen Zugriff, verwendet bei der Verbindung mit Netzwerkressourcen jedoch neue Anmeldeinformationen.|
|Remotedesktop (erfolgreich)|RemoteInteractive|v|Wenn der Remotedesktopclient für die Freigabe lokaler Geräte und Ressourcen konfiguriert ist, können auch diese gefährdet sein.|
|Remotedesktop (Fehler – Anmeldetyp verweigert)|RemoteInteractive|-|Wenn bei der Anmeldung über RDP ein Fehler auftritt, werden die Anmeldeinformationen standardmäßig nur sehr kurz gespeichert. Wenn der Computer gefährdet ist, ist dies möglicherweise nicht der Fall.|
|Net use * \\\SERVER|Netzwerk|-||
|Net use * \\\SERVER /u:user|Netzwerk|-||
|MMC-Snap-Ins für Remotecomputer|Netzwerk|-|Beispiel: Computerverwaltung, Ereignisanzeige, Geräte-Manager, Dienste|
|PowerShell WinRM|Netzwerk|-|Beispiel: Enter-PSSession Server|
|PowerShell WinRM mit CredSSP|NetworkClearText|v|New-PSSession server<br />-Authentication Credssp<br />-Credential cred|
|PsExec ohne explizite Anmeldeinformationen|Netzwerk|-|Beispiel: PsExec \\\server cmd|
|PsExec mit expliziten Anmeldeinformationen|Netzwerk und interaktiv|v|PsExec \\\server -u user -p pwd cmd<br />Erstellt mehrere Anmeldesitzungen.|
|Remoteregistrierung|Netzwerk|-||
|Remotedesktopgateway|Netzwerk|-|Authentifizierung gegenüber Remotedesktopgateway.|
|Geplanter Task|Batch (Stapel)|v|Das Kennwort wird auch als geheime LSA-Information auf dem Datenträger gespeichert.|
|Tools als Dienst ausführen|Dienst|v|Das Kennwort wird auch als geheime LSA-Information auf dem Datenträger gespeichert.|
|Überprüfung auf Sicherheitsrisiken|Netzwerk|-|Bei den meisten Überprüfungen werden Netzwerkanmeldungen verwendet. Einige Anbieter implementieren jedoch möglicherweise andere Anmeldeverfahren, die ein höheres Risiko für einen Diebstahl von Anmeldeinformationen zur Folge haben.|

Informationen zur Webauthentifizierung finden Sie in der Tabelle unten:

|Verbindungsmethode|Anmeldetyp|Wiederverwendbare Anmeldeinformationen auf dem Ziel|Kommentare|
|-----------|-------|--------------------|------|
|IIS-Standardauthentifizierung|NetworkCleartext<br />(IIS 6.0 und höher)<p>Interactive (Interaktiv)<br />(vor IIS 6.0)|v||
|Integrierte Windows-Authentifizierung (IIS)|Netzwerk|-|NTLM- und Kerberos-Anbieter.|

Spaltendefinitionen:

- **Anmeldetyp** identifiziert den Anmeldetyp, der von der Verbindung initiiert wird.
- **Wiederverwendbare Anmeldeinformationen auf dem Ziel** gibt an, dass die folgenden Typen von Anmeldeinformationen im LSASS-Prozessspeicher auf dem Zielcomputer gespeichert werden, auf dem das angegebene Konto lokal angemeldet wird:
   - LM- und NT-Hashes
   - Kerberos TGTs
   - Nur-Text-Kennwort (falls zutreffend).

Die Symbole in dieser Tabelle sind wie folgt definiert:

- (-) zeigt an, dass die Anmeldeinformationen nicht offengelegt werden.
- (v) zeigt an, dass die Anmeldeinformationen offengelegt werden.

Bei Verwaltungsanwendungen, die nicht in dieser Tabelle aufgeführt sind, können Sie den Anmeldetyp anhand des entsprechenden Felds in den überwachten Anmeldeereignissen ermitteln. Weitere Informationen finden Sie unter [Anmeldeereignisse überwachen](https://technet.microsoft.com/library/cc787567(v=ws.10).aspx).

Auf Windows-basierten Computern werden alle Authentifizierungen als einer von mehreren Anmeldetypen verarbeitet (unabhängig davon, welches Authentifizierungsprotokoll oder welcher Authenticator verwendet wird). Diese Tabelle enthält die gängigsten Anmeldetypen sowie die zugehörigen Attribute im Hinblick auf den Diebstahl von Anmeldeinformationen:

|Anmeldetyp|#|Akzeptierte Authenticators|Wiederverwendbare Anmeldeinformationen in LSA-Sitzung|Beispiele|
|-------|---|--------------|--------------------|------|
|Interaktiv (lokale Anmeldung)|2|Kennwort, Smartcard,<br />andere|Ja|Konsolenanmeldung,<br />RUNAS,<br />Lösungen zur Remotesteuerung von Hardware (z. B. Netzwerk-KVM oder Remotezugriff/Lights-Out-Karte in Servern)<br />IIS-Standardauthentifizierung (vor IIS 6.0)|
|Netzwerk|3|Kennwort,<br />NT-Hash,<br />Kerberos-Ticket|Nein (Ausnahme: Wenn die Delegierung aktiviert ist, sind Kerberos-Tickets vorhanden)|NET USE,<br />RPC-Aufrufe,<br />Remoteregistrierung,<br />Integrierte Windows-Authentifizierung (IIS),<br />SQL-Windows-Authentifizierung,|
|Batch (Stapel)|4|Kennwort (üblicherweise als geheime LSA-Daten gespeichert)|Ja|Geplante Aufgaben|
|Dienst|5|Kennwort (üblicherweise als geheime LSA-Daten gespeichert)|Ja|Windows-Dienste|
|NetworkCleartext|8|Kennwort|Ja|IIS-Standardauthentifizierung (IIS 6.0 und höher),<br />Windows PowerShell mit CredSSP|
|NewCredentials|9|Kennwort|Ja|RUNAS/NETZWERK|
|RemoteInteractive|10|Kennwort, Smartcard,<br />andere|Ja|Remotedesktop (früher „Terminaldienste“)|

Spaltendefinitionen:

- **Anmeldetyp** ist der Typ der angeforderten Anmeldung.
- **#** ist der numerische Bezeichner für den Anmeldetyp, der in Überwachungsereignissen des Sicherheitsereignisprotokolls aufgeführt wird.
- **Akzeptierte Authenticators** gibt an, welche Typen von Authenticators eine Anmeldung dieses Typs initiieren können.
- **Wiederverwendbare Anmeldeinformationen in einer LSA-Sitzung** gibt an, ob der Anmeldetyp zur Folge hat, dass die LSA-Sitzung die Anmeldeinformationen (z. B. Nur-Text-Kennwörter, NT-Hashes oder Kerberos-Tickets) speichert, sodass diese gegebenenfalls für die Authentifizierung gegenüber anderer Netzwerkressourcen verwendet werden können.
- Unter **Beispiele** sind gängige Szenarien aufgeführt, in denen der Anmeldetyp verwendet wird.

> [!NOTE]
> Weitere Informationen zu Anmeldetypen finden Sie unter [SECURITY_LOGON_TYPE enumeration](https://technet.microsoft.com/library/aa380129(VS.85).aspx) (SECURITY_LOGON_TYPE-Enumeration).
