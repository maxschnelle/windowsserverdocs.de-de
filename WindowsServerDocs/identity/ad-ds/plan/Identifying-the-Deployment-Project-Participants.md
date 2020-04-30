---
ms.assetid: 50bd2566-e03c-4884-b5c4-895c8aab80aa
title: Bestimmen der Teilnehmer am Bereitstellungsprojekt
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: efb240fabc4272a4dbef4cb7e86d7058cedb9584
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624168"
---
# <a name="identifying-the-deployment-project-participants"></a>Bestimmen der Teilnehmer am Bereitstellungsprojekt

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der erste Schritt beim Einrichten eines Bereitstellungs Projekts für Active Directory-Domäne-Dienst (AD DS) besteht darin, die Entwurfs-und Bereitstellungs Projektteams einzurichten, die für die Verwaltung der Entwurfsphase und der Bereitstellungs Phase des Active Directory Projektzyklen zuständig sind. Außerdem müssen Sie die Einzelpersonen und Gruppen ermitteln, die für das besitzende und das Verwalten des Verzeichnisses zuständig sind, nachdem die Bereitstellung abgeschlossen ist.

- [Definieren von projektspezifischen Rollen](#BKMK_1)

- [Einrichten von Besitzern und Administratoren](#BKMK_2)

- [Projektteams werden aufgebaut](#BKMK_3)

## <a name="defining-project-specific-roles"></a><a name="BKMK_1"></a>Definieren von projektspezifischen Rollen
Ein wichtiger Schritt beim Einrichten der Projektteams besteht darin, die Personen zu identifizieren, die projektspezifische Rollen enthalten sollen. Hierzu gehören der Executive-Sponsor, der Projekt Architekt und der Projektmanager. Diese Personen sind verantwortlich für die Ausführung des Active Directory Bereitstellungs Projekts.

Nachdem Sie den Projektarchitekten und den Projektmanager bestellt haben, richten diese Personen Kanäle der Kommunikation innerhalb der Organisation ein, erstellen Projekt Zeitpläne und identifizieren die Personen, die Mitglieder der Projektteams werden, beginnend mit den verschiedenen Besitzern.

### <a name="executive-sponsor"></a>Executive-Sponsor
Das Bereitstellen einer Infrastruktur, wie z. b. AD DS, kann eine große Auswirkung auf eine Organisation haben. Aus diesem Grund ist es wichtig, dass Sie einen Führungskräfte haben, der den Geschäftswert der Bereitstellung versteht, das Projekt auf der Führungsebene unterstützt und Konflikte im gesamten Unternehmen lösen kann.

### <a name="project-architect"></a>Projekt Architekt
Für jedes Active Directory Bereitstellungs Projekt ist ein Projekt Architekt erforderlich, um den Entscheidungsfindungsprozess für Active Directory Entwurf und die Bereitstellung zu verwalten. Der Architekt bietet technisches Fachwissen, das Sie beim Entwerfen und Bereitstellen von AD DS unterstützt.

> [!NOTE]
> Wenn kein vorhandenes Personal in Ihrer Organisation über eine Verzeichnis Entwurfs Darstellung verfügt, empfiehlt es sich, einen externen Berater einzustellen, der Experte für Active Directory Entwurf und Bereitstellung ist.

Die Zuständigkeiten der Active Directory Projektarchitekten umfassen Folgendes:

- Besitz des Active Directory Entwurfs

- Verstehen und Aufzeichnen der Begründung für wichtige Entwurfsentscheidungen

- Sicherstellen, dass der Entwurf die geschäftlichen Anforderungen der Organisation erfüllt

- Einrichten von Konsens zwischen Entwurfs-, Bereitstellungs-und Betriebsteams

- Grundlegendes zu den Anforderungen AD DS integrierter Anwendungen

Der endgültige Active Directory Entwurf muss eine Kombination aus Geschäftszielen und technischen Entscheidungen widerspiegeln. Daher muss der Projekt Architekt Entwurfsentscheidungen prüfen, um sicherzustellen, dass Sie sich an Geschäftszielen orientieren.

### <a name="project-manager"></a>Projektmanager
Der Projektmanager ermöglicht die Zusammenarbeit über Unternehmenseinheiten hinweg und zwischen Technologie Verwaltungs Gruppen. Im Idealfall ist der Active Directory Bereitstellungs Projekt-Manager eine Person aus der Organisation, die mit den Betriebsrichtlinien der IT-Gruppe und den Entwurfs Anforderungen für die Gruppen, die die Bereitstellung AD DS vorbereiten, vertraut ist. Der Projektmanager überwacht das gesamte Bereitstellungs Projekt, beginnend mit dem Entwurf und der Fortsetzung der Implementierung und stellt sicher, dass das Projekt im Zeitplan und innerhalb des Budgets verbleibt. Der Projektmanager umfasst die folgenden Aufgaben:

- Bereitstellen grundlegender Projektplanung, z. b. Planung und Budgetierung

- Fortschritt des Active Directory Entwurfs-und Bereitstellungs Projekts

- Sicherstellen, dass die entsprechenden Personen an jedem Teil des Entwurfsprozesses beteiligt sind

- Fungieren als einzelner Kontaktpunkt für das Active Directory Bereitstellungs Projekt

- Einrichten der Kommunikation zwischen Entwurfs-, Bereitstellungs-und Betriebsteams

- Einrichten und Verwalten der Kommunikation mit dem Executive-Sponsor im gesamten Bereitstellungs Projekt

## <a name="establishing-owners-and-administrators"></a><a name="BKMK_2"></a>Einrichten von Besitzern und Administratoren
In einem Active Directory Bereitstellungs Projekt sind Personen, die Besitzer sind, für die Verwaltung verantwortlich, um sicherzustellen, dass die Bereitstellungs Aufgaben abgeschlossen sind und dass Active Directory Entwurfs Spezifikationen die Anforderungen der Organisation erfüllen. Besitzer haben nicht unbedingt Zugriff auf die Verzeichnis Infrastruktur und müssen diese direkt bearbeiten. Administratoren sind die Personen, die für die Ausführung der erforderlichen Bereitstellungs Aufgaben zuständig sind. Administratoren verfügen über den Netzwerk Zugriff und die erforderlichen Berechtigungen, um das Verzeichnis und seine Infrastruktur zu bearbeiten.

Die Rolle des Besitzers ist "strategisch" und "Manager". Besitzer sind verantwortlich für die Kommunikation mit Administratoren über die Aufgaben, die für die Implementierung des Active Directory Entwurfs erforderlich sind, wie z. b. das Erstellen neuer Domänen Controller innerhalb der Gesamtstruktur. Die Administratoren sind für die Implementierung des Entwurfs im Netzwerk gemäß den Entwurfs Spezifikationen verantwortlich.

In großen Organisationen füllen verschiedene Personen Besitzer-und Administrator Rollen aus. in einigen kleinen Organisationen fungiert die gleiche Person jedoch möglicherweise sowohl als Besitzer als auch als Administrator.

### <a name="service-and-data-owners"></a>Dienst-und Daten Besitzer
Die tägliche Verwaltung von AD DS umfasst zwei Arten von Besitzern:

- Dienst Besitzer, die für die Planung und langfristige Wartung der Active Directory-Infrastruktur zuständig sind und sicherstellen, dass das Verzeichnis weiterhin funktionsfähig ist und die in Vereinbarungen zum Service Level eingerichteten Ziele beibehalten werden.
- Daten Besitzer, die für die Wartung der im Verzeichnis gespeicherten Informationen verantwortlich sind. Dies umfasst die Verwaltung von Benutzer-und Computer Konten und die Verwaltung lokaler Ressourcen wie Mitglieds Server und Arbeitsstationen.

Es ist wichtig, den Active Directory Dienst und die Daten Besitzer frühzeitig zu identifizieren, damit Sie an einem möglichst großen Teil des Entwurfsprozesses teilnehmen können. Da der Dienst und die Daten Besitzer für die langfristige Verwaltung des Verzeichnisses nach Abschluss des Bereitstellungs Projekts verantwortlich sind, ist es wichtig, dass diese Personen Eingaben bezüglich der Organisations Anforderungen bereitstellen und sich mit der Art und Weise vertraut machen, warum bestimmte Entwurfsentscheidungen getroffen werden. Zu den Dienst Besitzern gehören der Gesamtstruktur Besitzer, der Besitzer des Active Directory-Domäne Naming Systems (DNS) und der Besitzer der Standort Topologie. Zu den Daten Besitzern gehören Organisations Einheits Besitzer.

### <a name="service-and-data-administrators"></a>Dienst-und Daten Administratoren
Der Vorgang AD DS umfasst zwei Arten von Administratoren: Dienst Administratoren und Daten Administratoren. Dienst Administratoren implementieren Richtlinien Entscheidungen, die von Dienst Besitzern getroffen werden, und behandeln die alltäglichen Aufgaben, die mit der Verwaltung des Verzeichnis Dienstanbieter und der Infrastruktur verknüpft sind. Dies umfasst die Verwaltung der Domänen Controller, auf denen der Verzeichnisdienst gehostet wird, die Verwaltung anderer Netzwerkdienste, wie z. b. DNS, die für AD DS erforderlich sind, das Steuern der Konfiguration von Gesamtstruktur weiten Einstellungen und das sicherstellen, dass das Verzeichnis immer verfügbar ist.

Dienst Administratoren sind auch für die Ausführung laufender Active Directory Bereitstellungs Aufgaben verantwortlich, die nach Abschluss des anfänglichen Windows Server 2008 Active Directory Bereitstellungs Vorgangs erforderlich sind. Wenn beispielsweise das Verzeichnis zunimmt, werden Dienst Administratoren zusätzliche Domänen Controller erstellen und Vertrauens Stellungen zwischen Domänen nach Bedarf einrichten oder entfernen. Aus diesem Grund muss das Active Directory Bereitstellungs teamdienst Administratoren einschließen.

Sie müssen darauf achten, dass Sie Dienst Administrator Rollen nur vertrauenswürdigen Personen in der Organisation zuweisen. Da diese Personen die Möglichkeit haben, die Systemdateien auf Domänen Controllern zu ändern, können Sie das Verhalten von AD DS ändern. Sie müssen sicherstellen, dass die Dienst Administratoren in Ihrer Organisation Personen sind, die mit den Betriebs-und Sicherheitsrichtlinien in Ihrem Netzwerk vertraut sind, und die wissen, dass Sie diese Richtlinien erzwingen müssen.

Daten Administratoren sind Benutzer innerhalb einer Domäne, die sowohl für die Verwaltung von Daten, die in AD DS gespeichert sind, wie z. b. Benutzer-und Gruppenkonten, als auch für die Verwaltung von Computern, die Mitglieder Ihrer Domäne sind. Daten Administratoren steuern Teilmengen von Objekten im Verzeichnis und haben keine Kontrolle über die Installation oder Konfiguration des Verzeichnis Dienstanbieter.

Daten Administrator Konten werden standardmäßig nicht bereitgestellt. Nachdem das Entwurfs Team festgelegt hat, wie Ressourcen für die Organisation verwaltet werden sollen, müssen Domänen Besitzer Daten Administrator Konten erstellen und Ihnen basierend auf dem Satz von Objekten, für die die Administratoren verantwortlich sein müssen, die entsprechenden Berechtigungen delegieren.

Es empfiehlt sich, die Anzahl von Dienst Administratoren in Ihrer Organisation auf die Mindestanzahl zu beschränken, um sicherzustellen, dass die Infrastruktur weiterhin funktionsfähig ist. Die meisten Verwaltungsaufgaben können von Daten Administratoren ausgeführt werden. Dienst Administratoren benötigen eine viel größere Qualifikation, da Sie für die Verwaltung des Verzeichnisses und der Infrastruktur, die es unterstützt, verantwortlich sind. Daten Administratoren benötigen nur die erforderlichen Kenntnisse, um ihren Teil des Verzeichnisses zu verwalten. Das Aufteilen von Arbeits Zuweisungen auf diese Weise führt zu Kosteneinsparungen für das Unternehmen, da nur eine kleine Anzahl von Administratoren trainiert werden muss, um das gesamte Verzeichnis und seine Infrastruktur zu betreiben und zu verwalten.

Beispielsweise muss ein Dienst Administrator wissen, wie einer Gesamtstruktur eine Domäne hinzugefügt wird. Dies umfasst das Installieren der Software zum Konvertieren eines Servers in einen Domänen Controller und das Bearbeiten der DNS-Umgebung, sodass der Domänen Controller nahtlos in der Active Directory Umgebung zusammengeführt werden kann. Ein Daten Administrator muss nur wissen, wie die spezifischen Daten verwaltet werden, für die Sie verantwortlich sind, z. b. die Erstellung neuer Benutzerkonten für neue Mitarbeiter in der Abteilung.

Das Bereitstellen von AD DS erfordert Koordination und Kommunikation zwischen vielen verschiedenen Gruppen, die am Betrieb der Netzwerkinfrastruktur beteiligt sind. Diese Gruppen sollten Dienst-und Daten Besitzer benennen, die für die Darstellung der verschiedenen Gruppen während des Entwurfs-und Bereitstellungs Prozesses zuständig sind.

Nachdem das Bereitstellungs Projekt fertiggestellt wurde, sind diese Dienst-und Daten Besitzer weiterhin für den Teil der Infrastruktur verantwortlich, der von Ihrer Gruppe verwaltet wird. In einer Active Directory Umgebung sind diese Besitzer der Gesamtstruktur Besitzer, der DNS für AD DS Besitzer, der Standort topologiebesitzer und der Besitzer der Organisationseinheit. Die Rollen dieser Dienst-und Daten Besitzer werden in den folgenden Abschnitten erläutert.

#### <a name="forest-owner"></a>Gesamtstruktur Besitzer
Der Gesamtstruktur Besitzer ist in der Regel ein leitender Informationstechnologie-Manager in der Organisation, der für den Active Directory Bereitstellungs Prozess verantwortlich ist und der letztendlich für die Aufrechterhaltung der Dienst Bereitstellung innerhalb der Gesamtstruktur verantwortlich ist, nachdem die Bereitstellung fertiggestellt wurde. Der Gesamtstruktur Besitzer weist Personen zu, die anderen Besitz Rollen zu füllen, indem er wichtige Mitarbeiter innerhalb der Organisation identifiziert, die die erforderlichen Informationen zur Netzwerkinfrastruktur und zu administrativen Anforderungen einbringen können. Der Gesamtstruktur Besitzer ist für Folgendes zuständig:

- Bereitstellung der Gesamtstruktur-Stamm Domäne zum Erstellen der Gesamtstruktur

- Bereitstellung des ersten Domänen Controllers in jeder Domäne zum Erstellen der Domänen, die für die Gesamtstruktur erforderlich sind

- Mitgliedschaften der Dienst Administrator Gruppen in allen Domänen der Gesamtstruktur

- Erstellung des Entwurfs der OE-Struktur für jede Domäne in der Gesamtstruktur

- Delegierung der administrativen Autorität an Organisationseinheiten-Besitzer

- Änderungen am Schema

- Änderungen an den Gesamtstruktur weiten Konfigurationseinstellungen

- Implementierung bestimmter Gruppenrichtlinie Richtlinien Einstellungen, einschließlich Domänen Benutzerkonto-Richtlinien wie differenzierten Kenn Wort-und Konto Sperrungs Richtlinien

- Geschäftsrichtlinien Einstellungen, die für Domänen Controller gelten

- Alle anderen Gruppenrichtlinie Einstellungen, die auf Domänen Ebene angewendet werden

Der Gesamtstruktur Besitzer verfügt über die Autorität für die gesamte Gesamtstruktur. Es liegt in der Verantwortung des Gesamtstruktur Besitzers, Gruppenrichtlinie und Geschäftsrichtlinien festzulegen und die Personen, die Dienst Administratoren sind, auszuwählen. Der Gesamtstruktur Besitzer ist ein Dienst Besitzer.

#### <a name="dns-for-ad-ds-owner"></a>DNS für AD DS Besitzer
Der DNS für AD DS Besitzer ist eine Person, die ein umfassendes Verständnis der vorhandenen DNS-Infrastruktur und des vorhandenen Namespace der Organisation hat.

Der DNS für AD DS Besitzer ist für Folgendes verantwortlich:

- Fungieren als Verbindung zwischen dem Entwurfs Team und der IT-Gruppe, die derzeit die DNS-Infrastruktur besitzt

- Bereitstellen der Informationen zum vorhandenen DNS-Namespace der Organisation zur Unterstützung bei der Erstellung des neuen Active Directory Namespace

- Arbeiten mit dem Bereitstellungs Team, um sicherzustellen, dass die neue DNS-Infrastruktur entsprechend den Spezifikationen des Entwurfs Teams bereitgestellt wird und ordnungsgemäß funktioniert

- Verwalten des DNS für AD DS-Infrastruktur, einschließlich DNS-Server Dienst und DNS-Daten

Der DNS für AD DS Besitzer ist ein Dienst Besitzer.

#### <a name="site-topology-owner"></a>Besitzer der Standort Topologie
Der Besitzer der Standort Topologie ist mit der physischen Struktur des Organisations Netzwerks vertraut, einschließlich der Zuordnung einzelner Subnetze, Router und Netzwerk Bereiche, die über langsame Verbindungen verbunden sind. Der Besitzer der Standort Topologie ist für Folgendes zuständig:

- Grundlegendes zur physischen Netzwerktopologie und deren Auswirkungen auf AD DS

- Grundlegendes zur Auswirkung der Active Directory Bereitstellung auf das Netzwerk

- Bestimmen der Active Directory logischen Standorte, die erstellt werden müssen

- Aktualisieren von Standort Objekten für Domänen Controller beim Hinzufügen, ändern oder Entfernen eines Subnetzes

- Erstellen von Standort Verknüpfungen, Standort Verknüpfungs Brücken und manuellen Verbindungs Objekten

Der Besitzer der Standort Topologie ist ein Dienst Besitzer.

#### <a name="ou-owner"></a>Besitzer der Organisationseinheit
Der Besitzer der Organisationseinheit ist für die Verwaltung der im Verzeichnis gespeicherten Daten verantwortlich. Diese Person muss mit den Betriebs-und Sicherheitsrichtlinien vertraut sein, die im Netzwerk vorhanden sind. Organisationseinheiten Besitzer können nur die Aufgaben ausführen, die von den Dienst Administratoren an Sie delegiert wurden, und Sie können nur die Aufgaben auf dem Organisationseinheiten ausführen, dem Sie zugewiesen sind. Folgende Aufgaben können dem OE-Besitzer zugewiesen werden:

- Ausführen aller Konto Verwaltungsaufgaben innerhalb der zugewiesenen Organisationseinheit

- Verwalten von Arbeitsstationen und Mitglieds Servern, die Mitglieder der zugewiesenen Organisationseinheit sind

- Delegieren der Autorität an lokale Administratoren innerhalb ihrer zugewiesenen Organisationseinheit

Der Besitzer der Organisationseinheit ist ein Daten Besitzer.

## <a name="building-project-teams"></a><a name="BKMK_3"></a>Projektteams werden aufgebaut
Active Directory Projektteams sind temporäre Gruppen, die für das Abschließen Active Directory Entwurfs-und Bereitstellungs Aufgaben zuständig sind. Wenn das Active Directory Bereitstellungs Projekt fertiggestellt ist, übernehmen die Besitzer die Verantwortung für das Verzeichnis, und die Projektteams können den Vorgang aufheben.

Die Größe der Projektteams variiert je nach Größe des Unternehmens. In kleinen Organisationen kann eine einzelne Person mehrere Zuständigkeiten in einem Projektteam abdecken und an mehr als einer Phase der Bereitstellung beteiligt sein. Große Unternehmen benötigen ggf. größere Teams mit unterschiedlichen Personen oder sogar unterschiedlichen Teams, die die verschiedenen Zuständigkeitsbereiche abdecken. Die Größe der Teams ist nicht wichtig, solange alle Bereiche der Zuständigkeit zugewiesen sind und die Entwurfs Ziele der Organisation erfüllt werden.

### <a name="identifying-potential-forest-owners"></a>Identifizieren potenzieller Gesamtstruktur Besitzer
Identifizieren Sie die Gruppen innerhalb Ihrer Organisation, die über die erforderlichen Ressourcen verfügen, um den Benutzern im Netzwerk Verzeichnisdienste bereitzustellen. Diese Gruppen gelten als potenzielle Gesamtstruktur Besitzer.

Durch die Trennung von Dienst-und Datenverwaltung in AD DS kann die IT-Infrastruktur (oder Gruppen) einer Organisation den Verzeichnisdienst verwalten, während lokale Administratoren in jeder Gruppe die Daten verwalten, die zu ihren eigenen Gruppen gehören. Potenzielle Gesamtstruktur Besitzer verfügen über die erforderliche Autorität für die Netzwerkinfrastruktur, um AD DS bereitzustellen und zu unterstützen.

Für Organisationen, die über eine zentrale Infrastruktur-IT-Gruppe verfügen, ist die IT-Gruppe in der Regel der Gesamtstruktur Besitzer und somit der potenzielle Gesamtstruktur Besitzer für zukünftige bereit Stellungen. Organisationen, die eine Reihe unabhängiger Infrastruktur-IT-Gruppen beinhalten, haben eine Reihe potenzieller Gesamtstruktur Besitzer. Wenn Ihre Organisation bereits über eine Active Directory Infrastruktur verfügt, sind alle aktuellen Gesamtstruktur Besitzer auch potenzielle Gesamtstruktur Besitzer für neue bereit Stellungen.

Wählen Sie einen der potenziellen Gesamtstruktur Besitzer aus, der als Gesamtstruktur Besitzer für jede Gesamtstruktur fungiert, die Sie für die Bereitstellung in Erwägung ziehen. Diese potenziellen Gesamtstruktur Besitzer sind dafür verantwortlich, mit dem Entwurfs Team zu ermitteln, ob Ihre Gesamtstruktur tatsächlich bereitgestellt wird oder ob eine alternative Vorgehensweise (z. b. das beitreten zu einer anderen vorhandenen Gesamtstruktur) eine bessere Nutzung der verfügbaren Ressourcen und dennoch Ihren Anforderungen entspricht. Der Gesamtstruktur Besitzer (oder die Besitzer) in Ihrer Organisation sind Mitglieder des Active Directory Designteams.

### <a name="establishing-a-design-team"></a>Einrichten eines Entwurfs Teams
Das Active Directory-Entwurfs Team ist dafür verantwortlich, alle Informationen zu sammeln, die erforderlich sind, um Entscheidungen zum Entwurf der Active Directory logischen Struktur zu treffen.

Die Zuständigkeiten des Entwurfs Teams umfassen Folgendes:

- Festlegen, wie viele Gesamtstrukturen und Domänen erforderlich sind und welche Beziehungen zwischen den Gesamtstrukturen und Domänen bestehen

- Arbeiten mit Daten Besitzern, um sicherzustellen, dass der Entwurf Ihre Sicherheits-und Verwaltungsanforderungen erfüllt

- Arbeiten mit den aktuellen Netzwerkadministratoren, um sicherzustellen, dass die aktuelle Netzwerkinfrastruktur den Entwurf unterstützt und dass sich der Entwurf nicht negativ auf vorhandene Anwendungen auswirkt, die im Netzwerk bereitgestellt werden

- Arbeiten mit Vertretern der Sicherheitsgruppe des Unternehmens, um sicherzustellen, dass der Entwurf die bewährten Sicherheitsrichtlinien erfüllt

- Entwerfen von OE-Strukturen, die angemessene Schutzstufen und die ordnungsgemäße Delegierung der Zertifizierungsstelle für die Daten Besitzer zulassen

- Arbeiten mit dem Bereitstellungs Team zum Testen des Entwurfs in einer Lab-Umgebung, um sicherzustellen, dass er wie geplant funktioniert, und Ändern des Entwurfs nach Bedarf, um alle auftretenden Probleme zu beheben

- Erstellen eines Standorts der Standort Topologie, der die Replikations Anforderungen der Gesamtstruktur erfüllt und gleichzeitig die Überlastung der verfügbaren Bandbreite verhindert Weitere Informationen zum Entwerfen der Standort Topologie finden Sie unter [Entwerfen der Standort Topologie für Windows Server 2008 AD DS](https://technet.microsoft.com/library/cc772013.aspx).

- Arbeiten mit dem Bereitstellungs Team, um sicherzustellen, dass der Entwurf ordnungsgemäß implementiert ist

Das Entwurfs Team umfasst die folgenden Mitglieder:

- Potenzielle Gesamtstruktur Besitzer

- Projekt Architekt

- Projektmanager

- Personen, die für das Einrichten und Verwalten von Sicherheitsrichtlinien im Netzwerk zuständig sind

Während des Entwurfsprozesses der logischen Struktur identifiziert das Entwurfs Team die anderen Besitzer. Diese Personen müssen mit der Teilnahme am Entwurfsprozess beginnen, sobald Sie identifiziert werden. Nachdem das Bereitstellungs Projekt an das Bereitstellungs Team übergeben wurde, ist das Entwurfs Team dafür verantwortlich, den Bereitstellungs Prozess zu überwachen, um sicherzustellen, dass der Entwurf ordnungsgemäß implementiert wird. Das Entwurfs Team führt auch Änderungen am Entwurf basierend auf dem Feedback von Tests durch.

### <a name="establishing-a-deployment-team"></a>Einrichten eines Bereitstellungs Teams
Das Active Directory Bereitstellungs Team ist für das Testen und Implementieren des Entwurfs der Active Directory logischen Struktur verantwortlich. Dies umfasst die folgenden Aufgaben:

- Einrichten einer Testumgebung, die die Produktionsumgebung ausreichend emuliert

- Testen des Entwurfs durch Implementieren der vorgeschlagenen Gesamtstruktur und Domänen Struktur in einer Lab-Umgebung, um zu überprüfen, ob diese die Ziele der einzelnen Rollen Besitzer erfüllt

- Entwickeln und Testen von Migrationsszenarien, die vom Design in einer Lab-Umgebung vorgeschlagen werden

- Stellen Sie sicher, dass sich jeder Besitzer beim Testvorgang anmeldet, um sicherzustellen, dass die richtigen Entwurfs Features getestet werden.

- Testen des Bereitstellungs Vorgangs in einer Pilot Umgebung

Wenn die Entwurfs-und Testaufgaben vollständig ausgeführt werden, führt das Bereitstellungs Team die folgenden Aufgaben aus:

- Erstellt die Gesamtstrukturen und Domänen gemäß dem Design der Active Directory logischen Struktur.

- Erstellt die Standorte und Standort Verknüpfungs Objekte nach Bedarf basierend auf dem Entwurf der Standort Topologie.

- Stellt sicher, dass die DNS-Infrastruktur für die Unterstützung von AD DS konfiguriert ist und dass alle neuen Namespaces in den vorhandenen Namespace der Organisation integriert werden.

Das Active Directory Bereitstellungs Team umfasst die folgenden Mitglieder:

- Gesamtstruktur Besitzer

- DNS für AD DS Besitzer

- Besitzer der Standort Topologie

- OU-Besitzer

Das Bereitstellungs Team arbeitet während der Bereitstellungs Phase mit dem Dienst und den Daten Administratoren zusammen, um sicherzustellen, dass die Mitglieder des Betriebsteams mit dem neuen Design vertraut sind. Dadurch wird sichergestellt, dass der Besitz beim Abschluss des Bereitstellungs Vorgangs reibungslos verläuft. Nach Abschluss des Bereitstellungs Prozesses wird die Verantwortung für die Beibehaltung der neuen Active Directory Umgebung an das Betriebsteam weitergeleitet.

### <a name="documenting-the-design-and-deployment-teams"></a>Dokumentieren der Entwurfs-und Bereitstellungs Teams
Dokumentieren Sie die Namen und Kontaktinformationen für die Personen, die am Entwurf und der Bereitstellung von AD DS teilnehmen werden. Bestimmen Sie, wer für die einzelnen Rollen in den Entwurfs-und Bereitstellungs Teams verantwortlich sein wird. Diese Liste enthält zunächst die potenziellen Gesamtstruktur Besitzern, den Projektmanager und den Projektarchitekten. Wenn Sie die Anzahl der Gesamtstrukturen ermitteln, die Sie bereitstellen werden, müssen Sie möglicherweise neue Entwurfs Teams für weitere Gesamtstrukturen erstellen. Beachten Sie, dass Sie die Dokumentation aktualisieren müssen, wenn sich die Team Mitgliedschaften ändern und während des Entwurfsprozesses die verschiedenen Active Directory Besitzer identifiziert werden. Für ein Arbeitsblatt, das Sie bei der Dokumentation der Entwurfs-und Bereitstellungs Teams für jede Gesamtstruktur unterstützt, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip aus den [Auftrags Hilfen für das Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608) herunter, und öffnen Sie "Design and Deployment Team Information" (DSSLOGI_1. doc).
