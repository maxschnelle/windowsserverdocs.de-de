---
ms.assetid: 50bd2566-e03c-4884-b5c4-895c8aab80aa
title: Bestimmen der Teilnehmer am Bereitstellungsprojekt
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 962825494c613dfef808ce54dfba22727abf6878
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834651"
---
# <a name="identifying-the-deployment-project-participants"></a>Bestimmen der Teilnehmer am Bereitstellungsprojekt

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der erste Schritt bei der Herstellung von einem Bereitstellungsprojekt für Active Directory Domain Services (AD DS) wird zum Herstellen des Entwurfs und Bereitstellung Projektteams, die verantwortlich für die Verwaltung der Entwurfsphase und der Phase der Bereitstellung des Active Directory-Projekts werden der Reihe. Darüber hinaus müssen Sie ermitteln, die Personen und Gruppen für Besitz und verwalten das Verzeichnis aus, nach dem Abschluss der Bereitstellung verantwortlich ist.  
  
-   [Definieren von projektspezifischen Rollen](#BKMK_1)  
  
-   [Einrichten der Besitzer und Administratoren](#BKMK_2)  
  
-   [Erstellen von Projekt-teams](#BKMK_3)  
  
## <a name="BKMK_1"></a>Definieren von projektspezifischen Rollen  
Ein wichtiger Schritt bei der Herstellung der Projektteams ist um Personen zu identifizieren, die projektspezifische Rollen enthalten sind. Dazu gehören dem ausführenden Auftraggeber der Projektarchitekt und der Projektmanager. Diese Personen sind verantwortlich für die Ausführung des Active Directory-Bereitstellungsprojekts.  
  
Nachdem Sie die Projektarchitekt und der Projektmanager beauftragen, diese Personen Kommunikationskanäle in der gesamten Organisation einzurichten, erstellen Projektzeitpläne und identifizieren Sie die Personen, die Mitglieder der Projektteams, beginnend mit ist der verschiedene Besitzer.  
  
### <a name="executive-sponsor"></a>Ausführenden Auftraggeber  
Bereitstellen einer Infrastruktur wie AD DS kann eine breit gefächerte auf einer Organisation auswirken. Aus diesem Grund ist es wichtig, um einen Sponsor erhalten, die den Geschäftswert der Bereitstellung erkennt, das Projekt, bei der Unternehmensführung unterstützt und Lösen von Konflikten in der gesamten Organisation helfen.  
  
### <a name="project-architect"></a>Project architect  
Jede Active Directory-Bereitstellungsprojekts ist erforderlich, ein Projektarchitekt, um den Active Directory Entwurfs- und zur entscheidungsfindung zu verwalten. Der Architekt bietet technischen Fachkenntnisse, um den Prozess für das Entwerfen und Bereitstellen von AD DS unterstützen.  
  
> [!NOTE]  
> Bei keinem vorhandenen Mitarbeiter in Ihrer Organisation Directory-Designs, die auftreten, empfiehlt es sich um einen externen Berater zu engagieren, der Experte in Active Directory-Entwurf und Bereitstellung.  
  
Die Zuständigkeiten der Active Directory-Projekt-Architekt umfassen Folgendes:  
  
-   Besitzer von Active Directory-Designs  
  
-   Verstehen und die Gründe für wichtige entwurfsentscheidungen aufzeichnen  
  
-   Sicherstellen, dass der Entwurf die geschäftlichen Anforderungen der Organisation erfüllt  
  
-   Herstellen einer Übereinstimmung zwischen dem Entwurf, Bereitstellung und Operations-teams  
  
-   Grundlegendes zu den Anforderungen von AD DS-integrierte Anwendungen  
  
Die letzte Active Directory-Entwurf muss es sich um eine Kombination von Unternehmenszielen und technische Entscheidungen widerspiegeln. Aus diesem Grund muss der Projektarchitekt prüfen, entwurfsentscheidungen, um sicherzustellen, dass sie die geschäftlichen Ziele ausgerichtet.  
  
### <a name="project-manager"></a>Projektmanager  
Der Projektmanager erleichtert die Zusammenarbeit Unternehmenseinheiten und zwischen Verwaltungsgruppen Technologie. Im Idealfall ist der Projektmanager für Active Directory-Bereitstellung ein Benutzer innerhalb der Organisation, die mit den betrieblichen Richtlinien von der IT-Gruppe und die entwurfsanforderungen für die Gruppen, die Vorbereitung der Bereitstellung von AD DS sind vertraut ist. Der Projektmanager die gesamte Bereitstellungsprojekt überwacht, beginnend mit Design aus, und Sie den Vorgang fortsetzen, durch die Implementierung und stellt sicher, dass das Projekt nach Zeitplan und im Rahmen des Budgets bleiben. Die Aufgaben des Projektmanagers umfassen Folgendes:  
  
-   Einfaches Projekt planen, wie z. B. die Planung und-Budgetierung bereitstellen  
  
-   Status für das Active Directory-Entwurf und Bereitstellung von Projekt vorantreiben  
  
-   Sicherstellen, dass die entsprechenden Personen in jedem Teil des Entwurfsprozesses beteiligt sind  
  
-   Dient als zentrale Kontaktstelle für die Active Directory-Bereitstellungsprojekts  
  
-   Beim Herstellen der Kommunikation zwischen dem Entwurf, Bereitstellung und Operations-teams  
  
-   Einrichtung und Wartung der Kommunikation mit dem ausführenden Auftraggeber in das Bereitstellungsprojekt enthält Artefakte  
  
## <a name="BKMK_2"></a>Einrichten der Besitzer und Administratoren  
In einer Active Directory-Bereitstellungsprojekts sind Personen, die Besitzer sind frei, die verantwortlich Verwaltung, um Sie sicher, dass die Bereitstellung, die Aufgaben abgeschlossen sind und dieser Active Directory-Designs, dass die Spezifikationen die Anforderungen der Organisation zu erfüllen. Besitzer nicht notwendigerweise Zugriff auf oder die Directory-Infrastruktur direkt bearbeiten. Administratoren sind die Personen, die für die Durchführung der erforderlichen Bereitstellungsaufgaben verantwortlich. Administratoren können den Zugriff auf das Netzwerk und die erforderlichen Berechtigungen zum Bearbeiten des Verzeichnisses und seiner Infrastruktur.  
  
Die Rolle des Besitzers ist strategische und Manager beschäftigt. Besitzer sind verantwortlich für die Kommunikation mit Administratoren der erforderlichen Aufgaben für die Implementierung von Active Directory-Designs wie z. B. die Erstellung neuer Domänencontroller in der Gesamtstruktur. Die Administratoren sind dafür verantwortlich, für den Entwurf entsprechend der Design-Spezifikationen implementieren.  
  
In großen Organisationen geben die verschiedene Personen Rollen "Besitzer" und "Administrator; in einigen kleinen Organisationen möglicherweise jedoch die gleiche Person als den Besitzer und der Administrator fungieren.  
  
### <a name="service-and-data-owners"></a>Dienst- und Besitzer  
Verwalten von AD DS auf täglicher Basis umfasst zwei Arten von Besitzer:  
  
-   Dienst-Besitzer, die sind verantwortlich für die Planung und langfristige Wartung von Active Directory-Infrastruktur und sicherstellen, dass das Verzeichnis weiterhin funktionsfähig ist und die Ziele, die in den Vereinbarungen zum Servicelevel eingerichtet, verwaltet werden  
  
-   Der Besitzer der Daten, die verantwortlich für die Verwaltung der Informationen im Verzeichnis gespeichert sind. Dies schließt Benutzer und Computer-kontoverwaltung und Verwaltung von lokalen Ressourcen wie z. B. MemberServer und Arbeitsstationen.  
  
Es ist wichtig, um die Active Directory-Dienst und die Daten Besitzer frühzeitig zu erkennen, damit sie so großen Teil des Entwurfsprozesses möglichst teilnehmen können. Da die Dienst- und Besitzer für die langfristige Wartung des Verzeichnisses verantwortlich sind, nach Abschluss des Bereitstellungsprojekts, ist es wichtig, dass diese Personen als Eingabe in Bezug auf die organisatorischen Anforderungen und mit vertraut sein, wie und warum Einige entwurfsentscheidungen erfolgen. Dienstbesitzer gehören die Gesamtstrukturbesitzer, der Besitzer des Active Directory Domain Naming System (DNS) und der Besitzer der Website-Topologie. Besitzer der Daten enthalten, Besitzer der Organisationseinheit (OU).  
  
### <a name="service-and-data-administrators"></a>Dienst- und Administratoren  
Der Vorgang der AD DS umfasst zwei Arten von Administratoren: service und Datenadministratoren. Dienstadministratoren richtlinienentscheidungen Dienstbesitzer implementieren und Verarbeiten der täglichen Aufgaben im Zusammenhang mit Wartung und der Infrastruktur. Dazu gehören, verwalten die Domänencontroller, auf denen sind, die der Directory-Dienst hostet, Verwalten von anderen Netzwerkdiensten, wie z. B. DNS, der für AD DS erforderlich sind, Steuern der Konfiguration von Einstellungen für die Gesamtstruktur und sicherstellen, dass das Verzeichnis befindet sich immer verfügbar.  
  
Dienstadministratoren sind auch zuständig für den Abschluss der laufender Active Directory-Bereitstellungsaufgaben, die erforderlich sind, nachdem die anfängliche Windows Server 2008 Active Directory-Bereitstellungsvorgang abgeschlossen ist. Z. B. als Anforderungen an die Erhöhung der Verzeichnis, Dienstadministratoren zusätzliche Domänencontroller zu erstellen und einrichten oder Vertrauensstellungen zwischen Domänen zu entfernen, je nach Bedarf. Aus diesem Grund muss das Active Directory-Bereitstellungsteam Dienstadministratoren enthalten.  
  
Sie müssen sorgfältig Dienstadministratorrollen nur für vertrauenswürdige Personen in der Organisation zugewiesen sein. Da diese Personen die Möglichkeit, ändern die Systemdateien auf einem Domänencontroller verfügen, können sie das Verhalten von AD DS ändern. Sie müssen sicherstellen, dass die Dienstadministratoren in Ihrer Organisation sind Personen, die mit die Betriebsdatenbank vertraut sind und von Sicherheitsrichtlinien, die in Ihrem Netzwerk sind und wer verstehen, müssen diese Richtlinien durchzusetzen.  
  
Datenadministratoren sind Benutzer in einer Domäne dafür verantwortlich, sowohl sind für die Verwaltung von Daten, die in AD DS wie z. B. Benutzer- und Gruppenkonten gespeichert werden und für die Verwaltung von Computern, die Mitglieder der Domäne sind. Data-Administratoren steuern, Teilmengen von Objekten innerhalb des Verzeichnisses und haben keinen Einfluss auf die Installation oder Konfiguration des Verzeichnisdiensts.  
  
Administratorkonten für die Daten werden nicht standardmäßig bereitgestellt. Nachdem das Entwurfsteam bestimmt, wie Ressourcen werden für die Organisation verwaltet werden, müssen Domänenbesitzer Administratorkonten für Daten erstellen und Delegieren sie die entsprechenden Berechtigungen, die basierend auf den Satz von Objekten, die für die Administratoren sind, verantwortlich sein .  
  
Es wird empfohlen, um die Anzahl der Administratoren in Ihrer Organisation, die minimale Anzahl erforderlich, um sicherzustellen, dass die Infrastruktur weiterhin funktionsfähig. Die meisten Verwaltungsaufgaben kann von Datenadministratoren ausgeführt werden. Dienstadministratoren müssen eine viel größere Qualifikation festgelegt werden, da sie verantwortlich sind für die Verwaltung des Verzeichnisses und der Infrastruktur, die es unterstützt. Datenadministratoren benötigen nur die erforderlichen Kenntnisse für ihren Teil des Verzeichnisses verwalten. Division arbeitsvorgaben auf diese Weise führt kosteneinsparungen für Unternehmen, da nur eine kleine Anzahl von Administratoren zum betreiben und Verwalten des gesamten Verzeichnisses und seiner Infrastruktur trainiert werden muss.  
  
Beispielsweise muss ein Dienstadministrator zu verstehen, wie Sie eine Domäne in einer Gesamtstruktur hinzufügen. Dies schließt wie zum Installieren der Software zum Konvertieren von eines Servers in einem Domänencontroller und DNS-Umgebung zu bearbeiten, sodass der Domänencontroller nahtlos in Active Directory-Umgebung zusammengeführt werden kann. Ein Datenadministrator muss nur wissen, wie Sie die spezifischen Daten zu verwalten, denen sie für die beispielsweise durch die Erstellung von neuen Benutzerkonten für neue Mitarbeiter des Fachbereichs verantwortlich sind.  
  
Bereitstellen von AD DS erfordert, Koordination und Kommunikation zwischen vielen verschiedenen Gruppen, die in den Vorgang der Netzwerkinfrastruktur einbezogen. Diese Gruppen sollten Dienst- und Datenbesitzer beauftragen, die für die verschiedenen Gruppen darstellen, während der Entwurfs-und Bereitstellung zuständig sind.  
  
Nachdem das Bereitstellungsprojekt abgeschlossen ist, weiterhin diese Besitzer Dienst- und verantwortlich für den Teil der Infrastruktur, die von der Gruppe verwaltet werden. In einer Active Directory-Umgebung sind diese Besitzer auf, der Gesamtstrukturbesitzer, das DNS für AD DS-Besitzer, der Besitzer der Website-Topologie und der Besitzer der Organisationseinheit. Die Rollen der diese Besitzer Dienst und die Daten werden in den folgenden Abschnitten erläutert.  
  
#### <a name="forest-owner"></a>Gesamtstrukturbesitzer  
Der Gesamtstrukturbesitzer ist in der Regel einen leitenden Informationen Informationstechnologie (IT)-Manager in der Organisation, für den Active Directory-Bereitstellungsprozess zuständig ist und für wen ist letztendlich verantwortlich für die Verwaltung der Bereitstellung von Diensten in der Gesamtstruktur nach, der Bereitstellung ist abgeschlossen. Der Gesamtstrukturbesitzer weist die Personen, die zum Ausfüllen der anderen Rollen der dateneigentümerschaft durch Identifizieren der wichtigsten Mitarbeiter innerhalb der Organisation, die erforderlichen Informationen zur Netzwerkinfrastruktur und verwaltungsanforderungen beitragen können. Der Gesamtstrukturbesitzer ist für Folgendes zuständig:  
  
-   Bereitstellung von Gesamtstruktur-Stammdomäne die Gesamtstruktur erstellen  
  
-   Bereitstellung des ersten Domänencontrollers in jeder Domäne, um die Domänen, die erforderlich sind, für die Gesamtstruktur zu erstellen  
  
-   Mitgliedschaften, die der Administrator-Gruppen in allen Domänen der Gesamtstruktur  
  
-   Erstellen des Entwurfs der OE-Struktur für jede Domäne in der Gesamtstruktur  
  
-   Delegierung von Verwaltungsrechten OU-Besitzern  
  
-   Änderungen am schema  
  
-   Änderungen an den Gesamtstruktur-Konfigurationseinstellungen  
  
-   Implementierung von bestimmte Gruppenrichtlinien-Richtlinieneinstellungen, einschließlich der Domäne Benutzer Kontorichtlinien wie z. B. eine differenzierte Kennwort- und Sperrrichtlinien  
  
-   Business-Richtlinieneinstellungen, die für Domänencontroller gelten  
  
-   Alle anderen gruppenrichtlinieneinstellungen, die auf der Domänenebene angewendet werden  
  
Der Gesamtstrukturbesitzer hat die Berechtigung über die vollständige Gesamtstruktur. Es ist Aufgabe des Besitzers der Gesamtstruktur, Gruppenrichtlinien und Business-Richtlinien einzurichten und wählen Sie die Personen, die Dienstadministratoren sind. Der Gesamtstrukturbesitzer ist der Dienstbesitzer eines.  
  
#### <a name="dns-for-ad-ds-owner"></a>DNS für AD DS-Besitzer  
Das DNS für AD DS-Besitzer ist eine Person, die umfassende Informationen zu den vorhandenen DNS-Infrastruktur und dem vorhandenen Namespace des Unternehmens verfügt.  
  
Der DNS für den Besitzer der AD DS ist für Folgendes zuständig:  
  
-   Dient als Verbindungsglied zwischen dem Designteam und die IT-Gruppe, die derzeit im Besitz die DNS-Infrastruktur ist  
  
-   Die Informationen zu vorhandenen DNS-Namespace der Organisation bei der Erstellung der neuen Active Directory-namespace  
  
-   Arbeiten mit dem Bereitstellungsteam sicherstellen, dass die neue DNS-Infrastruktur, gemäß der Spezifikationen des das Designteam bereitgestellt wird und, dass er ordnungsgemäß funktioniert  
  
-   Verwalten von DNS für AD DS-Infrastruktur, einschließlich der DNS-Serverdienst und DNS-Daten  
  
Das DNS für AD DS-Besitzer ist ein Besitzer des Diensts.  
  
#### <a name="site-topology-owner"></a>Standorttopologiebesitzer  
Der Besitzer der Website-Topologie ist vertraut, mit der physischen Struktur von Netzwerk der Organisation, einschließlich Zuordnung der einzelnen Subnetze und Router Netzwerkbereiche, die über langsame Verbindungen verbunden sind. Der Besitzer der Website-Topologie ist für Folgendes zuständig:  
  
-   Verstehen der physischen Netzwerktopologie sowie die Auswirkungen auf AD DS  
  
-   Verstehen der Auswirkungen der Active Directory-Bereitstellung auf des Netzwerks  
  
-   Bestimmen die logischen Active Directory-Standorte, die erstellt werden müssen  
  
-   Standortobjekte für Domänencontroller aktualisieren, wenn ein Subnetz hinzugefügt wird, geändert oder entfernt  
  
-   Erstellen standortverknüpfungen, Standortverknüpfungsbrücken und manuelle Verbindungsobjekte  
  
Der Besitzer der Website-Topologie ist ein Besitzer des Diensts.  
  
#### <a name="ou-owner"></a>Besitzer der Organisationseinheit  
Der Besitzer der Organisationseinheit ist verantwortlich für die Verwaltung von Daten im Verzeichnis gespeichert. Diese Person muss vertraut, mit der Betriebs- und Sicherheitsrichtlinien, die sich auf das Netzwerk befinden. Führen Sie OU-Besitzer können nur solche Tasks, die von den Dienstadministratoren an sie delegiert wurden, und sie können nur solche Tasks ausführen, auf die Organisationseinheiten, die sie zugewiesen sind. Die folgenden: Aufgaben, die Besitzer der Organisationseinheit zugewiesen werden können  
  
-   Durchführen von Verwaltungsaufgaben für alle Konto in ihrer zugewiesenen Organisationseinheit  
  
-   Verwalten von Arbeitsstationen und Mitgliedsservern, die Mitglied ihrer Organisationseinheit zugewiesen sind.  
  
-   Delegieren von Berechtigungen für lokale Administratoren in ihrer zugewiesenen Organisationseinheit  
  
Der Besitzer der Organisationseinheit ist einem Datenbesitzer.  
  
## <a name="BKMK_3"></a>Erstellen von Projekt-teams  
Active Directory-Projektteams sind temporäre Gruppen, die zum Abschließen der Active Directory-Entwurf und Bereitstellung von Aufgaben verantwortlich sind. Wenn die Active Directory-Bereitstellungsprojekts abgeschlossen ist, die Besitzer verantwortlich für das Verzeichnis, und die Projektteams ösen können.  
  
Die Größe der Projektteams variiert entsprechend der Größe der Organisation. In kleinen Unternehmen kann eine einzelne Person mehrere Zuständigkeitsbereiche in einem Projektteam behandelt und in mehreren Phasen der Bereitstellung einbezogen werden. Große Organisationen möglicherweise größere Teams mit verschiedenen Personen oder sogar von verschiedenen Teams, die für die verschiedenen Bereiche der Verantwortung. Die Größe des Teams ist nicht wichtig, solange alle Zuständigkeitsbereiche zugewiesen sind, und die Ziele beim Entwurf des Unternehmens erfüllt werden.  
  
### <a name="identifying-potential-forest-owners"></a>Identifizieren mögliche Gesamtstrukturbesitzer  
Identifizieren Sie die Gruppen in Ihrer Organisation, die besitzen und kontrollieren die Ressourcen, die zum Bereitstellen von Verzeichnisdiensten für Benutzer im Netzwerk erforderlich sind. Diese Gruppen gelten als mögliche Gesamtstrukturbesitzer.  
  
Die Trennung von Dienst- und -Verwaltung in AD DS ermöglicht die Infrastruktur, die IT-Gruppe (oder Gruppen) einer Organisation, den Directory-Dienst zu verwalten, während der lokale Administratoren in jeder Gruppe die Daten zu verwalten, die ihre eigenen Gruppen angehört. Mögliche Gesamtstrukturbesitzer haben die erforderliche Berechtigung, über die Netzwerkinfrastruktur, bereitstellen und Unterstützung für AD DS.  
  
Für Organisationen mit einer zentralisierten Infrastruktur IT-Gruppe ist die IT-Gruppe in der Regel der Gesamtstrukturbesitzer und somit die potenziellen Gesamtstrukturbesitzer für alle zukünftigen Bereitstellungen an. Organisationen, die eine Zahl enthalten unabhängige IT-Infrastruktur-Gruppen haben eine Reihe von möglichen Gesamtstrukturbesitzer. Wenn Ihre Organisation bereits Active Directory-Infrastruktur verfügt, sind alle aktuellen Gesamtstrukturbesitzer auch mögliche Besitzer von Gesamtstrukturen für neue Bereitstellungen.  
  
Wählen Sie eine der möglichen Gesamtstrukturbesitzer, die als Gesamtstrukturbesitzer, für jede Gesamtstruktur fungiert, die Sie für die Bereitstellung in Betracht ziehen. Diese potenzielle Gesamtstrukturbesitzer sind verantwortlich für die Arbeit mit dem Entwurfsteam, um zu bestimmen, ob der Gesamtstruktur tatsächlich bereitgestellt wird oder eine alternative Vorgehensweise Aktion (z. B. das Beitreten zu einer anderen vorhandenen Gesamtstruktur) ist eine bessere Verwendung von den verfügbaren Ressourcen und immer noch ihren Anforderungen entspricht. Die Gesamtstrukturbesitzer (oder Besitzer) in Ihrer Organisation sind Mitglied der Active Directory-Design-Team.  
  
### <a name="establishing-a-design-team"></a>Einrichten eines Entwicklungsteams  
Das Active Directory-Entwicklungsteam ist verantwortlich für das Sammeln alle Informationen erforderlich, um Entscheidungen bezüglich der Active Directory-Design der logischen Struktur.  
  
Das Entwurfsteam die Zuständigkeiten umfassen Folgendes:  
  
-   Bestimmen, wie viele Gesamtstrukturen und Domänen erforderlich sind und welche Beziehungen zwischen den Gesamtstrukturen und Domänen  
  
-   Zusammenarbeiten mit Datenbesitzern von sichergestellt, dass der Entwurf ihre Sicherheits- und verwaltungsanforderungen entspricht.  
  
-   Arbeiten mit den aktuellen Netzwerkadministratoren, stellen Sie sicher, dass die aktuelle Netzwerkinfrastruktur, den Entwurf unterstützt und der Entwurf nicht nachteilig auf die vorhandene Anwendungen auf das Netzwerk auswirkt  
  
-   Arbeiten mit Vertretern der Sicherheitsgruppe der Organisation sicherstellen, dass der Entwurf festgelegter Sicherheitsrichtlinien entspricht  
  
-   Entwerfen der OE-Strukturen, die angemessenen Schutz und die richtige Delegierung von Autorität, die Besitzer der Daten zulassen  
  
-   Arbeiten mit dem Bereitstellungsteam das Design zu testen in einem Lab Umgebung, um sicherzustellen, dass sie als geplant und ändern den Entwurf als zum Beheben etwaiger Probleme, die auftreten  
  
-   Erstellen eine Entwerfen der Standorttopologie, erfüllt die Anforderungen für die Replikation der Gesamtstruktur und verhindern Sie die Überladung der verfügbaren Bandbreite. Weitere Informationen zum Entwerfen der Standorttopologie finden Sie unter [entwerfen die Website-Topologie für Windows Server 2008 AD DS](https://technet.microsoft.com/library/cc772013.aspx).  
  
-   Arbeiten mit dem Bereitstellungsteam, um sicherzustellen, dass der Entwurf ordnungsgemäß implementiert ist  
  
Das Designteam enthält die folgenden Elemente:  
  
-   Mögliche Gesamtstrukturbesitzer  
  
-   Project architect  
  
-   Projektmanager  
  
-   Personen, die für das Einrichten und Verwalten von Sicherheitsrichtlinien im Netzwerk zuständig sind  
  
Während des Entwurfsprozesses der logischen Struktur identifiziert das Entwurfsteam die anderen Besitzer an. Diese Personen müssen Starten des Entwurfsprozesses teilnehmen, sobald sie identifiziert werden. Nachdem das Bereitstellungsprojekt enthält Artefakte an das Bereitstellungsteam übergeben wird, ist das Entwurfsteam verantwortlich für die Überwachung des Bereitstellungsprozesses, um sicherzustellen, dass der Entwurf ordnungsgemäß implementiert wird. Das Designteam nimmt außerdem Änderungen am Entwurf, basierend auf Feedback aus testen.  
  
### <a name="establishing-a-deployment-team"></a>Eine vom Bereitstellungsteam einrichten  
Das Active Directory-Bereitstellungsteam ist verantwortlich für das Testen und implementieren die logische Struktur von Active Directory-Designs. Dies umfasst die folgenden Aufgaben:  
  
-   Einrichten einer testumgebung, die die produktionsumgebung ausreichend emuliert  
  
-   Testen den Entwurf durch die Implementierung der vorgeschlagenen Struktur der Gesamtstruktur und Domäne in einer testumgebung, um sicherzustellen, dass es sich um die Ziele der einzelnen Rollenbesitzer erfüllt  
  
-   Entwickeln und Testen alle Migrationsszenarien vorgeschlagen, mit der Absicht in einer Lab-Umgebung  
  
-   Sicherstellen, dass jeder Besitzer für den Testprozess abgezeichnet um sicherzustellen, dass die richtigen Funktionen getestet werden  
  
-   Testen den Bereitstellungsvorgang in einer pilotumgebung  
  
Wenn Sie den Entwurf und die Tests Aufgaben abgeschlossen sind, führt das Bereitstellungsteam die folgenden Aufgaben aus:  
  
-   Erstellt die Gesamtstrukturen und Domänen gemäß der logischen Struktur von Active Directory-Designs  
  
-   Erstellt die Sites und Standortverknüpfungsobjekte nach Bedarf für das Entwerfen der Standorttopologie basierend  
  
-   Stellt sicher, dass die DNS-Infrastruktur für die Unterstützung von AD DS konfiguriert ist und alle neuen Namespaces dem vorhandenen Namespace der Organisation integriert werden  
  
Das Active Directory-Bereitstellungsteam enthält die folgenden Elemente:  
  
-   Gesamtstrukturbesitzer  
  
-   DNS für AD DS-Besitzer  
  
-   Standorttopologiebesitzer  
  
-   OU-Besitzer  
  
Das Bereitstellungsteam funktioniert mit den Administratoren Dienst und die Daten während der Bereitstellungsphase, um sicherzustellen, dass Mitglieder des Betriebsteams mit dem neuen Entwurf vertraut sind. Dadurch wird einen sanfter Übergang von Besitz sichergestellt, wenn der Bereitstellungsvorgang abgeschlossen ist. Nach Abschluss des Bereitstellungsprozesses übergibt die Verantwortung für die Verwaltung der neuen Active Directory-Umgebung, dem Betriebsteam.  
  
### <a name="documenting-the-design-and-deployment-teams"></a>Dokumentieren den Entwurf und Bereitstellung von teams  
Dokumentieren Sie die Namen und Kontaktinformationen für die Personen, die in den Entwurf und Bereitstellung von AD DS einbezogen werden. Identifizieren Sie, die auf den Entwurf und Bereitstellung von Teams für jede Rolle zuständig ist. Diese Liste enthält zunächst die potenziellen Gesamtstrukturbesitzer und der Projektmanager der Projektarchitekt. Wenn Sie die Anzahl der Gesamtstrukturen, die Sie bereitstellen ermitteln, müssen Sie neue Designteams für weitere Gesamtstrukturen zu erstellen. Beachten Sie, dass Sie der Dokumentation zu aktualisieren, wie Teammitgliedschaften ändern und wie Sie die verschiedenen Active Directory-Besitzer während des Entwurfs identifizieren müssen. Laden Sie für ein Arbeitsblatt, die Ihnen helfen, den Entwurf und Bereitstellung von Teams für jede Gesamtstruktur dokumentiert, Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit ([ https://go.microsoft.com/fwlink/?LinkID=102558 ](https://go.microsoft.com/fwlink/?LinkID=102558)), und öffnen Sie "Entwurf und Bereitstellung Team Information" (DSSLOGI_1.doc).  
  


