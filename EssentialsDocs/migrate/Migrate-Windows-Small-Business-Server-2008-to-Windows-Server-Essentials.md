---
title: Migration von Windows Small Business Server 2008 zu Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 71e3243e-2da9-409a-ae1f-813d4c9062e1
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 81bb6a55efa3fef0154eda500e13928ac5db5b9e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625840"
---
# <a name="migrate-windows-small-business-server-2008-to-windows-server-essentials"></a>Migration von Windows Small Business Server 2008 zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

In diesem Leitfaden wird beschrieben, wie Sie eine vorhandene Windows SSB 2008-Domäne &reg; auf neuer Hardware zu Windows Server 2012 Essentials migrieren und dann die Einstellungen und Daten migrieren. Außerdem wird in diesem Handbuch beschrieben, wie Sie den vorhandenen Server aus dem Windows Server Essentials-Netzwerk entfernen, nachdem Sie die Migration abgeschlossen haben.

> [!NOTE]
>  Um Probleme während der Migration zu vermeiden, empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dieses Dokument zu lesen, bevor Sie mit der Migration beginnen.
>
> [!NOTE]
>
>  Informationen zum Migrieren der Serverdaten zur neuesten Version von Windows Server Essentials finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).


## <a name="additional-resources"></a>Zusätzliche Ressourcen
 Links zu weiteren Informationen, Tools und Communityressourcen, die Ihnen beim Migrationsprozess behilflich sein können finden Sie auf der Website [Windows Small Business Server-Migration](https://go.microsoft.com/fwlink/?LinkId=217520).

## <a name="terms-and-definitions"></a>Begriffe und Definitionen
 **Quell Server:** Der vorhandene Server, von dem Sie die Einstellungen und Daten migrieren.

 **Ziel Server:** Der neue Server, auf den Sie die Einstellungen und Daten migrieren.

## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses
 Dieses Migrationshandbuch umfasst folgende Schritte:


1.  [Bereiten Sie den Quell Server auf die Migration zu Windows Server Essentials](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)vor.  Sie müssen sicherstellen, dass der Quellserver und das Netzwerk für die Migration bereit sind. Mit den Schritten in diesem Abschnitt können Sie den Quellserver sichern, die Systemintegrität des Quellservers prüfen, die aktuellen Service Packs und Fixes installieren und die Netzwerkkonfiguration überprüfen.

2.  [Installieren Sie Windows Server Essentials im Migrations Modus](Install-Windows-Server-Essentials-in-migration-mode.md).  In diesem Abschnitt werden die Schritte beschrieben, die Sie ausführen müssen, um Windows Server Essentials im Migrations Modus auf dem Ziel Server zu installieren.

3.  [Fügen Sie Computer dem neuen Windows Server Essentials-Netzwerk hinzu](Join-computers-to-the-new-Windows-Server-Essentials-network.md).  In diesem Abschnitt wird das Hinzufügen von Client Computern zum neuen Windows Server Essentials-Netzwerk und das Aktualisieren Gruppenrichtlinie Einstellungen behandelt.

4.  [Verschieben Sie SBS 2008-Einstellungen und Daten auf den Ziel Server](./move-windows-sbs-2008-to-the-destination-server-for-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.

5.  [Aktivieren Sie die Ordner Umleitung auf dem Windows Server Essentials-Ziel Server](Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.

6.  Tiefer stufen [und Entfernen des Quell Servers aus dem neuen Windows Server Essentials-Netzwerk](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers müssen Sie eine Gruppenrichtlinienaktualisierung erzwingen und den Quellserver tiefer stufen.

7.  [Führen Sie die Aufgaben nach der Migration für die Windows Server Essentials-Migration durch](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Nachdem Sie die Migration aller Einstellungen und Daten zu Windows Server Essentials abgeschlossen haben, können Sie zugelassene Computerbenutzer Konten zuordnen.

8.  [Führen Sie das Windows Server Essentials-Best Practices Analyzer](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)aus.  Nachdem Sie die Migration der Einstellungen und Daten zu Windows Server Essentials abgeschlossen haben, sollten Sie den Windows Server Essentials-BPA ausführen.


 Mehrere der Migrationsverfahren erfordern das Öffnen einer Eingabeaufforderung als Administrator.

###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a> So öffnen Sie ein Eingabe Aufforderungs Fenster auf dem Quell Server als Administrator

1.  Klicken Sie auf %%amp;quot;Start%%amp;quot;.

2.  Geben Sie im Suchfeld %%amp;quot;cmd%%amp;quot; ein.

3.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf "cmd", und klicken Sie dann auf "Als Administrator ausführen".

#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>So öffnen Sie auf dem Zielserver ein Eingabeaufforderungsfenster als Administrator

1.  Geben Sie auf dem**Start** Startbildschirm im Suchfeld **cmd** ein.

2.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.