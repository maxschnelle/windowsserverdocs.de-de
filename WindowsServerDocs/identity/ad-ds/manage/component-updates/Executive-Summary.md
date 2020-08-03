---
ms.assetid: 85ca191c-0cc7-4453-a72c-42060ddf2ea2
title: Kurzfassung
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 3755f1cdaa5dfb49083c9e3c3e8b6a8c4edb40d2
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87518848"
---
# <a name="executive-summary"></a>Kurzfassung

>Gilt für: Windows Server 2012

>[!IMPORTANT]
>Die folgende Dokumentation wurde in 2013 geschrieben und wird nur zu historischen Zwecken bereitgestellt.  Zurzeit überprüfen wir diese Dokumentation und unterliegen Änderungen.  Die aktuellen bewährten Methoden werden möglicherweise nicht angezeigt.

Keine Organisation mit einer IT-Infrastruktur ist gegen Angriffe immun, aber wenn geeignete Richtlinien, Prozesse und Kontrollen implementiert werden, um die Schlüsselsegmente der Computerinfrastruktur eines Unternehmens zu schützen, kann es möglich sein, ein Sicherheitsrisiko zu verhindern, das zu einem umfassenden Kompromiss der Computerumgebung wächst.

Diese Zusammenfassung ist als eigenständiges Dokument gedacht, das den Inhalt des Dokuments zusammenfasst, das Empfehlungen enthält, die Organisationen bei der Verbesserung der Sicherheit Ihrer Active Directory-Installationen unterstützen. Durch die Implementierung dieser Empfehlungen können Organisationen Sicherheitsaktivitäten identifizieren und priorisieren, Schlüsselsegmente der Computerinfrastruktur Ihres Unternehmens schützen und Steuerelemente erstellen, die die Wahrscheinlichkeit erfolgreicher Angriffe auf kritische Komponenten der IT-Umgebung erheblich verringern.

Obwohl in diesem Dokument die häufigsten Angriffe gegen Active Directory und Gegenmaßnahmen erläutert werden, um die Angriffsfläche zu reduzieren, enthält es auch Empfehlungen für die Wiederherstellung im Fall eines umfassenden kompromittierten Problems. Die einzige Möglichkeit zur Wiederherstellung im Falle einer umfassenden Gefährdung von Active Directory besteht darin, dass Sie vor dem Auftreten der Kompromittierung vorbereitet werden.

Die Hauptabschnitte dieses Dokuments lauten:

- Wege der Gefährdung

- Reduzieren der Angriffsfläche für Active Directory

- Überwachen von Active Directory auf Anzeichen für einen Kompromiss

- Planen der Gefährdung

## <a name="avenues-to-compromise"></a>Wege der Gefährdung
Dieser Abschnitt enthält Informationen zu einigen der am häufigsten genutzten Sicherheitsrisiken, die von Angreifern zum kompromittieren der Infrastruktur von Kunden verwendet werden. Sie enthält allgemeine Kategorien von Sicherheitsrisiken und deren Verwendung zum anfänglichen durchdringen der Kunden Infrastrukturen, propagieren der Gefährdung über zusätzliche Systeme und schließlich Active Directory und Domänen Controllern, um die vollständige Kontrolle über die Gesamtstrukturen der Organisation zu erhalten. Es bietet keine detaillierten Empfehlungen zur Behandlung der einzelnen Sicherheitsrisiken, insbesondere in den Bereichen, in denen die Sicherheitsrisiken nicht zum direkten Ziel Active Directory verwendet werden. Allerdings haben wir für jede Art von Sicherheits Anfälligkeit Links zu zusätzlichen Informationen bereitgestellt, die zum Entwickeln von Gegenmaßnahmen und zur Verringerung der Angriffsfläche der Organisation verwendet werden.

Die folgenden Themen sind enthalten:

- **Anfängliche Verletzungs Ziele** : die meisten Informations Sicherheitsverletzungen beginnen mit der Gefährdung kleiner Teile der Infrastruktur eines Unternehmens, häufig ein oder zwei Systeme gleichzeitig. Diese anfänglichen Ereignisse oder Einstiegspunkte in das Netzwerk ausnutzen häufig Schwachstellen, die möglicherweise behoben wurden, aber nicht. Zu den häufigsten Sicherheitsrisiken gehören:
  - Lücken bei Antiviren-und antischadsoftwarebereitstellungen
  - Unvollständiges Patchen
  - Veraltete Anwendungen und Betriebssysteme
  - Fehlkonfiguration
  - Fehlende sichere Anwendungs Entwicklungsverfahren

