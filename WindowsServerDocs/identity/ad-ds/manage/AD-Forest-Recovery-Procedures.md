---
title: Wiederherstellung der AD-Gesamtstruktur - Verfahren
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.technology: identity-adds
ms.openlocfilehash: 0d427448c8d2a6616b87a524bcc941fc8555cbd4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390311"
---
# <a name="ad-forest-recovery---procedures"></a>Wiederherstellung der AD-Gesamtstruktur - Verfahren

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Dieser Abschnitt enthält Verfahren für die Wiederherstellung in der Gesamtstruktur. Die Prozeduren gelten für Windows Server 2016, 2012 R2 und 2012 und gelten auch für Windows Server 2008 R2 und 2008 mit einigen geringfügigen Ausnahmen.

Prozeduren, die unterschiedliche Schritte für Windows Server 2003 enthalten, finden Sie unter Gesamtstruktur [Wiederherstellung mit Windows Server 2003-Domänen Controllern](AD-Forest-Recovery-Windows-Server-2003.md)  

Im folgenden finden Sie eine Liste der Prozeduren, die zum Sichern und Wiederherstellen von Domänen Controllern und Active Directory verwendet werden.

- [Sichern eines vollständigen Servers](AD-Forest-Recovery-Backing-up-a-Full-Server.md)  
- [Sichern der System Statusdaten](AD-Forest-Recovery-Backing-up-System-State.md)  
- [Ausführen einer vollständigen Server Wiederherstellung](AD-Forest-Recovery-Perform-a-Full-Recovery.md)  
- [Durchführen einer autoritativen Synchronisierung von DFSR-replizierten SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
- [Ausführen einer nicht autoritativen Wiederherstellung von Active Directory Domain Services](AD-Forest-Recovery-Nonauthoritative-Restore.md)  

In den folgenden Schritten wird erläutert, wie Sie eine autoritative Wiederherstellung von SYSVOL gleichzeitig durchführen.  

- [Konfigurieren des DNS-Server Dienstanbieter](AD-Forest-Recovery-Configure-DNS.md)  
- [Entfernen des globalen Katalogs](AD-Forest-Recovery-Remove-GC.md)  
- [Erhöhen des Werts von verfügbaren RID-Pools](AD-Forest-Recovery-Raise-RID-Pool.md)  
- [Der aktuelle RID-Pool wird ungültig gemacht.](AD-Forest-Recovery-Invaildate-RID-Pool.md)  
- [Übernahme einer Betriebs Master Rolle](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)  
- [Bereinigen nach einer Wiederherstellung](AD-Forest-Recovery-Cleanup.md)
- [Bereinigen von Metadaten entfernter Beschreib barer Domänen Controller](AD-Forest-Recovery-Cleaning-Metadata.md)  
- [Zurücksetzen des Computer Konto Kennworts des Domänen Controllers](AD-Forest-Recovery-Reset-Computer-Account-DC.md)  
- [Zurücksetzen des krbtgt-Kennworts](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)  
- [Zurücksetzen eines Vertrauensstellungs Kennworts auf einer Seite der Vertrauensstellung](AD-Forest-Recovery-Reset-Trust.md)  
- [Hinzufügen des globalen Katalogs](AD-Forest-Recovery-Add-GC.md)  
- [Ressourcen zum Überprüfen, ob die Replikation funktioniert](AD-Forest-Recovery-Verify-Replication.md)  

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [AD-Gesamtstruktur Wiederherstellung: Entwerfen eines benutzerdefinierten Wiederherstellungs Plans](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD-Gesamtstruktur Wiederherstellung: Identifizieren des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur Wiederherstellung: Bestimmen der Wiederherstellung](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD-Gesamtstruktur Wiederherstellung: Ausführen der ersten Wiederherstellung](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
- [AD-Gesamtstruktur Wiederherstellung: häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur mit mehreren](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Active Directory-Gesamtstruktur Wiederherstellung mit Windows Server 2003-Domänen Controllern](AD-Forest-Recovery-Windows-Server-2003.md) 
