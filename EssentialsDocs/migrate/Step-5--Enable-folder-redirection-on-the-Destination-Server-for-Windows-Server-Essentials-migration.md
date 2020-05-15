---
title: 'Schritt 5: Aktivieren der Ordnerumleitung auf dem Zielserver für die Migration nach Windows Server Essentials'
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: d3925f80-552d-431f-b2a6-2af202e50ca4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9f698111bd88619406e47db9d484c2197e91dd83
ms.sourcegitcommit: 2f072c0c02e3e0deae331ca64b375d63b89d0522
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83404537"
---
# <a name="step-5-enable-folder-redirection-on-the-destination-server-for-windows-server-essentials-migration"></a>Schritt 5: Aktivieren der Ordnerumleitung auf dem Zielserver für die Migration nach Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.  
  
 Verwenden Sie zunächst das Windows Server Essentials-Dashboard, um die Ordner Umleitung auf dem Ziel Server zu aktivieren. Löschen Sie daraufhint die alte Gruppenrichtlinieneinstellung zur Ordnerumleitung.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>So aktivieren Sie die Ordnerumleitung auf dem Zielserver  
  
1.  Öffnen Sie auf dem Ziel Server das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie in der Navigationsleiste **Geräte**.  
  
3.  Klicken Sie im Bereich**Geräteaufgaben** auf **Implementieren von Gruppenrichtlinien**.  
  
4.  Wählen Sie auf der Seite **Aktivieren der Richtlinie für die Ordnerumleitung** die Ordner aus, die umgeleitet werden sollen, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite **Sicherheitsrichtlinieneinstellungen aktivieren** auf **Fertig stellen**.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>Löschen der alten Gruppenrichtlinieneinstellung zur Ordnerumleitung.  
  
1. Öffnen Sie auf dem Zielserver das Verwaltungstool **Gruppenrichtlinienverwaltung**.  
  
2. Erweitern Sie in **Gruppenrichtlinienverwaltung**den Eintrag **Gesamtstruktur:**<em>IhrNetzwerkDomänenname</em>den Eintrag **Domänen**den Eintrag *IhrNetzwerkDomänenname*und erweitern Sie dann **Gruppenrichtlinienobjekte**.  
  
3. Klicken Sie mit der rechten Maustaste auf die Richtlinie, die Sie löschen möchten und klicken Sie dann auf **Löschen**.  
  
4. Lesen Sie die Warnung und klicken Sie dann auf **Ja**.  
  
5. Schließen Sie die **Gruppenrichtlinienverwaltung**.  
  
   Um die Änderung für die Ordnerumleitung zu übernehmen, müssen Netzwerkbenutzer zuerst ihre Computer abmelden und dann wieder anmelden. Dadurch wird die Übertragung von allen umgeleiteten Ordnern auf den Zielserver sichergestellt .  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Ordnerumleitung auf dem Zielserver aktiviert. Gehen Sie jetzt zu [Schritt 6: herabstufen und Entfernen des Quell Servers aus dem neuen Windows Server Essentials-Netzwerk](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  
  

Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

