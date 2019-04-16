---
ms.assetid: 85ca191c-0cc7-4453-a72c-42060ddf2ea2
title: Zusammenfassung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c218a4d66e8208cf627bc93be50bf11ea2fbf862
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="executive-summary"></a>Zusammenfassung

>Gilt für: Windows Server 2012

>[!IMPORTANT] 
>Die folgende Dokumentation wurde 2013 und dienen nur zu liegen.  Derzeit überprüfen wir in dieser Dokumentation und unterliegt Änderungen.  Es kann nicht bewährte Methoden wider.

Keine Organisation mit einer Infrastruktur Informationstechnologie (IT) ist gegen Angriffe immun, aber wenn geeigneten Richtlinien, Prozessen und Steuerelemente implementiert werden, um die wichtigsten Segmente für IT-Infrastruktur eines Unternehmens schützen, ist es eventuell möglich, um zu verhindern, dass ein Ereignis Verletzung zu einer Großhandelsvertrieb Gefährdung der IT-Umgebung wächst.  
  
Diese Zusammenfassung soll als eigenständiges Dokument zusammenfassen des Inhalts des Dokuments, enthält Empfehlungen, die dabei Organisationen helfen in der Verbesserung der Sicherheit ihrer Active Directory-Installationen nützlich sein. Durch die Implementierung dieser Empfehlung, werden Organisationen zu identifizieren und priorisieren-Aktivitäten, wichtigsten Segmente für computing-Infrastruktur der Organisation zu schützen, und erstellen Sie Steuerelemente, die erheblich die Wahrscheinlichkeit, dass erfolgreiche Angriffe auf wichtige Komponenten der IT-Umgebung verringern können.  
  
Obwohl in diesem Dokument wird, die am häufigsten verwendeten Angriffe auf Active Directory und Gegenmaßnahmen erläutert, um die Angriffsfläche zu verringern, enthält auch Vorschläge für die Wiederherstellung im Fall einer kompletten Kompromittierung. Die einzige sichere Möglichkeit zum Wiederherstellen im Falle einer kompletten Kompromittierung des Active Directory ist für die Gefährdung vorbereitet werden, bevor es auftritt.  
  
Sind die wichtigsten Abschnitte dieses Dokuments:  
  
-   Wege der Gefährdung  
  
-   Reduzieren der Angriffsfläche für Active Directory  
  
-   Überwachen von Active Directory auf Anzeichen für Sicherheitsgefährdungen  
  
-   Planen der Gefährdung  
  
## <a name="avenues-to-compromise"></a>Wege der Gefährdung  
Dieser Abschnittenthält Informationen zu einigen der am häufigsten Nutzung Schwachstellen von Angreifern verwendet werden, um Kunden Infrastrukturen gefährden. Es enthält allgemeine Kategorien von Sicherheitslücken und wie diese verwendet werden, Kunden Infrastrukturen anfänglich einzudringen, Gefährdung auf zusätzliche Systeme verteilt, und schließlich Active Directory und Domänencontroller, um die vollständige Kontrolle über die Organisationen Gesamtstrukturen zu erhalten. Er bietet detaillierte Vorschläge über jede Art von Sicherheitsrisiko, insbesondere in den Bereichen, in denen die Sicherheitslücken nicht verwendet werden, um Active Directory direkt als Ziel-Adressierung. Allerdings haben für jede Art von Sicherheitsrisiko, wir bereitgestellt Links zu weiteren Informationen zum Entwickeln von Gegenmaßnahmen und Reduzieren der Angriffsfläche für die Organisation.  
  
Eingeschlossen sind die folgenden Themen:  
  
-   **Erste Verletzung Ziele** -Sicherheitslücken für die meisten Informationen beginnen Sie mit der Gefährdung der kleinere Textmengen der Infrastruktur häufig ein oder Zwei-Systeme einer Organisation zu einem Zeitpunkt. Diese erste Ereignisse oder Einstiegspunkte in das Netzwerk nutzen häufig Sicherheitsrisiken, die konnte wurden behoben, aber nicht im selben. Häufigsten Sicherheitslücken sind:  
  
    -   Lücken in Antiviren- und Antischadsoftware-Bereitstellungen  
  
    -   Unvollständige Patches  
  
    -   Veraltete Anwendungen und Betriebssystemen  
  
    -   Falsche Konfiguration  
  
    -   Mangel an sicheren Methoden für die Anwendungsentwicklung  
  
