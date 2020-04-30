---
ms.assetid: bd64a766-5362-4f29-b963-5465c2bb79e7
title: Planen der Platzierung der Rolle „Betriebsmaster“
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e6142d3facb32a81d8d7c54afe9c2f60fc9eb674
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81623808"
---
# <a name="planning-operations-master-role-placement"></a>Planen der Platzierung der Rolle „Betriebsmaster“

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS) unterstützt die Multimasterreplikation von Verzeichnis Daten. Dies bedeutet, dass jeder Domänen Controller Verzeichnisänderungen annehmen und die Änderungen auf allen anderen Domänen Controllern replizieren kann. Bestimmte Änderungen, wie z. b. Schema Änderungen, sind jedoch unpraktisch für die Ausführung im multimasterstil. Aus diesem Grund enthalten bestimmte Domänen Controller, die als Betriebs Master bezeichnet werden, Rollen, die für die Annahme von Anforderungen für bestimmte spezifische Änderungen zuständig sind.

> [!NOTE]
> Die Inhaber von Betriebs Master Rollen müssen in der Lage sein, Informationen in die Active Directory Datenbank zu schreiben. Aufgrund der schreibgeschützten Daten Bank Active Directory auf einem schreibgeschützten Domänen Controller (Read-Only Domain Controller, RODC) **können RODCs nicht als Inhaber von Betriebs Master Rollen fungieren**.

Drei Betriebs Master Rollen (auch als Flexible Single Master Operations oder FSMO bezeichnet) sind in jeder Domäne vorhanden:

- Der Emulator-Betriebs Master des primären Domänen Controllers (PDC) verarbeitet alle Kenn Wort Aktualisierungen.

- Der RID-Betriebs Master (relative ID) verwaltet den globalen RID-Pool für die Domäne und ordnet allen Domänen Controllern lokale RIDs-Pools zu, um sicherzustellen, dass alle in der Domäne erstellten Sicherheits Prinzipale über einen eindeutigen Bezeichner verfügen.
- Der Infrastruktur Betriebs Master für eine bestimmte Domäne verwaltet eine Liste der Sicherheits Prinzipale aus anderen Domänen, die Mitglieder von Gruppen innerhalb der Domäne sind.

Zusätzlich zu den drei Betriebs Master Rollen auf Domänen Ebene sind zwei Betriebs Master Rollen in jeder Gesamtstruktur vorhanden:

- Der Schema Betriebs Master regelt Änderungen am Schema.
- Der Domänen Namen-Betriebs Master fügt Domänen und andere Verzeichnis Partitionen (z. b. Domain Name System (DNS)-Anwendungs Partitionen) der Gesamtstruktur hinzu und entfernt diese.

Platzieren Sie die Domänen Controller, auf denen diese Betriebs Master Rollen gehostet werden, in Bereichen, in denen die Netzwerk Zuverlässigkeit hoch ist, und stellen Sie sicher, dass der PDC-Emulator und der RID-Master

Die Inhaber von Betriebs Master Rollen werden automatisch zugewiesen, wenn der erste Domänen Controller in einer bestimmten Domäne erstellt wird. Die zwei Rollen auf Gesamtstruktur Ebene (Schema Master und Domänen namens Master) werden dem ersten Domänen Controller zugewiesen, der in einer Gesamtstruktur erstellt wurde. Außerdem werden den ersten Domänen Controllern, die in einer Domäne erstellt werden, die drei Rollen auf Domänen Ebene (RID-Master, Infrastruktur Master und PDC-Emulator) zugewiesen.

> [!NOTE]
> Inhaber Zuweisungen für die automatische Betriebs Master Rolle werden nur erstellt, wenn eine neue Domäne erstellt wird und wenn ein aktueller Rollen Inhaber herabgestuft wird. Alle anderen Änderungen an Rollen Besitzern müssen von einem Administrator initiiert werden.

Diese automatischen Betriebs Master Rollenzuweisungen können zu einer sehr hohen CPU-Auslastung auf dem ersten Domänen Controller führen, der in der Gesamtstruktur oder in der Domäne erstellt wird. Um dies zu vermeiden, weisen Sie Betriebs Master Rollen unterschiedlichen Domänen Controllern in Ihrer Gesamtstruktur oder Domäne zu (übertragen). Platzieren Sie die Domänen Controller, die Betriebs Master Rollen hosten, in Bereichen, in denen das Netzwerk zuverlässig ist und auf die die Betriebs Master von allen anderen Domänen Controllern in der Gesamtstruktur zugreifen können.

