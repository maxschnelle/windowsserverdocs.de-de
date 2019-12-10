---
title: Leistungs Verlauf für Server
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/05/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: bbfc92f7926b93f5f6716514e64672f4aa304c0f
ms.sourcegitcommit: e817a130c2ed9caaddd1def1b2edac0c798a6aa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/09/2019
ms.locfileid: "74945250"
---
# <a name="performance-history-for-servers"></a>Leistungs Verlauf für Server

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der Leistungs Verlauf ausführlich beschrieben, der für-Server erfasst wurde. Der Leistungs Verlauf ist für jeden Server im Cluster verfügbar.

   > [!NOTE]
   > Der Leistungs Verlauf kann für einen nicht herunter zufügenden Server nicht erfasst werden. Die Sammlung wird automatisch fortgesetzt, wenn der Server wieder verfügbar ist.

## <a name="series-names-and-units"></a>Reihen Namen und Einheiten

Diese Reihen werden für jeden berechtigten Server erfasst:

| Reihen                           | Einheit    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | percent |
| `clusternode.cpu.usage.guest`    | percent |
| `clusternode.cpu.usage.host`     | percent |
| `clusternode.memory.total`       | Bytes   |
| `clusternode.memory.available`   | Bytes   |
| `clusternode.memory.usage`       | Bytes   |
| `clusternode.memory.usage.guest` | Bytes   |
| `clusternode.memory.usage.host`  | Bytes   |

Außerdem werden Laufwerks Reihen wie `physicaldisk.size.total` für alle berechtigten Laufwerke aggregiert, die an den Server angefügt sind, und Netzwerkadapter Reihen wie `networkadapter.bytes.total` werden für alle berechtigten Netzwerkadapter aggregiert, die mit dem Server verbunden sind.

## <a name="how-to-interpret"></a>Interpretieren

| Reihen                           | Interpretieren                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | Prozentsatz der Prozessorzeit, die sich nicht im Leerlauf befindet.                        |
| `clusternode.cpu.usage.guest`    | Prozentsatz der Prozessorzeit, die für die Anforderung des Gasts (virtueller Computer) verwendet wird |
| `clusternode.cpu.usage.host`     | Prozentsatz der Prozessorzeit, die für den Host Bedarf verwendet wird.                    |
| `clusternode.memory.total`       | Der gesamte physische Speicher des Servers.                              |
| `clusternode.memory.available`   | Der verfügbare Arbeitsspeicher des Servers.                                   |
| `clusternode.memory.usage`       | Der zugewiesene (nicht verfügbare) Arbeitsspeicher des Servers.                   |
| `clusternode.memory.usage.guest` | Der der Gast Anforderung (virtueller Computer) zugeordnete Arbeitsspeicher.               |
| `clusternode.memory.usage.host`  | Der Host Bedarf zugeordnete Arbeitsspeicher.                                  |

## <a name="where-they-come-from"></a>Woher Sie stammen

Die `cpu.*` Reihe wird abhängig davon, ob Hyper-V aktiviert ist, von verschiedenen Leistungsindikatoren gesammelt.

Wenn Hyper-V aktiviert ist:

| Reihen                           | Quellen Counter |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

Mit den `% Total Run Time` Indikatoren wird sichergestellt, dass der Leistungs Verlauf alle Verwendungs Attribute verwendet.

Wenn Hyper-V nicht aktiviert ist:

| Reihen                           | Quellen Counter |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *zero* |
| `clusternode.cpu.usage.host`     | *identisch mit der Gesamtauslastung* |

Ungeachtet der unvollkommenen Synchronisierung ist `clusternode.cpu.usage` immer `clusternode.cpu.usage.host` Plus `clusternode.cpu.usage.guest`.

Mit dem gleichen Nachteil ist `clusternode.cpu.usage.guest` immer die Summe der `vm.cpu.usage` für alle virtuellen Maschinen auf dem Host Server.

Die `memory.*` Reihe sind (in Kürze verfügbar).

  > [!NOTE]
  > Leistungsindikatoren werden über das gesamte Intervall gemessen, nicht als Stichprobe. Wenn sich der Server z. b. für 9 Sekunden im Leerlauf befindet, aber in der 10. Sekunde zu 100% CPU-Spitzen, wird sein `clusternode.cpu.usage` im Durchschnitt in diesem 10-Sekunden-Intervall als 10% aufgezeichnet. Dadurch wird sichergestellt, dass der Leistungs Verlauf alle Aktivitäten erfasst und stabil ist.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden [Sie das Get-clusternode-](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode) Cmdlet:

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>Weitere Informationen:

- [Leistungs Verlauf für direkte Speicherplätze](performance-history.md)
