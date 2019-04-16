---
ms.assetid: bd64a766-5362-4f29-b963-5465c2bb79e7
title: Planen der Platzierung der Rolle "Betriebsmaster"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9d271ed3a54e78106aed0d4dbfdb610cc8b9a460
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="planning-operations-master-role-placement"></a>Planen der Platzierung der Rolle "Betriebsmaster"

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Active Directory-Domänendienste (AD DS) unterstützt die Multimasterreplikation von Verzeichnisdaten, d.h. alle Domänencontroller kann Directory Änderungen übernehmen und die Änderungen auf alle anderen Domänencontroller replizieren. Bestimmte Änderungen, z.B. Schemaänderungen, sind jedoch nicht die ideale multimaster Weise ausführen. Aus diesem Grund halten Sie bestimmte Domänencontroller als Betriebsmaster Rollen für die Annahme von Anforderungen für bestimmte bestimmten Änderungen zuständig.  
  
> [!NOTE]  
> Betriebsmasterrolle müssen einige Informationen in Active Directory-Datenbank schreiben können. Aufgrund der schreibgeschützten Natur der Active Directory-Datenbank auf einem schreibgeschützten Domänencontroller (RODC) können nicht RODCs als Betriebsmasterrolle fungieren.  
  
Es gibt drei Betriebsmasterrollen (auch bekannt als flexible single master Operations bzw. FSMO bezeichnet) in jeder Domäne:  
  
-   Emulationsbetriebsmaster des primären Domänencontrollers (PDC) verarbeitet alle Kennwort-Updates.  
  
-   Die relative ID RID-Betriebsmaster verwaltet den globalen RID-Pool für die Domäne und ordnet lokalen RID-Pools auf alle Domänencontroller, um sicherzustellen, dass alle Sicherheitsprinzipale in der Domäne erstellt einen eindeutigen Bezeichner haben.  
  
-   Der Infrastrukturbetriebsmaster für eine bestimmte Domäne verwaltet eine Liste der Sicherheitsprinzipale aus anderen Domänen, die Mitglieder von Gruppen in der Domäne sind.  
  
Zusätzlich zu den drei auf Domänenebene Betriebsmasterrollen es gibt zwei Betriebsmasterrollen in jeder Gesamtstruktur:  
  
-   Der Schemabetriebsmaster regelt die Änderung des Schemas.  
  
-   Der Betriebsmaster Domäne hinzugefügt und entfernt Domänen und anderen Verzeichnispartitionen (z.B. Domain Name System (DNS) Anwendungspartitionen), zu und von der Gesamtstruktur.  
  
Platzieren Sie den Domänencontroller hostet diese Betriebsmasterfunktionen in Bereichen, in denen die Zuverlässigkeit des Netzwerks hoch ist, und stellen Sie sicher, dass der PDC-Emulator und der RID-Master durchgängig verfügbar sind.  
  
Betriebsmasterrolle werden automatisch zugewiesen, wenn der erste Domänencontroller in einer bestimmten Domäne erstellt wird. Den ersten Domänencontroller in einer Gesamtstruktur erstellt werden die beiden auf Gesamtstrukturebene Rollen (Schemamaster und Domänennamenmaster) zugewiesen. Darüber hinaus werden die drei Funktionen der Domänenebene (RID-Master, Infrastrukturmaster und PDC-Emulator) des ersten Domänencontrollers in einer Domäne erstellte zugewiesen.  
  
> [!NOTE]  
> Automatische Zuweisung von Inhaber Betriebsmasterfunktionen erfolgen nur, wenn eine neue Domäne erstellt wird und wenn eine aktuelle Inhaber der Rolle herabgestuft wird. Alle anderen Änderungen an Rollenbesitzer müssen von einem Administrator initiiert werden.  
  
Diese automatische Zuweisung von Betriebsmasterfunktionen kann sehr hohen CPU-Auslastung auf dem ersten Domänencontroller in der Gesamtstruktur oder in der Domäne erstellt. Um dies zu vermeiden, weisen Sie (übertragen) Betriebsmasterfunktionen zu verschiedenen Domänencontrollern in der Gesamtstruktur bzw. Domäne. Platzieren Sie den Domänencontroller, dass der Host in Bereichen Betriebsmasterfunktionen, in denen das Netzwerk zuverlässig ist, und, in denen die Betriebsmaster über alle anderen Domänencontroller in der Gesamtstruktur zugegriffen werden können.  
  
