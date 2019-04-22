---
title: Leistungsverlauf für Server
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/0s/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: 33fd62376e9769c23fc6b00eefde9a9b95eb4650
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820591"
---
# <a name="performance-history-for-servers"></a>Leistungsverlauf für Server

> Gilt für: Windows Server-Insider – Vorschau

Dieser Unterabschnitt von [– Leistungsverlauf für "direkte Speicherplätze"](performance-history.md) beschreibt ausführlich den Leistungsverlauf für Server gesammelt. Leistungsverlauf für ist für jeden Server im Cluster verfügbar.

   > [!NOTE]
   > Leistungsverlauf für kann nicht für einen Server gesammelt werden, die nicht verfügbar ist. Sammlung wird automatisch fortgesetzt, wenn der Server wieder verfügbar ist.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Dieser Reihe werden für jeden berechtigten Server erfasst:

| Serie                           | Einheit    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | Prozent |
| `clusternode.cpu.usage.guest`    | Prozent |
| `clusternode.cpu.usage.host`     | Prozent |
| `clusternode.memory.total`       | Bytes   |
| `clusternode.memory.available`   | Bytes   |
| `clusternode.memory.usage`       | Bytes   |
| `clusternode.memory.usage.guest` | Bytes   |
| `clusternode.memory.usage.host`  | Bytes   |

Darüber hinaus, wie z. B. Laufwerk Reihe `physicaldisk.size.total` werden aggregiert für alle geeigneten Laufwerke, die angefügt werden, auf dem Server, und Network Adapter-Serie, wie z. B. `networkadapter.bytes.total` werden aggregiert für alle berechtigten Netzwerkadapter, die mit dem Server verbunden.

## <a name="how-to-interpret"></a>Gewusst wie: interpretieren

| Serie                           | Gewusst wie: interpretieren                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | Prozentsatz der Prozessorzeit, die nicht im Leerlauf befindet.                        |
| `clusternode.cpu.usage.guest`    | Prozentsatz der Prozessorzeit für den Gast (dem virtuellen Computer) bei Bedarf verwendet. |
| `clusternode.cpu.usage.host`     | Prozentsatz der Prozessorzeit für den Host bei Bedarf verwendet.                    |
| `clusternode.memory.total`       | Der gesamte physische Speicher des Servers.                              |
| `clusternode.memory.available`   | Der verfügbare Arbeitsspeicher des Servers.                                   |
| `clusternode.memory.usage`       | Der zugeordnete (nicht verfügbar) Arbeitsspeicher des Servers.                   |
| `clusternode.memory.usage.guest` | Der Gast (dem virtuellen Computer) bei Bedarf zugewiesene Arbeitsspeicher.               |
| `clusternode.memory.usage.host`  | Der Host bei Bedarf zugewiesene Arbeitsspeicher.                                  |

## <a name="where-they-come-from"></a>Wo diese herkommen

Die `cpu.*` Reihe werden gesammelt, von verschiedenen Leistungsindikatoren, abhängig davon, ob Hyper-V aktiviert ist.

Wenn die Hyper-V aktiviert ist:

| Serie                           | Source-Indikator |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

Mithilfe der `% Total Run Time` Leistungsindikatoren wird sichergestellt, dass – Leistungsverlauf für die gesamte Nutzung Attribute.

Wenn Hyper-V nicht aktiviert ist:

| Serie                           | Source-Indikator |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *zero* |
| `clusternode.cpu.usage.host`     | *identisch mit gesamtnutzung* |

Abweichend von perfekt Synchronisierung `clusternode.cpu.usage` ist immer `clusternode.cpu.usage.host` plus `clusternode.cpu.usage.guest`.

Mit der gleichen Einschränkung `clusternode.cpu.usage.guest` ist immer die Summe der `vm.cpu.usage` für alle virtuellen Computer, auf dem Host.

Die `memory.*` Reihen sind (in Kürze verfügbar).

  > [!NOTE]
  > Leistungsindikatoren werden anhand des gesamten Intervalls, nicht entnommen gemessen. Wenn der Server für 9 Sekunden, aber auf 100 % CPU-Spitzen im zweiten 10. im Leerlauf ist z. B. die `clusternode.cpu.usage` aufgezeichnet werden als 10 % durchschnittliche Intervall 10 Sekunden. Dadurch wird der Leistungsverlauf erfasst alle Aktivitäten und ist stabil, um Rauschen.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden der [Get-ClusterNode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode) Cmdlet:

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>Siehe auch

- [Leistungsverlauf für "direkte Speicherplätze"](performance-history.md)
