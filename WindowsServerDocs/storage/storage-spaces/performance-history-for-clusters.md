---
title: Leistungs Verlauf für Cluster
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ee2e85723cc2449e8cb9c42ccb7d6b761482e3a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474867"
---
# <a name="performance-history-for-clusters"></a>Leistungs Verlauf für Cluster

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der Leistungs Verlauf beschrieben, der für Cluster erfasst wurde.

Es sind keine Reihen vorhanden, die von der Cluster Ebene stammen. Stattdessen werden Server Reihen, wie z `clusternode.cpu.usage` . b., für alle Server im Cluster aggregiert. Volumereihen, wie z `volume.iops.total` . b., werden für alle Volumes im Cluster aggregiert. Und Laufwerks Reihen, wie z `physicaldisk.size.total` . b., werden für alle Laufwerke im Cluster aggregiert.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie das Cmdlet " [Get-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster) ":

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Leistungsverlauf für Direkte Speicherplätze](performance-history.md)