Sie sollten auch festlegen, Standbymodus (alternative) Operations Master für alle Vorgänge Betriebsmasterfunktionen. Der Standbymodus Betriebsmaster sind Domänencontroller, die an denen Sie die Betriebsmasterfunktionen übertragen konnte für den Fall, dass Sie die ursprünglichen Rolleninhaber fehl. Sicherstellen Sie, dass die Standby Betriebsmaster direkte Replikationspartner von der tatsächlichen Betriebsmastern.  
  
## <a name="planning-the-pdc-emulator-placement"></a>Planen der Platzierung der PDC-emulator  
Der PDC-Emulator werden die Änderungen von Computerkontenkennwörtern verarbeitet. Nur ein Domänencontroller fungiert als PDC-Emulator in jeder Domäne in der Gesamtstruktur.  
  
Auch wenn alle Domänencontroller auf Windows2000, Windows Server2003 und Windows Server2008 aktualisiert werden, und die Domäne auf der einheitlichen Windows2000-Domänenfunktionsebene betrieben wird, erhält der PDC-Emulator während die Replikation der Änderungen von Computerkontenkennwörtern von anderen Domänencontroller in der Domäne ausgeführt. Wenn ein Kennwort kürzlich geändert wurde, wird diese Änderung auf alle Domänencontroller in der Domäne repliziert werden. Wenn die Authentifizierung bei der Anmeldung an einem anderen Domänencontroller aufgrund eines falschen Kennworts fehlschlägt, leitet die Authentifizierungsanforderung zu dem PDC-Emulator mit Domänencontrollers vor der Entscheidung, ob die annehmen oder Ablehnen des Anmeldeversuchs weiter.  
  
Platzieren Sie den PDC-Emulator an einem Ort, der eine große Anzahl von Benutzern aus dieser Domäne weiterleiten Vorgänge, bei Bedarf Kennwort enthält. Darüber hinaus stellen Sie sicher, dass die Position auch an andere Orte zur Minimierung der Replikationswartezeit verbunden ist.  
  
Ein Arbeitsblatt, hilft Ihnen bei der Dokumentation der Informationen zu sollen platzieren PDC-Emulators und die Anzahl der Benutzer für jede Domäne, die an jedem Standort dargestellt wird, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558) ), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, und öffnen Sie die Platzierung der Stammdomänencontroller der (DSSTOPO_4.doc).  
  
