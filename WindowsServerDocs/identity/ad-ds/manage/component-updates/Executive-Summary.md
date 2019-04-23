---
ms.assetid: 85ca191c-0cc7-4453-a72c-42060ddf2ea2
title: Kurzfassung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a3eecec9d47f91bb6a9ba549abc3bf62482b2f49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863281"
---
# <a name="executive-summary"></a>Kurzfassung

>Gilt für: Windows Server 2012

>[!IMPORTANT] 
>Die folgende Dokumentation wurde in 2013 geschrieben, und es wird nur zu historischen Zwecken bereitgestellt.  Derzeit überprüfen wir in dieser Dokumentation und unterliegt Änderungen.  Es kann nicht die aktuelle bewährte Methoden wider.

Keine Organisation mit einer Infrastruktur der Informationstechnologie (IT) gegen Angriffe immun ist, aber wenn geeigneten Richtlinien, Prozesse und Steuerelemente implementiert werden, um die wichtigsten Segmente der Computerinfrastruktur eines Unternehmens zu schützen, ist es eventuell möglich verhindern Sie, dass ein Ereignis einer sicherheitsverletzung achsenbezeichnungsschriftgrad durch Vergrößern an eine umfassende Gefährdung der IT-Umgebung.  
  
Dieser zusammenfassende Darstellung dient als eigenständiges Dokument zusammenfassen der Inhalte des Dokuments an, die Empfehlungen enthält, die Organisationen bei der Verbesserung der Sicherheits ihrer Active Directory-Installationen zu unterstützen, werden nützlich sein. Durch die Implementierung dieser Empfehlungen können kann Organisationen zu identifizieren und priorisieren Sicherheitsaktivitäten, wichtigsten Segmente für die Computerinfrastruktur ihres Unternehmens zu schützen und Steuerelemente erstellen, die die Wahrscheinlichkeit erheblich zu verringern erfolgreicher Angriffe auf wichtige Komponenten der IT-Umgebung.  
  
Obwohl in diesem Dokument wird, die am häufigsten verwendeten Angriffe gegen die Active Directory und Gegenmaßnahmen erläutert, um die Angriffsfläche zu verringern, enthält es auch Empfehlungen für die Wiederherstellung bei Verlust. Die einzige sichere Möglichkeit, im Falle einer umfassenden Gefährdung der Active Directory wiederherzustellen, ist für die Beeinträchtigung vorbereitet werden, bevor sie vorgenommen.  
  
Sind die wichtigsten Abschnitte dieses Dokuments:  
  
-   Wege der Gefährdung  
  
-   Reduzieren der Angriffsfläche für Active Directory  
  
-   Überwachen von Active Directory auf Anzeichen für einen Kompromiss  
  
-   Planen der Gefährdung  
  
## <a name="avenues-to-compromise"></a>Wege der Gefährdung  
Dieser Abschnitt enthält Informationen zu einigen der am häufigsten wirksame Sicherheitsrisiken, die von Angreifern verwendet werden, um die Kunden-Infrastrukturen zu gefährden. Sie enthält allgemeine Kategorien von Sicherheitsrisiken und deren Verwendung sind anfänglich durchdringen Kunden Infrastrukturen, Gefährdung über zusätzliche Systeme hinweg verteilt und schließlich Active Directory und Domänencontroller, um abgeschlossen zu erhalten. die Kontrolle über die Organisationen Gesamtstrukturen. Es bietet keine detaillierte Empfehlungen zur Adressierung von jeder Art von Sicherheitsrisiko, insbesondere in den Bereichen, die in denen die Sicherheitslücken nicht verwendet werden, um direkt auf die Active Directory als Ziel. Jedoch für jeden Typ des Sicherheitsrisikos aufgeführten Links zu weiteren Informationen, Gegenmaßnahmen entwickeln und Reduzieren der Angriffsfläche des Unternehmens mit.  
  
Umfasst die folgenden Themen:  
  
