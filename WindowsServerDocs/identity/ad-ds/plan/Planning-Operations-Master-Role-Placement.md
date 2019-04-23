---
ms.assetid: bd64a766-5362-4f29-b963-5465c2bb79e7
title: Planen der Platzierung der Rolle „Betriebsmaster“
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a3fbe76302199888dce19f845b1c838c07facb82
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870891"
---
# <a name="planning-operations-master-role-placement"></a>Planen der Platzierung der Rolle „Betriebsmaster“

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory-Domänendienste (AD DS) unterstützt die Multimasterreplikation von Verzeichnisdaten, d. h. einen beliebigen Domänencontroller kann Änderungen übernehmen und die Änderungen auf allen anderen Domänencontrollern repliziert werden. Es gibt jedoch bestimmte Änderungen, z. B. schemaänderungen, unpraktisch, die auf mehreren Mastern Weise ausführen. Aus diesem Grund speichern für bestimmte Domänencontroller, bekannt als der Betriebsmaster Rollen für die Annahme von Anforderungen für bestimmte spezifischen Änderungen zuständig.  
  
> [!NOTE]  
> Betriebsmasterrolle müssen einige Informationen in Active Directory-Datenbank schreiben können. Aufgrund der Active Directory-Datenbank auf einem schreibgeschützten Domänencontroller (RODC), nur-Lese **RODCs können nicht als Betriebsmasterrolle dienen**.  
  
Drei Betriebsmasterrollen (auch bekannt als flexible einfache Mastervorgänge oder FSMO-Funktion) in jeder Domäne vorhanden ist:  
  
- Emulationsbetriebsmaster des primären Domänencontrollers (PDC) verarbeitet alle kennwortaktualisierungen an.  

- Der relativen ID (RID) Betriebsmaster verwaltet den globale RID-Pool für die Domäne und ordnet lokalen RIDs Pools auf allen Domänencontrollern, um sicherzustellen, dass alle Sicherheitsprinzipale in der Domäne erstellt einen eindeutigen Bezeichner verfügen.  
- Der Infrastrukturbetriebsmaster für eine bestimmte Domäne verwaltet eine Liste der Sicherheitsprinzipale aus anderen Domänen, die Mitglieder von Gruppen in der Domäne sind.  

Zusätzlich zu den drei auf Domänenebene Betriebsmasterrollen zwei Betriebsmasterrollen, die in jeder Gesamtstruktur vorhanden sein:  
  
- Der Schemabetriebsmaster gesteuert, wie Änderungen am Schema.  
- Vorgänge der Domänennamenmaster hinzugefügt und entfernt die Domänen und andere Partitionen (z. B. Domain Name System (DNS) Anwendungspartitionen) in und aus der Gesamtstruktur.  
  
Platzieren Sie den Domänencontroller hostet diese Betriebsmasterrollen in Bereichen, in denen Zuverlässigkeit des Netzwerks hoch ist, und stellen Sie sicher, dass der PDC-Emulator und dem RID-Master durchgängig verfügbar sind.  
  
Betriebsmasterrolle werden automatisch zugewiesen, wenn der erste Domänencontroller in einer bestimmten Domäne erstellt wird. Der erste Domänencontroller in einer Gesamtstruktur erstellt werden die beiden auf Gesamtstrukturebene-Rollen (Schemamaster und Domänennamenmaster) zugewiesen. Darüber hinaus werden die drei Rollen der Domänenebene (RID-Master, Infrastruktur-Master und PDC-Emulator) des ersten Domänencontrollers, der Domäne zugewiesen.  
  
> [!NOTE]  
> Automatische Zuweisung von Inhaber Betriebsmasterfunktionen erfolgen nur, wenn eine neue Domäne erstellt wird und eine aktuelle Inhaber der Rolle tiefer gestuft wird. Alle weiteren Änderungen an der Rolleninhaber müssen von einem Administrator initiiert werden.  
  
Diese automatische Zuweisung von Betriebsmasterfunktionen kann sehr hohen CPU-Auslastung auf dem ersten Domänencontroller in der Gesamtstruktur oder in der Domäne erstellt. Um dies zu vermeiden, weisen Sie (Transfer)-Vorgänge Betriebsmasterrollen auf verschiedenen Domänencontrollern in Ihrer Gesamtstruktur oder Domäne an. Platzieren Sie die Domänencontroller, dass der Host in Bereichen Betriebsmasterfunktionen, in denen das Netzwerk zuverlässig ist und, in denen die Betriebsmaster von allen anderen Domänencontrollern in der Gesamtstruktur zugegriffen werden kann.  
  
