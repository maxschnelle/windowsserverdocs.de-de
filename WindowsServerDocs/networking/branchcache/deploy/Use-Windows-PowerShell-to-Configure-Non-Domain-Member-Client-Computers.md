---
title: Verwenden von WindowsPowerShell zum Konfigurieren von Clientcomputern für die keine Domänenmitglieder sind
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a5415d9fa5a4af806f23a1af9c907b1f02e9627b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Verwenden von WindowsPowerShell zum Konfigurieren von Clientcomputern für die keine Domänenmitglieder sind

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können dieses Verfahren für den verteilten Cachemodus BranchCache-Clientcomputer manuell konfigurieren oder Modus für gehostete Caches.  
  
> [!NOTE]  
> Wenn Sie BranchCache-Clientcomputer mithilfe von Gruppenrichtlinien konfiguriert haben, überschreiben die gruppenrichtlinieneinstellungen jegliche manuelle Konfiguration der Clientcomputer, auf die die Richtlinien angewendet werden.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
### <a name="to-enable-branchcache-distributed-or-hosted-cache-mode"></a>So aktivieren Sie BranchCache-Modus verteilten oder gehosteten Caches  
  
1.  Führen Sie auf dem BranchCache-Clientcomputer, die Sie konfigurieren möchten Windows PowerShell als Administrator, und führen Sie dann einen der folgenden.  
  
    -   Zum Konfigurieren des Clientcomputer für den verteilten Cachemodus BranchCache Geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE.  
  
        `Enable-BCDistributed`  
  
    -   Zum Konfigurieren des Clientcomputer für BranchCache-gehosteten Cachemodus Geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE.  
  
        `Enable-BCHostedClient`  
  
        > [!TIP]  
        > Wenn Sie die verfügbaren gehosteten Cacheservern angeben möchten, verwenden Sie die `-ServerNames` Parameter durch ein Komma getrennte Liste von die gehosteten Cacheserver als Wert des Parameters. Wenn Sie zwei gehostete Cacheserver mit dem Namen HCS1 und HCS2 haben, konfigurieren Sie den Clientcomputer für den Modus für gehostete Caches z. B. mit dem folgenden Befehl.  
        >   
        > `Enable-BCHostedClient -ServerNames HCS1,HCS2`  
  


