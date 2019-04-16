---
title: "Migrieren von früheren Versionen nach Windows Server Essentials oder Windows Server Essentials Experience"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/20116
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2974fb3a-5150-43fd-a73f-3e5074eb5d03
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 213ee4304d9d4ebdb7580f7f78fdaca78aa454c9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>Migrieren von früheren Versionen nach Windows Server Essentials oder Windows Server Essentials Experience

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Handbuch beschreibt die von früheren Versionen von Windows Small Business Server und Windows Server Essentials (einschließlich Windows Server Essentials, Windows Small Business Server 2011 Standard, Windows Small Business Server 2011 Essentials, Windows Small Business Server 2008 und Windows Small Business Server 2003) zu Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle migrieren.  
  
 **Für Umgebungen mit bis zu 25 Benutzern und 50 Geräten**, Sie können die Schritte in dieser Anleitung zum Migrieren von früheren Versionen von Windows SBS zu Windows Server Essentials.  
  
 **Für Umgebungen mit bis zu 100 Benutzern und 200 Geräten**, können Sie die gleiche Anweisungen zum Migrieren auf die Standard oder Datacenter-Editionen von Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle ausführen.  
  
> [!NOTE]
>  Zur Vermeidung von Problemen während der Migration, empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dass Sie dieses Dokument lesen, bevor Sie mit die Migration beginnen.  
  
## <a name="terms-and-definitions"></a>Begriffe und Definitionen  
 **Quellserver** der vorhandenen Server, von dem Sie Ihre Einstellungen und Daten migrieren.  
  
 **Zielserver** der neue Server, auf den migrieren Sie die Einstellungen und Daten.  
  
## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses  
 Dieses Migrationshandbuch umfasst die folgenden Schritte aus:  
  
1.  [Schritt 1: Vorbereiten die Quelle für Windows Server Essentials-Migration](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und dem Netzwerk für die Migration bereit sind. Dieser Abschnitt führt Sie durch den Quellserver sichern, die Systemintegrität des Quellservers auswerten, die neuesten Servicepacks und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2.  [Schritt 2: Installieren Sie Windows Server Essentials als einen neuen Replikatdomänencontroller](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md). In diesem Abschnitt wird beschrieben, wie zum Installieren von Windows Server Essentials oder Windows Server 2012 R2 Standard (mit aktivierter Windows Server Essentials Experience-Rolle) als Domänencontroller.  
  
3.  [Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md).  In diesem Abschnitt wird erläutert, wie Hinzufügen von Clientcomputern mit dem neuen Server Windows Server Essentials ausgeführt wird und die gruppenrichtlinieneinstellungen aktualisiert werden.  
  
4.  [Schritt 4: Verschieben von Einstellungen und Daten auf den Zielserver für Windows Server Essentials-Migration](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5.  [Schritt 5: Aktivieren der ordnerumleitung auf dem Zielserver für Windows Server Essentials-Migration](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Wenn die ordnerumleitung auf dem Quellserver aktiviert ist, können Sie Aktivieren der ordnerumleitung auf dem Zielserver, und löschen Sie die alte Gruppenrichtlinie zur Ordnerumleitung-Einstellung.  
  
6.  [Schritt 6: Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers aus dem Netzwerk, müssen Sie eine Aktualisierung der Gruppenrichtlinie zu erzwingen und den Quellserver tiefer stufen.  
  
7.  [Schritt 7: Ausführen von Aufgaben nach der Migration für die Windows Server Essentials-Migration](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md).  Nach Abschluss der Migration aller Einstellungen und Daten zu Windows Server Essentials, sollten Sie Benutzerkonten zugelassene Computer zuordnen.  
  
8.  [Schritt 8: Ausführen der Windows Server Essentials Best Practices Analyzer](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nach Abschluss der Migration der Einstellungen und Daten zu Windows Server Essentials, sollten Sie die Windows Server Essentials Best Practices Analyzer (BPA) ausführen.  
  
 Mehrere der Migrationsverfahren erfordern, dass Sie ein Eingabeaufforderungsfenster als Administrator öffnen. Die folgenden Verfahren wird erläutert, wie das geht.  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a>So öffnen Sie ein Eingabeaufforderungsfenster auf dem Quellserver als administrator  
  
1.  Klicken Sie auf **starten**.  
  
2.  Geben Sie in das Suchfeld **Cmd**.  
  
3.  In der Liste der Ergebnisse, mit der rechten Maustaste **Cmd**, und klicken Sie dann auf **als Administrator ausführen**.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>So öffnen Sie ein Eingabeaufforderungsfenster auf dem Zielserver als administrator  
  
1.  Auf der **starten** Bildschirm, in das Suchfeld, geben **Cmd**.  
  
2.  In der Liste der Ergebnisse, mit der rechten Maustaste **Cmd**, und klicken Sie dann auf **als Administrator ausführen**.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