Sie sollten auch festlegen, Standby (alternative) Operations Master für alle Vorgänge Betriebsmasterrollen. Der standby-Betriebsmaster sind Domänencontroller, die an denen Sie die Betriebsmasterfunktionen übertragen konnte, Fall, dass die ursprünglichen Rolleninhaber fehlschlagen. Stellen Sie sicher, dass die standby-Betriebsmaster direkten Replikationspartner der tatsächlichen Betriebsmaster sind.  
  
## <a name="planning-the-pdc-emulator-placement"></a>Planen der Platzierung der PDC-emulator

Der PDC-Emulator verarbeitet Änderungen am Client-Kennwort. Nur ein Domänencontroller fungiert als PDC-Emulator in jeder Domäne in der Gesamtstruktur.  
  
Auch wenn alle Domänencontroller Windows 2000, Windows Server 2003 und Windows Server 2008 aktualisiert werden, und die Domäne auf der systemeigenen Windows 2000-Funktionsebene ausgeführt wird, empfängt der PDC-Emulator Zugriffscode Replikation von kennwortänderungen ausgeführt von anderen Domänencontrollern in der Domäne. Wenn ein Kennwort kürzlich geändert wurde, wird diese Änderung auf alle Domänencontroller in der Domäne repliziert. Wenn die Anmeldeauthentifizierung auf einem anderen Domänencontroller aufgrund eines falschen Kennworts ein Fehler auftritt, weitergeleitet dieses Domänencontrollers die Authentifizierungsanforderung für dem PDC-Emulator vor der Entscheidung, ob das annehmen oder Ablehnen des Anmeldeversuchs an.  
  
Platzieren Sie den PDC-Emulator in einem Speicherort, der eine große Anzahl von Benutzern aus der Domäne für das Kennwort, die Weiterleitung von Vorgängen, bei Bedarf enthält. Darüber hinaus stellen Sie sicher, dass der Speicherort und an anderen Speicherorten zur Minimierung der Replikationswartezeit verbunden ist.  
  
