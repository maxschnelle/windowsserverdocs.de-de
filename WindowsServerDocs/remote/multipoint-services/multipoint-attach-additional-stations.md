---
title: Anfügen zusätzlicher Stationen an den Multipoint-Server
description: Hinzufügen von weiteren Stationen zu ihrer Multipoint Services-Bereitstellung
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d78ebf4e-0968-4014-9a42-9f75cc50cb52
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 45340f02b120b1431b1f58a58ed03ea40e17a14c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394747"
---
# <a name="attach-additional-stations-to-multipoint-services"></a>Anfügen zusätzlicher Stationen an Multipoint Services
In ihrer Multipoint Services-Umgebung verwenden die Benutzer Stationen, um eine Verbindung mit Multipoint Services herzustellen und ihre Arbeit zu erledigen. Die Stationen sind die Benutzer Endpunkte zum Herstellen einer Verbindung mit dem Computer, auf dem Multipoint Services ausgeführt wird.  
  
Multipoint Services unterstützt drei Arten von Stationen:  
  
-   Direkt mit Videos verbundene Stationen  
  
-   USB-Verbindungen mit Clientverbindungen (und USB-über-Ethernet-Verbindungen mit einem Client verbundene Stationen)  
  
-   Verbundene RDP-over-LAN-Stationen  
  
Die Klassifizierungen basieren auf der Hardware der Station und der Art der verwendeten Verbindung. Sie können Verbindungstypen für Ihre Stationen kombinieren und abgleichen. Die einzige Voraussetzung ist, dass es sich bei der primären Station (die Sie zuvor installiert haben) um eine Station mit direkt Videoverbindung handeln muss. Weitere Informationen zu Station-Setups finden Sie unter [Multipoint-Stationen](MultiPoint-services-Stations.md).  
  
Anweisungen zum Einrichten der einzelnen Stations Stationen finden Sie in den folgenden Abschnitten:  
  
-   [Einrichten einer Station mit direkter Videoverbindung](Set-up-a-direct-video-connected-station-in-MultiPoint-services.md)  
  
-   [Einrichten einer verbundenen USB-Station ohne Clients](Set-up-a-USB-zero-client-connected-station-in-MultiPoint-services.md)  
  
-   [Einrichten einer mittels RDP über LAN verbundenen Station](Set-up-an-RDP-over-LAN-connected-station-in-MultiPoint-services.md)  
  
Einen ausführlichen Vergleich der Stations Typen finden Sie unter [Stations Typvergleich](multipoint-services-stations.md#BKMK_StationTypeComparison).  
  
> [!NOTE]  
> -   In den Vorgehensweisen zum Anfügen von Stationen wird nicht beschrieben, wie Sie zwischen Hubs oder downstreamhubs einrichten. Informationen dazu, wo Sie diese Hubs installieren, finden Sie unter [Multipoint-Stationen](MultiPoint-services-Stations.md).  
> -   In einigen Fällen müssen Sie möglicherweise Station Virtual Desktops erstellen, die auf virtuellen Computern ausgeführt werden. Beispielsweise verwenden Sie Anwendungen, die nicht auf Windows Server oder Anwendungen installiert werden können, auf denen nicht mehrere Instanzen auf demselben Host Computer ausgeführt werden. Weitere Informationen finden Sie unter [Erstellen von virtuellen Windows 10 Enterprise-Desktops für Stationen](Create-Windows-10-Enterprise-virtual-desktops-for-stations.md).  
  
> [!TIP]  
> Es ist hilfreich, die Stationen in der Reihenfolge ihrer physischen Standorte zu erstellen, damit Sie sequenziell in Multipoint Server identifiziert werden. Wenn Sie den Namen einer Station später ändern möchten, können Sie dies in Multipoint Manager tun. Weitere Informationen finden Sie unter Neuzuordnen aller Stationen in Hilfe und Support für Multipoint-Server.