---
title: "Wiederherstellung der Active Directory-Gesamtstruktur - Schrittefür die Wiederherstellung der Gesamtstruktur"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 29988c262897649173e039cc052bb64f38a1a0ca
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
#<a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>Wiederherstellung der Active Directory-Gesamtstruktur - Schrittefür die Wiederherstellung der Gesamtstruktur 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

Dieser Abschnittenthält eine Übersicht über die empfohlenen Schrittefür die Wiederherstellung einer Gesamtstruktur. Schrittezur Wiederherstellung der Gesamtstruktur werden später ausführlich beschrieben.  
  
 Die folgende Liste fasst die Wiederherstellungsschritte auf hoher Ebene:  
  
1.  [Identifizieren Sie das Problem](AD-Forest-Recovery-Identify-the-Problem.md)  
  
     Arbeiten mit IT und Microsoft-Support, bestimmen Sie den Umfang des Problems und mögliche Ursachen und mögliche Gegenmaßnahmen mit allen Projektbeteiligten evaluieren. In vielen Fällen sollte die Wiederherstellung der gesamten Gesamtstruktur die letzte Option.  
  
2.  [Entscheiden Sie, wie die Gesamtstruktur wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)  
  
     Nachdem Sie ermittelt haben, dass die Wiederherstellung der Gesamtstruktur erforderlich ist, vollständige Preliminary Schritteaus, um die Vorbereitungen treffen: Ermitteln der aktuellen Gesamtstruktur, die Funktionen, die jeder Domänencontroller entscheiden, welche Domänencontroller, führt um für jede Domäne wiederherzustellen, und stellen Sie sicher, dass alle beschreibbaren Domänencontroller offline geschaltet werden, zu identifizieren.  
  
3.  [Führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
  
     Isoliert Wiederherstellen von einem Domänencontroller für jede Domäne, bereinigen sie, und schließen Sie die Domänen. Zurücksetzen von privilegierten Konten, und beheben Sie Probleme aufgrund von Sicherheitslücken in dieser Phase.  
  
4.  [Erneut bereitstellen, verbleibende DCs](AD-Forest-Recovery-Restore-Additional-DCs.md)  
  
     Erneut bereitstellen der Gesamtstruktur, die sie in den Zustand vor Auftreten des Fehlers zurück. Dieser Schrittmuss an Ihre spezifischen Entwurf und Anforderungen angepasst werden. Klonen virtualisierter Domänencontroller können diesen Vorgang beschleunigen.  
  
5.  [Bereinigung](AD-Forest-Recovery-Cleanup.md)  
  
     Nach der Wiederherstellung Funktionen Konfigurieren der Namensauflösung nach Bedarf neu, und rufen Sie Branchenanwendungen arbeiten.  

  
 Die Schrittein diesem Handbuch dienen zur gefährliche Daten in der wiederhergestellten Gesamtstruktur darin die Möglichkeit zu verringern. Möglicherweise müssen Sie folgendermaßen vor, um für Faktoren wie der Konto zu ändern:  
  
-   Skalierbarkeit  
-   Remote-Verwaltung  
-   Geschwindigkeit der Wiederherstellung  

