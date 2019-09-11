---
title: Minroot
description: Konfigurieren von Host-CPU-Ressourcen Steuerungen
keywords: Windows 10, Hyper-V
author: allenma
ms.date: 12/15/2017
ms.topic: article
ms.prod: windows-10-hyperv
ms.service: windows-10-hyperv
ms.assetid: ''
ms.openlocfilehash: 92de899a39aed05e2f598fcb3aae3fbae3f1cb67
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872041"
---
# <a name="hyper-v-host-cpu-resource-management"></a>Verwaltung von CPU-Ressourcen für Hyper-V-Hosts

Die in Windows Server 2016 oder höher eingeführten CPU-Ressourcen Steuerungen für Hyper-v-Hosts ermöglichen Hyper-v-Administratoren, die CPU-Ressourcen des Host Servers zwischen dem Stammverzeichnis, der Verwaltungs Partition und den Gast-VMS besser zu verwalten und zuzuordnen. Mithilfe dieser Steuerelemente können Administratoren eine Teilmenge der Prozessoren eines Host Systems für die Stamm Partition festlegen. Dies kann die von einem Hyper-V-Host ausgeführte Arbeit von den Arbeits Auslastungen, die auf virtuellen Gast Computern ausgeführt werden, trennen, indem Sie Sie in separaten Teilmengen der System Prozessoren ausführen.

Ausführliche Informationen zu Hardware für Hyper-v-Hosts finden Sie unter [System Anforderungen für Windows 10 Hyper-v](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements).

## <a name="background"></a>Hintergrund

Vor dem Festlegen von Steuerelementen für die CPU-Ressourcen von Hyper-v-Hosts ist es hilfreich, die Grundlagen der Hyper-v-Architektur zu überprüfen.  
Eine allgemeine Zusammenfassung finden Sie im Abschnitt " [Hyper-V-Architektur](https://docs.microsoft.com/windows-server/administration/performance-tuning/role/hyper-v-server/architecture) ".
Dies sind wichtige Konzepte für diesen Artikel:

* Hyper-V erstellt und verwaltet virtuelle Computer Partitionen, für die Compute-Ressourcen zugeordnet und freigegeben werden, unter Kontrolle über den Hypervisor.  Partitionen bieten starke Isolations Grenzen zwischen allen virtuellen Gast Computern und zwischen Gast-VMS und der Stamm Partition.

* Die Stamm Partition ist selbst eine virtuelle Computer Partition, obwohl Sie über eindeutige Eigenschaften und weitaus größere Berechtigungen als virtuelle Gastcomputer verfügt.  Die Stamm Partition stellt die Verwaltungsdienste zur Verfügung, die alle virtuellen Gastcomputer steuern, Unterstützung für virtuelle Geräte für Gäste bereitstellen und alle Geräte-e/a für virtuelle Gast Maschinen verwalten.  Microsoft empfiehlt dringend, keine anwendungsworkloads in einer Host Partition auszuführen.

* Jeder virtuelle Prozessor (VP) der Stamm Partition ist 1:1 einem zugrunde liegenden logischen Prozessor (LP) zugeordnet.  Ein Host-VP wird immer auf der gleichen zugrunde liegenden LP ausgeführt – es gibt keine Migration der VPS der Stamm Partition.  

* Standardmäßig können die LPs, auf denen Host-VPS ausgeführt wird, auch Gast-VPS ausführen.

* Ein Gast-VP kann vom Hypervisor geplant werden, damit er auf allen verfügbaren logischen Prozessoren ausgeführt werden kann.  Der Hypervisor-Planer kümmert sich um die zeitliche Cache Lokalität, die NUMA-Topologie und viele andere Faktoren beim Planen eines Gast-VP-Diensts. letztlich könnte der VP auf jeder Host-LP geplant werden.

## <a name="the-minimum-root-or-minroot-configuration"></a>Die minimale Stamm-oder minroot-Konfiguration

