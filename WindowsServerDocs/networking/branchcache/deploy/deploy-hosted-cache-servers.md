---
title: Bereitstellen von gehosteten Cacheserver (Optional)
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 96d03b42-6cd9-4905-b6a2-dc36130dd24f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b19680e933e7a33871816578b63c5a141db0ce00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826211"
---
# <a name="deploy-hosted-cache-servers-optional"></a>Bereitstellen von gehosteten Cacheserver (Optional)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, installieren und Konfigurieren von BranchCache-gehosteten Cacheserver, die in Filialen befinden, in der Sie gehosteten BranchCache-Cachemodus bereitstellen möchten. Mit BranchCache in Windows Server 2016 können Sie mehrere gehostete Cacheserver in einer Zweigstelle bereitstellen.  
  
> [!IMPORTANT]  
> Dieser Schritt ist optional, da Modus "verteilter Cache" nicht mit einen gehosteten Cacheserver-Server-Computer in Zweigstellen erfordert. Wenn Sie nicht beabsichtigen bereitstellen Modus für gehostete Caches in Zweigstellen, Sie müssen sich nicht um einen gehosteten Cacheserver bereitzustellen, und Sie müssen nicht die Schritte in diesem Verfahren ausführen.  
  
Sie müssen ein Mitglied sein **Administratoren**, oder führen Sie dieses Verfahren entspricht.  
  
### <a name="to-install-and-configure-a-hosted-cache-server"></a>Installieren und konfigurieren einen gehosteten Cacheserver  
  
1.  Führen Sie auf dem Computer, den Sie als gehosteten Cacheserver konfigurieren möchten den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung zur Installation der BranchCache-Funktion.  
  
    `Install-WindowsFeature BranchCache -IncludeManagementTools`  
  
2.  Konfigurieren Sie den Computer als gehosteten Cacheserver, indem Sie eine der folgenden Befehle aus:  
  
    -   Um einen nicht in die Domäne eingebundenen Computer als gehosteten Cacheserver konfigurieren zu können, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.  
  
        `Enable-BCHostedServer`  
  
    -   Um einem zur Domäne gehörenden Computer als einen gehosteten Cacheserver konfigurieren und registrieren ein Dienstverbindungspunkts in Active Directory für die automatisch nach gehosteten Cacheservern gesucht von Clientcomputern, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und klicken Sie dann Drücken Sie die EINGABETASTE.  
  
        `Enable-BCHostedServer -RegisterSCP`  
  
3.  Überprüfen die richtige Konfiguration des gehosteten cacheservers, geben den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung, und drücken dann die EINGABETASTE.  
  
    `Get-BCStatus`  
  
    > [!NOTE]  
    > Nach dem Ausführen dieses Befehls im Abschnitt **HostedCacheServerConfiguration**, den Wert für **HostedCacheServerIsEnabled** ist **"true"**. Wenn Sie die Domäne eingebundenen gehosteten Cacheserver um einen Dienstverbindungspunkt (SCP) im Active Directory, dessen Wert für zu registrieren konfiguriert **HostedCacheScpRegistrationEnabled** ist **"true"**.  
  

