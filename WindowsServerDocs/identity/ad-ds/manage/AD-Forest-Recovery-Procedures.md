---
title: Wiederherstellung der AD-Gesamtstruktur - Verfahren
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.technology: identity-adds
ms.openlocfilehash: da45e3b20c370a2a37b0eab31a78216434dd60be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827721"
---
# <a name="ad-forest-recovery---procedures"></a>Wiederherstellung der AD-Gesamtstruktur - Verfahren

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Dieser Abschnitt enthält Verfahren im Zusammenhang mit der Gesamtstruktur-Wiederherstellungsprozess. Die Prozeduren gelten für Windows Server 2016, 2012 R2, 2012 und gelten auch für Windows Server 2008 R2 und 2008 mit einigen kleineren Ausnahmen.

Prozeduren, die Schritte umfassen, die für Windows Server 2003 variieren befinden sich unter [Wiederherstellung der Gesamtstruktur mit Windows Server 2003-Domänencontrollern](AD-Forest-Recovery-Windows-Server-2003.md).  

Im folgenden finden eine Liste von Prozeduren, die in der Sicherung und Wiederherstellung von Domänencontrollern und Active Directory verwendet werden.

- [Einen vollständigen Server sichern](AD-Forest-Recovery-Backing-up-a-Full-Server.md)  
- [Sicherung der Systemstatusdaten](AD-Forest-Recovery-Backing-up-System-State.md)  
- [Ausführen einer vollständigen Wiederherstellungs](AD-Forest-Recovery-Perform-a-Full-Recovery.md)  
- [Ausführen einer autoritativen Synchronisierung der DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
- [Ausführen einer nicht autorisierenden Wiederherstellung von Active Directory Domain Services](AD-Forest-Recovery-Nonauthoritative-Restore.md)  

Diese Schritte wird erläutert, wie eine autorisierende Wiederherstellung von SYSVOL zur gleichen Zeit durchzuführen.  

- [Konfigurieren des DNS-Server-Diensts](AD-Forest-Recovery-Configure-DNS.md)  
- [Entfernen des globalen Katalogs](AD-Forest-Recovery-Remove-GC.md)  
- [Auslösen den Wert des verfügbaren RID-pools](AD-Forest-Recovery-Raise-RID-Pool.md)  
- [Den aktuelle RID-Pool ungültig](AD-Forest-Recovery-Invaildate-RID-Pool.md)  
- [Übernehmen einer Betriebsmasterfunktion](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)  
- [Das Bereinigen nach einer Wiederherstellung](AD-Forest-Recovery-Cleanup.md)
- [Bereinigen von Metadaten entfernter beschreibbarer Domänencontroller](AD-Forest-Recovery-Cleaning-Metadata.md)  
- [Zurücksetzen des Kennworts für das Computerkonto des Domänencontrollers](AD-Forest-Recovery-Reset-Computer-Account-DC.md)  
- [Das Krbtgt-Kennwort zurücksetzen](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)  
- [Zurücksetzen eines Kennworts vertrauen auf einer Seite der Vertrauensstellung](AD-Forest-Recovery-Reset-Trust.md)  
- [Hinzufügen des globalen Katalogs](AD-Forest-Recovery-Add-GC.md)  
- [Ressourcen, um sicherzustellen, dass die Replikation funktioniert](AD-Forest-Recovery-Verify-Replication.md)  

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der Gesamtstruktur der Active Directory - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten eines Wiederherstellungsplans für die benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Gesamtstruktur des Active Directory - Ermittlung des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur-Wiederherstellung: Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - erste Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server 2003-Domänencontrollern](AD-Forest-Recovery-Windows-Server-2003.md) 
