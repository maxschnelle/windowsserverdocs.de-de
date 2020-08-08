---
title: Virtualisierung der Active Directory-Gesamtstruktur
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.openlocfilehash: e02fbf15ee3f9edc68bbfc479c2ab06aba32a959
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943753"
---
# <a name="active-directory-forest-recovery-virtualization"></a>Virtualisierung der Gesamtstruktur Wiederherstellung Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

In diesem Thema wird das Feature für das Klonen virtualisierter Domänen Controller in Windows Server 2016, 2012 R2 und 2012 beschrieben.

## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>Verwenden des Klonens von virtualisierten Domänen Controllern zum beschleunigen der Wiederherstellung

Das Klonen von virtualisierten Domänen Controllern (DC) vereinfacht und beschleunigt den Prozess zum Installieren zusätzlicher virtualisierter DCS in einer Domäne, insbesondere an zentralen Standorten, wie z. b. Rechenzentren, in denen mehrere DCS auf Hypervisoren ausgeführt werden. Nachdem Sie einen virtuellen Domänen Controller in jeder Domäne aus einer Sicherung wieder hergestellt haben, können zusätzliche DCS in jeder Domäne schnell online geschaltet werden, indem der virtualisierte DC-Klon Vorgang verwendet wird. Sie können den ersten virtualisierten Domänen Controller vorbereiten, den Sie wiederherstellen, Herunterfahren und dann die virtuelle Festplatte so oft wie nötig kopieren, um geklonte virtualisierte DCS zum Erstellen der Domäne zu erstellen.

Folgende Anforderungen gelten für das Klonen virtualisierter Domänen Controller:

- Der Hypervisor muss VM-generationid unterstützen. Hyper-V in Windows Server 2016, 2012 und Windows 8 ist ein Beispiel für einen Hypervisor, der "VM-generationid" unterstützt. Wenden Sie sich an den Hypervisor-Anbieter, wenn "VM-generationid" unterstützt wird.
- Der virtualisierte Domänen Controller, der als Quelle für das Klonen verwendet wird, muss Windows Server 2016 oder 2012 ausführen und Mitglied der Gruppe klonbare Domänen Controller sein.
- Der PDC-Emulator muss Windows Server 2016 oder 2012 ausführen. Sie können den PDC-Emulator Klonen, wenn er virtualisiert ist.

Eine Schritt-für-Schritt-Anleitung zum Klonen von virtualisierten Domänen Controllern finden Sie unter [Einführung in die Virtualisierung Active Directory Domain Services (AD DS) (Stufe 100)](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md). Ausführliche Informationen dazu, wie das Klonen virtualisierter Domänen Controller funktioniert, finden Sie unter [Technische Referenz für virtualisierte Domänen Controller (Stufe 300)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md).

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
