---
title: AD-Gesamtstruktur Wiederherstellung Virtualisierung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adfs
ms.openlocfilehash: 08b0c4a4c5ed230f91241fcfb67db1749935c5e2
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
# <a name="active-directory-forest-recovery-virtualization"></a>Virtualisierung der Active Directory-Gesamtstruktur-Wiederherstellung

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

Dieses Thema beschreibt die virtualisierten Domänencontroller-Klonfunktion in Windows Server2016 und 2012 R2 2012.  
 
## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>Klonen virtualisierter Domänencontroller verwenden, um die Wiederherstellung der Gesamtstruktur zu beschleunigen.  
 Klonen virtualisierter Domänencontroller (DC) vereinfacht und beschleunigt den Prozess für die Installation zusätzlicher virtualisierte Domänencontroller in einer Domäne, insbesondere in zentralisierte Speicherorten, z.B. Rechenzentren, in denen mehrere Domänencontroller auf Hypervisoren ausführen. Nachdem Sie eine virtuelle Domänencontroller in jeder Domäne aus einer Sicherung wiederhergestellt haben, können zusätzliche Domänencontroller in jeder Domäne schnell online geschaltet werden mithilfe des virtualisierten Domänencontrollers Prozess für das Klonen. Sie können die ersten virtualisierten Domänencontroller, die Sie wiederherstellen, fahren Sie ihn herunter, und kopieren Sie vorbereiten, virtuelle Festplatte wie oft als erforderlich, um geklonte erstellen virtualisierter Domänencontroller der Domäne erstellen.  
  
 Die Anforderungen für das Klonen von virtualisierten Domänencontroller werden:  
  
-   Der Hypervisor muss VM-GenerationID unterstützen. Hyper-V in Windows Server2016 2012 und Windows8 ist ein Beispiel für ein Hypervisor, der VM-GenerationID unterstützt. Überprüfen Sie den Hypervisor-Hersteller, wenn VM-GenerationID unterstützt wird.  
  
-   Des virtualisierten Domänencontrollers, die als Quelle zum Klonen verwendet wird muss Windows Server2016 oder 2012 ausführen und ein Mitglied der Gruppe "Klonbare Domänencontroller".  
  
-   Der PDC-Emulator muss Windows Server2016 oder 2012 ausgeführt. Sie können die PDC-Emulator klonen, wenn es virtualisiert ist.  
  
 Eine schrittweise Anleitung zur Durchführung DC Klonen virtualisiert, finden Sie unter [Introduction to Active Directory-Domänendienste (AD DS) Virtualization (Level100)](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md). Weitere Informationen dazu, wie DC Klonen Works virtualisiert, finden Sie unter [virtualisierte technische Referenz für Domänencontroller (Level300)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md).  

-   [Wiederherstellung der Active Directory-Gesamtstruktur - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Konzipierung einen Wiederherstellungsplan benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - identifizieren](AD-Forest-Recovery-Identify-the-Problem.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
-   [AD-Gesamtstruktur-Wiederherstellung – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server2003-Domänencontroller](AD-Forest-Recovery-Windows-Server-2003.md) 

  
