---
title: Unterstützung der Virtualisierung von MultiPoint Services
description: Beschreibt die Verwendung von Multipoint Services mit Hyper-V
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 3f0864b8-a087-4890-94ef-05efbd3c4241
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b2a07a71703887c9636cd02ca642be4cc4ddb47b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951805"
---
# <a name="multipoint-services-virtualization-support"></a>Unterstützung der Virtualisierung von MultiPoint Services
Multipoint Services unterstützt die Hyper-V-Rolle auf zwei Arten:

-   Multipoint Services können als Gast Betriebssystem auf einem Server mit Hyper-V bereitgestellt werden.

-   Multipoint Services können als Virtualisierungsserver verwendet werden.

Beim Ausführen von Multipoint Services auf einem virtuellen Computer werden die Hyper-V-Tools zum Verwalten von Betriebssystemen verwendet. Zu diesen Tools gehören Checkpoint-und Rollback-Features, die es Ihnen ermöglichen, virtuelle Computer zu exportieren und zu importieren. Bei größeren Installationen können Sie Server konsolidieren, indem Sie mehrere virtuelle Multipoint Services-Computer auf einem einzelnen physischen Server ausführen. Mögliche Szenarien:

-   Ein einzelner Classroom oder Lab verfügt über mehr als 20 Arbeitsplätze. Anstatt mehrere physische Computer bereitzustellen, auf denen Multipoint Services ausgeführt wird, können Sie mehrere virtuelle Maschinen auf einem einzelnen physischen Computer bereitstellen.

    > [!NOTE]
    > Sie können mehrere Multipoint-Server, unabhängig davon, ob physisch oder virtuell, über eine einzelne Multipoint Manager-Konsole verwalten.

-   Der Multipoint-Server wird auf einem virtuellen Computer mit einer anderen Serverinfrastruktur auf demselben physischen Computer ausgeführt. In diesem Fall zentralisiert diese Serverinfrastruktur die Domäne, die Sicherheit und die Daten für das Netzwerk. Der Multipoint-Server stellt Remotedesktopdienste bereit und zentralisiert die Desktops.

> [!NOTE]
> Beim Ausführen von Multipoint Services auf einem virtuellen Computer werden USB-over-Ethernet-und RDP-Client Stationen unterstützt. Direkt Video-und USB-Client verbundene Stationen werden nicht unterstützt.

Weitere Informationen zur Hyper-v-Rolle finden Sie unter [Hyper-v](../../virtualization/hyper-v/hyper-v-on-windows-server.md).