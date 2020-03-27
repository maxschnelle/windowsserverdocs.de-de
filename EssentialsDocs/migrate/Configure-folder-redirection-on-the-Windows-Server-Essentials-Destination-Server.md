---
title: Konfigurieren der Ordnerumleitung auf dem Windows Server Essentials-Zielserver
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe77ba67-128c-4fc3-9361-30fa6af42516
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 44fb54a654689285c5db6d178e6d1c714779b91b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310602"
---
# <a name="configure-folder-redirection-on-the-windows-server-essentials-destination-server"></a>Konfigurieren der Ordnerumleitung auf dem Windows Server Essentials-Zielserver

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Führen Sie diese Aufgabe aus, wenn die Ordnerumleitung auf dem Quellserver aktiviert ist.  
  
 Löschen Sie zuerst die alte Gruppenrichtlinieneinstellung zur Ordnerumleitung. Verwenden Sie dann das Windows Server Essentials-Dashboard, um die Ordner Umleitung auf dem Ziel Server zu aktivieren.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>Löschen der alten Gruppenrichtlinieneinstellung zur Ordnerumleitung.  
  
1. Öffnen Sie auf dem Zielserver das Verwaltungstool **Gruppenrichtlinienverwaltung**.  
  
2. Erweitern Sie in **Gruppenrichtlinienverwaltung**den Eintrag **Gesamtstruktur:** <em>IhrNetzwerkDomänenname</em>den Eintrag **Domänen**den Eintrag *IhrNetzwerkDomänenname*und erweitern Sie dann **Gruppenrichtlinienobjekte**.  
  
3. Klicken Sie mit der rechten Maustaste auf **SBS Gruppenrichtlinien-Ordnerumleitung** und klicken Sie dann auf **Löschen**.  
  
4. Klicken Sie mit der rechten Maustaste auf **SBS Gruppenrichtlinien-Sicherheitsvorlagen** und klicken Sie dann auf **Löschen**.  
  
5. Lesen Sie die Warnung und klicken Sie dann auf **Ja**.  
  
6. Schließen Sie **Gruppenrichtlinienverwaltung**.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>So aktivieren Sie die Ordnerumleitung auf dem Zielserver  
  
1. Öffnen Sie auf dem Ziel Server das Windows Server Essentials-Dashboard.  
  
2. Klicken Sie in der Navigationsleiste auf **Geräte**.  
  
3. Klicken Sie im Bereich**Geräteaufgaben** auf **Implementieren von Gruppenrichtlinien**.  
  
4. Wählen Sie auf der Seite **Aktivieren der Richtlinie für die Ordnerumleitung** die Ordner aus, die umgeleitet werden sollen, und klicken Sie dann auf **Weiter**.  
  
5. Klicken Sie auf der Seite **Sicherheitsrichtlinieneinstellungen aktivieren** auf **Fertig stellen**.  
  
   Um die Änderung an der Ordnerumleitung zu übernehmen, müssen Netzwerkbenutzer zuerst ihren Computer abmelden und dann wieder anmelden. Dadurch wird die Übertragung von allen umgeleiteten Ordnern auf den Zielserver sichergestellt .
