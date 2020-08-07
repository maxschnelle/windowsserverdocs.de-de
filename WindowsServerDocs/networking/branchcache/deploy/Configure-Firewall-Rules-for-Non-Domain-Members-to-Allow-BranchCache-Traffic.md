---
title: Konfigurieren von Firewallregeln für Nichtdomänenmitglieder zum Zulassen von BranchCache-Datenverkehr
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 414f28c72817e91c56c91b6fd6acbb48e786cbd8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971927"
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>Konfigurieren von Firewallregeln für Nichtdomänenmitglieder zum Zulassen von BranchCache-Datenverkehr

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe der Informationen in diesem Thema können Sie Firewallprodukte von Drittanbietern konfigurieren und einen Client Computer manuell mit Firewallregeln konfigurieren, die das Ausführen von BranchCache im Modus "verteilter Cache" zulassen.

> [!NOTE]
> -   Wenn Sie BranchCache-Client Computer mithilfe von Gruppenrichtlinie konfiguriert haben, überschreiben die Gruppenrichtlinie Einstellungen jegliche manuelle Konfiguration der Client Computer, auf die die Richtlinien angewendet werden.
> -   Wenn Sie BranchCache mit DirectAccess bereitgestellt haben, können Sie die Einstellungen in diesem Thema verwenden, um IPsec-Regeln für das Zulassen von BranchCache-Datenverkehr zu konfigurieren.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Konfigurationsänderungen vorzunehmen.

## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS-PCCRD]: Protokoll für das Zwischenspeichern und Abrufen von Peer Inhalten
Verteilte Cacheclients müssen eingehenden und ausgehenden MS-PCCRD-Datenverkehr zulassen, der mit dem WS-Discovery-Protokoll (Web Services Dynamic Discovery) übertragen wird.

Firewalleinstellungen müssen zusätzlich zum eingehenden und ausgehenden Datenverkehr Multicast Datenverkehr zulassen. Sie können die folgenden Einstellungen verwenden, um Firewallausnahmen für den Modus "Verteilter Cache" zu konfigurieren.

IPv4-Multicast: 239.255.255.250

IPv6-Multicast: FF02:: C

Eingehender Datenverkehr: lokaler Port: 3702, Remoteport: kurzlebige

Ausgehender Datenverkehr: lokaler Port: kurzlebige, Remoteport: 3702

Programm:% systemroot% \system32\svchost.exe (BranchCache-Dienst [PeerDistSvc])

## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS-PCCRR]: Zwischenspeichern und Abrufen von Peer Inhalten: Abruf Protokoll
Clients für verteilte Caches müssen einen eingehenden und ausgehenden MS-PCCRR-Datenverkehr zulassen, der in das HTTP 1,1-Protokoll übertragen wird, wie in Request for Comments (RFC) 2616 dokumentiert.

Firewalleinstellungen müssen einen eingehenden und ausgehenden Datenverkehr zulassen. Sie können die folgenden Einstellungen verwenden, um Firewallausnahmen für den Modus "Verteilter Cache" zu konfigurieren.

Eingehender Datenverkehr: lokaler Port: 80, Remoteport: kurzlebige

Ausgehender Datenverkehr: lokaler Port: kurzlebige, Remoteport: 80



