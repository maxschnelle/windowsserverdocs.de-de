---
title: Wiederherstellung des AD-Gesamtstruktur - Konzipierung einer AD-Gesamtstruktur Wiederherstellungsplan
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 17381f30-55f2-4e00-977a-b701675fa4ff
ms.technology: identity-adfs
ms.openlocfilehash: 6754509ccac352895b9370e63adf1b69548953bf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>
# <a name="ad-forest-recovery---devising-an-ad-forest-recovery-plan"></a>Wiederherstellung des AD-Gesamtstruktur - Konzipierung einer AD-Gesamtstruktur Wiederherstellungsplan

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

Abhängig von Ihrer Umgebung und die unternehmensanforderungen zu erfüllen müssen Sie möglicherweise oder müssen nicht alle in diesem Handbuch zum Ausführen einer Wiederherstellung erfolgreich Gesamtstruktur beschriebenen Schritteausführen. Angesichts der Tatsache, dass dieser Anleitung nur als Vorlage für die Wiederherstellung der Gesamtstruktur verwendet wird, ist es wichtig, dass Sie einen benutzerdefinierten Gesamtstruktur Wiederherstellungsplan entwickeln, der Ihre Umgebung umfasst und Ihren geschäftlichen Anforderungen erfüllt.  
  
 In der Gesamtstruktur Wiederherstellungsplan, sollten Sie z.B. eine detaillierte Replikationstopologie der Gesamtstrukturen verfügen. Die Karte sollten alle Informationen zu den Domänencontrollern, z.B. ihren Namen, ihren Rollen und Sicherungsstatus und die Vertrauensstellungen zwischen ihnen aufgelistet. Ein Tool, das Sie zum Erstellen einer topologiezuordnung verwenden können, finden Sie unter [Microsoft Active Directory-Topologie Diagrammer](https://www.microsoft.com/download/details.aspx?id=13380).  
  
 Sie sollten Ihre Wiederherstellungsplan Gesamtstruktur mindestens einmal im Jahr üben. Außerdem ist es sinnvoll, eine Gesamtstruktur-Wiederherstellung einen Drilldown ausführen, bei mitgliedschaftsänderungen der Gruppe "Organisations-Admins oder Domänen-Admins". Dadurch wird sichergestellt, dass Ihre Informationen Informationstechnologie (IT) Mitarbeiter vollständig der Gesamtstruktur Wiederherstellungsplan versteht.

## <a name="next-steps"></a>Nächste Schritte
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Konzipierung einen Wiederherstellungsplan benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - identifizieren](AD-Forest-Recovery-Identify-the-Problem.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
-   [AD-Gesamtstruktur-Wiederherstellung – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server2003-Domänencontroller](AD-Forest-Recovery-Windows-Server-2003.md) 
