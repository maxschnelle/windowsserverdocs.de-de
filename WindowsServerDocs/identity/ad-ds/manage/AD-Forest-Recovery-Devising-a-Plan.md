---
title: 'AD-Gesamtstruktur Wiederherstellung: Entwerfen eines Active Directory-Wiederherstellungs Plans'
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 17381f30-55f2-4e00-977a-b701675fa4ff
ms.openlocfilehash: 259b4ccf7f40a40e71c74e8b9cee0baf7900e756
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939780"
---
# <a name="ad-forest-recovery---devising-an-ad-forest-recovery-plan"></a>AD-Gesamtstruktur Wiederherstellung: Entwerfen eines Active Directory-Wiederherstellungs Plans

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Abhängig von Ihrer Umgebung und Ihren geschäftlichen Anforderungen müssen Sie möglicherweise alle in dieser Anleitung beschriebenen Schritte ausführen, um eine erfolgreiche Wiederherstellung der Gesamtstruktur auszuführen. Da dieses Handbuch nur als Vorlage für die Wiederherstellung der Gesamtstruktur dient, ist es wichtig, dass Sie einen benutzerdefinierten Plan für die Gesamtstruktur Wiederherstellung entwerfen, der Ihrer Umgebung entspricht und Ihren geschäftlichen Anforderungen entspricht.

Im Wiederherstellungs Plan für die Gesamtstruktur sollten Sie z. b. über eine detaillierte Topologiezuordnung der Gesamtstrukturen verfügen. Die Zuordnung sollte alle Informationen zu den DCS auflisten, z. b. ihre Namen, ihre Rollen und den Sicherungs Status sowie die Vertrauens Stellungen zwischen Ihnen. Ein Tool, das Sie verwenden können, um eine Topologiekarte zu erstellen, finden Sie unter [Microsoft Active Directory Topologie-Diagramm](https://www.microsoft.com/download/details.aspx?id=13380).

Sie sollten den Wiederherstellungs Plan für die Gesamtstruktur mindestens einmal pro Jahr üben. Außerdem empfiehlt es sich, einen Wiederherstellungs Vorgang für die Gesamtstruktur durchzuführen, wenn sich die Mitgliedschaft in der Gruppe Organisations-Admins oder Domänen-Admins geändert hat. Dadurch wird sichergestellt, dass Ihre IT-Mitarbeiter den Wiederherstellungs Plan für die Gesamtstruktur vollständig verstehen.

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