Sie müssen auf die Informationen zu Standorten finden in der PDC-Emulatoren platziert, beim Bereitstellen von Regionaldomänen werden müssen. Weitere Informationen zum Bereitstellen von Regionaldomänen finden Sie unter [Bereitstellen von Windows Server2008 Regionaldomänen](https://technet.microsoft.com/library/cc755118.aspx).  
  
## <a name="requirements-for-infrastructure-master-placement"></a>Anforderungen für die Infrastruktur-Master-Platzierung  

Der Infrastrukturmaster aktualisiert die Namen der Sicherheitsprinzipale aus anderen Domänen, die Gruppen in ihrer eigenen Domäne hinzugefügt werden. Wenn beispielsweise ein Benutzer von einer Domäne ein Mitglied einer Gruppe in einer Domäne zweiter ist, und den Namen des Benutzers in die erste Domäne geändert wird, die zweite Domäne nicht benachrichtigt, dass der Name des Benutzers in die Liste der Mitglieder der Gruppe aktualisiert werden muss. Da Domänencontroller in einer Domäne Sicherheitsprinzipale auf Domänencontroller in einer anderen Domäne repliziert werden, bemerkt die zweite Domäne nie über die Änderung der Abwesenheit des Infrastrukturmasters.  
  
Der Infrastrukturmaster Gruppenmitgliedschaften ständig überwacht, Sicherheitsprinzipale aus anderen Domänen suchen. Wenn es gefunden wird, wird mit den Sicherheitsprinzipal Domäne zu überprüfen, ob die Informationen aktualisiert werden. Wenn die Informationen nicht mehr aktuell ist, wird der Infrastrukturmaster führt die Aktualisierung und dann wird die Änderung auf andere Domänencontroller in der Domäne repliziert.  
  
Zwei Ausnahmen gelten für diese Regel. Wenn alle Domänencontroller globale Katalogserver sind, ist der Domänencontroller, die Infrastrukturmasterrolle unwichtig – da globale Kataloge die aktualisierte Informationen unabhängig von der Domäne repliziert werden, die sie angehören. Zweitens ist die Gesamtstruktur nur eine Domäne verfügt, der Domänencontroller, die Infrastrukturmasterrolle unwichtig – da Sicherheitsprinzipale aus anderen Domänen nicht vorhanden sind.  
  
Platzieren Sie den Infrastruktur-Master auf einem Domänencontroller, der auch ein globaler Katalogserver ist. Wenn der Infrastrukturmaster und der globale Katalog auf dem gleichen Domänencontroller sind, wird der Infrastrukturmaster nicht funktionieren. Der Infrastrukturmaster werden nie Daten finden, die nicht mehr aktuell ist. Es werden daher niemals Änderungen auf andere Domänencontroller in der Domäne repliziert.  
  
## <a name="operations-master-placement-for-networks-with-limited-connectivity"></a>Operations Master-Platzierung für Netzwerke mit eingeschränkter Konnektivität  
Beachten Sie, wenn Ihre Umgebung verfügt, einen zentralen Standort oder Hubstandort, in dem Sie die Betriebsmasterrolle platzieren können, bestimmte den Betrieb von Domänencontrollern, die abhängig von der Verfügbarkeit von Vorgängen mit Rolle master, den Inhaber betroffen sein könnte.  
  
Nehmen wir beispielsweise an, dass eine Organisation Sites A, B, C erstellt und d standortverknüpfungen zwischen bestehen A und B zwischen B und C sowie zwischen C und d Netzwerkkonnektivität spiegelt genau die Netzwerkkonnektivität die standortverknüpfungen. In diesem Beispiel alle Vorgänge des Betriebsmasters sich im befinden Standort und die Option aus, um **Brücke zwischen allen standortverknüpfungen** nicht aktiviert ist.  
  
Obwohl diese Konfiguration erfolgreiche Replikation zwischen den Standorten führt, gelten die Operations-Masterrolle Funktionen die folgenden Einschränkungen:  
  
-   Domänencontroller an Standorten, C und D können nicht zugegriffen werden den PDC-Emulator an Standort A um ein Kennwort zu aktualisieren oder um sie zur Eingabe eines Kennworts zu überprüfen, die vor kurzem aktualisiert wurde.  
  
-   Domänencontroller an Standorten, C und D können nicht RID-Master Standort A um einen anfänglichen RID-Pool nach der Installation von Active Directory zu erhalten und RID-Pools aktualisieren, wie sie ausgeschöpft zugegriffen werden.  
  
-   Domänencontroller an Standorten, C und D können nicht hinzufügen oder entfernen, Directory, DNS oder benutzerdefinierte Anwendungsverzeichnispartitionen.  
  
-   Domänencontroller an Standorten, C und D ändern nicht Schema.  
  
Ein Arbeitsblatt, die Sie beim Planen der Platzierung der Betriebsmasterrolle unterstützen, finden Sie unter Auftrag Hilfsmittel für [Windows Server2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558)Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip herunterladen und Platzierung der Stammdomänencontroller der (DSSTOPO_4.doc) zu öffnen.  
  
Sie müssen auf diese Informationen finden Sie bei der Erstellung der Gesamtstruktur-Stammdomäne und regionalen Domänen. Weitere Informationen zum Bereitstellen von Gesamtstruktur-Stammdomäne, finden Sie unter Bereitstellen von einem [Bereitstellen einer Gesamtstruktur-Stammdomäne von Windows Server2008](https://technet.microsoft.com/library/cc731174.aspx). Weitere Informationen zum Bereitstellen von Regionaldomänen finden Sie unter [Bereitstellen von Windows Server2008 Regionaldomänen](https://technet.microsoft.com/library/cc755118.aspx).  
  


