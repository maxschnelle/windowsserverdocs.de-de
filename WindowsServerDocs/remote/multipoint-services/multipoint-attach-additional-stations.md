---
title: Fügen Sie zusätzliche Sender an Ihr MultiPoint-server
description: Fügen Sie weitere Stationen auf Ihrem MultiPoint Services-Bereitstellung
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 57fc8ed6774c3266298ecd98e8f609ec01f63ef6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889261"
---
# <a name="attach-additional-stations-to-multipoint-services"></a>Fügen Sie zusätzliche Stationen mit MultiPoint Services
In Ihrem MultiPoint Services-Umgebung können Ihre Benutzer Stationen mit MultiPoint Services herstellen, und führen Sie ihre Arbeit. Die Stationen werden die Benutzer-Endpunkte für die Verbindung mit dem Computer, auf dem Multipoint Services ausgeführt wird.  
  
MultiPoint Services unterstützt drei Arten von Station:  
  
-   Im Video direkt verbundene Stationen  
  
-   USB 0 (null), Client verbundene Stationen (und USB über Ethernet-0 (null) Client verbundene Stationen)  
  
-   RDP-Over-LAN verbundene Stationen  
  
Die Klassifizierungen basieren auf einer Station für die Hardware und die Art der Verbindung, der verwendet wird. Sie mischen und Zuordnen von Verbindungstypen für Ihre Stationen. Die einzige Voraussetzung ist, dass die primäre Station (die Sie zuvor installiert haben) auf einer Station Direct-Video-Verbindung sein muss. Weitere Informationen zu Station-Setups, finden Sie unter [MultiPoint-Stationen](MultiPoint-services-Stations.md).  
  
Anweisungen dazu, wie Sie jede Art von Station einrichten, finden Sie in der folgenden:  
  
-   [Einrichten einer Station Direct-Video-Verbindung](Set-up-a-direct-video-connected-station-in-MultiPoint-services.md)  
  
-   [Richten Sie ein USB-zero Client verbundene station](Set-up-a-USB-zero-client-connected-station-in-MultiPoint-services.md)  
  
-   [Einrichten einer Station RDP-Over-LAN-Verbindung](Set-up-an-RDP-over-LAN-connected-station-in-MultiPoint-services.md)  
  
Einen ausführlichen Vergleich der Station-Typen finden Sie unter [Station Typvergleich](multipoint-services-stations.md#BKMK_StationTypeComparison).  
  
> [!NOTE]  
> -   Die Verfahren für das Anfügen von Stationen werden nicht zwischen Hubs "oder" downstreamhubs einrichten beschrieben. Informationen dazu, wo diese Hubs zu installieren, finden Sie unter [MultiPoint-Stationen](MultiPoint-services-Stations.md).  
> -   In einigen Fällen müssen Sie möglicherweise Station virtuelle Desktops erstellen, die auf virtuellen Computern ausgeführt. Verwenden Sie z. B. Anwendungen, die unter Windows Server installiert werden können oder Anwendungen, die nicht mehrere Instanzen auf demselben Hostcomputer ausgeführt werden. Weitere Informationen finden Sie unter [Erstellen von Windows 10 Enterprise-Desktops für Stationen](Create-Windows-10-Enterprise-virtual-desktops-for-stations.md).  
  
> [!TIP]  
> Es ist nützlich, um Ihre Stationen in der Reihenfolge ihrer physischen Standorten erstellen, sodass sie nacheinander im MultiPoint-Server identifiziert werden. Wenn Sie später den Namen einer Station ändern möchten, möglich, die im MultiPoint-Manager. Weitere Informationen finden Sie in der Neuzuordnung alle Kontrollstationen in MultiPoint Server-Hilfe und Support.