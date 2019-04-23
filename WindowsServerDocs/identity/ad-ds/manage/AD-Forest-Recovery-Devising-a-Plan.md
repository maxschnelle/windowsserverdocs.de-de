---
title: Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten einer AD-Gesamtstruktur Wiederherstellungsplan
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 17381f30-55f2-4e00-977a-b701675fa4ff
ms.technology: identity-adds
ms.openlocfilehash: edfc874fe030c6394bc8bda95c49e61951e78f43
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881781"
---
# <a name="ad-forest-recovery---devising-an-ad-forest-recovery-plan"></a>Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten einer AD-Gesamtstruktur Wiederherstellungsplan

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Je nach Umgebung und geschäftlichen Anforderungen Sie können oder müssen möglicherweise nicht alle in diesem Handbuch für eine erfolgreiche Gesamtstruktur Recovery beschriebenen Schritte ausführen. Angesichts der Tatsache, dass dieses Handbuch nur als Vorlage für die Wiederherstellung der Gesamtstruktur dient, ist es wichtig, dass Sie einen benutzerdefinierten Gesamtstruktur Disaster Recovery Plan entwickeln, der Ihrer Umgebung passt und Ihre geschäftsanforderungen erfüllt.  
  
In Ihren Plan für die Gesamtstruktur, sollten Sie z. B. eine detaillierte Topologie-Karte Ihrer Gesamtstrukturen enthalten. Die Zuordnung sollte alle Informationen über die DCs, z. B. ihren Namen, ihre Rollen und Status der Sicherung und die Vertrauensstellungen zwischen ihnen auflisten. Ein Tool, das Sie zum Erstellen einer Topologiekarte verwenden können, finden Sie unter [Microsoft Active Directory-Topologie Diagrammer](https://www.microsoft.com/download/details.aspx?id=13380).  
  
Üben Sie Ihren Plan für die Gesamtstruktur mindestens einmal im Jahr. Darüber hinaus ist es eine gute Idee, die eine Übung für die Gesamtstruktur ausführen, wenn mitgliedschaftsänderungen der Gruppe "Organisations-Admins oder Domänen-Admins" vorhanden sind. Dadurch wird sichergestellt, dass Ihre (IT) Personal Wiederherstellungsplan Gesamtstruktur vollständig verstanden hat.

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
