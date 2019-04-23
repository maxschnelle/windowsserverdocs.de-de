---
title: Verwalten von BranchCache in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828801"
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Verwalten von BranchCache in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

BranchCache hilft Ihnen bei der internetnutzung zu optimieren, Verbessern der Leistung von netzwerkanwendungen und Reduzieren des Datenverkehrs in Ihre Wide Area Network (WAN), wenn die Windows Server Essentials-Server Remote in Ihrem Büro befindet, oder wenn Clientcomputer mit einem lokalen Server verwenden cloudbasierte Ressourcen wie z. B. SharePoint Online-Bibliotheken verbunden ist.  
  
 Mit BranchCache aktiviert, wenn ein Clientcomputer Inhalte von einem Remotecomputer Windows Server Essentials-Server, den Inhalt angefordert wird in der lokalen Zweigstelle zwischengespeichert. Danach können andere Computer in derselben Zweigstelle den Inhalt lokal abrufen, anstatt ihn erneut über das WAN vom Server abzurufen. Dadurch kann die Leistung von Netzwerkanwendungen verbessert und die Bandbreitenbelegung im WAN reduziert werden.  
  
 Ob der Windows Server Essentials-Server lokal oder remote ist, kann BranchCache verbessern, Antwortzeiten für freigegebenen Serverordner und Web-Inhalte, die auf dem Server (z. B. SharePoint Online-Bibliotheken) gehostet wird.  
  
 Da für BranchCache keine neue Hardware oder Änderungen der Netzwerktopologie erforderlich sind, stellt dieses Feature eine einfache Möglichkeit zur Verbesserung zur Optimierung der Auslastung der Netzwerkbandbreite und Verbesserung der Reaktionszeiten für Dienste und Ressourcen dar, auf die über das WAN zugegriffen wird.  
  
## <a name="branchcache-scenarios"></a>Szenarien für BranchCache  
 Es gibt drei grundlegende Szenarien für die Nutzung von BranchCache mit einem Remoteserver:  
  
-   Ihre Windows Server Essentials-Server wird in Microsoft Azure gehostet.  
  
-   Ihre Windows Server Essentials-Server wird im Rechenzentrum eines Dienstanbieters von Drittanbietern gehostet werden.  
  
-   Ihr Windows Server Essentials-Server ist in einer anderen Zweigstelle an einem anderen physischen Standort.  
  
## <a name="distributed-cache-mode"></a>Modus "Verteilter Cache"  
 BranchCache ist in Windows Server Essentials in implementiert *Modus "verteilter Cache"*, einem von zwei in BranchCache verfügbar. Im Modus "Verteilter Cache" wird der Inhaltscache in einer Zweigstelle auf Clientcomputer verteilt. Da keine zusätzliche Hardware oder Topologieänderungen erforderlich sind, eignet sich dieser Modus für kleine Zweigstellen, die einen Remoteserver verwenden oder über einen lokalen Server auf cloudbasierte Dienste wie SharePoint Online zugreifen. Wenn Sie BranchCache in Windows Server Essentials aktivieren, wird der Modus "verteilter Cache" implementiert.  
  
> [!NOTE]
>  In größeren Zweigstellen mit mehr als einem Subnetz oder einer großen Anzahl von Mitarbeitern, die Netzwerkanwendungen nutzen, kann es vorteilhaft sein, BranchCache im *Modus "Gehosteter Cache"* zu implementieren. Im Modus "Gehosteter Cache" werden Cache-Inhalte auf einem oder mehreren gehosteten Cacheservern in der Zweigstelle gespeichert.
  
## <a name="requirements"></a>Anforderungen  
 Um BranchCache in Windows Server Essentials verwenden zu können, müssen die Server und Clientcomputer die folgenden Anforderungen erfüllen:  
  
-   Der Server muss das Betriebssystem Windows Server Essentials oder Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter-Betriebssystem mit der Windows Server Essentials Experience-Rolle ausgeführt werden.  
  
     Auf einem Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter-Server wird BranchCache hinzugefügt, wenn Sie die Windows Server Essentials Experience-Rolle hinzufügen. Um BranchCache aktivieren, müssen Sie Windows Server Essentials-Dashboard mit Domänenadministrator-Anmeldeinformationen anmelden.  
  
-   Client-Computern müssen das Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Enterprise oder Windows 8.1 Enterprise-Betriebssystem ausgeführt werden.  
  
-   Im Modus "Verteilter Cache" müssen alle Clientcomputer im selben Subnetz enthalten sein.  
  
    > [!NOTE]
    >  Wenn Sie Clientcomputer mit Ihrem Windows Server Essentials-Server verbunden haben, ohne sie der Domäne beitreten zu lassen, sind diese Computer standardmäßig von der Cachenutzung ausgeschlossen. Um einen nicht zur Domäne gehörigen Clientcomputer für die Cachenutzung zu aktivieren, führen Sie das Windows PowerShell-Cmdlet [Enable-BCDistributed](https://technet.microsoft.com/library/hh848398.aspx) auf dem Clientcomputer aus. Weitere Informationen finden Sie unter [BranchCache-Server-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh848392.aspx).  
 
  
## <a name="turn-branchcache-on"></a>Aktivieren von BranchCache  
 Um BranchCache im Modus "verteilter Cache" zu aktivieren, klicken Sie einfach eine Schaltfläche auf dem Windows Server Essentials-Dashboard. Die Cachenutzung beginnt sofort und erfolgt unbemerkt.  
  
#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>So aktivieren Sie BranchCache in Windows Server Essentials  
  
1.  Melden Sie sich auf dem Windows Server Essentials-Server mit Ihrem Administratorkonto an.  
  
2.  Klicken Sie auf der Windows Server Essentials-Dashboard auf **Einstellungen**.  
  
     Der Setup-Assistent wird geöffnet.  
  
3.  Klicken Sie auf **BranchCache**.  
  
4.  Klicken Sie auf der Seite **BranchCache-Einstellungen** auf **Einschalten**.  
  
## <a name="use-windows-powershell-to-turn-branchcache-on-or-off"></a>Aktivieren/Deaktivieren von BranchCache mit Windows PowerShell  
 Sie können Windows PowerShell zum Überprüfen des Status von BranchCache (aktiviert oder deaktiviert) und Aktivieren bzw. Deaktivieren von BranchCache verwenden.  
  
#### <a name="to-turn-branchcache-on-or-off-using-windows-powershell"></a>So aktivieren/deaktivieren Sie BranchCache mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell auf dem Server als Administrator. Klicken Sie auf der Seite **Start** mit der rechten Maustaste auf **Windows PowerShell**, klicken Sie dann auf **Als Administrator ausführen**und anschließend auf **Ja**.  
  
2.  Führen Sie an der Eingabeaufforderung eines der folgenden Cmdlets aus:  
  
    -   Um den Status von BranchCache (aktiviert oder deaktiviert) zu überprüfen, geben Sie Folgendes ein:  
  
        ```powershell  
        Get-WSSBranchCacheStatus  
        ```  
  
    -   Zum Aktivieren von BranchCache geben Sie Folgendes ein:  
  
        ```powershell  
        Enable-WSSBranchCache  
        ```  
  
    -   Zum Deaktivieren von BranchCache geben Sie Folgendes ein:  
  
        ```powershell  
        Disable-WSSBranchCache  
        ```  
  
## <a name="see-also"></a>Siehe auch  
    
-   [Übersicht über die BranchCache](https://technet.microsoft.com/library/hh831696.aspx)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