-   **Ursprüngliche Ziele der sicherheitsverletzung** – die meisten Verletzungen der datensicherheit beginnen Sie mit der Kompromittierung von kleine Teile der Infrastruktur – häufig ein oder zwei-Systeme eines Unternehmens zu einem Zeitpunkt. Die ersten Ereignisse bzw. Einstiegspunkte mit dem Netzwerk nutzen häufig Sicherheitsrisiken, die konnte wurden behoben, aber nicht waren. Häufig auftretender Schwachstellen sind:  
  
    -   Lücken in der Antiviren- und Antischadsoftware-Bereitstellungen  
  
    -   Unvollständige Patchen  
  
    -   Veraltete Anwendungen und Betriebssysteme  
  
    -   Misconfiguration  
  
    -   Mangel an Methoden für die sichere Anwendungsentwicklung  
  
-   **Attraktive Konten für den Diebstahl von Anmeldeinformationen** -Angriffen mit gestohlenen Anmeldeinformationen sind in dem ein Angreifer zuerst erhält privilegierten Zugriff auf einen Computer in einem Netzwerk, und verwendet dann die kostenlos verfügbare Tools, um die Anmeldeinformationen aus der Sitzungen, die von anderen extrahieren angemeldeten Konten.   
    In diesem Abschnitt enthalten, lauten wie folgt:  
  
    -   **Aktivitäten, die die Wahrscheinlichkeit, dass der Gefährdung erhöhen** : Da das Ziel der Diebstahl von Anmeldeinformationen in der Regel hoch privilegierter Domänenkonten und "sehr wichtig Person" ist (VIP)-Konten, es ist wichtig, dass Administratoren sich der sein Aktivitäten, die die Wahrscheinlichkeit eines Erfolgs eines Angriffs Diebstahl von Anmeldeinformationen zu erhöhen. Diese Aktivitäten sind:  
  
        -   Anmelden an der ungeschützten Computer mit privilegierten Konten  
  
        -   Browsen im Internet mit einem Konto mit weit reichenden Berechtigungen  
  
        -   Konfigurieren von lokalen privilegierten Konten mit den gleichen Anmeldeinformationen über Systeme hinweg  
  
        -   Overpopulation oder übermäßiger Verwendung privilegierter Gruppen  
  
        -   Unzureichende Verwaltung der Sicherheit der Domänencontroller.  
  
    -   **Berechtigungen der Erhöhung der Rechte und Weitergabe** -bestimmte Konten, Server und Komponenten der Infrastruktur sind in der Regel das primäre Ziel von Angriffen mit Active Directory. Diese Konten sind:  
  
        -   Dauerhaft privilegierte Konten  
  
        -   VIP-Konten  
  
        -   Active Directory-Konten "Berechtigung Attached"  
  
        -   Domänencontroller  
  
        -   Anderer Infrastrukturdienste, die Identität und Zugriff Configuration Management, z. B. public Key-Infrastruktur (PKI)-Server und Systems Management Server betreffen.  
  
## <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory  
Dieser Abschnitt konzentriert sich auf technischen Kontrollmechanismen, um die Angriffsfläche einer Active Directory-Installation zu verringern. In diesem Abschnitt enthalten, sind die folgenden Themen:  
  
-   Die **privilegierte Konten und Gruppen in Active Directory** Abschnitt beschreibt die höchste privilegierte Konten und Gruppen in Active Directory und die Mechanismen, mit dem privilegierte Konten werden geschützt. Innerhalb von Active Directory sind drei integrierte Gruppen den höchsten Berechtigungen Gruppen im Verzeichnis (Organisations-Admins, Domänen-Admins und Administratoren), obwohl eine Reihe von zusätzlichen Gruppen und Konten auch geschützt werden sollen.  
  
-   Die **implementieren mit Minimalprivilegien Verwaltungsmodellen** Abschnitt geht es um das Risiko, der die Verwendung der höher privilegierten Konten für alltägliche Verwaltungsaufgaben zusätzlich zur Bereitstellung von Empfehlungen enthält, identifizieren Reduzieren dieser Risiken.  
  
