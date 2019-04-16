---
title: Verwalten von BranchCache in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6e05aec-d07c-4e0b-94ab-f20279e9ffd1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 13d1d439eb9eeb60de9779d783e36405aee3ddfc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Verwalten von BranchCache in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

BranchCache hilft Ihnen beim Optimieren der Nutzung des Internets, Verbessern der Leistung von netzwerkanwendungen, und Reduzieren des Datenverkehrs in Ihrem Wide Area Network (WAN) bei der Windows Server Essentials-Server Remote von Ihrem Büro befindet oder wenn Clientcomputer mit einem lokalen Server verbunden cloudbasierte Ressourcen wie SharePoint Online-Bibliotheken verwenden.  
  
 Mit BranchCache aktiviert, wenn ein Clientcomputer Inhalte von einem Windows Server Essentials Remoteserver, den Inhalt anfordert wird in der lokalen Zweigstelle zwischengespeichert. Danach können andere Computer im selben Büro den Inhalt lokal erneut herunterladen des Inhalts vom Server über das WAN abrufen. Dies kann die Leistung von netzwerkanwendungen verbessert und die Auslastung der Netzwerkbandbreite über das WAN reduziert.  
  
 Ob Ihr Windows Server Essentials-Server lokal oder remote ist, kann BranchCache verbessert werden Reaktionszeiten für freigegebenen Serverordner und Web-Inhalte, die auf dem Server (z. B. SharePoint Online-Bibliotheken) gehostet werden.  
  
 Da BranchCache keine neue Hardware oder Änderungen der Netzwerktopologie erforderlich sind, können Sie dieses Feature eine einfache Möglichkeit zum Optimieren der Auslastung der Netzwerkbandbreite und Verbesserung der Reaktionszeiten für Dienste und Ressourcen, die über das WAN zugegriffen.  
  
## <a name="branchcache-scenarios"></a>BranchCache-Szenarien  
 Es gibt drei grundlegende Szenarien für die Verwendung von BranchCache mit einem remote-Server:  
  
-   Der Windows Server Essentials-Server wird in Microsoft Azure gehostet.  
  
-   Ihre Windows Server Essentials-Server wird im Datencenter eines Drittanbieter-Dienstanbieters gehostet.  
  
-   Ihr Windows Server Essentials-Server ist in einer anderen Zweigstelle an einem anderen physischen Standort.  
  
## <a name="distributed-cache-mode"></a>Modus für verteilte Caches  
 BranchCache ist in Windows Server Essentials in implementiert *Modus für verteilte Caches*, eine der zwei in BranchCache verfügbaren cachemodi. Im Modus für verteilte Caches wird der inhaltscache in der Zweigstelle auf Clientcomputer verteilt. Da keine zusätzliche Hardware oder Änderungen der Netzwerktopologie erforderlich sind, eignet sich dieser Modus für kleine Zweigstellen, die einen Remoteserver oder einen lokalen Server auf cloudbasierte Dienste wie SharePoint Online zugreifen. Wenn Sie BranchCache in Windows Server Essentials aktivieren, wird der Modus für verteilte Caches implementiert.  
  
> [!NOTE]
>  In größeren Zweigstellen mit mehr als einem Subnetz oder mit einer großen Anzahl von Mitarbeitern, die netzwerkanwendungen nutzen, es kann hilfreich sein, um BranchCache in implementieren *Modus für gehostete Caches*. Im Modus für gehostete Caches wird der Cache-Inhalte auf einem oder mehreren gehosteten Cacheserver in der Zweigstelle gespeichert.
  
## <a name="requirements"></a>Anforderungen  
 Um BranchCache in Windows Server Essentials verwenden, müssen die Server und Clientcomputer die folgenden Anforderungen erfüllen:  
  
-   Der Server muss das Betriebssystem Windows Server Essentials oder Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter-Betriebssystem mit Windows Server Essentials Experience-Rolle ausgeführt werden.  
  
     Auf einem Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter Server wird BranchCache hinzugefügt, wenn Sie Windows Server Essentials Experience-Rolle hinzufügen. Um BranchCache aktivieren, müssen Sie sich bei Windows Server Essentials-Dashboard mit Domänenadministrator-Anmeldeinformationen anmelden.  
  
-   Client-Computer müssen die Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Enterprise oder Windows 8.1 Enterprise-Betriebssystem ausgeführt werden.  
  
-   Im Modus für verteilte Caches müssen alle Clientcomputer in demselben Subnetz sein.  
  
    > [!NOTE]
    >  Wenn Sie Clientcomputer mit dem Windows Server Essentials-Server verbunden, ohne dass sie der Domäne beitritt, werden ausgeschlossen, dass diese Computer standardmäßig Zwischenspeichern. Führen Sie einen Clientcomputer, die nicht an einer Domäne eingebunden ist in Zwischenspeichern einbezogen werden, die [Enable-BCDistributed](https://technet.microsoft.com/library/hh848398.aspx) Windows PowerShell-Cmdlet auf dem Clientcomputer. Weitere Informationen finden Sie unter [BranchCache-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh848392.aspx).  
 
  
## <a name="turn-branchcache-on"></a>Aktivieren von BranchCache  
 Um BranchCache im Modus für verteilte Caches zu aktivieren, klicken Sie einfach eine Schaltfläche auf der Windows Server Essentials-Dashboard. Cachenutzung beginnt sofort und erfolgt unbemerkt.  
  
#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>So aktivieren Sie BranchCache in Windows Server Essentials  
  
1.  Melden Sie sich auf dem Windows Server Essentials-Server mit Ihrem Administratorkonto an.  
  
2.  Klicken Sie auf dem Windows Server Essentials-Dashboard auf **Einstellungen**.  
  
     Der Assistent wird geöffnet.  
  
3.  Klicken Sie auf **BranchCache**.  
  
4.  Auf der **BranchCache-Einstellungen** auf **aktivieren**.  
  
## <a name="use-windows-powershell-to-turn-branchcache-on-or-off"></a>Verwenden Sie Windows PowerShell zum Aktivieren oder deaktivieren Sie BranchCache  
 Sie können Windows PowerShell zum Überprüfen des Status von BranchCache (aktiviert oder deaktiviert) und zum Aktivieren oder deaktivieren Sie BranchCache verwenden.  
  
#### <a name="to-turn-branchcache-on-or-off-using-windows-powershell"></a>Um BranchCache aktivieren oder deaktivieren mithilfe von Windows PowerShell  
  
1.  Öffnen Sie auf dem Server Windows PowerShell als Administrator. Auf der **starten** Seite, mit der rechten Maustaste **Windows PowerShell**, klicken Sie auf **als Administrator ausführen**, und klicken Sie dann auf **Ja**.  
  
2.  Geben Sie die folgenden Cmdlets in der Befehlszeile.  
  
    -   Um den Status von BranchCache (aktiviert oder deaktiviert) zu überprüfen, geben Sie Folgendes ein:  
  
        ```powershell  
        Get-WSSBranchCacheStatus  
        ```  
  
    -   Wenn BranchCache aktivieren möchten, geben Sie Folgendes ein:  
  
        ```powershell  
        Enable-WSSBranchCache  
        ```  
  
    -   Zum Deaktivieren von BranchCache Geben Sie Folgendes ein:  
  
        ```powershell  
        Disable-WSSBranchCache  
        ```  
  
## <a name="see-also"></a>Siehe auch  
    
-   [BranchCache (Übersicht)](https://technet.microsoft.com/library/hh831696.aspx)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