- **Attraktive Konten für den Diebstahl** von Anmelde Informationen: Angriffe durch Diebstahl von Anmelde Informationen sind solche, bei denen ein Angreifer anfänglich privilegierten Zugriff auf einen Computer in einem Netzwerk erhält und dann frei verfügbare Tools verwendet, um Anmelde Informationen aus den Sitzungen anderer angemeldeter Konten zu extrahieren. Dieser Abschnitt enthält die folgenden Punkte:
  - **Aktivitäten, die die Wahrscheinlichkeit einer Gefährdung erhöhen** : da das Ziel des Diebstahls von Anmelde Informationen in der Regel sehr privilegierte Domänen Konten und "sehr wichtige Personen"-Konten (VIP) ist, ist es für Administratoren wichtig, sich mit Aktivitäten vertraut zu machen, die die Wahrscheinlichkeit eines Erfolgs bei einem Diebstahl von Anmelde Informationen erhöhen. Diese Aktivitäten sind:

    - Anmelden bei ungesicherten Computern mit privilegierten Konten

    - Durchsuchen des Internets mit einem Konto mit hohen Berechtigungen

    - Konfigurieren von lokalen privilegierten Konten mit denselben Anmelde Informationen über Systeme hinweg

    - Übermäßige Auffüllung und übermäßige Verwendung privilegierter Domänen Gruppen

    - Unzureichende Verwaltung der Sicherheit von Domänen Controllern.

  - Rechte Erweiterungen **und** weitergabespezifische Konten, Server und Infrastrukturkomponenten sind in der Regel die Hauptziele von Angriffen gegen Active Directory. Diese Konten sind:

    - Konten mit dauerhafter Berechtigung

    - VIP-Konten

    - Active Directory Konten mit Berechtigungs Anfügung

    - Domänencontroller

    - Andere Infrastrukturdienste, die sich auf die Identitäts-, Zugriffs-und Konfigurations Verwaltung auswirken, z. b. PKI-Server (Public Key-Infrastruktur) und Systems Management Server

## <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory
Dieser Abschnitt konzentriert sich auf technische Kontrollen, um die Angriffsfläche einer Active Directory-Installation zu verringern. Dieser Abschnitt enthält die folgenden Themen:

- Im Abschnitt **privilegierte Konten und Gruppen in Active Directory** werden die Konten und Gruppen mit den höchsten Berechtigungen in Active Directory sowie die Mechanismen erläutert, mit denen privilegierte Konten geschützt werden. In Active Directory sind drei integrierte Gruppen die höchsten Berechtigungs Gruppen im Verzeichnis (Organisations-Admins, Domänen-Admins und Administratoren), obwohl eine Reihe zusätzlicher Gruppen und Konten ebenfalls geschützt werden sollten.

- Der Abschnitt zur **Implementierung von Verwaltungs Modellen mit geringsten Rechten** konzentriert sich auf die Ermittlung des Risikos, dass die Verwendung von Konten mit hohen Berechtigungen für die tägliche Verwaltung und die Bereitstellung von Empfehlungen zur Minderung dieses Risikos.

Übermäßige Berechtigungen werden nicht nur in Active Directory in kompromittierten Umgebungen gefunden. Wenn eine Organisation die Gewohnheit hat, mehr Berechtigungen zu erteilen, als erforderlich ist, wird Sie in der Regel in der gesamten Infrastruktur gefunden:

- In Active Directory

- Auf Mitglieds Servern

- Auf Arbeitsstationen

- In Anwendungen

- In Datenrepository

- Im Abschnitt **Implementieren von sicheren administrativen Hosts** werden sichere administrative Hosts beschrieben, bei denen es sich um Computer handelt, die zur Unterstützung der Verwaltung von Active Directory und verbundenen Systemen konfiguriert sind. Diese Hosts sind für administrative Funktionen reserviert und führen keine Software aus, wie z. b. e-Mail-Anwendungen, Webbrowser oder Produktivitätssoftware (z. b. Microsoft Office).

Dieser Abschnitt enthält die folgenden Punkte:

- **Grundsätze für die Erstellung sicherer administrativer Hosts** : die folgenden allgemeinen Prinzipien sollten berücksichtigt werden:
  - Verwalten Sie niemals ein vertrauenswürdiges System von einem nicht vertrauenswürdigen Host.
  - Verlassen Sie sich beim Ausführen privilegierter Aktivitäten nicht auf einen einzelnen Authentifizierungs Faktor.
  - Vergessen Sie nicht, die physische Sicherheit beim Entwerfen und Implementieren sicherer administrativer Hosts zu vergessen.

- **Sichern von Domänen Controllern gegen Angriffe** : Wenn ein böswilliger Benutzer privilegierten Zugriff auf einen Domänen Controller erhält, kann dieser Benutzer die Active Directory Datenbank und durch Erweiterung sämtliche Systeme und Konten, die von Active Directory verwaltet werden, ändern, beschädigen und zerstören.

Dieser Abschnitt enthält die folgenden Themen:

