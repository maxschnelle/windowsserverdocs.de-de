---
title: Bereitstellen eines Netzwerkrichtlinienservers
description: Dieses Thema enthält Links zu Inhalten der Netzwerkrichtlinienserver-Bereitstellung für Windows Server 2016 und enthält Links zu weiteren Anleitungen zum NPS.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: daf62e2a593014e16bcb5fd16542b2e9c75b9c1d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-network-policy-server"></a>Bereitstellen eines Netzwerkrichtlinienservers

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema Informationen zum Bereitstellen des Netzwerkrichtlinienservers verwenden.

>[!NOTE]
>Weitere Dokumentation Network Policy Server können Sie die folgenden Abschnitte der Bibliothek verwenden.  
>- [Erste Schrittemit dem Netzwerkrichtlinienserver](nps-getstart-top.md)
>- [Planen eines Netzwerkrichtlinienservers](nps-plan-top.md)
>- [Verwalten eines Netzwerkrichtlinienservers](nps-manage-top.md)

Windows Server 2016 Core Network Guide enthält einen Abschnitt zum Planen und Installieren von Netzwerkrichtlinienserver \(NPS\) und die Technologien, die in diesem Handbuch dargestellten dienen als Voraussetzung für die Bereitstellung von NPS in Active Directory-Domäne. Weitere Informationen finden Sie im Abschnitt "Bereitstellen von NPS1" in der Windows Server 2016 [Kernnetzwerkhandbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1).

## <a name="deploy-nps-server-certificates-for-vpn-and-8021x-access"></a>Bereitstellen von NPS-Serverzertifikate für VPN- und Zugriff mit 802.1X-Authentifizierung

Wenn wie Extensible Authentication Protocol \(EAP\) und geschütztes EAP-Authentifizierungsmethoden bereitstellen sollen, die der Serverzertifikate auf dem NPS-Server erforderlich ist, können Sie NPS-Serverzertifikate bereitstellen, mit dem Guide [Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="deploy-nps-for-8021x-wireless-access"></a>Bereitstellen von NPS für drahtlosen Zugriff mit 802.1X-Authentifizierung

Zum Bereitstellen von NPS für den drahtlosen Zugriff können Sie den Guide mit einem [Bereitstellung Kennwort-basierte Drahtloszugriff mit 802.1X-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access).

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Bereitstellen von NPS für Windows10-VPN-Zugriff

Sie können NPS verwenden, um Verbindungsanforderungen für \(VPN\) immer auf VPN-Verbindungen für Remotemitarbeiter zu verarbeiten, die Computer und Geräte mit Windows10 verwenden.

Weitere Informationen finden Sie in der [Remote Access immer auf VPN-Bereitstellung Anleitung für Windows Server2016 und Windows10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

