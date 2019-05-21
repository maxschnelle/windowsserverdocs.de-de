---
title: Konfigurieren der Ordnerumleitung auf dem Windows Server Essentials-Zielserver
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827371"
---
# <a name="configure-folder-redirection-on-the-windows-server-essentials-destination-server"></a>Konfigurieren der Ordnerumleitung auf dem Windows Server Essentials-Zielserver

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Führen Sie diese Aufgabe aus, wenn die Ordnerumleitung auf dem Quellserver aktiviert ist.  
  
 Löschen Sie zuerst die alte Gruppenrichtlinieneinstellung zur Ordnerumleitung. Verwenden Sie dann das Windows Server Essentials-Dashboard zum Aktivieren der ordnerumleitung auf dem Zielserver an.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>Löschen der alten Gruppenrichtlinieneinstellung zur Ordnerumleitung.  
  
1.  Öffnen Sie auf dem Zielserver das Verwaltungstool **Gruppenrichtlinienverwaltung**.  
  
2.  In **Gruppenrichtlinienverwaltung**, erweitern Sie **Gesamtstruktur:***Ihrnetzwerkdomänenname*, erweitern Sie **Domänen**, erweitern Sie *Ihrnetzwerkdomänenname* , und erweitern Sie dann **Group Policy Objects**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **SBS Gruppenrichtlinien-Ordnerumleitung**und klicken Sie dann auf **Löschen**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **SBS Gruppenrichtlinien-Sicherheitsvorlagen** und klicken Sie dann auf **Löschen**.  
  
5.  Lesen Sie die Warnung und klicken Sie dann auf **Ja**.  
  
6.  Schließen Sie **Gruppenrichtlinienverwaltung**.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>So aktivieren Sie die Ordnerumleitung auf dem Zielserver  
  
1.  Öffnen Sie auf dem Zielserver Windows Server Essentials-Dashboard ein.  
  
2.  Klicken Sie in der Navigationsleiste auf **Geräte**.  
  
3.  Klicken Sie im Bereich**Geräteaufgaben** auf **Implementieren von Gruppenrichtlinien**.  
  
4.  Wählen Sie auf der Seite **Aktivieren der Richtlinie für die Ordnerumleitung** die Ordner aus, die umgeleitet werden sollen, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite **Sicherheitsrichtlinieneinstellungen aktivieren** auf **Fertig stellen**.  
  
 Um die Änderung an der Ordnerumleitung zu übernehmen, müssen Netzwerkbenutzer zuerst ihren Computer abmelden und dann wieder anmelden. Dadurch wird die Übertragung von allen umgeleiteten Ordnern auf den Zielserver sichergestellt .