Außerdem sollten Sie Standby-Betriebs Master (Alternate) für alle Betriebs Master Rollen festlegen. Bei den standbyvorgängen handelt es sich um Domänen Controller, für die Sie die Betriebs Master Rollen übertragen können, falls die ursprünglichen Rollen Inhaber fehlschlagen. Stellen Sie sicher, dass die standbyvorgängen direkt Replikations Partner der tatsächlichen Betriebs Master sind.

## <a name="planning-the-pdc-emulator-placement"></a>Planen der Platzierung des PDC-Emulators

Der PDC-Emulator verarbeitet Client Kennwort-Änderungen. Nur ein Domänen Controller fungiert in jeder Domäne in der Gesamtstruktur als PDC-Emulator.

Auch wenn alle Domänen Controller auf Windows 2000, Windows Server 2003 und Windows Server 2008 aktualisiert wurden und die Domäne auf der systemeigenen Windows 2000-Funktionsebene ausgeführt wird, empfängt der PDC-Emulator die bevorzugte Replikation von Kenn Wort Änderungen, die von anderen Domänen Controllern in der Domäne ausgeführt werden. Wenn ein Kennwort kürzlich geändert wurde, nimmt diese Änderung Zeit in die Replikation auf allen Domänen Controllern in der Domäne. Wenn die Anmelde Authentifizierung auf einem anderen Domänen Controller aufgrund eines ungültigen Kennworts fehlschlägt, leitet dieser Domänen Controller die Authentifizierungsanforderung an den PDC-Emulator weiter, bevor er entscheidet, ob der Anmeldeversuch angenommen oder abgelehnt wird.

Platzieren Sie den PDC-Emulator an einem Speicherort, der bei Bedarf eine große Anzahl von Benutzern aus dieser Domäne für Vorgänge zur Kenn Wort Weiterleitung enthält. Stellen Sie außerdem sicher, dass der Standort mit anderen Standorten verbunden ist, um die Replikations Latenz zu minimieren.

Ein Arbeitsblatt unterstützt Sie bei der Dokumentation der Informationen zum Platzieren von PDC-Emulatoren und der Anzahl der Benutzer für jede Domäne, die an jedem Standort dargestellt wird, unter [Auftrags Hilfen für Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), Download Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip und Open Domain Controller Placement (DSSTOPO_4. doc).

