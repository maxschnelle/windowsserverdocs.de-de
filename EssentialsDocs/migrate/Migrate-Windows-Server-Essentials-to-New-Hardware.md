---
title: Migration von Windows Server Essentials zu neuer Hardware
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f695ae90-3160-407b-bebf-9e460f22c86d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 61106439a63a75143a9cca0989c70370adfedd38
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-windows-server-essentials-to-new-hardware"></a>Migration von Windows Server Essentials zu neuer Hardware

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Handbuch beschreibt die Migration von einer vorhandenen Windows Server® 2012 Essentials-Domäne mit Windows Server Essentials auf neuer Hardware und die anschließende Migration der Einstellungen und Daten. Dieses Handbuch beschreibt auch zum Entfernen des vorhandenen Servers aus dem Windows Server Essentials-Netzwerk nach Abschluss der Migration.  
  
> [!NOTE]
>  Zur Vermeidung von Problemen während der Migration empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dass Sie dieses Dokument lesen, bevor Sie mit die Migration beginnen.  
  
> [!NOTE]

>  Zum Migrieren Ihrer Serverdaten auf die neueste Version von Windows Server Essentials finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  

  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
 Links zu weiteren Informationen, Tools und Communityressourcen, die Sie bei der Migration unterstützen, finden Sie auf der [Windows Small Business Server Migration](https://go.microsoft.com/fwlink/?LinkId=217520) Website.  
  
## <a name="terms-and-definitions"></a>Begriffe und Definitionen  
 **Quellserver:** der vorhandenen Server, von dem Sie Ihre Einstellungen und Daten migrieren.  
  
 **Zielserver:** der neue Server, auf den migrieren Sie die Einstellungen und Daten.  
  
## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses  
 Dieses Migrationshandbuch umfasst die folgenden Schritte aus:  
  

1.  [Vorbereiten des Quelle für Windows Server Essentials-Migration](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und dem Netzwerk für die Migration bereit sind. Dieser Abschnitt führt Sie durch den Quellserver sichern, die Systemintegrität des Quellservers auswerten, die neuesten Servicepacks und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2.  [Installieren von Windows Server Essentials im Migrationsmodus](Install-Windows-Server-Essentials-in-migration-mode.md).  Dieser Abschnitt beschreibt die Schritte, die Sie ausführen sollten, um Windows Server Essentials im Migrationsmodus auf dem Zielserver zu installieren.  
  
3.  [Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Join-computers-to-the-new-Windows-Server-Essentials-server.md).  Dieser Abschnitt behandelt, Hinzufügen von Clientcomputern zum neuen Windows Server Essentials-Server und die gruppenrichtlinieneinstellungen aktualisiert wird.  
  
4.  [Verschieben von Einstellungen und Daten auf den Zielserver für Windows Server Essentials-Migration](Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5.  [Konfigurieren der ordnerumleitung auf dem Windows Server Essentials-Zielserver](Configure-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Wenn die ordnerumleitung auf dem Quellserver aktiviert ist, können Sie Aktivieren der ordnerumleitung auf dem Zielserver, und löschen Sie die alte Gruppenrichtlinie zur Ordnerumleitung-Einstellung.  
  
6.  [Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers aus dem Netzwerk, müssen Sie eine Aktualisierung der Gruppenrichtlinie zu erzwingen und den Quellserver tiefer stufen.  
  
7.  [Ausführen von Aufgaben nach der Migration zu Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Nach Abschluss der Migration aller Einstellungen und Daten zu Windows Server Essentials, sollten Sie Benutzerkonten zugelassene Computer zuordnen.  
  
8.  [Führen Sie die Windows Server Essentials Best Practices Analyzer](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nach Abschluss der Migration der Einstellungen und Daten zu Windows Server Essentials, sollten Sie herunterladen und Ausführen von BPA für Windows Server Essentials.  
  
 Mehrere der Migrationsverfahren erfordern, dass Sie ein Eingabeaufforderungsfenster als Administrator öffnen.  
  
#### <a name="to-open-a-command-prompt-window-as-an-administrator"></a>Öffnen Sie ein Eingabeaufforderungsfenster als administrator  
  
1.  Auf der **starten** Bildschirm, in das Suchfeld, geben **Cmd**.  
  
2.  In der Liste der Ergebnisse, mit der rechten Maustaste **Cmd**, und klicken Sie dann auf **als Administrator ausführen**.