-   **Attraktive Konten für den Diebstahl von Anmeldeinformationen** -Methoden des Anmeldeinformationsdiebstahls in dem ein Angreifer erhält zunächst privilegierten Zugriff auf einen Computer in einem Netzwerk und verwendet dann kostenlos verfügbare Tools zum Extrahieren von Anmeldeinformationen aus der Sitzungen von anderen Konten angemeldet sind.   
    In diesem Abschnittenthalten sind die folgenden:  
  
    -   **Aktivitäten, die erhöhen die Wahrscheinlichkeit, dass der Gefährdung** –, da das Ziel des Diebstahls von Anmeldeinformationen in der Regel privilegierter Domänenkonten und "sehr wichtig Person ist" (VIP) Konten, es ist wichtig für Administratoren Standardfeature Aktivitäten, die die Wahrscheinlichkeit eines Erfolgs eines Angriffs Diebstahl von Anmeldeinformationen zu erhöhen. Diese Aktivitäten werden:  
  
        -   Unsichere von Computern mit privilegierten Konten anmelden  
  
        -   Browsen im Internet mit einem sehr privilegierten Konto  
  
        -   Konfigurieren von lokalen privilegierte Konten mit denselben Anmeldeinformationen in mehreren Systemen  
  
        -   Overpopulation und die übermäßige Verwendung privilegierter Gruppen  
  
        -   Nicht genügend Verwaltung der Sicherheit von Domänencontrollern.  
  
    -   **Berechtigung für erhöhte Rechte und Weitergabe** -bestimmte Konten, Server und Infrastrukturkomponenten sind in der Regel die primären Ziele von Angriffen auf Active Directory. Diese Konten sind:  
  
        -   Dauerhaft privilegierte Konten  
  
        -   VIP-Konten  
  
        -   Active Directory-Konten "Rechte angefügten"  
  
        -   Domänencontroller  
  
        -   Andere Infrastrukturdienste, die Identität, Zugriff und Configuration Management, z.B. public Key-Infrastruktur (PKI)-Servern und Systems Management Server betreffen.  
  
## <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory  
Dieser Abschnittkonzentriert sich auf technische Sicherheitselemente zum Reduzieren der Angriffsfläche einer Active Directory-Installation. In diesem Abschnittenthalten, werden die folgenden Themen:  
  
-   Die **privilegierte Konten und Gruppen in Active Directory** Abschnittwird erläutert, die höchste privilegierte Konten und Gruppen in Active Directory und die Mechanismen, die durch die privilegierte Konten geschützt werden. In Active Directory sind drei integrierte Gruppen die höchsten Berechtigung Gruppen in das Verzeichnis (Organisations-Admins, Domänen-Admins und Administratoren), obwohl zahlreiche weitere Gruppen und Konten ebenfalls geschützt werden sollen.  
  
-   Die **implementieren geringsten Verwaltungsmodellen** Abschnittkonzentriert sich auf identifizieren das Risiko, die die Verwendung von sehr privilegierten Konten für die tägliche Verwaltung zeigt, außerdem zum Bereitstellen von Empfehlungen, um dieses Risiko zu verringern.  
  
Übermäßige Rechte ist nicht nur in gefährdeten Umgebungen in Active Directory gefunden. Wenn ein Unternehmen auch gewähren weitere Berechtigungen als nötig entwickelt wurde, wird es in der Regel innerhalb der Infrastruktur gefunden:  
  
-   In Active Directory  
  
-   Auf Mitgliedsservern  
  
-   Auf Arbeitsstationen  
  
-   In Anwendungen  
  
-   Daten-Repositorys  
  
-   Die **Implementieren von sicheren Administrative Hosts** Abschnittwird beschrieben, sichere administrative Hosts, die Computer sind, die zur Unterstützung der Verwaltung von Active Directory und verbundenen Systeme konfiguriert sind. Diese Hosts Verwaltungsfunktionen zugeordnet sind und Software, z.B. E-Mail-Anwendungen, Webbrowser und Produktivitäts-Software (z.B. Microsoft Office) werden nicht ausgeführt.  
  
In diesem Abschnittenthalten sind die folgenden:  
  
-   **Prinzipien für das Erstellen von sicheren Administrative Hosts** -die allgemeine Prinzipien zu beachten sind:  
  
    -   Verwalten Sie nie ein vertrauenswürdiges System von einer weniger vertrauenswürdigen Host.  
  
    -   Verlassen Sie sich nicht auf einem einzelnen authentifizierungsfaktors beim privilegierter Aktivitäten ausführen.  
  
    -   Vergessen Sie nicht die physische Sicherheit beim Entwerfen und implementieren sichere administrative Hosts.  
  
-   **Sichern von Domänencontrollern vor Angriffen Domäne** -ein böswilliger Benutzer privilegierten Zugriff auf einen Domänencontroller erhält, die Benutzer kann ändern, beschädigt und zerstören die Active Directory-Datenbank und durch die Erweiterung aller Systeme und Konten, die von Active Directory verwaltet werden.  
  
In diesem Abschnittenthalten, werden die folgenden Themen:  
  
