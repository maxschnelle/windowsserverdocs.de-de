---
title: Leistungs Verlauf für Server
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 02/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 262c35e7d91fe43d2ade955d4606279f8d428f6a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946333"
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
| `clusternode.cpu.usage`          | Prozent |
| `clusternode.cpu.usage.guest`    | Prozent |
| `clusternode.cpu.usage.host`     | Prozent |
| `clusternode.memory.total`       | Byte   |
| `clusternode.memory.available`   | Byte   |
| `clusternode.memory.usage`       | Byte   |
| `clusternode.memory.usage.guest` | Byte   |
| `clusternode.memory.usage.host`  | Byte   |

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

Mithilfe der `% Total Run Time` Leistungsindikatoren wird sichergestellt, dass der Leistungs Verlauf alle Verwendungs Attribute verwendet

Wenn Hyper-V nicht aktiviert ist:

| Reihen                           | Quellen Counter |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *Zins* |
| `clusternode.cpu.usage.host`     | *identisch mit der Gesamtauslastung* |

Ungeachtet der unvollkommenen Synchronisierung `clusternode.cpu.usage` ist immer `clusternode.cpu.usage.host` Plus `clusternode.cpu.usage.guest` .

Mit dem gleichen Nachteil `clusternode.cpu.usage.guest` ist immer die Summe von `vm.cpu.usage` für alle virtuellen Maschinen auf dem Host Server.

Die `memory.*` Reihe ist (in Kürze verfügbar).

  > [!NOTE]
  > Leistungsindikatoren werden über das gesamte Intervall gemessen, nicht als Stichprobe. Wenn sich der Server z. b. für 9 Sekunden im Leerlauf befindet, in der 10. Sekunde aber eine Spitzen Auslastung von 100% beträgt, wird der Wert im `clusternode.cpu.usage` Durchschnitt in diesem 10-Sekunden-Intervall als 10% aufgezeichnet. Dadurch wird sichergestellt, dass der Leistungs Verlauf alle Aktivitäten erfasst und stabil ist.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden [Sie das Get-clusternode-](/powershell/module/failoverclusters/get-clusternode) Cmdlet:

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="additional-references"></a>Weitere Verweise

- [Leistungsverlauf für Direkte Speicherplätze](performance-history.md)
