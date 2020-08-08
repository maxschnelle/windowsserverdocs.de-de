---
title: Leistungs Verlauf für Cluster
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: ea80be97e3940850f9892c50c534c3449fd3ecdb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954667"
---
# <a name="performance-history-for-clusters"></a>Leistungs Verlauf für Cluster

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der Leistungs Verlauf beschrieben, der für Cluster erfasst wurde.

Es sind keine Reihen vorhanden, die von der Cluster Ebene stammen. Stattdessen werden Server Reihen, wie z `clusternode.cpu.usage` . b., für alle Server im Cluster aggregiert. Volumereihen, wie z `volume.iops.total` . b., werden für alle Volumes im Cluster aggregiert. Und Laufwerks Reihen, wie z `physicaldisk.size.total` . b., werden für alle Laufwerke im Cluster aggregiert.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie das Cmdlet " [Get-Cluster](/powershell/module/failoverclusters/get-cluster) ":

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="additional-references"></a>Weitere Verweise

- [Leistungsverlauf für Direkte Speicherplätze](performance-history.md)
