---
title: Migrieren von früheren Versionen nach Windows Server Essentials oder Windows Server Essentials Experience
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883871"
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>Migrieren von früheren Versionen nach Windows Server Essentials oder Windows Server Essentials Experience

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Handbuch beschreibt die Migration von früheren Versionen von Windows Small Business Server und Windows Server Essentials (einschließlich Windows Server Essentials, Windows Small Business Server 2011 Standard, Windows Small Business Server 2011 Essentials, Windows Small Business Server 2008 und Windows Small Business Server 2003) zu Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle.  
  
 **Für Umgebungen mit bis zu 25 Benutzern und 50 Geräten**, Sie können die Schritte in diesem Handbuch Migrieren von früheren Versionen von Windows SBS zu Windows Server Essentials.  
  
 **Für Umgebungen mit bis zu 100 Benutzern und 200 Geräten**, können Sie die gleiche Anweisungen zum Migrieren auf die Standard oder Datacenter-Editionen von Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle ausführen.  
  
> [!NOTE]
>  Zum Vermeiden von Problemen während der Migration, empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dieses Dokument vor dem Beginn der Migration zu lesen.  
  
## <a name="terms-and-definitions"></a>Begriffe und Definitionen  
 **Quellserver** Der vorhandene Server, von dem Sie die Einstellungen und Daten migrieren.  
  
 **Zielserver** Der neue Server, auf den Sie die Einstellungen und Daten migrieren.  
  
## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses  
 Dieses Migrationshandbuch umfasst die folgenden Schritte:  
  
1.  [Schritt 1: Vorbereiten des Quelle für Windows Server Essentials-Migration](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und das Netzwerk für die Migration bereit sind. Mit den Schritten in diesem Abschnitt können Sie den Quellserver sichern, die Systemintegrität des Quellservers prüfen, die aktuellen Service Packs und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2.  [Schritt 2: Installieren von Windows Server Essentials als ein neuer replikatsdomänencontroller](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md). Dieser Abschnitt beschreibt, wie zum Installieren von Windows Server Essentials oder Windows Server 2012 R2 Standard (mit aktivierter Windows Server Essentials Experience-Rolle) als Domänencontroller.  
  
3.  [Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md).  In diesem Abschnitt wird das Hinzufügen von Clientcomputern mit dem neuen Server, Windows Server Essentials ausgeführt wird, und Aktualisieren von gruppenrichtlinieneinstellungen erläutert.  
  
4.  [Schritt 4: Verschieben von Einstellungen und Daten auf den Zielserver für Windows Server Essentials-Migration](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5.  [Schritt 5: Aktivieren der ordnerumleitung auf dem Zielserver für Windows Server Essentials-Migration](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.  
  
6.  [Schritt 6: Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Vor dem Entfernen des Quellservers müssen Sie eine Gruppenrichtlinienaktualisierung erzwingen und den Quellserver tiefer stufen.  
  
7.  [Schritt 7: Ausführen von Aufgaben nach der Migration für die Windows Server Essentials-Migration](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md).  Nach Abschluss der Migration aller Einstellungen und Daten zu Windows Server Essentials, können Sie Benutzerkonten zugelassene Computer zuordnen möchten.  
  
8.  [Schritt 8: Ausführen der Windows Server Essentials Best Practices Analyzer](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nach Abschluss der Migration der Einstellungen und Daten zu Windows Server Essentials sollten Sie die Windows Server Essentials Best Practices Analyzer (BPA) ausführen.  
  
 Mehrere der Migrationsverfahren erfordern das Öffnen einer Eingabeaufforderung als Administrator. In den folgenden Verfahren wird erläutert, wie hierbei vorzugehen ist.  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a> So öffnen Sie ein Eingabeaufforderungsfenster auf dem Quellserver als administrator  
  
1.  Klicken Sie auf **Start**.  
  
2.  Geben Sie im Suchfeld **Cmd** ein.  
  
3.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>So öffnen Sie auf dem Zielserver ein Eingabeaufforderungsfenster als Administrator  
  
1.  Geben Sie auf dem**Start** Startbildschirm im Suchfeld **cmd** ein.  
  
2.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

