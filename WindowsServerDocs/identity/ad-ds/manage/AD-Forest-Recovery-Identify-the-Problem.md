---
title: Active Directory Gesamtstruktur-Wiederherstellung - identifizieren Sie das Problem
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 1e9ede12dade0b5f1149eae784620520a8866e30
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="identify-the-problem"></a>Identifizieren Sie das Problem

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2
  
 Wenn Symptome eines Ausfalls gesamtstrukturweite angezeigt werden, z.B. in Ereignisprotokolle oder andere überwachen Lösungen mit Microsoft-Support, um die Ursache des Fehlers zu ermitteln, und bewerten Sie möglichen Abhilfen.  
 
## <a name="examples-of-forest-wide-failures"></a>Beispiele für Fehler bei der Gesamtstruktur 
  
-   Alle Domänencontroller wurden logisch beschädigt oder zu einem Punkt, an Geschäftskontinuität nicht möglich ist, physisch beschädigt; Beispielsweise sind alle Business-Anwendungen, die abhängig von AD DS nicht funktionsfähig.  
  
-   Ein böswilliger Administrator hat die Active Directory-Umgebung gefährdet.  
  
-   Ein Angreifer absichtlich – oder ein Administrator versehentlich – führt ein Skript, das beschädigte Daten in der Gesamtstruktur verteilt.  
  
-   Ein Angreifer absichtlich – oder ein Administrator versehentlich – erweitert das Active Directory-Schema mit Schadsoftware oder in Konflikt stehenden Änderungen.  
  
-   Ein Angreifer hat Schadsoftware auf Domänencontrollern installieren verwaltet, und Sie die Microsoft Support von der Gesamtstruktur aus einer Sicherung wiederherstellen empfohlen.  
  
    > [!IMPORTANT]
    >  In diesem Dokument wird nicht behandelt Sicherheitsaspekte zur Vorgehensweise beim Wiederherstellen einer Gesamtstruktur, die gehackt oder gefährdet wurden. Im Allgemeinen empfiehlt es, gehen Sie folgendermaßen vor Pass-the-Hash von Techniken zum Sichern der Umgebung. Weitere Informationen finden Sie unter [Mitigating Pass-the-Hash (PtH)-Angriffen und anderen Techniken zum Diebstahl](https://www.microsoft.com/download/details.aspx?id=36036).  
  
-   Keiner der Domänencontroller kann mit Replikationspartnern replizieren.  
  
-   In AD DS auf jedem Domänencontroller können keine Änderungen vorgenommen werden.  
  
-   Neue Domänencontroller können in einer beliebigen Domäne installiert werden.  
  
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
