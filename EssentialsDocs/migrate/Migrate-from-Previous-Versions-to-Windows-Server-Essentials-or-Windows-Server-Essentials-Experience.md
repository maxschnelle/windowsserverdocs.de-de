---
title: Migrieren von früheren Versionen nach Windows Server Essentials oder Windows Server Essentials Experience
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 2974fb3a-5150-43fd-a73f-3e5074eb5d03
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 55b31785de6e17232a717d534fcb21a24d9052bd
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318895"
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>Migrieren von früheren Versionen nach Windows Server Essentials oder Windows Server Essentials Experience

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

In dieser Anleitung wird die Migration von früheren Versionen von Windows Small Business Server und Windows Server Essentials (einschließlich Windows Server Essentials, Windows Small Business Server 2011 Standard, Windows Small Business Server 2011 Essentials, Windows) beschrieben. Small Business Server 2008 und Windows Small Business Server 2003) zu Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle.  
  
 **Für Umgebungen mit bis zu 25 Benutzern und 50 Geräten**können Sie die Schritte in dieser Anleitung befolgen, um von früheren Versionen von Windows SSB zu Windows Server Essentials zu migrieren.  
  
 **Für Umgebungen mit bis zu 100 Benutzern und 200 Geräten**können Sie denselben Leitfaden befolgen, um zu den Standard-oder Datacenter-Editionen von Windows Server 2012 R2 zu migrieren, auf denen die Rolle "Windows Server Essentials-Umgebung" installiert ist.  
  
> [!NOTE]
>  Zum Vermeiden von Problemen während der Migration, empfiehlt das Windows Server Essentials-Produktentwicklungsteam dringend, dieses Dokument vor dem Beginn der Migration zu lesen.  
  
## <a name="terms-and-definitions"></a>Begriffe und Definitionen  
 **Quellserver** Der vorhandene Server, von dem Sie die Einstellungen und Daten migrieren.  
  
 **Zielserver** Der neue Server, auf den Sie die Einstellungen und Daten migrieren.  
  
## <a name="migration-process-summary"></a>Zusammenfassung des Migrationsprozesses  
 Dieses Migrationshandbuch umfasst die folgenden Schritte:  
  
1. [Schritt 1: Vorbereiten des Quell Servers für die Migration von Windows Server Essentials](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Sie müssen sicherstellen, dass der Quellserver und das Netzwerk für die Migration bereit sind. Mit den Schritten in diesem Abschnitt können Sie den Quellserver sichern, die Systemintegrität des Quellservers prüfen, die aktuellen Service Packs und Fixes installieren und die Netzwerkkonfiguration überprüfen.  
  
2. [Schritt 2: Installieren Sie Windows Server Essentials als neuen Replikat Domänen Controller](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md). In diesem Abschnitt wird beschrieben, wie Sie Windows Server Essentials oder Windows Server 2012 R2 Standard (mit aktivierter Rolle "Windows Server Essentials-Rolle") als Domänen Controller installieren.  
  
3. [Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md).  In diesem Abschnitt wird erläutert, wie Sie Client Computer mit dem neuen Server verknüpfen, auf dem Windows Server Essentials ausgeführt wird, und Gruppenrichtlinie Einstellungen aktualisieren.  
  
4. [Schritt 4: Verschieben von Einstellungen und Daten auf den Ziel Server für die Migration zu Windows Server Essentials](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Dieser Abschnitt enthält Informationen zum Migrieren von Daten und Einstellungen vom Quellserver.  
  
5. [Schritt 5: Aktivieren Sie die Ordner Umleitung auf dem Ziel Server für die Migration zu Windows Server Essentials](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Wenn die Ordnerumleitung auf dem Quellserver installiert ist, können Sie sie auch auf dem Zielserver aktivieren und anschließend die alte Gruppenrichtlinieneinstellung %%amp;quot;Ordnerumleitung%%amp;quot; löschen.  
  
6. [Schritt 6: herabstufen und Entfernen des Quell Servers aus dem neuen Windows Server Essentials-Netzwerk](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)  Vor dem Entfernen des Quellservers müssen Sie eine Gruppenrichtlinienaktualisierung erzwingen und den Quellserver tiefer stufen.  
  
7. [Schritt 7: Ausführen von Aufgaben nach der Migration für die Migration zu Windows Server Essentials](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md).  Nachdem Sie die Migration aller Einstellungen und Daten zu Windows Server Essentials abgeschlossen haben, können Sie zugelassene Computerbenutzer Konten zuordnen.  
  
8. [Schritt 8: Ausführen des Windows Server Essentials-Best Practices Analyzer](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Nachdem Sie die Migration der Einstellungen und Daten zu Windows Server Essentials abgeschlossen haben, sollten Sie das Windows Server Essentials-Best Practices Analyzer (BPA) ausführen.  
  
   Mehrere der Migrationsverfahren erfordern das Öffnen einer Eingabeaufforderung als Administrator. In den folgenden Verfahren wird erläutert, wie hierbei vorzugehen ist.  
  
###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a>So öffnen Sie ein Eingabe Aufforderungs Fenster auf dem Quell Server als Administrator  
  
1.  Klicken Sie auf **Start**.  
  
2.  Geben Sie im Suchfeld **Cmd** ein.  
  
3.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>So öffnen Sie auf dem Zielserver ein Eingabeaufforderungsfenster als Administrator  
  
1.  Geben Sie auf dem**Start** Startbildschirm im Suchfeld **cmd** ein.  
  
2.  Klicken Sie in der Ergebnisliste mit der rechten Maustaste auf **cmd**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

