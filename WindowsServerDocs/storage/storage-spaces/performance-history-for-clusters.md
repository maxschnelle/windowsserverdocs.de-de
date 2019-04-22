---
title: Leistungsverlauf für Cluster
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: 68596cbdcf8593cd3017c8ae5d0836891c78229c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818771"
---
# <a name="performance-history-for-clusters"></a>Leistungsverlauf für Cluster

> Gilt für: Windows Server-Insider – Vorschau

Dieser Unterabschnitt von [– Leistungsverlauf für "direkte Speicherplätze"](performance-history.md) beschreibt den Leistungsverlauf für Cluster gesammelt.

Es sind keine Reihen, die auf der Clusterebene stammen. Stattdessen Server Reihe, z. B. `clusternode.cpu.usage`, werden für alle Server im Cluster aggregiert. Volume-Serie, wie z. B. `volume.iops.total`, werden für alle Volumes im Cluster aggregiert. Und Serie wie z. B. `physicaldisk.size.total`, werden für alle Laufwerke im Cluster aggregiert.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden der [Get-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster) Cmdlet:

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>Siehe auch

- [Leistungsverlauf für "direkte Speicherplätze"](performance-history.md)
