---
title: Bereitstellen eines Netzwerkrichtlinienservers
description: Dieses Thema enthält Links zu Netzwerk Richtlinien Server-Bereitstellungs Inhalten für Windows Server 2016 und enthält Links zu weiteren Anleitungen zu NPS.
manager: brianlic
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e83e71e87ae9cb442299861125ffb524ef3c1c81
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996852"
---
# <a name="deploy-network-policy-server"></a>Bereitstellen eines Netzwerkrichtlinienservers

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema finden Sie Informationen zum Bereitstellen des Netzwerk Richtlinien Servers.

>[!NOTE]
>Weitere Informationen zur Netzwerk Richtlinien Server-Dokumentation finden Sie in den folgenden Bibliotheks Abschnitten.
>- [Erste Schritte mit dem Netzwerkrichtlinienserver](nps-getstart-top.md)
>- [Planen eines Netzwerkrichtlinienservers](nps-plan-top.md)
>- [Verwalten eines Netzwerkrichtlinienservers](nps-manage-top.md)

Das Handbuch zum Windows Server 2016-Kern Netzwerk enthält einen Abschnitt zum Planen und Installieren von Netzwerk Richtlinien Server \( -NPS \) . die im Handbuch dargestellten Technologien dienen als Voraussetzungen für die Bereitstellung von NPS in einer Active Directory Domäne. Weitere Informationen finden Sie im Abschnitt "Bereitstellen von NPS1" im Windows Server 2016- [Kern Netzwerk Handbuch](../../core-network-guide/core-network-guide.md#BKMK_deployNPS1).

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>Bereitstellen von NPS-Zertifikaten für VPN-und 802.1 x-Zugriff

Wenn Sie Authentifizierungsmethoden wie Extensible Authentication Protocol \( EAP \) und geschütztes EAP bereitstellen möchten, die die Verwendung von Server Zertifikaten auf Ihrem NPS erfordern, können Sie NPS-Zertifikate mit dem Handbuch Bereitstellen von [Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen](../../core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments.md)bereitstellen.

## <a name="deploy-nps-for-8021x-wireless-access"></a>Bereitstellen von NPS für den drahtlos Zugriff mit 802.1 x

Zum Bereitstellen von NPS für den drahtlosen Zugriff können Sie das Handbuch Bereitstellen von Kenn [Wort basiertem 802.1 x authentifizierten drahtlosen Zugriff](../../core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access.md)verwenden.

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Bereitstellen von NPS für Windows 10-VPN-Zugriff

Sie können NPS verwenden, um Verbindungsanforderungen für Always on VPN-Verbindungen für virtuelle private Netzwerke \( \) für Remote Mitarbeiter zu verarbeiten, die Computer und Geräte unter Windows 10 verwenden.

Weitere Informationen finden Sie im [Bereitstellungs Handbuch für RAS-Always on für Windows Server 2016 und Windows 10](../../../remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy.md).