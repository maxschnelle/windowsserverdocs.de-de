---
title: Migration von Windows Server Essentials zu neuer Hardware
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: f59e84877606f65d3f8eb6fd9dc39fe701af8a5a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432937"
---
# <a name="migrate-windows-server-essentials-to-new-hardware"></a>Migration von Windows Server Essentials zu neuer Hardware

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Handbuch beschreibt die Migration von einer vorhandenen Windows Server® 2012 Essentials-Domäne mit Windows Server Essentials auf neuer Hardware und die anschließende Migration der Einstellungen und Daten. Dieses Handbuch wird beschrieben, wie nach dem Abschluss der Migration Ihres vorhandenen Servers aus dem Windows Server Essentials-Netzwerk zu entfernen.  
  
> [!NOTE]
>  Zur Vermeidung von Problemen bei der Migration empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dass das Dokument zu lesen, bevor Sie mit die Migration beginnen.  
> 
> [!NOTE]
> 
>  Zum Migrieren Ihrer Serverdaten auf die neueste Version von Windows Server Essentials finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  

  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
 Links zu weiteren Informationen, Tools und Communityressourcen, helfen Ihnen beim Migrationsprozess, finden Sie auf die [Windows Small Business Server-Migration](https://go.microsoft.com/fwlink/?LinkId=217520) Website.  
  
## <a name="terms-and-definitions"></a>Begriffe und Definitionen  
 **Quellserver:** Der vorhandene Server, von dem Sie die Einstellungen und Daten migrieren.  
  
 **Zielserver:** Der neue Server, zu dem Sie die Einstellungen und Daten migrieren.  
  
## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses  
 Dieses Migrationshandbuch umfasst folgende Schritte:  
  

1. [Vorbereiten des Quelle für Windows Server Essentials-Migration](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und das Netzwerk für die Migration bereit sind. Mit den Schritten in diesem Abschnitt können Sie den Quellserver sichern, die Systemintegrität des Quellservers prüfen, die aktuellen Service Packs und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2. [Installieren von Windows Server Essentials im Migrationsmodus](Install-Windows-Server-Essentials-in-migration-mode.md).  Dieser Abschnitt beschreibt die Schritte, die Sie ausführen sollten, um Windows Server Essentials auf dem Zielserver im Migrationsmodus installieren.  
  
3. [Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Join-computers-to-the-new-Windows-Server-Essentials-server.md).  Dieser Abschnitt enthält, Hinzufügen von Clientcomputern zum neuen Windows Server Essentials-Server und gruppenrichtlinieneinstellungen aktualisiert wird.  
  
4. [Verschieben von Einstellungen und Daten auf den Zielserver für Windows Server Essentials-Migration](Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5. [Konfigurieren der ordnerumleitung auf dem Windows Server Essentials-Zielserver](Configure-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.  
  
6. [Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers müssen Sie eine Gruppenrichtlinienaktualisierung erzwingen und den Quellserver tiefer stufen.  
  
7. [Ausführen von Aufgaben nach der Migration zu Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Nach Abschluss der Migration aller Einstellungen und Daten zu Windows Server Essentials, können Sie Benutzerkonten zugelassene Computer zuordnen möchten.  
  
8. [Ausführen der Windows Server Essentials Best Practices Analyzer](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nach Abschluss der Migration der Einstellungen und Daten zu Windows Server Essentials herunter, und führen Sie den BPA für Windows Server Essentials.  
  
   Mehrere der Migrationsverfahren erfordern das Öffnen einer Eingabeaufforderung als Administrator.  
  
#### <a name="to-open-a-command-prompt-window-as-an-administrator"></a>Öffnen eines Eingabeaufforderungsfensters als Administrator.  
  
1.  Geben Sie auf dem**Start** Startbildschirm im Suchfeld **cmd** ein.  
  
2.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.
