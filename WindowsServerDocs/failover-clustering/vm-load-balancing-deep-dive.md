---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: Eingehender Einblick in den Lastenausgleich virtueller Computer
ms.topic: article
manager: eldenc
ms.author: johnmar
author: JasonGerend
ms.date: 09/19/2016
ms.openlocfilehash: 7fc9b449b11b5faf05ac279628f093053e292e8c
ms.sourcegitcommit: 7a8a608df059b4278a974c52ed7b865421a83aa6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/08/2020
ms.locfileid: "91833311"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>Eingehender Einblick in den Lastenausgleich virtueller Computer

> Gilt für: Windows Server 2019, Windows Server 2016

Der [Lastenausgleich des virtuellen](vm-load-balancing-overview.md) Computers optimiert die Auslastung von Knoten in einem Failovercluster. In diesem Dokument wird beschrieben, wie Sie den VM-Lastenausgleich konfigurieren und steuern.

## <a name="heuristics-for-balancing"></a><a id="heuristics-for-balancing"></a>Heuristik für den Ausgleich
Der Lastenausgleich des virtuellen Computers wertet die Auslastung eines Knotens basierend auf der folgenden Heuristik aus:
1. Aktueller **Speicher**Mangel: der Arbeitsspeicher ist die häufigste Ressourcen Einschränkung auf einem Hyper-V-Host.
2. CPU- **Auslastung** des Knotens, der über ein 5-minütiges Zeitfenster übermittelt wird: entschärfen eines Knotens im Cluster wird überlastet

## <a name="controlling-the-aggressiveness-of-balancing"></a><a id="controlling-aggressiveness-of-balancing"></a>Steuern der Aggressivität des Ausgleichs
Die Aggressivität des Ausgleichs basierend auf der Arbeitsspeicher-und CPU-Heuristik kann mithilfe von über die allgemeine Cluster Eigenschaft "autobalancerlevel" konfiguriert werden. Führen Sie Folgendes in PowerShell aus, um die Aggressivität zu steuern:

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| Autobalancerlevel | Aggressi | Verhalten |
|-------------------|----------------|----------|
| 1 (Standard) | Niedrig | Verschieben, wenn Host mehr als 80% geladen ist |
| 2 | Medium | Verschieben, wenn Host mehr als 70% geladen ist |
| 3 | Hoch | Durchschnittliche Knoten und verschieben, wenn der Host mehr als 5% oberhalb des Durchschnitts ist |

![Grafik von PowerShell zum Konfigurieren der Aggressivität des Ausgleichs](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-vm-load-balancing"></a>Steuern des VM-Lasten Ausgleichs
Der VM-Lastenausgleich ist standardmäßig aktiviert, und wenn ein Lastenausgleich durchgeführt wird, kann die allgemeine Eigenschaft "autobalancermode" des Clusters konfiguriert werden. So steuern Sie, wann die Knoten Fairness den Cluster ausgleicht

### <a name="using-failover-cluster-manager"></a>Verwenden von Failovercluster-Manager:
1. Klicken Sie mit der rechten Maustaste auf den Cluster Namen, und wählen Sie die Option "Eigenschaften"  ![ aus, um die Eigenschaft für den Cluster über Failovercluster-Manager](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  Wählen Sie das Bereich "Balancer" ![ aus, indem Sie die Option "Balancer" durch Failovercluster-Manager auswählen.](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>Mithilfe von PowerShell:
Führen Sie Folgendes aus:
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|Autobalancermode |Verhalten|
|:----------------:|:----------:|
|0| Disabled|
|1| Lastenausgleich bei Knoten Beitritt|
|2 (Standardwert)| Lastenausgleich für den Knoten Beitritt und alle 30 Minuten |

## <a name="vm-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a>VM-Lastenausgleich im Vergleich zur System Center Virtual Machine Manager dynamischen Optimierung
Mit dem Feature "Knoten Fairness" werden in-Box-Funktionen bereitgestellt, die auf bereit Stellungen ohne System Center Virtual Machine Manager (SCVMM) ausgerichtet sind. Die dynamische SCVMM-Optimierung ist der empfohlene Mechanismus zum Ausgleichen der Auslastung virtueller Maschinen in Ihrem Cluster für SCVMM-bereit Stellungen. SCVMM deaktiviert den Lastenausgleich der Windows Server-VM automatisch, wenn die dynamische Optimierung aktiviert ist.

## <a name="see-also"></a>Weitere Informationen
* [Übersicht über den Lastenausgleich virtueller Computer](vm-load-balancing-overview.md)
* [Failoverclustering](failover-clustering-overview.md)
* [Übersicht über Hyper-V](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
