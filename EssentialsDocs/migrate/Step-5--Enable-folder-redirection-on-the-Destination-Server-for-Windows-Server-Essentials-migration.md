---
title: "Schritt5: Aktivieren der ordnerumleitung auf dem Zielserver für Windows Server Essentials-Migration"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="step-5-enable-folder-redirection-on-the-destination-server-for-windows-server-essentials-migration"></a>Schritt5: Aktivieren der ordnerumleitung auf dem Zielserver für Windows Server Essentials-Migration

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Wenn die ordnerumleitung auf dem Quellserver aktiviert ist, können Sie Aktivieren der ordnerumleitung auf dem Zielserver, und löschen Sie die alte Gruppenrichtlinie zur Ordnerumleitung-Einstellung.  
  
 Verwenden Sie zunächst das Windows Server Essentials-Dashboard zum Aktivieren der ordnerumleitung auf dem Zielserver. Löschen Sie die alte Gruppenrichtlinie zur Ordnerumleitung-Einstellung.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>Zum Aktivieren der ordnerumleitung auf dem Zielserver  
  
1.  Öffnen Sie auf dem Zielserver Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie in der Navigationsleiste auf **Geräte**.  
  
3.  In der **Geräteaufgaben** Bereich, klicken Sie auf **Gruppenrichtlinie implementieren**.  
  
4.  Auf der **aktivieren Gruppenrichtlinie zur Ordnerumleitung** Seite, wählen Sie die Ordner umgeleitet werden, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Sicherheitsrichtlinieneinstellungen aktivieren** auf **Fertig stellen**.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>So löschen Sie die alte Gruppenrichtlinie zur Ordnerumleitung-Einstellung  
  
1.  Öffnen Sie auf dem Zielserver die **Gruppenrichtlinienverwaltung** Verwaltungstool.  
  
2.  In **die Gruppenrichtlinien-Verwaltungskonsole**, erweitern Sie **Gesamtstruktur:***YourNetworkDomainName*, erweitern Sie **Domänen**, erweitern Sie *YourNetworkDomainName*, und erweitern Sie dann **Group Policy Objects**.  
  
3.  Mit der rechten Maustaste der Richtlinie, die Sie löschen möchten, und klicken Sie dann auf **löschen**.  
  
4.  Lesen Sie die Warnung, und klicken Sie dann auf **Ja**.  
  
5.  Schließen **Gruppenrichtlinienverwaltung**.  
  
 Um die Änderung für die ordnerumleitung zu übernehmen, müssen Benutzer im Netzwerk ihren Computern abmelden und dann wieder anmelden. Dadurch wird die Übertragung von allen umgeleiteten Ordnern auf den Zielserver sichergestellt.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die ordnerumleitung auf dem Zielserver aktiviert. Lesen Sie jetzt [Schritt6: Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  
  

Alle Schrittefinden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

