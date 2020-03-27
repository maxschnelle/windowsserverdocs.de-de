---
title: Bereitstellen eines Netzwerkrichtlinienservers
description: Dieses Thema enthält Links zu Netzwerk Richtlinien Server-Bereitstellungs Inhalten für Windows Server 2016 und enthält Links zu weiteren Anleitungen zu NPS.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e91f5ce22bcd48e486052ecf54a13617301a058b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316149"
---
# <a name="deploy-network-policy-server"></a>Bereitstellen eines Netzwerkrichtlinienservers

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema finden Sie Informationen zum Bereitstellen des Netzwerk Richtlinien Servers.

>[!NOTE]
>Weitere Informationen zur Netzwerk Richtlinien Server-Dokumentation finden Sie in den folgenden Bibliotheks Abschnitten.  
>- [Ersten Schritte mit dem Netzwerk Richtlinien Server](nps-getstart-top.md)
>- [Planen des Netzwerk Richtlinien Servers](nps-plan-top.md)
>- [Netzwerk Richtlinien Server verwalten](nps-manage-top.md)

Das Handbuch zum Windows Server 2016-Kern Netzwerk enthält einen Abschnitt zum Planen und Installieren von Netzwerk Richtlinien Server-\(NPS-\), und die im Handbuch vorgestellten Technologien dienen als Voraussetzungen für die Bereitstellung von NPS in einer Active Directory-Domäne. Weitere Informationen finden Sie im Abschnitt "Bereitstellen von NPS1" im Windows Server 2016- [Kern Netzwerk Handbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1).

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>Bereitstellen von NPS-Zertifikaten für VPN-und 802.1 x-Zugriff

Wenn Sie Authentifizierungsmethoden wie Extensible Authentication Protocol \(EAP\) und geschütztes EAP bereitstellen möchten, die die Verwendung von Server Zertifikaten auf Ihrem NPS erfordern, können Sie NPS-Zertifikate mit dem Handbuch Bereitstellen von [Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)bereitstellen.

## <a name="deploy-nps-for-8021x-wireless-access"></a>Bereitstellen von NPS für den drahtlos Zugriff mit 802.1 x

Zum Bereitstellen von NPS für den drahtlosen Zugriff können Sie das Handbuch Bereitstellen von Kenn [Wort basiertem 802.1 x authentifizierten drahtlosen Zugriff](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)verwenden.

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Bereitstellen von NPS für Windows 10-VPN-Zugriff

Sie können NPS verwenden, um Verbindungsanforderungen für Always on virtuelles privates Netzwerk \(VPN-\) Verbindungen für Remote Mitarbeiter zu verarbeiten, die Computer und Geräte unter Windows 10 verwenden.

Weitere Informationen finden Sie im [Bereitstellungs Handbuch für RAS-Always on für Windows Server 2016 und Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