Sie müssen die Informationen zu Standorten, an denen Sie PDC-Emulatoren platzieren müssen, auf die Bereitstellung regionaler Domänen verweisen. Weitere Informationen zum Bereitstellen von regionalen Domänen finden Sie unter Bereitstellen von [regionalen Windows Server 2008-Domänen](https://technet.microsoft.com/library/cc755118.aspx).

## <a name="requirements-for-infrastructure-master-placement"></a>Anforderungen für die Platzierung der Infrastruktur Master

Der Infrastruktur Master aktualisiert die Namen von Sicherheits Prinzipalen aus anderen Domänen, die Gruppen in der eigenen Domäne hinzugefügt werden. Wenn ein Benutzer aus einer Domäne z. b. Mitglied einer Gruppe in einer zweiten Domäne ist und der Name des Benutzers in der ersten Domäne geändert wird, wird die zweite Domäne nicht benachrichtigt, dass der Name des Benutzers in der Mitgliedschafts Liste der Gruppe aktualisiert werden muss. Da Domänen Controller in einer Domäne Sicherheits Prinzipale nicht auf Domänen Controllern in einer anderen Domäne replizieren, wird die zweite Domäne nie von der Änderung der Abwesenheit des Infrastruktur Masters informiert.

Der Infrastruktur Master überwacht ständig Gruppenmitgliedschaften und sucht nach Sicherheits Prinzipalen aus anderen Domänen. Wenn ein solcher gefunden wird, überprüft er die Domäne des Sicherheits Prinzipals, um zu überprüfen, ob die Informationen aktualisiert wurden. Wenn die Informationen veraltet sind, wird das Update vom Infrastruktur Master durchführt, und dann wird die Änderung auf die anderen Domänen Controller in der Domäne repliziert.

Für diese Regel gelten zwei Ausnahmen. Wenn alle Domänen Controller als globale Katalogserver dienen, ist der Domänen Controller, der die Infrastruktur Master Rolle hostet, unerheblich, weil globale Kataloge die aktualisierten Informationen unabhängig von der Domäne replizieren, zu der Sie gehören. Zweitens: Wenn die Gesamtstruktur nur über eine Domäne verfügt, ist der Domänen Controller, der die Infrastruktur Master Rolle hostet, unerheblich, da keine Sicherheits Prinzipale aus anderen Domänen vorhanden sind.

Platzieren Sie den Infrastruktur Master nicht auf einem Domänen Controller, der auch globaler Katalogserver ist. Wenn sich der Infrastruktur Master und der globale Katalog auf demselben Domänen Controller befinden, funktioniert der Infrastruktur Master nicht. Der Infrastruktur Master findet nie Daten, die veraltet sind. aus diesem Grund werden keine Änderungen an den anderen Domänen Controllern in der Domäne repliziert.

## <a name="operations-master-placement-for-networks-with-limited-connectivity"></a>Betriebs Master Platzierung für Netzwerke mit eingeschränkter Konnektivität

Wenn Ihre Umgebung über einen zentralen Standort oder einen zentralen Hub-Standort verfügt, an dem Sie Betriebs Master Rollen Inhaber platzieren können, sind bestimmte Domänen Controller Vorgänge, die von der Verfügbarkeit dieser Betriebs Master Rollen Inhaber abhängen, möglicherweise beeinträchtigt.

Nehmen wir beispielsweise an, dass eine Organisation die Standorte a, b, C und d erstellt. zwischen a und b, zwischen B und c und zwischen c und d sind Standort Verknüpfungen vorhanden, die die Netzwerk Konnektivität der Standort Verknüpfungen exakt widerspiegeln. In diesem Beispiel werden alle Betriebs Master Rollen an Standort A platziert, und die Option zum über **Brücken aller Standort Verknüpfungen** ist nicht ausgewählt.

Obwohl diese Konfiguration zu einer erfolgreichen Replikation zwischen allen Standorten führt, gelten für die Betriebs Master-Rollen Funktionen folgende Einschränkungen:

- Die Domänen Controller an den Standorten C und D können nicht auf den PDC-Emulator an Standort A zugreifen, um ein Kennwort zu aktualisieren oder es auf ein kürzlich aktualisiertes Kennwort zu überprüfen.
- Die Domänen Controller an den Standorten C und D können nicht auf den RID-Master an Standort A zugreifen, um nach der Active Directory Installation einen ersten RID-Pool abzurufen und die RID-Pools zu aktualisieren, sobald sie erschöpft sind
- Domänen Controller an Standorten C und D können keine Verzeichnis-, DNS-oder benutzerdefinierten Anwendungs Partitionen hinzufügen oder entfernen.
- Die Domänen Controller an den Standorten C und D können keine Schema Änderungen vornehmen.

Ein Arbeitsblatt, das Sie bei der Planung der Platzierung von Betriebs Master Rollen unterstützt, finden Sie unter [Job Aids for Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), Download Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip und Open Domain Controller Placement (DSSTOPO_4. doc).

Sie müssen diese Informationen beachten, wenn Sie die Stamm Domäne der Gesamtstruktur und die regionalen Domänen erstellen. Weitere Informationen zum Bereitstellen der Stamm Domäne der Gesamtstruktur finden Sie unter Bereitstellen einer [Windows Server 2008](https://technet.microsoft.com/library/cc731174.aspx)-Gesamtstruktur-Stamm Domäne. Weitere Informationen zum Bereitstellen von regionalen Domänen finden Sie unter Bereitstellen von [regionalen Windows Server 2008-Domänen](https://technet.microsoft.com/library/cc755118.aspx).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Platzierung der Rolle "die Platzierung von Rollen" finden Sie im Thema zum unterstützen der [Platzierung und Optimierung von Rollen in Active Directory Domänen Controllern](https://support.microsoft.com/help/223346) .
