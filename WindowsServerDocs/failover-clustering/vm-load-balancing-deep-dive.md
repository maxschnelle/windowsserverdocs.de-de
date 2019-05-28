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
ms.openlocfilehash: 50213cf47c2c59f1775ae704e82ed51794715ac0
ms.sourcegitcommit: 276a480b470482cba4682caa3df4cd07ba5b7801
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66198549"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>VM-Lastenausgleich – ausführliche Informationen

> Gilt für: Windows Server 2019, Windows Server 2016

Die [Lastenausgleichsfunktion von Virtual Machine](vm-load-balancing-overview.md) optimiert die Auslastung von Knoten in einem Failovercluster. Dieses Dokument beschreibt, wie Sie zum Konfigurieren und steuern die VM-Lastenausgleich. 

## <a id="heuristics-for-balancing"></a>Die Heuristik für Lastenausgleich
VM Load Balancing wertet eines Knotens laden, die auf der folgenden Heuristik basiert:
1. Aktuelle **arbeitsspeicherauslastung**: Speicher ist der am häufigsten verwendeten ressourceneinschränkung auf einem Hyper-V-host
2. CPU **Auslastung** des Knotens, gemittelt über ein 5-Minuten-Fenster: Reduziert einen Knoten im Cluster als überbelegt

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

## <a name="controlling-vm-load-balancing"></a>Steuern des VM-Lastenausgleich
Lastenausgleich der VM ist standardmäßig aktiviert, und Zeitpunkt des Auftretens des Lastenausgleichs kann konfiguriert werden, indem die allgemeine Clustereigenschaft "AutoBalancerMode". So steuern, wenn Knotenfairness den Cluster ausgeglichen:

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
|0| Disabled| 
|1| Lastenausgleich auf Knoten zur Teilnahme am| 
|2 (Standard)| Lastenausgleich auf Knoten Join und alle 30 Minuten |

## <a name="vm-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a>VM-Lastenausgleich im Vergleich zu System Center Virtual Machine Manager-dynamische Optimierung
Die Funktion Knoten Ausgewogenheit bietet integrierte, die für Bereitstellungen ohne System Center Virtual Machine Manager (SCVMM) ausgerichtet ist. Dynamische Optimierung von SCVMM ist die empfohlene Methode zur Lastenausgleichs für virtuelle Computer in Ihrem Cluster für SCVMM-Bereitstellungen. SCVMM deaktiviert automatisch die Windows Server-VM den Lastenausgleich bei der dynamischen Optimierung aktiviert ist.

## <a name="see-also"></a>Siehe auch
* [VM Netzwerklastenausgleich – Übersicht](vm-load-balancing-overview.md)
* [Failoverclustering](failover-clustering-overview.md)
* [Hyper-V: Übersicht](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
