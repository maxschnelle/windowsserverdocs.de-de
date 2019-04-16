---
title: Bereitstellen von gehosteten Cacheserver (Optional)
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 96d03b42-6cd9-4905-b6a2-dc36130dd24f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d7345b9acf5ef5003cc2a811569083d7c12894a1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-hosted-cache-servers-optional"></a>Bereitstellen von gehosteten Cacheserver (Optional)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können dieses Verfahren zum Installieren und Konfigurieren von BranchCache-gehosteten Cacheserver, die sich in Filialen befinden, in der Sie BranchCache-gehosteten Cachemodus bereitstellen möchten. Mit BranchCache in Windows Server2016 können Sie mehrere gehostete Cacheserver in einer Zweigstelle bereitstellen.  
  
> [!IMPORTANT]  
> Dieser Schrittist optional, da Modus für verteilte Caches nicht auf einen gehosteten Server-Computer in Zweigstellen erforderlich sind. Wenn Sie nicht beabsichtigen bereitstellen Modus für gehostete Caches in Zweigstellen, Sie müssen nicht auf einen gehosteten Cacheserver bereitstellen und Sie müssen nicht die Schrittein diesem Verfahren.  
  
Sie müssen ein Mitglied sein **Administratoren**, oder eine gleichwertige, um dieses Verfahren auszuführen.  
  
### <a name="to-install-and-configure-a-hosted-cache-server"></a>So installieren und konfigurieren einen gehosteten Cacheserver  
  
1.  Führen Sie auf dem Computer, den Sie als einen gehosteten Cacheserver konfigurieren möchten den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung das BranchCache-Feature installieren.  
  
    `Install-WindowsFeature BranchCache -IncludeManagementTools`  
  
2.  Konfigurieren Sie den Computer als gehosteten Cacheserver mit einer der folgenden Befehle:  
  
    -   Um einen verbundenen Computer außerhalb der Domäne als gehosteten Cacheserver konfigurieren, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.  
  
        `Enable-BCHostedServer`  
  
    -   Zum Konfigurieren einer Domäne beigetreten Computer als gehosteten Cacheserver und um Service Connection Point in Active Directory automatisch nach gehosteten Cacheservern gesucht von Clientcomputern registrieren, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.  
  
        `Enable-BCHostedServer -RegisterSCP`  
  
3.  Überprüfen die richtige Konfiguration des gehosteten cacheservers, geben den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken dann die EINGABETASTE.  
  
    `Get-BCStatus`  
  
    > [!NOTE]  
    > Nach dem Ausführen dieses Befehls im Abschnitt **HostedCacheServerConfiguration**, den Wert für **HostedCacheServerIsEnabled** ist **True **. Wenn Sie einen Domäne verbundenen gehosteten Cacheserver einen Dienstverbindungspunkt (SCP) in Active Directory, den Wert für die Registrierung konfiguriert **HostedCacheScpRegistrationEnabled** ist **True **.  
  