Ein Arbeitsblatt, hilft Ihnen bei der Dokumentieren der Informationen zu sollen platzieren PDC-Emulatoren und die Anzahl der Benutzer für jede Domäne, die an jedem Standort dargestellt wird, finden Sie unter Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit ([ https://go.microsoft.com/fwlink/?LinkID=102558 ](https://go.microsoft.com/fwlink/?LinkID=102558)), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip herunterladen und öffnen Sie die Platzierung der Domänencontroller (DSSTOPO_4.doc).  
  
Sie müssen auf die Informationen zu Speicherorten finden in der PDC-Emulatoren zu platzieren, beim Bereitstellen von Regionaldomänen werden sollen. Weitere Informationen zum Bereitstellen von Regionaldomänen finden Sie unter [Bereitstellen von Windows Server 2008 Regionaldomänen](https://technet.microsoft.com/library/cc755118.aspx).  
  
## <a name="requirements-for-infrastructure-master-placement"></a>Anforderungen für die Infrastruktur-master-Platzierung  

Der Infrastrukturmaster aktualisiert die Namen von Sicherheitsprinzipalen aus anderen Domänen, die Gruppen in seiner eigenen Domäne hinzugefügt werden. Z. B. wenn ein Benutzer von einer Domäne ein Mitglied einer Gruppe in eine zweite Domäne ist aus, und den Namen des Benutzers in der ersten Domäne geändert wird, die zweite Domäne nicht benachrichtigt, dass der Name des Benutzers in die Liste der Mitglieder der Gruppe aktualisiert werden muss. Da Domänencontroller in einer Domäne Sicherheitsprinzipale auf Domänencontrollern in einer anderen Domäne nicht repliziert werden, wird die zweite Domäne nicht über die Änderung in Ermangelung der Infrastrukturmaster.  
  
Der Infrastrukturmaster Gruppenmitgliedschaften ständig überwacht, von Sicherheitsprinzipalen aus anderen Domänen suchen. Wenn es gefunden wird, wird mit der Domäne des Sicherheitsprinzipals, um sicherzustellen, dass die Informationen aktualisiert werden überprüft. Wenn die Informationen nicht mehr aktuell ist, wird der Infrastrukturmaster führt die Aktualisierung und die Änderung auf die anderen Domänencontroller in seiner Domäne repliziert werden.  
  
Zwei Ausnahmen gelten für diese Regel. Zuerst, wenn alle Domänencontroller über globale Katalogserver sind, ist der Domänencontroller, der die Infrastrukturmasterrolle hostet unbedeutend da globale Kataloge, die aktualisierte Informationen unabhängig von der Domäne repliziert, die sie angehören. Andererseits verfügt die Gesamtstruktur nur eine Domäne, ist der Domänencontroller, der die Infrastrukturmasterrolle hostet unbedeutend, da von Sicherheitsprinzipalen aus anderen Domänen nicht vorhanden sind.  
  
Platzieren Sie den Infrastruktur-Master nicht auf einem Domänencontroller, der auch ein globaler Katalogserver ist. Wenn die Infrastruktur-Master und den globalen Katalog auf dem gleichen Domänencontroller sind, funktioniert der Infrastrukturmaster nicht. Der Infrastrukturmaster werden nie Daten finden, die nicht mehr aktuell ist. aus diesem Grund werden sie niemals Änderungen auf die anderen Domänencontroller in der Domäne repliziert.  
  
## <a name="operations-master-placement-for-networks-with-limited-connectivity"></a>Operations master-Platzierung für Netzwerke mit eingeschränkter Konnektivität

Denken Sie daran, dass wenn Ihrer Umgebung vorhanden ist, einen zentralen Standort oder den Hub-Website, die in dem Sie die Betriebsmasterrolle platzieren können, bestimmte den Betrieb von Domänencontrollern, die abhängig von der Verfügbarkeit dieser Vorgänge mit Rolle beherrschen, die Platzhalter betroffen sein könnten.  
  
Nehmen wir beispielsweise an, dass eine Organisation, Standorten A, B, C erstellt und d standortverknüpfungen zwischen bestehen A und B, zwischen B und C sowie zwischen C und d Netzwerkkonnektivität spiegelt genau auf die Netzwerkverbindung, der die standortverknüpfungen. In diesem Beispiel alle Vorgänge, die Betriebsmasterrollen sich in befinden einer und die Option aus, um site **überbrücken aller standortverknüpfungen** nicht ausgewählt ist.  
  
Obwohl diese Konfiguration bei der erfolgreichen Replikation zwischen allen Standorten führt, weisen die Betriebsfunktionen der Schemabetriebsmaster-Rolle die folgenden Einschränkungen:  
  
- Domänencontroller an Standorten, C und D können nicht die PDC-Emulator an Standort A ein Kennwort zu aktualisieren oder ein Kennwort überprüft werden, die vor kurzem aktualisiert wurde zugegriffen werden.  
- Domänencontroller an Standorten, C und D können nicht an Standort A, die Sie erhalten einen ersten RID-Pool nach der Installation der Active Directory und RID-Pools aktualisieren, wie sie aufgebraucht werden der RID-Master zugegriffen werden.  
- Domänencontroller an Standorten, C und D nicht möglich oder Directory, DNS- oder benutzerdefinierte Anwendungspartitionen entfernen.  
- Domänencontroller an Standorten, C und D vornehmen keine Änderungen am Datenbankschema.  
  
Ein Arbeitsblatt, das Sie beim Planen der Platzierung der Operations-Rolle unterstützen, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip herunterladen, und öffnen Platzierung der Domänencontroller (DSSTOPO_4.doc).  
  
Sie benötigen, um auf diese Informationen verweisen, bei der Erstellung der Gesamtstruktur-Stammdomäne und Regionaldomänen. Weitere Informationen zum Bereitstellen der Stammdomäne der Gesamtstruktur finden Sie unter Bereitstellen von einer [Bereitstellen einer Gesamtstruktur-Stammdomäne von Windows Server 2008](https://technet.microsoft.com/library/cc731174.aspx). Weitere Informationen zum Bereitstellen von Regionaldomänen finden Sie unter [Bereitstellen von Windows Server 2008 Regionaldomänen](https://technet.microsoft.com/library/cc755118.aspx).  

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Platzierung der FSMO-Rolle finden Sie im Thema Unterstützung [FSMO Platzierung und-Optimierung für Active Directory-Domänencontroller](https://support.microsoft.com/help/223346)
