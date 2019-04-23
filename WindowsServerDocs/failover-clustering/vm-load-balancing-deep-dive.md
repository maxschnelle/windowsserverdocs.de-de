---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: VM-Lastenausgleich – ausführliche Informationen
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: f90802a8e77ade0b9f282730e7cb61c73a246018
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853421"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>VM-Lastenausgleich – ausführliche Informationen

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Windows Server 2016 führt die [Lastenausgleichsfunktion von Virtual Machine](vm-load-balancing-overview.md) um die Auslastung von Knoten in einem Failovercluster zu optimieren. In diesem Dokument wird beschrieben, wie Sie zum Konfigurieren und steuern <abbr title="VM">VM</abbr> Lastenausgleich. 

## <a id="heuristics-for-balancing"></a>Die Heuristik für Lastenausgleich
<abbr title="virtuellen Computer">VM</abbr> Lastenausgleich der virtuellen Computer eines Knotens laden basierend auf der folgenden Heuristik ergibt:
1. Aktuelle **arbeitsspeicherauslastung**: Speicher ist der am häufigsten verwendeten ressourceneinschränkung auf einem Hyper-V-host
2. <abbr title="Zentralprozessor">CPU</abbr> **Auslastung** des Knotens, gemittelt über ein 5-Minuten-Fenster: Reduziert einen Knoten im Cluster als überbelegt

## <a id="controlling-aggressiveness-of-balancing"></a>Steuern die Aggressivität für Lastenausgleich
Die Aggressivität der Lastenausgleich basierend auf den Arbeitsspeicher und CPU-Heuristiken kann konfiguriert werden, mit der durch die allgemeine Clustereigenschaft "AutoBalancerLevel". So steuern Sie die Aggressivität, führen Sie Folgendes in PowerShell

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | Aggressivität | Verhalten |
|-------------------|----------------|----------|
| 1 (Standard) | Niedrig | Verschoben Sie werden, wenn der Host mehr als 80 % geladen ist. |
| 2 | Mittel | Verschoben Sie werden, wenn der Host mehr als 70 % geladen ist. |
| 3 | Hoch | Durchschnittliche Anzahl der Knoten und verschieben, wenn der Host über mehr als 5 % überdurchschnittlich ist | 

![Grafik zu von einem PowerShell die Aggressivität der Lastenausgleich konfigurieren](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-abbr-titlevirtual-machinevmabbr-load-balancing"></a>Steuern der <abbr title="VM">VM</abbr> des Lastenausgleichs
<abbr title="virtuellen Computer">VM</abbr> Lastenausgleich ist standardmäßig aktiviert, und Zeitpunkt des Auftretens des Lastenausgleichs kann konfiguriert werden, indem die allgemeine Clustereigenschaft "AutoBalancerMode". So steuern, wenn Knotenfairness den Cluster ausgeglichen:

### <a name="using-failover-cluster-manager"></a>Verwenden Failovercluster-Manager:
1. Mit der rechten Maustaste auf den Namen Ihres Clusters, und wählen Sie die Option "Eigenschaften"  
    ![Grafik zu der Eigenschaft für Cluster mit Failovercluster-Manager auswählen](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  Wählen Sie im Bereich "Lastenausgleich"  
    ![Grafik zu der Auswahl der Option zum Lastenausgleich über Failovercluster-Manager](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>Mithilfe von PowerShell:
Führen Sie Folgendes:
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |Verhalten| 
|:----------------:|:----------:|
|0| Deaktiviert| 
|1| Lastenausgleich auf Knoten zur Teilnahme am| 
|2 (Standard)| Lastenausgleich auf Knoten Join und alle 30 Minuten |

## <a name="abbr-titlevirtual-machinevmabbr-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a><abbr title="Virtuelle Maschine">VM</abbr> Vs den Lastenausgleich. System Center Virtual Machine Manager-dynamische Optimierung
Die Funktion Knoten Ausgewogenheit bietet integrierte-Funktionen, die für Bereitstellungen ohne System Center Virtual Machine Manager vorgesehen ist (<abbr title="System Center Virtual Machine Manager">SCVMM</abbr>). <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> dynamische Optimierung ist die empfohlene Methode für die VM-Last in Ihrem Cluster für Netzwerklastenausgleich <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> Bereitstellungen. <abbr title="System Center Virtual Machine Manager">SCVMM</abbr> deaktiviert automatisch die Windows Server <abbr title="VM">VM</abbr> Lastenausgleich, wenn die dynamische Optimierung aktiviert ist.

## <a name="see-also"></a>Siehe auch
* [VM Netzwerklastenausgleich – Übersicht](vm-load-balancing-overview.md)
* [Failover-Clusterunterstützung](failover-clustering-overview.md)
* [Hyper-V: Übersicht](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