Übermäßige Rechte ist nicht nur in Active Directory in gefährdeten Umgebungen gefunden. Wenn eine Organisation sich mehr Berechtigungen als nötig erteilt entwickelt hat, wird es in der Regel in der gesamten Infrastruktur gefunden:  
  
-   In Active Directory  
  
-   Auf Mitgliedsservern  
  
-   Auf Arbeitsstationen  
  
-   In Anwendungen  
  
-   In den Datenrepositorys  
  
-   Die **sichere Administrative Hosts implementieren** Abschnitt wird beschrieben, sichere administrative Hosts, die Computer sind, die zur Unterstützung der Verwaltung von Active Directory und verbundenen Systemen konfiguriert sind. Diese Hosts zugewiesen werden, die Verwaltungsfunktionen und Software wie z. B. e-Mail-Anwendungen, Webbrowser oder Produktivitätssoftware (z. B. Microsoft Office) werden nicht ausgeführt.  
  
In diesem Abschnitt enthalten, lauten wie folgt:  
  
-   **Grundsätze für das Erstellen von sicheren Administrative Hosts** -sind die allgemeinen Prinzipien zu beachten:  
  
    -   Nie zu verwalten Sie ein vertrauenswürdiges System eines weniger vertrauenswürdigen Hosts.  
  
    -   Verlassen Sie sich nicht auf einem einzelnen authentifizierungsfaktors, beim Ausführen von Aktivitäten mit Berechtigungen.  
  
    -   Vergessen Sie nicht die physischen Sicherheit beim Entwerfen und implementieren sichere administrative Hosts.  
  
-   **Domain Controller gegen Angriffe schützen** -Wenn ein böswilliger Benutzer privilegierten Zugriff auf einen Domänencontroller erhält, dieser Benutzer kann ändern, beschädigen und zerstören die Active Directory-Datenbank und aller Systeme und Konten von Active Directory verwaltet werden.  
  
In diesem Abschnitt enthalten, sind die folgenden Themen:  
  
-   **Physische Sicherheit für Domänencontroller** -enthält Empfehlungen für die physischen Sicherheit für Domänencontroller in Rechenzentren, Remotestandorten und Zweigstellen bereitstellen.  
  
-   **Domänencontroller-Betriebssysteme** -enthält Empfehlungen zum Sichern von der Domäne Domänencontroller-Betriebssysteme.  
  
-   **Sichern Sie die Konfiguration von Domänencontrollern** -Native und die kostenlos verfügbare Tools und Einstellungen dienen zum Erstellen von Konfigurationsbasislinien für die Domänencontroller, die anschließend durch Gruppenrichtlinienobjekte (erzwungen werden können GPOs).  
  
## <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für einen Kompromiss  
Dieser Abschnitt enthält Informationen zu älteren Überwachungskategorien und Überwachungsrichtlinien-Unterkategorien (die in Windows Vista und Windows Server 2008 eingeführt wurden) und erweiterten Überwachungsrichtlinie (die in Windows Server 2008 R2 eingeführt wurde). Auch bereitgestellt sind Informationen über Ereignisse und Objekte für die Überwachung können Versuche, beeinträchtigen die Umgebung und einige zusätzliche Verweise, die verwendet werden können, zum Erstellen einer umfassenden Überwachungsrichtlinie für Active Directory angeben.  
  
In diesem Abschnitt enthalten, sind die folgenden Themen:  
  
-   **Windows-Überwachungsrichtlinie** – Windows-Sicherheitsereignisprotokollen verfügen über die Kategorien und Unterkategorien, die bestimmen, welche Sicherheitsereignisse überwacht und aufgezeichnet werden.  
  
-   **Empfehlungen zu Überwachungsrichtlinien** – in diesem Abschnitt wird beschrieben, die Windows-Standard-überwachungsrichtlinieneinstellungen, sicherheitsüberwachungs-Richtlinieneinstellungen, die von Microsoft und strengere wiederherstellungsanforderungen Empfehlungen für das Unternehmen zu verwenden, um wichtige Server überwachen sollten und Arbeitsstationen.  
  
