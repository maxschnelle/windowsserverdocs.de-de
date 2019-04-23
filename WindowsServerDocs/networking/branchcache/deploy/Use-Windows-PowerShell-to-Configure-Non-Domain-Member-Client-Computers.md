---
title: Konfigurieren Sie Clientcomputer nicht Mitglied einer Domäne mithilfe von Windows PowerShell
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9abb77e573d7b3f144ab831c655c81370a4a6af1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839951"
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Konfigurieren Sie Clientcomputer nicht Mitglied einer Domäne mithilfe von Windows PowerShell

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, einen BranchCache-Clientcomputer für den verteilten Cachemodus manuell konfigurieren oder Modus für gehostete Caches.  
  
> [!NOTE]  
> Wenn Sie BranchCache-Clientcomputern mithilfe einer Gruppenrichtlinie konfiguriert haben, überschreiben die gruppenrichtlinieneinstellungen jegliche manuelle Konfiguration der Clientcomputer, die auf die die Richtlinien angewendet werden.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
### <a name="to-enable-branchcache-distributed-or-hosted-cache-mode"></a>So aktivieren Sie BranchCache verteilten oder im gehosteten Cachemodus  
  
1.  Klicken Sie auf dem BranchCache-Clientcomputer, die Sie konfigurieren möchten, führen Sie Windows PowerShell als Administrator, und führen Sie dann eine der folgenden.  
  
    -   Um den Clientcomputer für BranchCache-Modus für verteilte Caches konfigurieren zu können, geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE.  
  
        `Enable-BCDistributed`  
  
    -   Um den Clientcomputer für den gehosteten BranchCache-Cachemodus konfigurieren zu können, geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE.  
  
        `Enable-BCHostedClient`  
  
        > [!TIP]  
        > Wenn Sie die verfügbaren gehosteten Cacheservern angeben möchten, verwenden Sie die `-ServerNames` Parameter durch ein Komma getrennte Liste von die gehosteten Cacheserver als Wert des Parameters. Wenn Sie zwei gehostete Cacheserver mit dem Namen HCS1 und HCS2 haben, konfigurieren Sie den Clientcomputer für den Modus "gehosteter Cache" z. B. mit dem folgenden Befehl.  
        >   
        > `Enable-BCHostedClient -ServerNames HCS1,HCS2`  
  


