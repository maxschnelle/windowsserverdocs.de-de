---
title: Überprüfen von Clientcomputereinstellungen
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 31ea58b0-d407-4f62-8ec6-6a1b19174042
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d628886186474d3f05d7961ca3d3b45b8bf12e73
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834051"
---
# <a name="verify-client-computer-settings"></a>Überprüfen von Clientcomputereinstellungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, um sicherzustellen, dass der Clientcomputer für BranchCache ordnungsgemäß konfiguriert ist.  
  
> [!NOTE]  
> Dieses Verfahren enthält Schritte zum manuellen Aktualisieren der Gruppenrichtlinie und für die BranchCache-Dienst neu zu starten. Sie müssen sich nicht um diese Aktionen ausführen, wenn Sie den Computer neu starten, wie sie in diesem Fall automatisch durchgeführt werden.  
  
Sie müssen ein Mitglied sein **Administratoren**, oder führen Sie dieses Verfahren entspricht.  
  
### <a name="to-verify-branchcache-client-computer-settings"></a>Um zu überprüfen, ob BranchCache für Clientcomputer  
  
1.  Um die Gruppenrichtlinie auf dem Clientcomputer zu aktualisieren, dessen BranchCache-Konfiguration, die Sie überprüfen möchten, führen Sie Windows PowerShell als Administrator, geben Sie den folgenden Befehl und dann die drücken Sie EINGABETASTE.  
  
    `gpupdate /force`  
  
2.  Für Clientcomputer, die im Modus "gehosteter Cache" konfiguriert sind, und sind so konfiguriert, gehosteten automatisch ermitteln Cacheservern nach Dienstverbindungspunkt, führen Sie die folgenden Befehle zum Beenden und starten Sie den BranchCache-Dienst.  
  
    `net stop peerdistsvc`  
  
    `net start peerdistsvc`  
  
3.  Überprüfen Sie den aktuellen operativen BranchCache-Modus, indem Sie den folgenden Befehl ausführen.  
  
    `Get-BCStatus`  
  
4.  Überprüfen Sie die Ausgabe der in Windows PowerShell die **Get-BCStatus** Befehl.  
  
    Der Wert für **BranchCacheIsEnabled** muss **"true"**.  
  
    In **ClientSettings**, den Wert für **CurrentClientMode** muss **DistributedClient** oder **HostedCacheClient**, je nachdem, auf die der Modus, in dem Sie konfiguriert haben, mithilfe dieses Handbuchs.  
  
    In **ClientSettings**, wenn Sie Modus "gehosteter Cache" konfiguriert und die Namen der die gehosteten Cacheserver während der Konfiguration bereitgestellt oder wenn der Client automatisch ermittelten gehostete Cacheserver, die mithilfe von Dienstverbindungspunkten,  **HostedCacheServerList** müssen einen Wert, der den Namen oder die Namen von die gehosteten Cacheserver übereinstimmt. Ist z. B. wenn der gehosteten Cacheserver HCS1 und der Domäne heißt "corp.contoso.com", den Wert für **HostedCacheServerList** ist **HCS1.corp.contoso.com**.  
  
5.  Wenn keines der oben Standardeinstellungen aufgelisteten BranchCache nicht die richtigen Werte, verwenden die Schritte in diesem Handbuch, um zu überprüfen, ob die Einstellungen der Gruppenrichtlinie oder lokale Computerrichtlinie als auch die Firewallausnahmen, die Sie konfiguriert haben, und stellen sicher, dass sind sie korrekt. Darüber hinaus entweder starten Sie den Computer neu, oder führen Sie die Schritte in diesem Verfahren zum Aktualisieren der Gruppenrichtlinie und den BranchCache-Dienst neu starten.  
  


