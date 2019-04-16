---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: VM-Lastenausgleich tiefer gehende
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 6ee092a2e51e2181a2203bc263377c4a8ec60246
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>VM-Lastenausgleich tiefer gehende

> Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Windows Server 2016 führt die [VM-Lastenausgleich](vm-load-balancing-overview.md) zur Optimierung der Auslastung der Knoten in einem Failovercluster. In diesem Dokument wird beschrieben, wie zum Konfigurieren und steuern <abbr title="virtuellen Computer">VM</abbr> des Lastenausgleichs. 

## <a id="heuristics-for-balancing"></a>Mithilfe von Heuristik für Lastenausgleich
<abbr title="Virtuelle Maschine">VM</abbr> VM Netzwerklastenausgleich eines Knotens laden basierend auf der folgenden Heuristik bewertet:
1. Aktuelle **speicherüberlastung**: Arbeitsspeicher ist die am häufigsten verwendeten Ressourcen Einschränkung auf einem Hyper-V-Host
2. <abbr title="Zentralprozessor">CPU</abbr> **Auslastung** des Knotens, gemittelt über einen 5-minütigen Zeitfenster: einen Knoten im Cluster zunehmend überbelegt reduziert

## <a id="controlling-aggressiveness-of-balancing"></a>Steuern der Aggressivität des Lastenausgleichs
Der Aggressivität der Netzwerklastenausgleich basierend auf den Arbeitsspeicher und CPU-Heuristik kann konfiguriert werden, mit der durch die allgemeine Clustereigenschaft 'AutoBalancerLevel'. So steuern Sie die Aggressivität den folgenden PowerShell ausführen:

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | Aggressivität | Verhalten |
|-------------------|----------------|----------|
| 1 (Standard) | Niedrig | Verschoben Sie werden, wenn der Host mehr als 80 % geladen ist. |
| 2 | Mittel | Verschoben Sie werden, wenn der Host über 70 % geladen ist. |
| 3 | Hoch | Verschoben Sie werden, wenn der Host mehr als 60 % geladen ist. | 

![Grafik in einem PowerShell der Aggressivität der Netzwerklastenausgleich zu konfigurieren](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-abbr-titlevirtual-machinevmabbr-load-balancing"></a>Steuern der <abbr title="virtuellen Computer">VM</abbr> des Lastenausgleichs
<abbr title="Virtuelle Maschine">VM</abbr> Netzwerklastenausgleich ist standardmäßig aktiviert und tritt der Lastenausgleich durch die allgemeine Clustereigenschaft "AutoBalancerMode" konfiguriert werden kann. Steuern, wann Beträge Fairness Knoten des Clusters:

### <a name="using-failover-cluster-manager"></a>Verwenden von Failovercluster-Manager:
1. Mit der rechten Maustaste auf der Clustername, und wählen Sie die Option "Eigenschaften"  
    ![Grafik der Eigenschaft für Cluster mit Failovercluster-Manager auswählen](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  Wählen Sie im Bereich "Lastenausgleich"  
    ![Grafik der Auswahl der Option Lastenausgleich über Failovercluster-Manager](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>Mithilfe von PowerShell:
Führen Sie folgenden Befehl:
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |Verhalten| 
|:----------------:|:----------:|
|0| Deaktiviert| 
|1| Lädt den Lastenausgleich auf Knoten beitreten| 
|2 (Standard)| Lädt den Lastenausgleich auf Knoten beitreten und alle 30 Minuten |

## <a name="abbr-titlevirtual-machinevmabbr-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a><abbr title="Virtuelle Maschine">VM</abbr> des Lastenausgleichs im Vergleich zu System Center Virtual Machine Manager dynamische Optimierung
Die Knoten Fairness Funktion bietet mitgelieferte, die zur Bereitstellung ohne System Center Virtual Machine Manager bestimmt ist (<abbr title="System Center Virtual Machine Manager">SCVMM</abbr>). <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> dynamische Optimierung ist der empfohlene Mechanismus für die Last der virtuellen Computer im Cluster für <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> Bereitstellungen. <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> automatisch deaktiviert, die Windows Server <abbr title="virtuellen Computer">VM</abbr> Lastenausgleich, wenn die dynamische Optimierung aktiviert ist.

## <a name="see-also"></a>Siehe auch
* [Virtuelle Maschine Netzwerklastenausgleich: Übersicht](vm-load-balancing-overview.md)
* [Failover-Clusterunterstützung](failover-clustering-overview.md)
* [Hyper-V (Übersicht)](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