-   **Physische Sicherheit für Domänencontroller** -enthält Empfehlungen für die Bereitstellung von Sicherheit für Domänencontroller in Rechenzentren, Zweigstellen und Remote-Standorten.  
  
-   **Domänencontroller-Betriebssysteme** -enthält Empfehlungen für die Sicherung der Domänenbenutzers Domänencontroller-Betriebssysteme.  
  
-   **Sichern Sie die Konfiguration von Domänencontrollern** -Konfiguration von systemeigenen und kostenlos verfügbare Tools und Einstellungen dienen zum Erstellen von Konfigurationsbasislinien für Domänencontroller, die anschließend durch Gruppenrichtlinienobjekte (GPOs) erzwungen werden kann.  
  
## <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für Sicherheitsgefährdungen  
Dieser Abschnittenthält Informationen über ältere Überwachungskategorien und Überwachungsrichtlinien-Unterkategorien (die in Windows Vista und Windows Server2008 eingeführt wurden) und erweiterte Überwachungsrichtlinie (die in Windows Server2008 R2 eingeführt wurde). Auch Informationen über Ereignisse und zu, die zu überwachenden Objekte können angeben, versucht, beeinträchtigen die Umgebung und einige weiteren Referenzen, die zum Erstellen von einer umfassenden Überwachungsrichtlinie für Active Directory verwendet werden können.  
  
In diesem Abschnittenthalten, werden die folgenden Themen:  
  
-   **Windows-Überwachungsrichtlinie** – Windows-Sicherheitsereignisprotokollen werden Kategorien und Unterkategorien, die bestimmen, welche Sicherheitsereignisse überwacht und aufgezeichnet werden.  
  
-   **Überwachen der Richtlinie Empfehlungen** – in diesem Abschnittwird beschrieben, die Windows-Standard-Überwachungsrichtlinieneinstellungen, Überwachungsrichtlinieneinstellungen, die von Microsoft und aggressiver Empfehlungen für Organisationen mit wichtigen Servern und Arbeitsstationen überwachen empfohlen werden.  
  
## <a name="planning-for-compromise"></a>Planen der Gefährdung  
Dieser Abschnittenthält Empfehlungen, mit dem Organisationen, die für eine Gefährdung vorbereiten, bevor er eintritt, implementieren-Steuerelemente, die ein Ereignis Gefährdung, bevor eine vollständige Verletzung zu erkennen können, und bieten Reaktion auf und Wiederherstellung von Richtlinien für Fälle, in denen eine vollständige Gefährdung des Verzeichnisses von Angreifern erreicht ist. In diesem Abschnittenthalten, werden die folgenden Themen:  
  
-   **Neuer Ansatz für den Ansatz** -enthält Entwurfsprinzipien und Richtlinien, um sichere Umgebungen zu erstellen, in die eine Organisation ihrer kritischsten Ressourcen einfügen kann. Diese Richtlinien sind wie folgt:  
  
    -   Identifizieren von Prinzipien für die Trennung und sichern wichtige Ressourcen  
  
    -   Definieren einen Plan beschränkt und Risiko-basierten Migration  
  
    -   Nutzung von "nonmigratory" Migrationen, bei Bedarf  
  
    -   Implementieren von "creative Zerstörung"  
  
    -   Isolieren von älteren Systemen und Anwendungen  
  
    -   Vereinfachung der Sicherheit für Endbenutzer  
  
-   **Warten einer mehr sicheren Umgebung** -enthält allgemeine Empfehlungen als Richtlinien verwendet werden, um bei der Entwicklung nicht nur wirksame, aber effektives Lifecycle Management verwenden soll. In diesem Abschnittenthalten, werden die folgenden Themen:  
  
    -   **Erstellen von Business-zentrierte Methoden für die Sicherheit für Active Directory** –, um effektiv verwalten des Lebenszyklus von Benutzern, Daten, Anwendungen und Systemen, die von Active Directory verwaltet werden, führen die folgenden Prinzipien.  
  
        -   **Weisen Sie ein Unternehmen Besitz Active Directory-Daten** -weisen Sie den Besitz des Infrastrukturkomponenten auf IT-Bereich. für Daten, die Active Directory-Domänendienste (AD DS) zur Unterstützung des Unternehmens, z.B. neue Mitarbeiter, neuen Anwendungen und neue Informationen Repositories hinzugefügt werden, sollte eine festgelegte Geschäftseinheiten oder einen Benutzer mit den Daten verknüpft werden.  
  
        -   **Implementieren Sie Business-Driven Lifecycle Management** -lebenszyklusverwaltung für Daten in Active Directory implementiert werden sollte.  
  
        -   **Alle Active Directory-Daten klassifizieren** -Geschäftsinhaber sollten Klassifizierung für Daten in Active Directory bereitstellen. Innerhalb der Klassifizierung Datenmodell sollten die Klassifizierung für die folgenden Active Directory-Daten enthalten sein:  
  
            -   **Systeme** -klassifizieren Server Auffüllungen, deren Betriebssystem ihrer Rolle die Anwendungen auf, und die IT und Geschäftsinhaber des Datensatzes.  
  
            -   **Anwendungen** -Anwendungen nach Funktionen, Benutzer und ihr Betriebssystem zu klassifizieren.  
  
            -   **Benutzer** -Konten in der Active Directory-Installationen, die am wahrscheinlichsten Ziel von Angreifern sein gekennzeichnet und überwacht werden sollten.  
  