- **Physische Sicherheit für Domänen Controller** : enthält Empfehlungen für die Bereitstellung physischer Sicherheit für Domänen Controller in Rechenzentren, Zweigstellen und Remote Standorten.

- **Domänen Controller-Betriebssysteme** : enthält Empfehlungen zum Sichern der Domänen Controller-Betriebssysteme.

- **Sichere Konfiguration von Domänen Controllern** : Native und frei verfügbare Konfigurationstools und-Einstellungen können verwendet werden, um sicherheitskonfigurationsbaselines für Domänen Controller zu erstellen, die anschließend von Gruppenrichtlinie Objekten (GPOs) erzwungen werden können.

## <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für einen Kompromiss
Dieser Abschnitt enthält Informationen zu älteren Überwachungs Kategorien und Unterkategorien von Überwachungs Richtlinien (die in Windows Vista und Windows Server 2008 eingeführt wurden) sowie erweiterte Überwachungs Richtlinien (die in Windows Server 2008 R2 eingeführt wurden). Außerdem werden Informationen zu den zu überwachenden Ereignissen und Objekten bereitgestellt, die versuchen, die Umgebung zu kompromittieren, sowie einige zusätzliche Verweise, die zum Erstellen einer umfassenden Überwachungsrichtlinie für Active Directory verwendet werden können.

Dieser Abschnitt enthält die folgenden Themen:

- **Windows** -Überwachungsrichtlinie: Windows-Sicherheits Ereignisprotokolle enthalten Kategorien und Unterkategorien, die bestimmen, welche Sicherheitsereignisse nachverfolgt und aufgezeichnet werden.

- **Empfehlungen** zu Überwachungs Richtlinien: in diesem Abschnitt werden die Standardeinstellungen für die Überwachungsrichtlinie von Windows, die Überwachungs Richtlinien Einstellungen, die von Microsoft empfohlen werden, sowie aggressivere Empfehlungen für Organisationen zum Überwachen kritischer Server und Arbeitsstationen beschrieben.

## <a name="planning-for-compromise"></a>Planen der Gefährdung
Dieser Abschnitt enthält Empfehlungen, die Organisationen dabei unterstützen, sich vor dem Eintreten auf eine Kompromittierung vorzubereiten, Steuerelemente zu implementieren, die ein Kompromittierung-Ereignis erkennen können, bevor eine vollständige Sicherheitsverletzung aufgetreten ist, und Richtlinien für die Reaktion und Wiederherstellung in Fällen bereitstellen, in denen eine vollständige Gefährdung des Verzeichnisses Dieser Abschnitt enthält die folgenden Themen:

- **Vorgehensweise** : enthält Grundsätze und Richtlinien zum Erstellen sicherer Umgebungen, in denen eine Organisation Ihre kritischsten Ressourcen platzieren kann. Diese Richtlinien lauten wie folgt:

    - Erkennen von Prinzipien zum Trennen und sichern kritischer Ressourcen

    - Definieren eines beschränkten, risikobasierten Migrationsplans

    - Nutzen von Migrationen ohne Migration bei Bedarf

    - Implementieren von "Creative Zerstörung"

    - Isolieren von Legacy Systemen und Anwendungen

    - Vereinfachen der Sicherheit für Endbenutzer

- Verwalten **einer sichereren Umgebung** : enthält allgemeine Empfehlungen, die als Richtlinien für die Entwicklung nicht nur effektiver Sicherheit, sondern für eine effektive Lebenszyklus Verwaltung verwendet werden sollen. Dieser Abschnitt enthält die folgenden Themen:

    - **Erstellen von geschäftsorientierten Sicherheitsmethoden für Active Directory** : um den Lebenszyklus der Benutzer, Daten, Anwendungen und Systeme, die von Active Directory verwaltet werden, effektiv zu verwalten, befolgen Sie diese Prinzipien.

        - **Weisen Sie Active Directory Daten einen Geschäfts Besitz** zu, und weisen Sie ihm den Besitz von Infrastrukturkomponenten zu. für Daten, die Active Directory Domain Services (AD DS) hinzugefügt werden, um das Unternehmen zu unterstützen, z. b. neue Mitarbeiter, neue Anwendungen und neue Informations Depots, sollte eine bestimmte Geschäftseinheit oder ein bestimmtes Benutzer mit den Daten verknüpft werden.

        - **Implementieren der geschäftsorientierten Lebenszyklus Verwaltung** : die Lebenszyklus Verwaltung sollte für Daten in Active Directory implementiert werden.

        - **Klassifizieren Sie alle Active Directory Daten** : Geschäftsinhaber sollten die Klassifizierung für Daten in Active Directory bereitstellen. Innerhalb des Daten Klassifizierungs Modells sollte die Klassifizierung für die folgenden Active Directory Daten eingeschlossen werden:

            - **Systeme** : klassifizieren der Server Population, Ihres Betriebssystems, ihrer Rolle, der Anwendungen, die auf Ihnen ausgeführt werden, und der IT-und Geschäftsinhaber von Datensätzen.

            - **Anwendungen** : klassifizieren Sie Anwendungen nach Funktionalität, Benutzerbasis und Betriebssystem.

            - **Benutzer** : die Konten in den Active Directory Installationen, bei denen es sich am ehesten um Angreifer handelt, sollten gekennzeichnet und überwacht werden.

