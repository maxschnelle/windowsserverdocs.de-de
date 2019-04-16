---
title: Der Leistungsverlauf für Cluster
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 68596cbdcf8593cd3017c8ae5d0836891c78229c
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1894319"
---
# <a name="performance-history-for-clusters"></a>Der Leistungsverlauf für Cluster

> Betrifft: Windows Server-Insider – Vorschau

Unterwebsites der [Verlauf Speicher Leerzeichen direkte](performance-history.md) beschrieben den Verlauf für Cluster erfasst wurden.

Es gibt kein Series, die Ebene der Cluster stammen. Stattdessen Server-Serie wie `clusternode.cpu.usage`, sind für alle Server im Cluster zusammengefasst. Volume-Serie wie `volume.iops.total`, für alle Datenträger im Cluster zusammengefasst werden. Und Serie, z. B. Laufwerk `physicaldisk.size.total`, sind für alle Laufwerke im Cluster zusammengefasst.

## <a name="usage-in-powershell"></a>Verwendung von Diensten in PowerShell

Verwenden Sie das Cmdlet [Get-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster) :

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>Weitere Informationen

- [Speicher Leerzeichen direkte Verlauf](performance-history.md)
