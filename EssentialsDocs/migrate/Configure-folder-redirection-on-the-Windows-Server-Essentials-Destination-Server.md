---
title: Konfigurieren der ordnerumleitung auf dem Windows Server Essentials-Zielserver
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe77ba67-128c-4fc3-9361-30fa6af42516
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 7cc1207f36d3a921b49cc3ecd02acf3fe4fa243c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-folder-redirection-on-the-windows-server-essentials-destination-server"></a>Konfigurieren der ordnerumleitung auf dem Windows Server Essentials-Zielserver

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Führen Sie diese Aufgabe aus, wenn die ordnerumleitung auf dem Quellserver aktiviert ist.  
  
 Löschen Sie zuerst die alte Gruppenrichtlinie zur Ordnerumleitung-Einstellung. Verwenden Sie dann die Windows Server Essentials-Dashboard zum Aktivieren der ordnerumleitung auf dem Zielserver.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>So löschen Sie die alte Gruppenrichtlinie zur Ordnerumleitung-Einstellung  
  
1.  Öffnen Sie auf dem Zielserver die **Gruppenrichtlinienverwaltung** Verwaltungstool.  
  
2.  In **die Gruppenrichtlinien-Verwaltungskonsole**, erweitern Sie **Gesamtstruktur:***YourNetworkDomainName*, erweitern Sie **Domänen**, erweitern Sie *YourNetworkDomainName*, und erweitern Sie dann **Group Policy Objects**.  
  
3.  Mit der rechten Maustaste **SBS Gruppenrichtlinien-Ordnerumleitung**, und klicken Sie dann auf **löschen**.  
  
4.  Mit der rechten Maustaste **SBS Gruppenrichtlinien-Sicherheitsvorlagen**, und klicken Sie dann auf **löschen**.  
  
5.  Lesen Sie die Warnung, und klicken Sie dann auf **Ja**.  
  
6.  Schließen **Gruppenrichtlinienverwaltung**.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>Zum Aktivieren der ordnerumleitung auf dem Zielserver  
  
1.  Öffnen Sie auf dem Zielserver Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie in der Navigationsleiste auf **Geräte**.  
  
3.  In der **Geräteaufgaben** Bereich, klicken Sie auf **Gruppenrichtlinie implementieren**.  
  
4.  Auf der **aktivieren Gruppenrichtlinie zur Ordnerumleitung** Seite, wählen Sie die Ordner umgeleitet werden, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Sicherheitsrichtlinieneinstellungen aktivieren** auf **Fertig stellen**.  
  
 Um die Änderung an der ordnerumleitung zu übernehmen, müssen Benutzer im Netzwerk ihren Computer abmelden und dann wieder anmelden. Dadurch wird die Übertragung von allen umgeleiteten Ordnern auf den Zielserver sichergestellt.