## <a name="summary-of-best-practices-for-securing-active-directory-domain-services"></a>Zusammenfassung der bewährten Methoden zum Sichern von Active Directory Domain Services
In der folgenden Tabelle finden Sie eine Zusammenfassung der Empfehlungen in diesem Dokument zum Sichern einer AD DS-Installation. Einige bewährte Methoden sind strategisch und erfordern umfassende Planungs-und Implementierungsprojekte. andere sind taktisch und konzentriert sich auf bestimmte Komponenten von Active Directory und zugehöriger Infrastruktur.

Die Vorgehensweise wird in der ungefähren Reihenfolge der Priorität aufgeführt, d. h., niedrigere Zahlen weisen eine höhere Priorität auf. Gegebenenfalls werden bewährte Methoden als präventiv oder als Detektiv bezeichnet. Alle diese Empfehlungen sollten bei Bedarf gründlich getestet und geändert werden, um die Merkmale und Anforderungen Ihrer Organisation zu erfüllen.

| **Bewährte Methode** | **Taktisch oder strategisch** | **Vorbeugend oder Detektive** |
|--|--|--|
| Patchen von Anwendungen. | Taktisch | Vorbeugend |
| Patchen von Betriebssystemen. | Taktisch | Vorbeugend |
| Bereitstellen und Aktualisieren von Antiviren-und Antischadsoftware auf allen Systemen und Überwachen von versuchen, Sie zu entfernen oder zu deaktivieren. | Taktisch | Beide |
| Überwachen von sensiblen Active Directory Objekten bei Änderungs versuchen und Fenstern für Ereignisse, die auf einen versuchten Kompromiss hinweisen können. | Taktisch | Ermittelnd |
| Schützen und Überwachen von Konten für Benutzer, die Zugriff auf sensible Daten haben | Taktisch | Beide |
| Verhindern, dass leistungsstarke Konten auf nicht autorisierten Systemen verwendet werden. | Taktisch | Vorbeugend |
| Entfernen Sie permanente Mitgliedschaft in Gruppen mit hohen Berechtigungen. | Taktisch | Vorbeugend |
| Implementieren Sie Steuerelemente, um bei Bedarf temporäre Mitgliedschaften in privilegierten Gruppen zu erteilen. | Taktisch | Vorbeugend |
| Implementieren Sie sichere administrative Hosts. | Taktisch | Vorbeugend |
| Verwenden Sie anwendungswhitelists auf Domänen Controllern, administrativen Hosts und anderen sensiblen Systemen. | Taktisch | Vorbeugend |
| Identifizieren Sie wichtige Assets, und priorisieren Sie Ihre Sicherheit und Überwachung. | Taktisch | Beide |
| Implementieren Sie für die Verwaltung des Verzeichnisses, der unterstützenden Infrastruktur und der in die Domäne eingebundenen Systeme die geringsten Berechtigungen, rollenbasierte Zugriffs Steuerungen. | Strategisch | Vorbeugend |
| Isolieren Sie ältere Systeme und Anwendungen. | Taktisch | Vorbeugend |
| Außerbetriebnahme veralteter Systeme und Anwendungen. | Strategisch | Vorbeugend |
| Implementieren Sie sichere Entwicklungs Lebenszyklus-Programme für benutzerdefinierte Anwendungen. | Strategisch | Vorbeugend |
| Implementieren Sie die Konfigurations Verwaltung, überprüfen Sie die Konformität regelmäßig, und evaluieren Sie Einstellungen mit jeder neuen Hardware-oder Softwareversion | Strategisch | Vorbeugend |
| Migrieren Sie kritische Assets mit strengen Sicherheits-und Überwachungsanforderungen in unberührte Gesamtstrukturen. | Strategisch | Beide |
| Vereinfachen Sie die Sicherheit für Endbenutzer. | Strategisch | Vorbeugend |
| Verwenden Sie Host basierte Firewalls zum Steuern und Sichern der Kommunikation. | Taktisch | Vorbeugend |
| Patchen von Geräten. | Taktisch | Vorbeugend |
| Implementieren Sie die geschäftsorientierte Lebenszyklus Verwaltung für IT-Ressourcen. | Strategisch | – |
| Erstellen oder aktualisieren Sie Wiederherstellungs Pläne für Vorfälle. | Strategisch | Nicht zutreffend |
