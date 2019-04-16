---
ms.assetid: 50bd2566-e03c-4884-b5c4-895c8aab80aa
title: Identifizieren der Teilnehmer am Bereitstellungsprojekt
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 57c24c2b2b48c712445ef7dca453de586d33a130
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="identifying-the-deployment-project-participants"></a>Identifizieren der Teilnehmer am Bereitstellungsprojekt

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Der erste Schritt beim Einrichten eines Bereitstellungsprojekts für Active Directory-Domänendienste (AD DS) wird das Design herstellen und wird Bereitstellung Projektteams, die zum Verwalten der Entwurfsphase und Phase der Bereitstellung des Projekts Active Directory zuständig sind. Darüber hinaus müssen Sie ermitteln, die Personen oder Gruppen, die für die besitzende und Wartung des Verzeichnisses nach Abschluss der Bereitstellung verantwortlich ist.  
  
-   [Definieren von Projekt-spezifische Funktionen](#BKMK_1)  
  
-   [Die Einrichtung einer Besitzer und-Administratoren](#BKMK_2)  
  
-   [Projektteams erstellen](#BKMK_3)  
  
## <a name="BKMK_1"></a>Definieren von Projekt-spezifische Funktionen  
Ein wichtiger Schritt bei der Ermittlung der Projektteams soll die Personen zu identifizieren, die Projekt-spezifische Funktionen enthalten sind. Dazu gehören die Geschäftsleitung, dem Projekt-Architekten und Projektmanager. Diese Personen sind verantwortlich für die Ausführung der Active Directory-Bereitstellungsprojekts.  
  
Nachdem Sie die Projekt-Architekten und Projektmanager ernennen, wird diese Personen Kommunikationskanäle in der gesamten Organisation herzustellen, Projektzeitpläne erstellen und identifizieren die Personen, die Mitglieder der Projektteams, die verschiedene Besitzer ab.  
  
### <a name="executive-sponsor"></a>Geschäftsleitung  
Bereitstellen einer Infrastruktur wie AD DS kann eine weitreichenden auf einer Organisation auswirken. Aus diesem Grund ist es wichtig, dass eine Geschäftsleitung, erkennt den Geschäftswert der Bereitstellung, unterstützt das Projekt auf Management-Ebene und können dazu beitragen, die Konflikte in der gesamten Organisation zu beheben.  
  
### <a name="project-architect"></a>Projekt architect  
Jeder Active Directory-Bereitstellungsprojekts erfordert eine Projekt-Architekten, Entwurfs- und Entscheidungsprozess für die Active Directory verwalten. Der Entwickler bietet Fachwissen zur Unterstützung bei der Prozess beim Entwerfen und Bereitstellen von AD DS.  
  
> [!NOTE]  
> Wenn keine vorhandenen Mitarbeiter in Ihrer Organisation Directory Design auftreten, empfiehlt es sich um ein externer Berater beauftragen Experte in Active Directory-Entwurf und Bereitstellung ist.  
  
Die folgenden: Aufgaben der Active Directory-Projekt Architekten  
  
-   Besitzt des Active Directory-Entwurfs  
  
-   Verstehen und Aufzeichnen der Gründe für die grundlegenden entwurfsentscheidungen  
  
-   Um sicherzustellen, dass das Design der geschäftlichen Anforderungen der Organisation erfüllt  
  
-   Die Einrichtung einer Übereinstimmung zwischen Entwurf, Bereitstellung und Operations-teams  
  
-   Grundlegendes zu den Anforderungen der AD DS-integrierte Anwendungen  
  
Die Active Directory-Entwurf muss es sich um eine Kombination aus Geschäftsziele und technische Entscheidungen widerspiegeln. Aus diesem Grund muss die Projekt-Architekten Designentscheidungen, um sicherzustellen, dass sie die Unternehmensziele ausgerichtet überprüfen.  
  
### <a name="project-manager"></a>Projekt-manager  
Der Projektmanager vereinfacht die Zusammenarbeit Geschäftsbereichen und zwischen Verwaltungsgruppen Technologie. Im Idealfall ist der Projektmanager für Active Directory-Bereitstellung einer Person in der Organisation, die mit der betrieblichen Richtlinien von der IT-Gruppe und die Designanforderungen für die Gruppen, die Vorbereiten der Bereitstellung von AD DS vertraut ist. Überwacht das gesamte Bereitstellungsprojekt, beginnend mit dem Entwurf und Implementierung fortgesetzt, und stellt sicher, dass das Projekt Zeitplan innerhalb des und bleibt. Die folgenden: Aufgaben der Projektmanager  
  
-   Bereitstellen von grundlegenden Projekt planen, wie z. B. die Planung und Budgetierung  
  
-   Fahren auf das Active Directory-Entwurf und Bereitstellung von Projekt Status  
  
-   Sicherstellen, dass die betreffenden Personen jeder Teil des Entwurfsprozesses beteiligt sind.  
  
-   Als zentrale Anlaufstelle für die Active Directory-Bereitstellungsprojekts  
  
-   Einrichten der Kommunikation zwischen Entwurf, Bereitstellung und Operations-teams  
  
-   Herstellen und Aufrechterhalten der Kommunikation mit der Geschäftsleitung im gesamten Bereitstellungsprojekt  
  
## <a name="BKMK_2"></a>Die Einrichtung einer Besitzer und-Administratoren  
In einer Active Directory-Bereitstellungsprojekts sind Personen, die Besitzer sind Handlungen von Verwaltung, um sicherzustellen, Bereitstellung, die Vorgänge abgeschlossen sind und die Active Directory-Entwurf, dass die Spezifikationen die Anforderungen der Organisation zu erfüllen. Besitzer nicht notwendigerweise haben Zugriff auf oder der Verzeichnisinfrastruktur direkt bearbeitet. Administratoren sind die Personen, die verantwortlich für die erforderlichen Bereitstellungsaufgaben ausführen. Administratoren können den Netzwerkzugriff und Berechtigungen erforderlich, um das Verzeichnis und dessen Infrastruktur zu bearbeiten.  
  
Die Rolle des Besitzers ist strategischen und leitender. Besitzer sind verantwortlich für die Kommunikation an Administratoren der erforderlichen Aufgaben für die Implementierung von Active Directory-Entwurf, z. B. die Erstellung neuer Domänencontroller in der Gesamtstruktur. Die Administratoren sind verantwortlich für die Implementierung des Entwurfs im Netzwerk gemäß der Design-Spezifikationen.  
  
In großen Organisationen füllen verschiedene Personen Besitzer und Administratorrollen. in einigen kleineren Unternehmen möglicherweise jedoch die gleiche Person als den Besitzer und der Administrator fungieren.  
  
### <a name="service-and-data-owners"></a>Dienst- und Datenbesitzer  
Verwalten von AD DS täglich umfasst zwei Arten von Besitzer:  
  
-   Dienstbesitzer sind verantwortlich für die Planung und langfristige Wartung der Active Directory-Infrastruktur und sicherstellen, dass das Verzeichnis weiterhin funktioniert und dass die Ziele Sitz in Vereinbarungen zum Servicelevel verwaltet werden  
  
-   Datenbesitzer, die für die Wartung der im Verzeichnis gespeicherten Informationen zuständig sind. Dazu gehören Benutzer- und Computerkonten und Verwaltung von lokalen Ressourcen wie z. B. Mitgliedsservern und Arbeitsstationen.  
  
Es ist wichtig, dass der Active Directory-Dienst und Datenbesitzer frühzeitig zu identifizieren, sodass sie so viel des Entwurfsprozesses möglichst teilnehmen können. Da die Dienst- und Datenbesitzer verantwortlich für den langfristigen Wartungsaufwand für das Verzeichnis sind nach dem Abschluss des Bereitstellungsprojekts, ist es wichtig, für diese Personen Eingabe in Bezug auf die organisatorischen Anforderungen und vertraut, wie und warum bestimmte entwurfsentscheidungen vorgenommen werden. Dienstbesitzer umfassen den Gesamtstrukturbesitzer, die Active Directory Domain Naming System (DNS-) Besitzer und der Besitzer der Website-Topologie. Datenbesitzer enthalten Besitzer der Organisationseinheit (OU).  
  
### <a name="service-and-data-administrators"></a>Dienst- und Administratoren  
Die Ausführung von AD DS umfasst zwei Arten von Administratoren: service und Datenadministratoren. Dienstadministratoren Implementieren der richtlinienentscheidungen Service Besitzer und Behandeln der täglichen Aufgaben im Zusammenhang mit den Verzeichnisdienst und die Infrastruktur verwalten. Dies umfasst das Verwalten von den Domänencontrollern, die hosten den Verzeichnisdienst Verwalten anderer Netzwerkdienste wie DNS, die für AD DS, Steuern der Konfiguration von Einstellungen für die Gesamtstruktur, und sicherstellen, dass das Verzeichnis immer verfügbar ist, erforderlich sind.  
  
Dienstadministratoren sind auch für Aufgaben laufende Active Directory-Bereitstellung, die erforderlich sind, nach Abschluss des ersten Windows Server 2008 Active Directory-Bereitstellungsprozesses verantwortlich. Z. B. als Belastung der Directory erhöhen, Dienstadministratoren Erstellen zusätzlicher Domänencontroller und herstellen oder Vertrauensstellungen zwischen Domänen zu entfernen, je nach Bedarf. Aus diesem Grund muss das Active Directory-Bereitstellungsteam Dienstadministratoren enthalten.  
  
Sie müssen darauf achten, dass nur für vertrauenswürdige Personen in der Organisation Service-Administratorrollen zuweisen können. Da diese Personen die Berechtigung zum Ändern der Systemdateien auf Domänencontrollern verfügen, können sie das Verhalten von AD DS ändern. Sie müssen sicherstellen, dass die Dienstadministratoren in Ihrer Organisation sind Personen, die mit dem operativen vertraut sind und Sicherheitsrichtlinien, die in Ihrem Netzwerk vorhanden sind und verstehen, die mit der Notwendigkeit, diese Richtlinien durchzusetzen.  
  
Datenadministratoren sind Benutzer in einer Domäne, die sowohl für die Verwaltung der Daten, die in AD DS, z. B. Benutzer- und Gruppenkonten gespeichert ist, und die Verwaltung von Computern, die Mitglieder der Domäne sind verantwortlich sind. Datenadministratoren steuern Teilmengen von Objekten innerhalb des Verzeichnisses und haben keine Kontrolle über die Installation oder die Konfiguration des Verzeichnisdiensts.  
  
Administratorkonten für die Daten werden nicht standardmäßig bereitgestellt. Nachdem das Entwurfsteam bestimmt, wie Ressourcen werden für die Organisation verwaltet werden, müssen Domänenbesitzer Daten Administratorkonten erstellen und Delegieren sie die entsprechenden Berechtigungen basierend auf den Satz von Objekten, die für die die Administratoren zuständig sind.  
  
Es empfiehlt sich, die Anzahl der Dienstadministratoren in Ihrer Organisation auf die minimale Anzahl erforderlich, um sicherzustellen, dass die Infrastruktur funktionieren weiterhin zur Verfügung. Die meisten Verwaltungsaufgaben kann von Datenadministratoren ausgeführt werden. Dienstadministratoren müssen eine viel größere Fähigkeit festgelegt werden, da diese sind zuständig für die Verwaltung das Verzeichnis und die Infrastruktur, die sie unterstützt. Datenadministratoren benötigen nur die erforderlichen Kenntnisse für ihren Teil des Verzeichnisses zu verwalten. Aufteilen von Aufgaben auf diese Weise führt kosteneinsparungen für die Organisation, da nur eine kleine Anzahl von Administratoren zum betreiben und warten das gesamte Verzeichnis und dessen Infrastruktur geschult werden muss.  
  
Beispielsweise muss ein Dienstadministrator zu verstehen, wie eine Domäne zu einer Gesamtstruktur hinzufügen. Dazu gehören wie zum Installieren der Software zum Konvertieren von eines Servers zu einem Domänencontroller und DNS-Umgebung zu manipulieren, sodass der Domänencontroller in Active Directory-Umgebung nahtlos zusammengeführt werden kann. Ein Datenadministrator muss nur zu wissen, wie Sie die Daten zu verwalten, denen sie für z. B. das Erstellen von neuen Benutzerkonten für neue Mitarbeiter in ihrer Abteilung verantwortlich sind.  
  
Bereitstellen von AD DS benötigt Koordinierung und die Kommunikation zwischen vielen verschiedenen Gruppen beteiligt der Netzwerkinfrastruktur. Diese Gruppen sollten Dienst- und Datenbesitzer ernennen, die für die Darstellung von verschiedenen Gruppen während des Prozesses Entwurfs- und zuständig sind.  
  
Nach Abschluss des Bereitstellungsprojekts weiterhin diese Dienst- und Datenbesitzer verantwortlich für den Teil der Infrastruktur ihrer Gruppe verwaltet werden. In einer Active Directory-Umgebung sind diese Besitzer der Gesamtstrukturbesitzer, das DNS für AD DS-Besitzer, der Besitzer der Website-Topologie und der Besitzer. In den folgenden Abschnitten werden die Rollen von diesen Dienst- und Datenbesitzer erläutert.  
  
#### <a name="forest-owner"></a>Besitzer der Gesamtstruktur  
Der Gesamtstrukturbesitzer ist in der Regel ein senior Informationen Informationstechnologie (IT)-Manager in der Organisation für die Active Directory-Bereitstellungsprozess zuständig ist, und wer ist letztendlich verantwortlich für die Verwaltung von Dienstleistungen innerhalb der Gesamtstruktur, nachdem die Bereitstellung abgeschlossen ist. Der Gesamtstrukturbesitzer weist Personen So füllen Sie andere Rollen Besitz durch Identifizieren der wichtigsten Mitarbeiter innerhalb der Organisation, die erforderlichen Informationen zur Netzwerkinfrastruktur und verwaltungsanforderungen beitragen können. Der Gesamtstrukturbesitzer ist für Folgendes zuständig:  
  
-   Bereitstellung von Gesamtstruktur-Stammdomäne die Gesamtstruktur erstellen  
  
-   Bereitstellung des ersten Domänencontrollers in jeder Domäne, die für die Gesamtstruktur erforderlichen Domänen erstellen  
  
-   Mitgliedschaft in der Administrator-Gruppen in allen Domänen der Gesamtstruktur  
  
-   Erstellen des Entwurfs der OU-Struktur für jede Domäne in der Gesamtstruktur  
  
-   Delegierung von Verwaltungsrechten an OU-Besitzer  
  
-   Änderung des Schemas  
  
-   Änderungen an Einstellungen für die Gesamtstruktur-Konfiguration  
  
-   Implementierung von bestimmte Richtlinie gruppenrichtlinieneinstellungen, einschließlich der Domäne Benutzer Kontorichtlinien z. B. differenzierte Kennwort- und Kontosperrungsrichtlinie  
  
-   Einstellungen für Unternehmen, die auf Domänencontroller anwenden  
  
-   Alle Einstellungen für Gruppenrichtlinien, die auf Domänenebene angewendet werden  
  
Der Gesamtstrukturbesitzer hat die Berechtigung für die gesamte Gesamtstruktur. Ist die Gesamtstruktur des Besitzers verantwortlich, Gruppenrichtlinien und Business-Richtlinien festlegen und die Personen auswählen, die Administratoren sind. Der Gesamtstrukturbesitzer ist ein Dienstbesitzer.  
  
#### <a name="dns-for-ad-ds-owner"></a>DNS für AD DS-Besitzer  
Der DNS für die AD DS-Besitzer handelt es sich um eine Person, die grundlegende Kenntnisse in der vorhandenen DNS-Infrastruktur und den vorhandenen Namespace der Organisation verfügt.  
  
Der DNS für die AD DS-Besitzer ist für Folgendes zuständig:  
  
-   Als Bindeglied zwischen dem Entwurfsteam und die IT-Gruppe, die DNS-Infrastruktur derzeit besitzt  
  
-   Die Informationen zu den vorhandenen DNS-Namespace der Organisation, die zur Unterstützung bei der Erstellung der neuen Active Directory-Namespace bereitstellen  
  
-   Arbeiten mit dem Bereitstellungsteam sicherstellen, dass den Spezifikationen für das Entwurfsteam die neue DNS-Infrastruktur bereitgestellt wird und dass er ordnungsgemäß ausgeführt wird  
  
-   Verwalten von DNS für die AD DS-Infrastruktur, einschließlich der DNS-Serverdienst und DNS-Daten  
  
Der DNS für die AD DS-Besitzer ist ein Dienstbesitzer.  
  
#### <a name="site-topology-owner"></a>Standorttopologiebesitzer  
Der Besitzer der Website-Topologie ist mit dem Netzwerk der Organisation, einschließlich der Zuordnung der einzelnen Subnetze, Router und Netzwerk-Bereiche, die über langsame Verbindungen verbunden sind die physische Struktur vertraut. Der Besitzer der Website-Topologie ist für Folgendes zuständig:  
  
-   Grundlegendes zu der physischen Netzwerktopologie und Einfluss der AD DS  
  
-   Verstehen, wie die Active Directory-Bereitstellung des Netzwerks auswirkt.  
  
-   Bestimmen der logischen Active Directory-Standorte, die erstellt werden müssen  
  
-   Standortobjekte für Domänencontroller aktualisieren, wenn ein Subnetz hinzugefügt wird, geändert oder entfernt  
  
-   Erstellen standortverknüpfungen, Standortverknüpfungsbrücken und manuelle Verbindungsobjekte  
  
Der Besitzer der Website-Topologie ist ein Dienstbesitzer.  
  
#### <a name="ou-owner"></a>OU-Besitzer  
Der Besitzer ist verantwortlich für die Verwaltung von Daten, die im Verzeichnis gespeichert. Diese Person muss mit dem operativen vertraut sind und Sicherheitsrichtlinien, die im Netzwerk vorhanden sind. OU-Besitzer können nur solche Tasks, die von den Dienstadministratoren an sie delegiert wurden ausführen, und sie können nur solche Tasks ausführen, für die Organisationseinheiten, denen sie zugewiesen sind. Die folgenden: Aufgaben, die dem Besitzer zugewiesen werden können  
  
-   Alle Verwaltungsaufgaben in ihren zugewiesenen Organisationseinheiten ausführen  
  
-   Verwalten von Arbeitsstationen und Servern, die Mitglieder einer Organisationseinheit zugewiesen sind  
  
-   Delegieren von Berechtigungen für lokale Administratoren in ihren zugewiesenen Organisationseinheiten  
  
Der Besitzer ist ein Datenbesitzer.  
  
## <a name="BKMK_3"></a>Projektteams erstellen  
Active Directory-Projektteams sind temporäre Gruppen, die zum Abschließen der Aufgaben zum Entwurf und zur Bereitstellung von Active Directory zuständig sind. Nach Abschluss der Active Directory-Bereitstellungsprojekts Verantwortung für die Besitzer für das Verzeichnis, und die Projektteams auflösen können.  
  
Die Größe der Projektteams variiert je nach der Größe der Organisation. In kleinen Unternehmen können Sie eine einzelne Person betreffen mehrere Bereiche Verantwortung in einem Projektteam und mehr als einer Phase der Bereitstellung beteiligt sein. Große Organisationen möglicherweise größere Teams mit anderen Personen oder sogar verschiedene Teams, die für die verschiedenen Bereiche des verantwortlich. Die Größe der Teams ist nicht wichtig, solange alle Bereiche der Verantwortung zugewiesen sind, und die Entwurfsziele der Organisation erfüllt werden.  
  
### <a name="identifying-potential-forest-owners"></a>Identifizieren potenzielle  
Identifizieren Sie die Gruppen in Ihrer Organisation, die besitzen und kontrollieren die erforderlichen Ressourcen für Verzeichnisdienste für Benutzer im Netzwerk bereitstellen. Diese Gruppen gelten als mögliche Gesamtstrukturbesitzer.  
  
Die Trennung der Dienst- und -Verwaltung in AD DS ermöglicht es der Infrastruktur, die IT-Gruppe (oder Gruppen) einer Organisation verwalten den Verzeichnisdienst in jeder Gruppe Lokale Administratoren die Daten zu verwalten, die eigene Gruppen angehört. Potenzielle haben die erforderlichen Berechtigungen für die Netzwerkinfrastruktur, Bereitstellung und Unterstützung von AD DS.  
  
Für Organisationen, die eine zentrale IT-Gruppe-Infrastruktur verfügen, ist die IT-Gruppe in der Regel der Gesamtstrukturbesitzer und daher der möglichen Gesamtstrukturbesitzer für alle zukünftigen Bereitstellungen. Organisationen, die eine Reihe von unabhängigen IT-Infrastruktur sind Gruppen eine Reihe von möglichen Gesamtstrukturbesitzer. Wenn Ihre Organisation bereits eine Active Directory-Infrastruktur verfügt, sind keine aktuellen Gesamtstrukturbesitzer auch mögliche Besitzer von Gesamtstrukturen für die Bereitstellung neuer.  
  
Wählen Sie eine der Gesamtstrukturbesitzer des potenziellen als der Gesamtstrukturbesitzer für jede Gesamtstruktur fungieren, die Sie für die Bereitstellung in Betracht ziehen. Diese mögliche Gesamtstrukturbesitzer sind verantwortlich für die Arbeit mit dem Entwurfsteam, um zu bestimmen, ob die Gesamtstruktur tatsächlich bereitgestellt wird oder wenn eine alternative Vorgehensweise (z. B. das Beitreten zu einer anderen vorhandenen Gesamtstruktur) eine bessere Verwendung der verfügbaren Ressourcen und weiterhin ihren Anforderungen entspricht. Der Gesamtstrukturbesitzer (oder Besitzer) in Ihrer Organisation sind Mitglieder der Active Directory-Entwicklungsteam.  
  
### <a name="establishing-a-design-team"></a>Einrichten eines Entwicklungsteams  
Das Active Directory-Entwicklungsteam ist verantwortlich für das Sammeln der Informationen, die zum treffen von Entscheidungen über die Active Directory-Entwurf der logischen Struktur erforderlich.  
  
Die folgenden: Aufgaben der das Entwurfsteam  
  
-   Bestimmen, wie viele Gesamtstrukturen und Domänen erforderlich sind und welche die Beziehungen zwischen den Gesamtstrukturen und Domänen  
  
-   Arbeiten mit Datenbesitzer sicherstellen, dass das Design ihre Sicherheits- und administrative Anforderungen entspricht.  
  
-   Arbeiten mit den aktuellen Netzwerkadministratoren, um sicherzustellen, dass die aktuelle Netzwerkinfrastruktur Design unterstützt und das Design nicht nachteilig auf vorhandene Anwendungen bereitgestellt werden, auf das Netzwerk auswirkt  
  
-   Arbeiten mit der Sicherheitsgruppe der Organisation Vertretern, um sicherzustellen, dass das Design eingerichteten Sicherheitsrichtlinien erfüllt  
  
-   Entwerfen OU-Strukturen, die die entsprechende Maß an Schutz und die richtigen Delegierung von Autorität für die Datenbesitzer zulassen  
  
-   Arbeiten mit dem Bereitstellungsteam den Entwurf Testen in einem Labor Umgebung, um sicherzustellen, dass sie als geplant und ändern das Design als erforderlich, um Probleme zu beheben, die auftreten  
  
-   Erstellen eines Standortentwurfs-Topologie, erfüllt die Replikation der Gesamtstruktur und Überladung der verfügbaren Bandbreite zu verhindern. Weitere Informationen zum Entwerfen der Standorttopologie finden Sie unter [entwerfen die Website-Topologie für Windows Server 2008 AD DS](https://technet.microsoft.com/library/cc772013.aspx).  
  
-   Arbeiten mit dem Bereitstellungsteam stellen Sie sicher, dass das Design ordnungsgemäß implementiert ist  
  
Das Entwurfsteam umfasst die folgenden Elemente:  
  
-   Potenzielle  
  
-   Projekt architect  
  
-   Projekt-manager  
  
-   Personen, die für das Einrichten und Verwalten von Sicherheitsrichtlinien auf das Netzwerk zuständig sind  
  
Während der Erstellung von logischen Struktur identifiziert das Entwurfsteam die anderen Besitzer. Diese Personen müssen Starten des Entwurfsprozesses teilnehmen, als sie erkannt werden. Nachdem das Bereitstellungsprojekt für das Bereitstellungsteam übergeben wird, ist das Entwurfsteam verantwortlich für die Überwachung des Bereitstellungsprozesses, um sicherzustellen, dass das Design ordnungsgemäß implementiert ist. Das Entwurfsteam ändert auch das Design basierend auf Feedback von Tests.  
  
### <a name="establishing-a-deployment-team"></a>Einrichten einer Bereitstellungsteam  
Das Active Directory-Bereitstellung-Team ist verantwortlich für das Testen und implementieren die Active Directory-Entwurf der logischen Struktur. Dies umfasst die folgenden Aufgaben:  
  
-   Einrichten einer testumgebung, die die produktionsumgebung ausreichend emuliert  
  
-   Testen das Design durch die Implementierung der vorgeschlagenen Struktur der Gesamtstruktur und Domäne in einer testumgebung, um sicherzustellen, dass die Ziele für jeden Besitzer erfüllt  
  
-   Entwickeln und Testen alle Migrationsszenarien vorgeschlagen, die für den Entwurf in einer testumgebung  
  
-   Und stellen Sie sicher, dass für jeden einzelnen Benutzer auf den Testprozess abmeldet, stellen Sie sicher, dass die richtigen Designfeatures testen  
  
-   Testen des Bereitstellungsvorgangs in einer Umgebung mit des Pilotprojekts  
  
Wenn das Design und die Testaufgaben abgeschlossen sind, führt das Bereitstellungsteam die folgenden Aufgaben aus:  
  
-   Erstellt die Gesamtstrukturen und Domänen gemäß der Active Directory-Entwurf der logischen Struktur  
  
-   Erstellt die Sites und Standortverknüpfungsobjekte bei Bedarf auf den Entwurf der Standorttopologie basierend  
  
-   Stellen Sie sicher, dass die DNS-Infrastruktur für die Unterstützung von AD DS konfiguriert ist und dass alle neuen Namespaces in der Organisation vorhandenen Namespaces integriert sind  
  
Das Active Directory-Bereitstellungsteam umfasst die folgenden Elemente:  
  
-   Besitzer der Gesamtstruktur  
  
-   DNS für AD DS-Besitzer  
  
-   Standorttopologiebesitzer  
  
-   OU-Besitzer  
  
Das Bereitstellungsteam funktioniert mit den Dienst- und Administratoren in der Bereitstellungsphase, um sicherzustellen, dass Mitglieder der Operations-Teams mit dem neuen Entwurf vertraut sind. Dadurch stellen Sie sicher einen gleichmäßigen Übergang des Besitzes nach Abschluss des Bereitstellungsvorgangs. Nach Abschluss des Bereitstellungsprozesses übergibt das Betriebsteam die Verantwortung für die Verwaltung der neuen Active Directory-Umgebung.  
  
### <a name="documenting-the-design-and-deployment-teams"></a>Dokumentieren den Entwurf und Bereitstellung von teams  
Dokumentieren Sie die Namen und Kontaktinformationen für Personen, die in den Entwurf und die Bereitstellung von AD DS teilnimmt. Bestimmen Sie, wer auf die Entwurfs- und Teams für jede Rolle zuständig ist. Diese Liste enthält zunächst die mögliche Gesamtstrukturbesitzer, Projektmanager und Architekten Projekt. Wenn Sie die Anzahl der Gesamtstrukturen, die Sie bereitstellen festlegen, müssen Sie möglicherweise neue Designteams für weitere Gesamtstrukturen zu erstellen. Beachten Sie, dass Sie der Dokumentation zu aktualisieren, wie die Team-Mitgliedschaften ändern und die verschiedenen Active Directory-Besitzer zu, während der Erstellung identifizieren benötigen. Herunterladen Sie bei einem Arbeitsblatt dokumentieren die Entwurfs- und Teams für jede Gesamtstruktur unterstützen Sie beim Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip vom Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), und öffnen Sie "Design und Team Informationen zur Bereitstellung" (DSSLOGI_1.doc).  
  


