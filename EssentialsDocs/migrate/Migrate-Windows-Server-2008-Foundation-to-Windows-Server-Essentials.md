---
title: Migrieren von Windows Server 2008 Foundation zu Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f22fc0a4-cb82-4e60-afe6-2d03145745e7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 22721833d3ba97c7860c949764d565415bbc7cab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-windows-server-2008-foundation-to-windows-server-essentials"></a>Migrieren von Windows Server 2008 Foundation zu Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Handbuch beschreibt die Migration einer vorhandenen Windows Server 2008 Foundation-Domäne mit Windows Server® 2012 Essentials auf neuer Hardware und die anschließende Migration der Einstellungen und Daten. Dieses Handbuch beschreibt auch zum Entfernen des vorhandenen Servers aus dem Windows Server Essentials-Netzwerk nach Abschluss der Migration.  
  
> [!NOTE]
>  Zur Vermeidung von Problemen während der Migration empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dass Sie dieses Dokument lesen, bevor Sie mit die Migration beginnen.  
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
 Links zu weiteren Informationen, Tools und Communityressourcen, die Sie bei der Migration unterstützen, finden Sie unter [Windows Small Business Server Migration](https://go.microsoft.com/fwlink/?LinkId=217520).  
  
## <a name="terms-and-definitions"></a>Begriffe und Definitionen  
 **Quellserver:** der vorhandenen Server, von dem Sie Ihre Einstellungen und Daten migrieren.  
  
 **Zielserver:** der neue Server, auf den migrieren Sie die Einstellungen und Daten.  
  
## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses  
 Dieses Migrationshandbuch umfasst die folgenden Schritte aus:  
  

1.  [Vorbereiten des Quelle für Windows Server Essentials-Migration](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und dem Netzwerk für die Migration bereit sind. Dieser Abschnitt führt Sie durch den Quellserver sichern, die Systemintegrität des Quellservers auswerten, die neuesten Servicepacks und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2.  [Installieren von Windows Server Essentials im Migrationsmodus](Install-Windows-Server-Essentials-in-migration-mode.md).  Dieser Abschnitt beschreibt die Schritte, die Sie ausführen sollten, um Windows Server Essentials im Migrationsmodus auf dem Zielserver zu installieren.  
  
3.  [Hinzufügen von Computern zum neuen Windows Server Essentials-Netzwerk](Join-computers-to-the-new-Windows-Server-Essentials-network.md).  Dieser Abschnitt behandelt Hinzufügen von Clientcomputern zum neuen Windows Server Essentials-Netzwerk und Aktualisieren von gruppenrichtlinieneinstellungen.  
  
4.  [Verschieben von Windows Server 2008 Foundation-Einstellungen und Daten auf den Zielserver](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5.  [Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers aus dem Netzwerk, müssen Sie eine Aktualisierung der Gruppenrichtlinie zu erzwingen und den Quellserver tiefer stufen.  
  
6.  [Ausführen von Aufgaben nach der Migration zu Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Nach Abschluss der Migration aller Einstellungen und Daten zu Windows Server Essentials, sollten Sie Benutzerkonten zugelassene Computer zuordnen.  
  
7.  [Führen Sie die Windows Server Essentials Best Practices Analyzer](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nach Abschluss der Migration der Einstellungen und Daten zu Windows Server Essentials, sollten Sie den BPA für Windows Server Essentials ausführen.  

1.  [Vorbereiten des Quelle für Windows Server Essentials-Migration](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und dem Netzwerk für die Migration bereit sind. Dieser Abschnitt führt Sie durch den Quellserver sichern, die Systemintegrität des Quellservers auswerten, die neuesten Servicepacks und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2.  [Installieren von Windows Server Essentials im Migrationsmodus](../migrate/Install-Windows-Server-Essentials-in-migration-mode.md).  Dieser Abschnitt beschreibt die Schritte, die Sie ausführen sollten, um Windows Server Essentials im Migrationsmodus auf dem Zielserver zu installieren.  
  
3.  [Hinzufügen von Computern zum neuen Windows Server Essentials-Netzwerk](../migrate/Join-computers-to-the-new-Windows-Server-Essentials-network.md).  Dieser Abschnitt behandelt Hinzufügen von Clientcomputern zum neuen Windows Server Essentials-Netzwerk und Aktualisieren von gruppenrichtlinieneinstellungen.  
  
4.  [Verschieben von Windows Server 2008 Foundation-Einstellungen und Daten auf den Zielserver](../migrate/Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5.  [Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers aus dem Netzwerk, müssen Sie eine Aktualisierung der Gruppenrichtlinie zu erzwingen und den Quellserver tiefer stufen.  
  
6.  [Ausführen von Aufgaben nach der Migration zu Windows Server Essentials](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Nach Abschluss der Migration aller Einstellungen und Daten zu Windows Server Essentials, sollten Sie Benutzerkonten zugelassene Computer zuordnen.  
  
7.  [Führen Sie die Windows Server Essentials Best Practices Analyzer](../migrate/Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nach Abschluss der Migration der Einstellungen und Daten zu Windows Server Essentials, sollten Sie den BPA für Windows Server Essentials ausführen.  

  
 Mehrere der Migrationsverfahren erfordern, dass Sie ein Eingabeaufforderungsfenster als Administrator öffnen.  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a>So öffnen Sie ein Eingabeaufforderungsfenster auf dem Quellserver als administrator  
  
1.  Klicken Sie auf **starten**.  
  
2.  Geben Sie in das Suchfeld **Cmd**.  
  
3.  In der Liste der Ergebnisse, mit der rechten Maustaste **Cmd**, und klicken Sie dann auf **als Administrator ausführen**.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>So öffnen Sie ein Eingabeaufforderungsfenster auf dem Zielserver als administrator  
  
1.  Auf der **starten** Bildschirm, in das Suchfeld, geben **Cmd**.  
  
2.  In der Liste der Ergebnisse, mit der rechten Maustaste **Cmd**, und klicken Sie dann auf **als Administrator ausführen**.