## <a name="planning-for-compromise"></a>Planen der Gefährdung  
Dieser Abschnitt enthält Empfehlungen, die Organisationen, die Vorbereitung einer Gefährdung, bevor sie vorgenommen, implementieren-Steuerelemente, die Erkennen eines Ereignisses Gefährdung, bevor eine vollständige sicherheitsverletzung aufgetreten ist, und stellen für Fälle, in denen Reaktions- und Richtlinien eine vollständige Gefährdung des Verzeichnisses wird von Angreifern erreicht. In diesem Abschnitt enthalten, sind die folgenden Themen:  
  
-   **Neuer Ansatz für den Ansatz** -enthält Prinzipien und Richtlinien, die sichere Umgebungen zu erstellen, in dem eine Organisation kann ihre wichtigsten Ressourcen platzieren. Diese Richtlinien sind wie folgt aus:  
  
    -   Identifizieren Prinzipien für die Trennung und schützen kritische Ressourcen  
  
    -   Definieren eines Plans für die Migration begrenzt, risikobasierten  
  
    -   Nutzen "nonmigratory" Migrationen, bei Bedarf  
  
    -   Implementieren von "creative Zerstörung"  
  
    -   Isolieren ältere Systeme und Anwendungen  
  
    -   Vereinfachung der Sicherheit für Endbenutzer  
  
-   **Verwalten einer mehr sichere Umgebung** -enthält allgemeine Empfehlungen als Richtlinien zur Entwicklung nicht nur effektive Sicherheit, sondern auch effektive Anwendungslebenszyklus-Verwaltung verwendet werden sollen. In diesem Abschnitt enthalten, sind die folgenden Themen:  
  
    -   **Erstellen geschäftskritische Sicherheitsmaßnahmen für Active Directory** : Informationen zum effektiven Verwaltung des Lebenszyklus von Benutzern, Daten, Anwendungen und Systeme, die von Active Directory verwaltet werden, befolgen diese Prinzipien.  
  
        -   **Weisen Sie eine Business Active Directory-Daten** -weisen den Besitz der Infrastrukturkomponenten IT; für Daten, die Active Directory Domain Services (AD DS) zur Unterstützung des Unternehmens, z. B. neue Mitarbeiter, neue Anwendungen hinzugefügt werden, und neue Informationen Repositories, eine angegebene Geschäftseinheit oder einen Benutzer sollten die Daten zugeordnet werden.  
  
        -   **Implementieren der Verwaltung des Identitätslebenszyklus Business-Driven** -Verwaltung des Identitätslebenszyklus sollten für Daten in Active Directory implementiert werden.  
  
        -   **Alle Active Directory-Daten klassifizieren** -Geschäftsinhaber sollten Klassifizierung für Daten in Active Directory bereitstellen. In das Datenmodell für die Klassifizierung sollte die Klassifizierung für die folgenden Active Directory-Daten enthalten sein:  
  
            -   **Systeme** -klassifizieren Server Auffüllungen, ihr Betriebssystem ihrer Rolle, und der IT-ausgeführten Anwendungen und Geschäftsinhaber des Datensatzes.  
  
            -   **Anwendungen** -Anwendungen durch Funktionen, Benutzer und ihr Betriebssystem zu klassifizieren.  
  
            -   **Benutzer** -Konten in Active Directory-Installationen, die am wahrscheinlichsten vor Angriffen zu schützen sind gekennzeichnet und überwacht werden soll.  
  
## <a name="summary-of-best-practices-for-securing-active-directory-domain-services"></a>Zusammenfassung der Best Practices for Securing Active Directory-Domänendienste  
Die folgende Tabelle enthält eine Zusammenfassung der Empfehlungen in diesem Dokument zum Sichern von AD DS-Installation. Einige bewährten Methoden sind strategischer Natur und erfordern eine umfassende Planung und Implementierung Projekte. andere sind taktischen und konzentriert sich auf bestimmte Komponenten von Active Directory und der zugehörigen Infrastruktur.  
  
