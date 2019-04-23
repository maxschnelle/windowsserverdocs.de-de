---
title: AD-Gesamtstruktur Recovery Virtualisierung
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: 23317f55fdce18e78ac3e7e1490f6fc4937fd062
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858451"
---
# <a name="active-directory-forest-recovery-virtualization"></a>Virtualisierung der Active Directory-Gesamtstruktur-Wiederherstellung

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Dieses Thema beschreibt die virtualisierten Domänencontroller-Klonfunktion in Windows Server 2016, 2012 R2 und 2012.  

## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>Klonen virtualisierter Domänencontroller verwenden, um die Wiederherstellung der Gesamtstruktur zu beschleunigen.

Klonen von virtualisierten Domänencontrollern (DC) vereinfacht und beschleunigt den Prozess für die Installation zusätzlicher virtualisierte Domänencontroller in einer Domäne, insbesondere in der zentralen Standorte wie Rechenzentren, in denen mehrere DCs Hypervisoren ausgeführt. Nachdem Sie eine virtuelle DC in jeder Domäne aus einer Sicherung wiederhergestellt haben, können zusätzliche DCs in jeder Domäne schnell online geschaltet werden mithilfe des virtualisierten Domänencontrollers, der Prozess für das Klonen. Sie können den ersten virtualisierten Domänencontroller, die Sie wiederherstellen, Herunterfahren und kopieren Sie vorbereiten, die virtuelle Festplatte oft als erforderlich, um den geklonten erstellen virtualisierter DCs der Domäne zu erstellen.  
  
Die Anforderungen zum Klonen von virtualisierten Domänencontroller sind:  
  
- Der Hypervisor die VM-Generations-ID muss unterstützt werden. Hyper-V unter Windows Server 2016, 2012 und Windows 8 ist ein Beispiel für einen Hypervisor, die VM-Generations-ID unterstützt. Überprüfen Sie bei Ihrem Hypervisor-Hersteller, ob die VM-Generations-ID unterstützt wird.  
- Des virtualisierten Domänencontrollers, der als Quelle zum Klonen verwendet wird, muss Windows Server 2016 oder 2012 ausführen und Mitglied der Gruppe "Klonbare Domänencontroller". 
- Der PDC-Emulator muss Windows Server 2016 oder 2012 ausgeführt werden. Sie können die PDC-Emulator klonen, wenn er virtualisiert ist.  
  
Eine schrittweise Anleitung zur Durchführung DC Klonen virtualisiert werden, finden Sie unter [Einführung in die Active Directory Domain Services (AD DS) Virtualization (Level 100)](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md). Details zum DC Klonen funktioniert virtualisiert werden, finden Sie unter [virtualisierte technische Referenz für Domänencontroller (Level 300)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md). 

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
