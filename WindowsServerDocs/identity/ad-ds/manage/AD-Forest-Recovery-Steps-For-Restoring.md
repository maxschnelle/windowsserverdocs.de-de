---
title: Wiederherstellung der Active Directory-Gesamtstruktur - Schritte für die Wiederherstellung der Gesamtstruktur
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 1712d3a636160f82495539afdd42ab2ee85ffae2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861471"
---
# <a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>Wiederherstellung der Active Directory-Gesamtstruktur - Schritte für die Wiederherstellung der Gesamtstruktur

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Dieser Abschnitt enthält eine Übersicht über die empfohlenen Schritte zum Wiederherstellen einer Gesamtstruktur. Schritte zur Wiederherstellung der Gesamtstruktur sind weiter unten im Detail beschrieben.  
  
In der folgende Liste sind die Wiederherstellungsschritte auf hoher Ebene zusammengefasst:  
  
1. [Ermittlung des Problems](AD-Forest-Recovery-Identify-the-Problem.md)  

   Arbeiten mit IT und Support von Microsoft zum Bestimmen des Umfangs des Problems und mögliche Ursachen und mögliche Abhilfen mit allen Projektbeteiligten auswerten. In vielen Fällen sollte die Wiederherstellung der gesamten Gesamtstruktur die letzte Option sein.  
  
2. [Entscheiden Sie, wie die Gesamtstruktur wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)  

   Nachdem Sie ermittelt, dass die Wiederherstellung der Gesamtstruktur erforderlich ist, vollständige Preliminary Schritte aus, um dafür vorbereiten: ermitteln die aktuellen Gesamtstruktur-Struktur, identifizieren Sie die Funktionen, die jeder DC entscheiden, welche Domänencontroller, führt um für jede Domäne wiederherzustellen, und stellen Sie sicher, dass alle beschreibbaren Domänencontroller werden offline geschaltet wird.  

3. [Erste Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)  

   In Isolation Wiederherstellung von einem Domänencontroller für jede Domäne, leeren sie den Ordner und verbinden Sie die Domänen. Zurücksetzen der privilegierte Konten, und Beheben von Problemen aufgrund von Sicherheitslücken in dieser Phase.  
  
4. [Erneutes Bereitstellen der verbleibenden DCs](AD-Forest-Recovery-Restore-Additional-DCs.md)  

   Erneutes Bereitstellen der Gesamtstruktur aus, um den Zustand vor dem Ausfall wiederherzustellen. Dieser Schritt muss an Ihre bestimmten Entwurf und Anforderungen angepasst werden. Klonen von virtualisierten Domänencontrollern können auf diesen Prozess zu beschleunigen.  

5. [Bereinigen](AD-Forest-Recovery-Cleanup.md)  

   Nach Funktionen wiederhergestellt wurde, Konfigurieren der namensauflösung nach Bedarf neu, und erhalten Sie LOB-Anwendungen arbeiten.  

Die Schritte in diesem Handbuch dienen der risikobehafteten Daten in der wiederhergestellten Gesamtstruktur Wiedereinführung unwahrscheinlich ist. Möglicherweise müssen Sie diese Schritte aus, um die Faktoren wie berücksichtigen zu ändern:  
  
- Skalierbarkeit  
- Remote-Verwaltung  
- Geschwindigkeit der Wiederherstellung  
