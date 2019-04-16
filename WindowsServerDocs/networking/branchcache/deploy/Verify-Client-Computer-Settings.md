---
title: Überprüfen von Clientcomputereinstellungen
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 31ea58b0-d407-4f62-8ec6-6a1b19174042
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d507f2097a9349cbefba520ad0dc143e0dd7452e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="verify-client-computer-settings"></a>Überprüfen von Clientcomputereinstellungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie überprüfen, ob der Clientcomputer für BranchCache ordnungsgemäß konfiguriert ist.  
  
> [!NOTE]  
> Dieses Verfahren enthält Schritte für das manuelle Aktualisieren der Gruppenrichtlinie und für die BranchCache-Dienst neu zu starten. Sie brauchen diese Aktionen ausführen, wenn Sie den Computer neu starten, wie sie in diesem Fall automatisch durchgeführt werden.  
  
Sie müssen ein Mitglied sein **Administratoren**, oder eine gleichwertige, um dieses Verfahren auszuführen.  
  
### <a name="to-verify-branchcache-client-computer-settings"></a>Überprüfen von Clientcomputereinstellungen für BranchCache  
  
1.  Um Gruppenrichtlinien auf dem Clientcomputer zu aktualisieren, deren BranchCache-Konfiguration, die Sie überprüfen möchten, führen Sie Windows PowerShell als Administrator, geben Sie folgenden Befehl, und drücken Sie dann die EINGABETASTE.  
  
    `gpupdate /force`  
  
2.  Für Clientcomputer, die im Modus für gehostete Caches konfiguriert sind und sind so konfiguriert, gehosteten automatisch erkennen Cacheservern nach Dienstverbindungspunkt, führen Sie die folgenden Befehle zum Beenden und starten Sie den BranchCache-Dienst neu.  
  
    `net stop peerdistsvc`  
  
    `net start peerdistsvc`  
  
3.  Überprüfen des aktuellen BranchCache-Betriebsmodus durch den folgenden Befehl ausführen.  
  
    `Get-BCStatus`  
  
4.  In Windows PowerShell, überprüfen Sie die Ausgabe von den **Get-BCStatus** Befehl.  
  
    Der Wert für **BranchCacheIsEnabled** sollte **True**.  
  
    In **ClientSettings**, den Wert für **CurrentClientMode** sollte **DistributedClient** oder **HostedCacheClient**, je nachdem, auf den Modus an, die Sie mithilfe dieser Anleitung konfiguriert.  
  
    In **ClientSettings**Modus für gehostete Caches konfiguriert und die Namen der die gehosteten Cacheserver während der Konfiguration bereitgestellt, und wenn der Client nicht automatisch gefunden hat gehostete Cacheserver, die mithilfe von Dienstverbindungspunkten, **HostedCacheServerList** müssen einen Wert, der als den oder die Namen der die gehosteten Cacheserver übereinstimmt. Wenn Sie der gehosteten Cacheserver HCS1 und die Domäne mit dem Namen ist z. B. "corp.contoso.com", der Wert für **HostedCacheServerList** ist **HCS1.corp.contoso.com**.  
  
5.  Wenn keines der oben Standardeinstellungen aufgelisteten BranchCache keinen die richtigen Werte, verwenden die Schritte in diesem Handbuch so überprüfen Sie die Einstellungen für Gruppenrichtlinien oder Richtlinien des lokalen Computers als auch die Firewallausnahmen, die von Ihnen konfigurierten, und stellen Sie sicher, dass sind sie richtig. Darüber hinaus werden entweder starten Sie den Computer neu, oder führen Sie die Schritte in diesem Verfahren zum Aktualisieren der Gruppenrichtlinie und den BranchCache-Dienst neu starten.  
  