Methoden sind ungefähre Reihenfolge ihrer Priorität, d. h. aufgeführt, die niedrigere Zahlen geben eine höhere Priorität. Zutreffend, best Practices, in dem als Preventative oder Detective Natur identifiziert sind. Alle diese Empfehlungen sollten gründlich getestet und nach Bedarf für die Merkmale und Anforderungen Ihrer Organisation geändert.  
  
  
||**Es wird empfohlen**|**Taktisch oder strategisch**|**Preventative oder Detective**|  
|-|-|-|-|  
|1|Patch-Anwendungen.|Taktisch|Preventative|  
|2|Patchen von Betriebssystemen.|Taktisch|Preventative|  
|3|Bereitstellen Sie und aktualisieren Sie die Antiviren-und Antischadsoftware sofort für alle Systeme und Überwachung von Versuche zu entfernen oder zu deaktivieren.|Taktisch|Beide|  
|4|Überwachen Sie vertrauliche Active Directory-Objekte für die Änderung Versuche und Windows für Ereignisse, die versuchten Kompromittierung hinweisen.|Taktisch|Detective|  
|5|Schützen und Überwachen von Konten für Benutzer mit Zugriff auf sensible Daten|Taktisch|Beide|  
|6|Verhindern Sie, dass leistungsstarke Konten, die auf nicht autorisierte Systeme verwendet wird.|Taktisch|Preventative|  
|7|Vermeiden Sie permanente Mitgliedschaft in sehr privilegierten Gruppen.|Taktisch|Preventative|  
|8|Implementieren Sie Kontrollen zum Erteilen temporären Mitgliedschaften in privilegierten Gruppen bei Bedarf.|Taktisch|Preventative|  
|9|Implementieren Sie sichere administrative Hosts.|Taktisch|Preventative|  
|10|Verwenden Sie Anwendungswhitelisting auf Domänencontrollern, administrativen Hosts und andere vertrauliche Systeme.|Taktisch|Preventative|  
|11|Identifizieren Kritischer Ressourcen und Priorisieren Sie die Sicherheit und Überwachung.|Taktisch|Beide|  
|12|Für die Verwaltung des Verzeichnisses, die unterstützende Infrastruktur und der Domäne Angehörige Systeme mit minimalprivilegien, rollenbasierte Zugriffssteuerung zu implementieren.|Strategisch|Preventative|  
|13|Isolieren Sie ältere Systeme und Anwendungen.|Taktisch|Preventative|  
|14|Außerbetriebnahme von älteren Systemen und Anwendungen.|Strategisch|Preventative|  
|15|Implementieren Sie sichere Softwareentwicklungs-Lebenszyklus-Programme für benutzerdefinierte Anwendungen.|Strategisch|Preventative|  
|16|Implementieren Sie der konfigurationsverwaltung, regelmäßig überprüfen Sie der Konformität und Werten Sie Einstellungen mit jeder neuen Version von Hardware oder Software aus.|Strategisch|Preventative|  
|17|Migrieren Sie kritische Ressourcen mit strengen Sicherheits- und überwachungsanforderungen für makellose Gesamtstrukturen.|Strategisch|Beide|  
|18|Vereinfachen Sie die Sicherheit für Endbenutzer.|Strategisch|Preventative|  
|19|Verwenden Sie hostbasierte Firewalls zum Steuerelement und sichere Kommunikation.|Taktisch|Preventative|  
|20|Patch-Geräte.|Taktisch|Preventative|  
|21|Implementieren Sie geschäftskritische Anwendungslebenszyklus-Verwaltung für IT-Ressourcen.|Strategisch|Nicht zutreffend|  
|22|Erstellen oder Aktualisieren von Incidents Wiederherstellungspläne.|Strategisch|Nicht zutreffend|  
  


