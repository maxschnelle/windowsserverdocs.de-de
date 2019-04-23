---
title: Migration von Windows Small Business Server 2011 Essentials zu Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32fc90d8-31c5-4c7e-9fe3-483cf3c35f78
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5d65429e31e43aa15d1631878ae7e1486e9fd60f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835151"
---
# <a name="migrate-windows-small-business-server-2011-essentials-to-windows-server-essentials"></a>Migration von Windows Small Business Server 2011 Essentials zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Handbuch beschreibt die Migration von einer vorhandenen Windows Small Business Server 2011 Essentials-Domäne zu Windows Server® 2012 Essentials, und die anschließende Migration der Einstellungen und Daten. Dieses Handbuch wird beschrieben, wie nach dem Abschluss der Migration Ihres vorhandenen Servers aus dem Windows Server Essentials-Netzwerk zu entfernen.  
  
> [!NOTE]
>  Zur Vermeidung von Problemen bei der Migration empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dass das Dokument zu lesen, bevor Sie mit die Migration beginnen.  
  
> [!NOTE]

>  Zum Migrieren Ihrer Serverdaten auf die neueste Version von Windows Server Essentials finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  

>  Zum Migrieren Ihrer Serverdaten auf die neueste Version von Windows Server Essentials finden Sie unter [Migrieren zu Windows Server Essentials](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  

  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
 Links zu weiteren Informationen, Tools und Communityressourcen, helfen Ihnen beim Migrationsprozess, finden Sie unter [Windows Small Business Server-Migration](https://go.microsoft.com/fwlink/?LinkId=217520).  
  
## <a name="terms-and-definitions"></a>Begriffe und Definitionen  
 **Quellserver:** Der vorhandene Server, von dem Sie die Einstellungen und Daten migrieren.  
  
 **Zielserver:** Der neue Server, zu dem Sie die Einstellungen und Daten migrieren.  
  
## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses  
 Dieses Migrationshandbuch umfasst folgende Schritte:  
  

1.  [Vorbereiten des Quelle für Windows Server Essentials-Migration](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und das Netzwerk für die Migration bereit sind. Mit den Schritten in diesem Abschnitt können Sie den Quellserver sichern, die Systemintegrität des Quellservers prüfen, die aktuellen Service Packs und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2.  [Installieren von Windows Server Essentials im Migrationsmodus](Install-Windows-Server-Essentials-in-migration-mode.md).  Dieser Abschnitt beschreibt die Schritte, die Sie ausführen sollten, um Windows Server Essentials auf dem Zielserver im Migrationsmodus installieren.  
  
3.  [Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Join-computers-to-the-new-Windows-Server-Essentials-server.md).  Dieser Abschnitt enthält, Hinzufügen von Clientcomputern zum neuen Windows Server Essentials-Server und gruppenrichtlinieneinstellungen aktualisiert wird.  
  
4.  [Verschieben von SBS 2011 Essentials-Einstellungen und Daten auf den Zielserver](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5.  [Aktivieren der ordnerumleitung auf dem Windows Server Essentials-Zielserver](Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.  
  
6.  [Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers müssen Sie eine Gruppenrichtlinienaktualisierung erzwingen und den Quellserver tiefer stufen.  
  
7.  [Ausführen von Aufgaben nach der Migration zu Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Nach Abschluss der Migration aller Einstellungen und Daten zu Windows Server Essentials, können Sie Benutzerkonten zugelassene Computer zuordnen möchten.  
  
8.  [Ausführen der Windows Server Essentials Best Practices Analyzer](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nach Abschluss der Migration der Einstellungen und Daten zu Windows Server Essentials herunter, und führen Sie den BPA für Windows Server Essentials.  

1.  [Vorbereiten des Quelle für Windows Server Essentials-Migration](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und das Netzwerk für die Migration bereit sind. Mit den Schritten in diesem Abschnitt können Sie den Quellserver sichern, die Systemintegrität des Quellservers prüfen, die aktuellen Service Packs und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2.  [Installieren von Windows Server Essentials im Migrationsmodus](../migrate/Install-Windows-Server-Essentials-in-migration-mode.md).  Dieser Abschnitt beschreibt die Schritte, die Sie ausführen sollten, um Windows Server Essentials auf dem Zielserver im Migrationsmodus installieren.  
  
3.  [Hinzufügen von Computern zum neuen Windows Server Essentials-Server](../migrate/Join-computers-to-the-new-Windows-Server-Essentials-server.md).  Dieser Abschnitt enthält, Hinzufügen von Clientcomputern zum neuen Windows Server Essentials-Server und gruppenrichtlinieneinstellungen aktualisiert wird.  
  
4.  [Verschieben von SBS 2011 Essentials-Einstellungen und Daten auf den Zielserver](../migrate/Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5.  [Aktivieren der ordnerumleitung auf dem Windows Server Essentials-Zielserver](../migrate/Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.  
  
6.  [Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers müssen Sie eine Gruppenrichtlinienaktualisierung erzwingen und den Quellserver tiefer stufen.  
  
7.  [Ausführen von Aufgaben nach der Migration zu Windows Server Essentials](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Nach Abschluss der Migration aller Einstellungen und Daten zu Windows Server Essentials, können Sie Benutzerkonten zugelassene Computer zuordnen möchten.  
  
8.  [Ausführen der Windows Server Essentials Best Practices Analyzer](../migrate/Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nach Abschluss der Migration der Einstellungen und Daten zu Windows Server Essentials herunter, und führen Sie den BPA für Windows Server Essentials.  

  
 Mehrere der Migrationsverfahren erfordern, dass Sie ein Eingabeaufforderungsfenster als Administrator öffnen.  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a> So öffnen Sie ein Eingabeaufforderungsfenster auf dem Quellserver als administrator  
  
1.  Klicken Sie auf **Start**.  
  
2.  Geben Sie im Suchfeld **Cmd** ein.  
  
3.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>So öffnen Sie ein Eingabeaufforderungsfenster auf dem Zielserver als Administrator  
  
1.  Geben Sie auf dem**Start** Startbildschirm im Suchfeld **cmd** ein.  
  
2.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.
