---
title: Unterstützung der Virtualisierung von MultiPoint Services
description: Beschreibt, wie MultiPoint Server mit Hyper-V
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f0864b8-a087-4890-94ef-05efbd3c4241
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 06d518dcea154ac2bab49a7d0e83a90f96be6e44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872521"
---
# <a name="multipoint-services-virtualization-support"></a>Unterstützung der Virtualisierung von MultiPoint Services
MultiPoint Services unterstützt die Hyper-V-Rolle auf zwei Arten:  
  
-   MultiPoint Services können als Gast-Betriebssystem auf einem Server mit Hyper-V bereitgestellt werden.  
  
-   MultiPoint Services können als ein Virtualisierungsserver verwendet werden.   
  
Ausführen von MultiPoint Services auf einem virtuellen Computer ermöglicht die Verwendung von Hyper-V-Verwaltungstools, um Betriebssysteme zu verwalten. Diese Tools umfassen Prüfpunkt- und Rollback-Features, und sie ermöglichen das Exportieren und Importieren von virtuellen Computern. Bei umfangreichen Installationen können Sie Server konsolidieren, indem Sie mehrere MultiPoint Services und virtuelle Computer auf einem einzelnen physischen Server ausgeführt. Mögliche Szenarien:  
  
-   Verfügt über mehr als 20 Arbeitsplätze, einen einzigen Kursraum oder Lab. Anstatt die Bereitstellung von mehreren physischen Computern, die MultiPoint Services ausgeführt wird, können Sie mehrere virtuelle Computer auf einem einzelnen physischen Computer bereitstellen.  
  
    > [!NOTE]  
    > Sie können mehrere MultiPoint-Server, ob physisch oder virtuell über eine einzige MultiPoint-Manager-Konsole verwalten.  
  
-   Der MultiPoint-Server wird auf einem virtuellen Computer mit einem anderen Server-Infrastruktur auf dem gleichen physischen Computer ausgeführt. In diesem Fall zentralisiert diese Serverinfrastruktur, die Domäne, die Sicherheit und die Daten für das Netzwerk. Der MultiPoint-Server Remote Desktop Services bietet und die Desktops zentralisieren.  
  
> [!NOTE]  
> MultiPoint Services auf einem virtuellen Computer ausgeführt wird, werden USB-Over-Ethernet und RDP-Client-Rechner unterstützt. Direkte Video und USB-0 (null) Client verbundene Stationen werden nicht unterstützt.  
  
Weitere Informationen über die Hyper-V-Rolle finden Sie unter [Hyper-V](../../virtualization/hyper-v/hyper-v-on-windows-server.md).  