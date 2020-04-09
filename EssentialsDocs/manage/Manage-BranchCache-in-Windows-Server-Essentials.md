---
title: Verwalten von BranchCache in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: f6e05aec-d07c-4e0b-94ab-f20279e9ffd1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a679973065a1d8b0033c0f00ca764aafe3546888
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852833"
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Verwalten von BranchCache in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Mithilfe von BranchCache können Sie die Internet Nutzung optimieren, die Leistung von vernetzten Anwendungen verbessern und den Datenverkehr in Ihrem WAN (Wide Area Network) reduzieren, wenn sich der Windows Server Essentials-Server Remote von Ihrem Büro befindet oder wenn Client Computer bei einer Verbindung mit einem lokalen Server werden cloudbasierte Ressourcen wie SharePoint Online-Bibliotheken verwendet.  
  
 Wenn BranchCache aktiviert ist und ein Client Computer Inhalt von einem Windows Server Essentials-Remote Server anfordert, wird der Inhalt in der lokalen Niederlassung zwischengespeichert. Danach können andere Computer in derselben Zweigstelle den Inhalt lokal abrufen, anstatt ihn erneut über das WAN vom Server abzurufen. Dadurch kann die Leistung von Netzwerkanwendungen verbessert und die Bandbreitenbelegung im WAN reduziert werden.  
  
 Unabhängig davon, ob der Windows Server Essentials-Server lokal oder Remote ist, kann BranchCache die Reaktionszeiten für freigegebene Server Ordner und Webinhalte verbessern, die auf dem Server gehostet werden (z. b. SharePoint Online-Bibliotheken).  
  
 Da für BranchCache keine neue Hardware oder Änderungen der Netzwerktopologie erforderlich sind, stellt dieses Feature eine einfache Möglichkeit zur Verbesserung zur Optimierung der Auslastung der Netzwerkbandbreite und Verbesserung der Reaktionszeiten für Dienste und Ressourcen dar, auf die über das WAN zugegriffen wird.  
  
## <a name="branchcache-scenarios"></a>Szenarien für BranchCache  
 Es gibt drei grundlegende Szenarien für die Nutzung von BranchCache mit einem Remoteserver:  
  
-   Der Windows Server Essentials-Server wird in Microsoft Azure gehostet.  
  
-   Ihr Windows Server Essentials-Server wird im Daten Center eines Drittanbieter Dienstanbieters gehostet.  
  
-   Der Windows Server Essentials-Server befindet sich in einem anderen Büro an einem anderen physischen Standort.  
  
## <a name="distributed-cache-mode"></a>Modus "Verteilter Cache"  
 In Windows Server Essentials wird BranchCache im Modus " *verteilter Cache*" implementiert, einem von zwei in BranchCache verfügbaren Cache Modi. Im Modus "Verteilter Cache" wird der Inhaltscache in einer Zweigstelle auf Clientcomputer verteilt. Da keine zusätzliche Hardware oder Topologieänderungen erforderlich sind, eignet sich dieser Modus für kleine Zweigstellen, die einen Remoteserver verwenden oder über einen lokalen Server auf cloudbasierte Dienste wie SharePoint Online zugreifen. Wenn Sie BranchCache in Windows Server Essentials aktivieren, wird der Modus "verteilter Cache" implementiert.  
  
> [!NOTE]
>  In größeren Zweigstellen mit mehr als einem Subnetz oder einer großen Anzahl von Mitarbeitern, die Netzwerkanwendungen nutzen, kann es vorteilhaft sein, BranchCache im *Modus "Gehosteter Cache"* zu implementieren. Im Modus "Gehosteter Cache" werden Cache-Inhalte auf einem oder mehreren gehosteten Cacheservern in der Zweigstelle gespeichert.
  
## <a name="requirements"></a>Voraussetzungen  
 Um BranchCache in Windows Server Essentials verwenden zu können, müssen die Server-und Client Computer die folgenden Anforderungen erfüllen:  
  
-   Auf dem Server muss das Betriebssystem Windows Server Essentials oder das Betriebssystem Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit der Windows Server Essentials-Rolle ausgeführt werden.  
  
     Auf einem Windows Server 2012 R2 Standard-oder Windows Server 2012 R2 Datacenter-Server wird BranchCache hinzugefügt, wenn Sie die Rolle "Windows Server Essentials-Benutzer" hinzufügen. Um BranchCache zu aktivieren, müssen Sie sich mit den Anmelde Informationen des Domänen Administrators beim Windows Server Essentials-Dashboard anmelden.  
  
-   Auf Client Computern muss das Betriebssystem Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Enterprise oder Windows 8.1 Enterprise ausgeführt werden.  
  
-   Im Modus "Verteilter Cache" müssen alle Clientcomputer im selben Subnetz enthalten sein.  
  
    > [!NOTE]
    >  Wenn Sie Clientcomputer mit Ihrem Windows Server Essentials-Server verbunden haben, ohne sie der Domäne beitreten zu lassen, sind diese Computer standardmäßig von der Cachenutzung ausgeschlossen. Um einen nicht zur Domäne gehörigen Clientcomputer für die Cachenutzung zu aktivieren, führen Sie das Windows PowerShell-Cmdlet [Enable-BCDistributed](https://technet.microsoft.com/library/hh848398.aspx) auf dem Clientcomputer aus. Weitere Informationen finden Sie unter [BranchCache-Server-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh848392.aspx).  
 
  
## <a name="turn-branchcache-on"></a>Aktivieren von BranchCache  
 Um BranchCache im Modus "verteilter Cache" zu aktivieren, klicken Sie einfach im Windows Server Essentials-Dashboard auf eine Schaltfläche. Die Cachenutzung beginnt sofort und erfolgt unbemerkt.  
  
#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>So aktivieren Sie BranchCache in Windows Server Essentials  
  
1.  Melden Sie sich mit Ihrem Administrator Konto beim Windows Server Essentials-Server an.  
  
2.  Klicken Sie im Windows Server Essentials-Dashboard auf **Einstellungen**.  
  
     Der Setup-Assistent wird geöffnet.  
  
3.  Klicken Sie auf **BranchCache**.  
  
4.  Klicken Sie auf der Seite **BranchCache-Einstellungen** auf **Einschalten**.  
  
## <a name="use-windows-powershell-to-turn-branchcache-on-or-off"></a>Aktivieren/Deaktivieren von BranchCache mit Windows PowerShell  
 Sie können Windows PowerShell zum Überprüfen des Status von BranchCache (aktiviert oder deaktiviert) und Aktivieren bzw. Deaktivieren von BranchCache verwenden.  
  
#### <a name="to-turn-branchcache-on-or-off-using-windows-powershell"></a>So aktivieren/deaktivieren Sie BranchCache mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell auf dem Server als Administrator. Klicken Sie auf der Seite **Start** mit der rechten Maustaste auf **Windows PowerShell**, klicken Sie dann auf **Als Administrator ausführen** und anschließend auf **Ja**.  
  
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
    
-   [BranchCache (Übersicht)](https://technet.microsoft.com/library/hh831696.aspx)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
