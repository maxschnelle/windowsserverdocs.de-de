---
title: Migration von Windows Small Business Server 2003 zu Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 119a7fbc-2c76-4aa3-8a7f-c7073d461b5b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f7dfa203f999e23b52c8fcf1f861a59f4f399d95
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852523"
---
# <a name="migrate-windows-small-business-server-2003-to-windows-server-essentials"></a>Migration von Windows Small Business Server 2003 zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

In diesem Leitfaden wird beschrieben, wie Sie eine vorhandene Windows SSB 2003-Domäne zu Windows Server&reg; 2012 Essentials auf neuer Hardware migrieren und dann die Einstellungen und Daten migrieren. Außerdem wird in diesem Handbuch beschrieben, wie Sie den vorhandenen Server aus dem Windows Server Essentials-Netzwerk entfernen, nachdem Sie die Migration abgeschlossen haben.  
  
> [!IMPORTANT]
>   Windows Server Essentials erfordert eine 64-Bit-Umgebung.  Windows Server Essentials unterstützt keine 32-Bit-Umgebung.  
> 
> [!NOTE]
>  Um Probleme während der Migration zu vermeiden, empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dieses Dokument zu lesen, bevor Sie mit der Migration beginnen.  
> 
> [!NOTE]
> 
>  Informationen zum Migrieren der Serverdaten zur neuesten Version von Windows Server Essentials finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  
> 
>  Informationen zum Migrieren der Serverdaten zur neuesten Version von Windows Server Essentials finden Sie unter [Migrieren zu Windows Server Essentials](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  

  
## <a name="additional-resources"></a>Weitere Ressourcen  
 Links zu weiteren Informationen, Tools und Communityressourcen, die Ihnen den Migrationsprozess erleichtern, finden Sie auf der [Windows Small Business Server-Migrations](https://go.microsoft.com/fwlink/?LinkId=217520) Website.  
  
## <a name="terms-and-definitions"></a>Begriffe und Definitionen  
 **Quell Server:** Der vorhandene Server, von dem Sie die Einstellungen und Daten migrieren.  
  
 **Ziel Server:** Der neue Server, auf den Sie die Einstellungen und Daten migrieren.  
  
## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses  
 Dieses Migrationshandbuch umfasst folgende Schritte:  
  

1.  [Bereiten Sie den Quell Server auf die Migration zu Windows Server Essentials](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)vor.  Sie müssen sicherstellen, dass der Quellserver und das Netzwerk für die Migration bereit sind. Mit den Schritten in diesem Abschnitt können Sie den Quellserver sichern, die Systemintegrität des Quellservers prüfen, die aktuellen Service Packs und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2.  [Installieren Sie Windows Server Essentials im Migrations Modus](Install-Windows-Server-Essentials-in-migration-mode.md).  In diesem Abschnitt werden die Schritte beschrieben, die Sie ausführen müssen, um Windows Server Essentials im Migrations Modus auf dem Ziel Server zu installieren.  
  
3.  [Fügen Sie Computer dem neuen Windows Server Essentials-Netzwerk hinzu](Join-computers-to-the-new-Windows-Server-Essentials-network.md).  In diesem Abschnitt wird das Hinzufügen von Client Computern zum neuen Windows Server Essentials-Netzwerk und das Aktualisieren Gruppenrichtlinie Einstellungen behandelt.  
  
4.  [Verschieben Sie SBS 2003-Einstellungen und Daten auf den Ziel Server](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5.  [Aktivieren Sie die Ordner Umleitung auf dem Windows Server Essentials-Ziel Server](Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.  
  
6.  Tiefer stufen [und Entfernen des Quell Servers aus dem neuen Windows Server Essentials-Netzwerk](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers müssen Sie eine Gruppenrichtlinienaktualisierung erzwingen und den Quellserver tiefer stufen.  
  
7.  [Führen Sie die Aufgaben nach der Migration für die Windows Server Essentials-Migration durch](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Nachdem Sie die Migration aller Einstellungen und Daten zu Windows Server Essentials abgeschlossen haben, können Sie zugelassene Computerbenutzer Konten zuordnen.  
  
8.  [Führen Sie das Windows Server Essentials-Best Practices Analyzer](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)aus.  Nachdem Sie die Migration der Einstellungen und Daten zu Windows Server Essentials abgeschlossen haben, sollten Sie den Windows Server Essentials-BPA herunterladen und ausführen.   

  
 Mehrere der Migrationsverfahren erfordern das Öffnen einer Eingabeaufforderung als Administrator.  
  
###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a>So öffnen Sie ein Eingabe Aufforderungs Fenster auf dem Quell Server als Administrator  
  
1.  Klicken Sie auf Start.  
  
2.  Geben Sie im Suchfeld Cmd ein.  
  
3.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf cmd, und klicken Sie dann auf Als Administrator ausführen.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>So öffnen Sie auf dem Zielserver ein Eingabeaufforderungsfenster als Administrator  
  
1.  Geben Sie auf dem**Start** Startbildschirm im Suchfeld **cmd** ein.  
  
2.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.
