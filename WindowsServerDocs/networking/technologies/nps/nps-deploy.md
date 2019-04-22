---
title: Bereitstellen eines Netzwerkrichtlinienservers
description: Dieses Thema enthält Links zu Inhalten der Netzwerkrichtlinienserver-Bereitstellung für Windows Server 2016, und enthält Links zu weiteren Anleitungen zum NPS.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8da8951a9c6ed5022c892bbf01b33614d38abc5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814841"
---
# <a name="deploy-network-policy-server"></a>Bereitstellen eines Netzwerkrichtlinienservers

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema Informationen zum Bereitstellen des Netzwerkrichtlinienservers verwenden.

>[!NOTE]
>Weitere Dokumentation für Network Policy Server können Sie die folgenden Abschnitte der Bibliothek.  
>- [Erste Schritte mit der Netzwerkrichtlinienserver](nps-getstart-top.md)
>- [Planen des Netzwerkrichtlinienservers](nps-plan-top.md)
>- [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md)

Windows Server 2016 Core Network Guide enthält einen Abschnitt zum Planen und Installieren von Netzwerkrichtlinienserver \(NPS\), und die Technologien, die in diesem Handbuch dargestellten dienen als Voraussetzung für die Bereitstellung von NPS in Active Directory-Domäne. Weitere Informationen finden Sie im Abschnitt "Bereitstellen von NPS1" in Windows Server 2016 [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1).

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>Bereitstellen von NPS-Zertifikaten für VPN und Zugriff mit 802.1X-Authentifizierung

Wenn Sie die Authentifizierungsmethoden wie die Extensible Authentication-Protokoll bereitstellen möchten \(EAP\) Protected EAP, die die Verwendung von Server benötigen Zertifikate auf den NPS, und Sie können NPS-Zertifikate bereitstellen, mit dem für [ Bereitstellen von Serverzertifikaten für 802.1X-authentifizierte Kabelnetzwerke und Drahtlosnetzwerke Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="deploy-nps-for-8021x-wireless-access"></a>Bereitstellen von NPS für drahtlosen Zugriff mit 802.1X-Authentifizierung

Um NPS für den drahtlosen Zugriff bereitzustellen, können Sie das Handbuch [Bereitstellung Kennwort-basierten Drahtloszugriff mit 802.1X-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access).

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Bereitstellen von NPS für Windows 10-VPN-Zugriff

Sie können NPS verwenden, zum Verarbeiten von verbindungsanforderungen für immer auf virtuelle Private Netzwerke \(VPN\) Verbindungen für Remotemitarbeiter, die Computer und Geräte mit Windows 10 verwenden.

Weitere Informationen finden Sie unter den [Remote Access immer auf VPN-Bereitstellung Handbuch für Windows Server 2016 und Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

