---
title: AD Gesamtstruktur-Wiederherstellung - identifizieren Sie das Problem
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: cb3cf45f778ff305c8fe5aad5e23f0257650d6f5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865521"
---
# <a name="identify-the-problem"></a>Ermittlung des Problems

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2
  
Wenn Symptome eines Fehlers eine gesamtstrukturweite angezeigt werden, z. B. in Ereignisprotokollen oder anderen überwachungslösungen, arbeiten mit Microsoft Support, um die Ursache des Fehlers zu ermitteln und bewerten möglichen Abhilfen.  

## <a name="examples-of-forest-wide-failures"></a>Beispiele für Gesamtstruktur-Fehler

- Alle Domänencontroller beschädigt logisch oder physisch zu einem Zeitpunkt an, dass die Geschäftskontinuität nicht möglich ist beschädigt; Alle unternehmensanwendungen, die AD DS abhängig sind beispielsweise nicht funktionsfähig.  
- Ein nicht autorisierter Administrator verfügt über die Active Directory-Umgebung gefährdet werden.  
- Ein Angreifer absichtlich – oder ein Administrator versehentlich – führt ein Skript aus, die Beschädigung von Daten über die Gesamtstruktur hinweg verteilt.  
- Ein Angreifer absichtlich – oder ein Administrator versehentlich – erweitert Active Directory-Schema mit Schadsoftware oder in Konflikt stehende Änderungen.  
- Ein Angreifer hat es geschafft, bösartigen Software auf DCs zu installieren, und Sie vom Microsoft Support die Gesamtstruktur aus einer Sicherung wiederherstellen hingewiesen worden sind.  
  
   > [!IMPORTANT]
   >  Dieses Dokument deckt nicht sicherheitsempfehlungen zur Vorgehensweise beim Wiederherstellen von einer Gesamtstruktur, die gehackt oder kompromittiert wurde. Im Allgemeinen empfiehlt es, führen Sie Pass-the-Hash von Techniken zum Absichern von der umgebungs. Weitere Informationen finden Sie unter [Mitigating Pass-the-Hash (PtH)-Angriffe und anderen Techniken zum Diebstahl von Anmeldeinformationen](https://www.microsoft.com/download/details.aspx?id=36036).
  
- Keiner der Domänencontroller kann mit den Replikationspartnern replizieren.  
- Änderungen können nicht in AD DS auf jedem Domänencontroller vorgenommen werden.  
- Neue Domänencontroller können nicht in einer beliebigen Domäne installiert werden.  
  
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
