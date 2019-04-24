---
title: Konfigurieren von Firewallregeln für Nichtdomänenmitglieder zum Zulassen von BranchCache-Datenverkehr
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 288865f0237969e0bed7e105f8d539759984275e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834771"
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>Konfigurieren von Firewallregeln für Nichtdomänenmitglieder zum Zulassen von BranchCache-Datenverkehr

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können die Informationen in diesem Thema verwenden, Firewall-Produkte von Drittanbietern zu konfigurieren und einen Clientcomputer manuell mit Firewallregeln zu konfigurieren, mit denen BranchCache im Modus "verteilter Cache" ausgeführt.  
  
> [!NOTE]  
> -   Wenn Sie BranchCache-Clientcomputern mithilfe einer Gruppenrichtlinie konfiguriert haben, überschreiben die gruppenrichtlinieneinstellungen jegliche manuelle Konfiguration der Clientcomputer, die auf die die Richtlinien angewendet werden.  
> -   Wenn Sie BranchCache mit DirectAccess bereitgestellt haben, können Sie die Einstellungen in diesem Thema verwenden, um IPsec-Regeln für das Zulassen von BranchCache-Datenverkehr zu konfigurieren.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Konfigurationsänderungen vorzunehmen.  
  
## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS-PCCRD]: Peer Content Caching and Retrieval-Discovery-Protokolls  
Verteilte Cacheclients müssen eingehenden und ausgehenden MS-PCCRD-Datenverkehr zulassen, der mit dem WS-Discovery-Protokoll (Web Services Dynamic Discovery) übertragen wird.  
  
Firewalleinstellungen müssen Multicastverkehr, der zusätzlich zu den eingehenden und ausgehenden Datenverkehr zulassen. Sie können die folgenden Einstellungen verwenden, um Firewallausnahmen für den Modus "Verteilter Cache" zu konfigurieren.  
  
IPv4-Multicast: 239.255.255.250  
  
IPv6-Multicast: FF02::C  
  
Eingehender Datenverkehr an: Lokaler Port: 3702, Remoteport: kurzlebige  
  
Ausgehende Nachrichten: Lokaler Port: Kurzlebig, Remoteport: 3702  
  
Programm: %systemroot%\system32\svchost.exe (BranchCache-Dienst [PeerDistSvc])  
  
## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS-PCCRR]: Peer Content Caching and Retrieval: Protokoll zum Abrufen von  
Verteilte cacheclients müssen ein- und ausgehenden MS-PCCRR-Datenverkehr zulassen, in das Protokoll HTTP 1.1 übertragen wird, wie Anforderungen für Kommentare (RFC) 2616.  
  
Firewalleinstellungen müssen eingehenden und ausgehenden Datenverkehr zulassen. Sie können die folgenden Einstellungen verwenden, um Firewallausnahmen für den Modus "Verteilter Cache" zu konfigurieren.  
  
Eingehender Datenverkehr an: Lokaler Port: 80, Remoteport: kurzlebige  
  
Ausgehende Nachrichten: Lokaler Port: Kurzlebig, Remoteport: 80  
  


