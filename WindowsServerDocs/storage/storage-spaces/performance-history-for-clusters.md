---
title: Leistungs Verlauf für Cluster
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7a5eec986d6e7d633f1917c599ab6fcd244c7008
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856203"
---
# <a name="performance-history-for-clusters"></a>Leistungs Verlauf für Cluster

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der Leistungs Verlauf beschrieben, der für Cluster erfasst wurde.

Es sind keine Reihen vorhanden, die von der Cluster Ebene stammen. Stattdessen werden Server Reihen, wie z. b. `clusternode.cpu.usage`, für alle Server im Cluster aggregiert. Volumereihen, wie z. b. `volume.iops.total`, werden für alle Volumes im Cluster aggregiert. Und Laufwerks Reihen, wie z. b. `physicaldisk.size.total`, werden für alle Laufwerke im Cluster aggregiert.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie das Cmdlet " [Get-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster) ":

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>Siehe auch

- [Leistungs Verlauf für direkte Speicherplätze](performance-history.md)
