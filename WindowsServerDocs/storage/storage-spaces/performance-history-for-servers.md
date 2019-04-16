---
title: Leistungsverlauf für Server
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/0s/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 33fd62376e9769c23fc6b00eefde9a9b95eb4650
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1894249"
---
# <a name="performance-history-for-servers"></a>Leistungsverlauf für Server

> Betrifft: Windows Server-Insider – Vorschau

Unterwebsites beschrieben der [Verlauf Speicher Leerzeichen direkte](performance-history.md) ausführlich der Verlauf für Server erfasst. Leistungsverlauf ist für jeden Server im Cluster verfügbar.

   > [!NOTE]
   > Leistungsverlauf kann nicht für einen Server erfasst werden sollen, die nicht verfügbar ist. Auflistung wird automatisch wieder aufgenommen, wenn der Server wieder verfügbar ist.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Diese Serie sind für jeden zu auswählbaren Server erfasst:

| Serie                           | Einheit    |
|----------------------------------|---------|
| `clusternode.cpu.usage`          | Prozent |
| `clusternode.cpu.usage.guest`    | Prozent |
| `clusternode.cpu.usage.host`     | Prozent |
| `clusternode.memory.total`       |  Bytes   |
| `clusternode.memory.available`   |  Bytes   |
| `clusternode.memory.usage`       |  Bytes   |
| `clusternode.memory.usage.guest` |  Bytes   |
| `clusternode.memory.usage.host`  |  Bytes   |

Darüber hinaus wie Laufwerk Datenreihe `physicaldisk.size.total` werden für alle Server und Network Adapter Serie wie zugeordnet zu auswählbaren Laufwerke aggregiert `networkadapter.bytes.total` für alle zu auswählbaren Netzwerkadapter, die mit dem Server verbundene zusammengefasst werden.

## <a name="how-to-interpret"></a>Wie interpretiert werden

| Serie                           | Wie interpretiert werden                                                      |
|----------------------------------|-----------------------------------------------------------------------|
| `clusternode.cpu.usage`          | Prozentsatz der Prozessorzeit an, die nicht im Leerlauf ist.                        |
| `clusternode.cpu.usage.guest`    | Prozentsatz der Prozessorzeit für bei Bedarf Gast (virtueller Computer) verwendet. |
| `clusternode.cpu.usage.host`     | Prozentsatz der Prozessorzeit für Host bei Bedarf verwendet.                    |
| `clusternode.memory.total`       | Gesamten physikalischen Arbeitsspeichers des Servers.                              |
| `clusternode.memory.available`   | Der verfügbare Arbeitsspeicher des Servers.                                   |
| `clusternode.memory.usage`       | Die (nicht verfügbar) reservierter Speicher des Servers.                   |
| `clusternode.memory.usage.guest` | Der Arbeitsspeicher, die bei Bedarf Gast (virtueller Computer) zugewiesen ist.               |
| `clusternode.memory.usage.host`  | Der Arbeitsspeicher, die bei Bedarf Host zugewiesen ist.                                  |

## <a name="where-they-come-from"></a>Kommen aus

Die `cpu.*` Serie aus verschiedenen Leistungsindikatoren abhängig davon, ob Hyper-V aktiviert ist gesammelt werden.

Wenn die Hyper-V aktiviert ist:

| Serie                           | Quelle Indikator |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Hyper-V Hypervisor Logical Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.guest`    | `Hyper-V Hypervisor Virtual Processor` > `_Total` > `% Total Run Time`      |
| `clusternode.cpu.usage.host`     | `Hyper-V Hypervisor Root Virtual Processor` > `_Total` > `% Total Run Time` |

Mithilfe der `% Total Run Time` Leistungsindikatoren wird sichergestellt, dass die Leistungsverlauf aller Attribute.

Wenn Hyper-V nicht aktiviert ist:

| Serie                           | Quelle Indikator |
|----------------------------------|----------------|
| `clusternode.cpu.usage`          | `Processor` > `_Total` > `% Processor Time` |
| `clusternode.cpu.usage.guest`    | *0 (null)* |
| `clusternode.cpu.usage.host`     | *identisch mit Gesamtverwendung* |

Ungeachtet der unvollständige Synchronisierung `clusternode.cpu.usage` handelt es sich immer `clusternode.cpu.usage.host` plus `clusternode.cpu.usage.guest`.

Mit der gleichen Einschränkung `clusternode.cpu.usage.guest` ist immer die Summe der `vm.cpu.usage` für alle virtuellen Computer, auf dem Hostserver.

Die `memory.*` Datenreihe sind (in KÜRZE).

  > [!NOTE]
  > Über die gesamte Intervall nicht aufgenommen werden Leistungsindikatoren gemessen. Wenn der Server für 9 Sekunden jedoch abgeschwächt werden auf 100 % CPU in der zweiten 10., im Leerlauf ist beispielsweise seine `clusternode.cpu.usage` , werden aufgezeichnet als 10 % durchschnittlich während dieses Intervalls 10 Sekunden. Dadurch wird sichergestellt, dessen Leistungsverlauf zeichnet alle Aktivitäten und ist robust, um Rauschen.

## <a name="usage-in-powershell"></a>Verwendung von Diensten in PowerShell

Verwenden Sie das Cmdlet [Get-ClusterNode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode) :

```PowerShell
Get-ClusterNode <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>Weitere Informationen

- [Speicher Leerzeichen direkte Verlauf](performance-history.md)