## <a name="summary-of-best-practices-for-securing-active-directory-domain-services"></a>Zusammenfassung der Best Practices for Securing Active Directory-Domänendienste  
Die folgende Tabelle enthält eine Zusammenfassung der Empfehlungen in diesem Dokument zum Sichern von AD DS-Installation. Einige bewährten Methoden sind strategischer Natur und umfassende Planung und Implementierung Projekte erforderlich. andere sind taktische und konzentrieren sich auf bestimmte Komponenten von Active Directory und die zugehörige Infrastruktur.  
  
Methoden sind in annähernder Reihenfolge der Priorität, demnach aufgeführt, untere Zahlen bedeuten höheren Priorität. In dem entsprechenden best Practices als präventive oder verschiedene Natur identifiziert werden. Alle diese empfohlenen sollte gründlich getestet und für Eigenschaften und Anforderungen Ihres Unternehmens nach Bedarf geändert.  
  
  
|-|-|-|-|  
||**Best Practice**|**taktisch oder strategisch**|**präventive oder verschiedene**|  
| 1 | Patch für Anwendungen. | Taktische | Präventive |  
| 2 | Patch für Betriebssysteme. | Taktische | Präventive |  
| 3 | Bereitstellen und aktualisieren Sie umgehend Antiviren- und Antischadsoftware in allen Systemen und Überwachung Versuche zu entfernen oder zu deaktivieren. | Taktische | Beide |  
| 4 | Überwachen Sie sensible Active Directory-Objekte bei Änderung und Windows nach Ereignissen, die versuchten Kompromittierung hinweisen. | Taktische | Verschiedene |  
| 5 | Schützen und Überwachen von Konten für Benutzer mit Zugriff auf sensible Daten | Taktische | Beide |  
| 6 | Verhindert, dass die Konten mit rechten auf nicht autorisierte Systeme verwendet werden. | Taktische | Präventive |  
| 7 | Permanente Mitgliedschaft in sehr privilegierten Gruppen zu beseitigen. | Taktische | Präventive |  
| 8 | Kontrollen zum Erteilen temporärer Mitgliedschaften in privilegierten Gruppen bei Bedarf zu implementieren. | Taktische | Präventive |  
| 9 | Implementieren Sie sichere administrative Hosts. | Taktische | Präventive |  
| 10 | Verwenden Sie Anwendungswhitelisting auf Domänencontrollern, administrative Hosts und andere sensible Systeme. | Taktische | Präventive |  
| 11 | kritische Ressourcen zu identifizieren und Priorisieren Sie die Sicherheit und Überwachung. | Taktische | Beide |  
| 12 | Implementieren der geringsten Berechtigungen, die rollenbasierte Zugriffssteuerung für die Verwaltung des Verzeichnisses, die unterstützende Infrastruktur und Domäne Angehörige Systeme. | Strategische | Präventive |  
| 13 | Ältere Systeme und Anwendungen zu isolieren. | Taktische | Präventive |  
| 14 | Außerbetriebnahme von älteren Systemen und Anwendungen. | Strategische | Präventive |  
| 15 | Implementieren sicherer Development Lifecycle-Programme für benutzerdefinierte Anwendungen. | Strategische | Präventive |  
| 16 | Implementieren der Verwaltung Kompatibilität regelmäßig prüfen und Bewerten von Einstellungen mit jeder neuen Version von Hardware oder Software. | Strategische | Präventive |  
| 17 | Migrieren Sie die kritische Ressourcen zu unberührte Gesamtstrukturen mit strenge Sicherheits- und Überwachen von Anforderungen. | Strategische | Beide |  
| 18 | Sicherheit für Endbenutzer zu vereinfachen. | Strategische | Präventive |  
| 19 | Verwenden Sie hostbasierten Firewalls für das Steuern und sichere Kommunikation. | Taktische | Präventive |  
| 20 | Patch für Geräte. | Taktische | Präventive |  
| 21 | Implementieren von Business-orientierte Lifecycle Management für IT-Ressourcen. | Strategische | N/V |  
| 22 | Wiederherstellung nach dem Vorfall Pläne erstellen oder aktualisieren. | Strategische | N/V |  
  


