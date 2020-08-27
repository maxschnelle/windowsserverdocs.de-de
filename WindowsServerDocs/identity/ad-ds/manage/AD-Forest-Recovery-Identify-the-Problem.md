---
title: 'Wiederherstellung der AD-Gesamtstruktur: Bestimmen des Problems'
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.openlocfilehash: fc285fb355b6539aac56c7c410de1e1f7da48f00
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939660"
---
# <a name="identify-the-problem"></a>Identifizieren des Problems

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Wenn Symptome eines Gesamtstruktur weiten Fehlers, z. b. in Ereignisprotokollen oder anderen Überwachungslösungen, auftreten, können Sie mit Microsoft-Support arbeiten, um die Ursache des Fehlers zu ermitteln und mögliche Abhilfemaßnahmen auszuwerten.

## <a name="examples-of-forest-wide-failures"></a>Beispiele für Gesamtstruktur weite Ausfälle

- Alle DCS sind logisch beschädigt oder physisch beschädigt an einem Punkt, an dem die Geschäftskontinuität nicht besteht. Beispielsweise sind alle Geschäftsanwendungen, die von AD DS abhängen, nicht funktionsfähig.
- Ein nicht autorisierter Administrator hat die Active Directory Umgebung kompromittiert.
- Ein Angreifer, der versehentlich –, oder ein Administrator – führt ein Skript aus, mit dem Daten Beschädigungen in der Gesamtstruktur verteilt werden.
- Ein Angreifer, der – oder ein Administrator versehentlich –, erweitert das Active Directory Schema durch böswillige oder widersprüchliche Änderungen.
- Ein Angreifer hat die Installation von Schadsoftware auf DCS verwaltet, und Sie haben Microsoft-Support, die Gesamtstruktur aus einer Sicherung wiederherzustellen.

   > [!IMPORTANT]
   >  In diesem Whitepaper werden keine Sicherheitsempfehlungen für die Wiederherstellung einer Gesamtstruktur behandelt, die gehackt oder kompromittiert wurde. Im Allgemeinen wird empfohlen, Pass-the-Hash-Entschärfungs Techniken zu befolgen, um die Umgebung zu Härten. Weitere Informationen finden Sie unter Entschärfung von [Pass-the-Hash-Angriffen (PTH) und anderen Techniken zum Diebstahl](https://www.microsoft.com/download/details.aspx?id=36036)von Anmelde Informationen.

- Keiner der DCS kann mit seinen Replikations Partnern repliziert werden.
- An einem beliebigen Domänen Controller können keine Änderungen AD DS vorgenommen werden.
- Neue DCS können nicht in einer Domäne installiert werden.

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
