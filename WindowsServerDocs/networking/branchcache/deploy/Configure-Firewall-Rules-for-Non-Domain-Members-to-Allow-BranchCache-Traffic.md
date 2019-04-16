---
title: Konfigurieren von Firewallregeln für Nichtdomänenmitglieder zum Zulassen von BranchCache-Datenverkehr
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e5f744141efc35bb493bcd95fad53eafbbc3f78d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>Konfigurieren von Firewallregeln für Nichtdomänenmitglieder zum Zulassen von BranchCache-Datenverkehr

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können die Informationen in diesem Thema Firewallprodukte von Drittanbietern konfigurieren und einen Clientcomputer manuell mit Firewall-Regeln konfigurieren, mit denen BranchCache im Modus für verteilte Caches ausführen können.  
  
> [!NOTE]  
> -   Wenn Sie BranchCache-Clientcomputer mithilfe von Gruppenrichtlinien konfiguriert haben, überschreiben die gruppenrichtlinieneinstellungen jegliche manuelle Konfiguration der Clientcomputer, auf die die Richtlinien angewendet werden.  
> -   Wenn Sie BranchCache mit DirectAccess bereitgestellt haben, können die Einstellungen in diesem Thema Sie zum Konfigurieren von IPSec-Regeln zum Zulassen von BranchCache-Datenverkehr.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden Gruppe mindestens erforderlich, um diese konfigurationsänderungen vorzunehmen.  
  
## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS-PCCRD]: Peer Content Caching and Retrieval-Discovery-Protokoll  
Verteilte cacheclients müssen eingehenden und ausgehenden MS-PCCRD-Datenverkehr zulassen, das Protokoll Web Services Dynamic Discovery (WS-Discovery) übertragen wird.  
  
Firewall-Einstellungen müssen die multicast-Datenverkehr zusätzlich zu eingehenden und ausgehenden Datenverkehr zulassen. Die folgenden Einstellungen können Sie die um Firewallausnahmen für den Modus für verteilte Caches zu konfigurieren.  
  
IPv4-Multicastbereiche: 239.255.255.250  
  
IPv6-Multicastadressen: FF02::C  
  
Eingehender Datenverkehr: lokalen Port: 3702, Remoteport: kurzlebige  
  
Ausgehender Datenverkehr: lokalen Port: Kurzlebig, Remoteport: 3702  
  
Programm: %systemroot%\system32\svchost.exe (BranchCache-Dienst [PeerDistSvc])  
  
## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS-PCCRR]: Peer Content Caching and Retrieval: Protokoll zum Abrufen von  
Verteilte cacheclients müssen eingehenden und ausgehenden MS-PCCRR-Datenverkehr zulassen, in das Protokoll HTTP 1.1 übertragen wird, wie in den Request for Comments (RFC) 2616 dokumentiert.  
  
Firewalleinstellungen müssen eingehenden und ausgehenden Datenverkehr zulassen. Die folgenden Einstellungen können Sie die um Firewallausnahmen für den Modus für verteilte Caches zu konfigurieren.  
  
Eingehender Datenverkehr: lokalen Port: 80, Remoteport: kurzlebige  
  
Ausgehender Datenverkehr: lokalen Port: Kurzlebig, Remoteport: 80  
  