Für frühe Versionen von Hyper-V gab es eine Obergrenze von 64 VPS pro Partition.  Dies gilt sowohl für die Stamm-als auch für die Gast Partitionen.  Da Systeme mit mehr als 64 logischen Prozessoren auf High-End-Servern auftraten, hat Hyper-V auch seine Host Skalierungs Grenzwerte entwickelt, um diese größeren Systeme zu unterstützen. zu einem Punkt, der einen Host mit bis zu 320 LPS unterstützt.  Allerdings hat das Limit von 64 VP pro Partition zu diesem Zeitpunkt eine Reihe von Herausforderungen und die Komplexität eingeführt, die die Unterstützung von mehr als 64 VPS pro Partition beeinträchtigen.  Um dies zu beheben, beschränkte Hyper-V die Anzahl der VPS, die auf die Stamm Partition festgestellt wurden, auf 64, auch wenn auf dem zugrunde liegenden Computer Viele logische Prozessoren verfügbar waren.  Der Hypervisor verwendet weiterhin alle verfügbaren LPs für das Ausführen von Gast-VPS, aber die Stamm Partition wird bei 64 künstlich gekappt.  Diese Konfiguration wurde als "minimale Stamm"-oder "minroot"-Konfiguration bezeichnet.  Leistungstests haben bestätigt, dass der Stamm selbst bei großen Systemen mit mehr als 64 LPs nicht mehr als 64 Stamm-VPS benötigt, um eine ausreichende Unterstützung für eine große Anzahl von Gast-VMS und Gast-VPS zu bieten – tatsächlich waren viel weniger als 64 Stamm-VPS häufig ausreichend. , abhängig von der Anzahl und Größe der Gast-VMS, der ausgeführter Workloads usw.

Dieses "minroot"-Konzept wird heute weiterhin verwendet.  Auch wenn Windows Server 2016 Hyper-V seine maximale Architekturunterstützung für Host LPs auf 512 LPs erweitert hat, ist die Stamm Partition weiterhin auf maximal 320 LPs beschränkt.

## <a name="using-minroot-to-constrain-and-isolate-host-compute-resources"></a>Verwenden von minroot zum einschränken und Isolieren von hostcomputeressourcen
Mit dem hohen Standard Schwellenwert von 320 LPs in Windows Server 2016 Hyper-V wird die minroot-Konfiguration nur auf den größten Server Systemen verwendet.  Diese Funktion kann jedoch vom Hyper-V-Host Administrator auf einen wesentlich niedrigeren Schwellenwert festgelegt werden. Dadurch wird die Menge der verfügbaren Host-CPU-Ressourcen für die Stamm Partition stark eingeschränkt.  Die genaue Anzahl der zu verwendenden Stamm-LPs muss natürlich sorgfältig ausgewählt werden, um die maximalen Anforderungen der virtuellen Computer und Arbeits Auslastungen zu unterstützen, die dem Host zugeordnet sind.  Allerdings können angemessene Werte für die Anzahl der Host LPs durch sorgfältige Bewertung und Überwachung von produktionsworkloads ermittelt und in nicht produktiven Umgebungen vor umfassender Bereitstellung überprüft werden.

## <a name="enabling-and-configuring-minroot"></a>Aktivieren und Konfigurieren von minroot

Die minroot-Konfiguration wird über Hypervisor-BCD-Einträge gesteuert. So aktivieren Sie minroot von einer cmd-Eingabeaufforderung mit Administratorrechten:

```
    bcdedit /set hypervisorrootproc n
```
Dabei steht n für die Anzahl der Stamm-VPS. 

Das System muss neu gestartet werden, und die neue Anzahl der Stamm Prozessoren bleibt für die Lebensdauer des Betriebssystem Starts erhalten.  Die minroot-Konfiguration kann zur Laufzeit nicht dynamisch geändert werden.

Wenn mehrere NUMA-Knoten vorhanden sind, erhält jeder Knoten `n/NumaNodeCount` Prozessoren.

Beachten Sie, dass Sie bei mehreren NUMA-Knoten sicherstellen müssen, dass die Topologie der VM so hoch ist, dass auf jedem NUMA-Knoten ausreichend freie LPs (d.h. LPs ohne Stamm-VPS) vorhanden sind, um die entsprechenden NUMA-Knoten-VPS des virtuellen Computers auszuführen.

## <a name="verifying-the-minroot-configuration"></a>Die minroot-Konfiguration wird überprüft.

Sie können die minroot-Konfiguration des Hosts mit dem Task-Manager überprüfen, wie unten gezeigt.

![](./media/minroot-taskman.png)

Wenn minroot aktiv ist, zeigt der Task-Manager zusätzlich zur Gesamtanzahl der logischen Prozessoren im System die Anzahl der logischen Prozessoren an, die dem Host derzeit zugewiesen sind.
 
