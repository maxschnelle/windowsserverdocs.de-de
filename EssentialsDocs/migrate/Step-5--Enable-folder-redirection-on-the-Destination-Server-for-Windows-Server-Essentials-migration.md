---
title: 'Schritt 5: Aktivieren der ordnerumleitung auf dem Zielserver für Windows Server Essentials-migration'
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3925f80-552d-431f-b2a6-2af202e50ca4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 613ff4c80a80ed4f3207cb0c1ead6db12c723e85
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815381"
---
# <a name="step-5-enable-folder-redirection-on-the-destination-server-for-windows-server-essentials-migration"></a>Schritt 5: Aktivieren der ordnerumleitung auf dem Zielserver für Windows Server Essentials-migration

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.  
  
 Verwenden Sie zunächst das Windows Server Essentials-Dashboard zum Aktivieren der ordnerumleitung auf dem Zielserver. Löschen Sie daraufhint die alte Gruppenrichtlinieneinstellung zur Ordnerumleitung.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>So aktivieren Sie die Ordnerumleitung auf dem Zielserver  
  
1.  Öffnen Sie auf dem Zielserver Windows Server Essentials-Dashboard ein.  
  
2.  Klicken Sie in der Navigationsleiste **Geräte**.  
  
3.  Klicken Sie im Bereich**Geräteaufgaben** auf **Implementieren von Gruppenrichtlinien**.  
  
4.  Wählen Sie auf der Seite **Aktivieren der Richtlinie für die Ordnerumleitung** die Ordner aus, die umgeleitet werden sollen, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite **Sicherheitsrichtlinieneinstellungen aktivieren** auf **Fertig stellen**.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>Löschen der alten Gruppenrichtlinieneinstellung zur Ordnerumleitung.  
  
1.  Öffnen Sie auf dem Zielserver das Verwaltungstool **Gruppenrichtlinienverwaltung**.  
  
2.  In **Gruppenrichtlinienverwaltung**, erweitern Sie **Gesamtstruktur:*** Ihrnetzwerkdomänenname*, erweitern Sie **Domänen**, erweitern Sie *Ihrnetzwerkdomänenname* , und erweitern Sie dann **Group Policy Objects**.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Richtlinie, die Sie löschen möchten und klicken Sie dann auf **Löschen**.  
  
4.  Lesen Sie die Warnung und klicken Sie dann auf **Ja**.  
  
5.  Schließen Sie **Gruppenrichtlinienverwaltung**.  
  
 Um die Änderung für die Ordnerumleitung zu übernehmen, müssen Netzwerkbenutzer zuerst ihre Computer abmelden und dann wieder anmelden. Dadurch wird die Übertragung von allen umgeleiteten Ordnern auf den Zielserver sichergestellt .  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Ordnerumleitung auf dem Zielserver aktiviert. Wechseln Sie nun zur [Schritt 6: Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  
  

Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

