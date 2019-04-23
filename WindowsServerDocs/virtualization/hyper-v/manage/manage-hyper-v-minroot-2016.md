---
title: Minroot
description: Konfigurieren von Host-CPU-Ressourcen-Steuerelementen
keywords: Windows 10, Hyper-V
author: allenma
ms.date: 12/15/2017
ms.topic: article
ms.prod: windows-10-hyperv
ms.service: windows-10-hyperv
ms.assetid: ''
ms.openlocfilehash: e1269c11df32c8ce95cc7455d47d7170e9d0b1c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844331"
---
# <a name="hyper-v-host-cpu-resource-management"></a>Hyper-V-Host-CPU-Ressourcenverwaltung

Hyper-V-Host die Steuerung von CPU-Ressourcen in Windows Server 2016 eingeführt oder höher können Hyper-V-Administratoren, die besser zu verwalten und Zuweisen von Host-Server-CPU-Ressourcen zwischen den "Root", oder die Management-Partition, und die Gast-VMs. Verwenden diese Steuerelemente, können Administratoren eine Teilmenge der Prozessoren eines Hostsystems auf der Stammpartition zuordnen. Dies kann die Arbeit in einem Hyper-V-Host, von den Workloads auf virtuellen Gastcomputern ausgeführt werden, indem Sie auf separaten Teilmengen der Systemprozessoren aufteilen.

Weitere Informationen zu den hardwareanforderungen für Hyper-V-Hosts finden Sie unter [Systemanforderungen für Windows 10 Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements).

## <a name="background"></a>Hintergrund

Vor der Einstellung steuert für Hyper-V-CPU-Ressourcen hosten, ist es hilfreich, um die Grundlagen der Hyper-V-Architektur zu überprüfen.  
Finden Sie eine allgemeine Übersicht, in der [Hyper-V-Architektur](https://docs.microsoft.com/windows-server/administration/performance-tuning/role/hyper-v-server/architecture) Abschnitt.
Dies sind wichtige Konzepte in diesem Artikel:

* Hyper-V erstellt und verwaltet virtuelle Computer-Partitionen, über welche, die Compute Ressourcen zugeordnet und freigegeben werden, von der Hypervisor kontrolliert werden.  Partitionen bieten hohe Isolationsgrenzen zwischen aller virtuellen Gastcomputer sowie zwischen virtuellen Gastcomputern sowie die Root-Partition.

* Das Stammpartition ist selbst ein VM-Partition, obwohl es sich um eindeutige Eigenschaften und viel mehr Berechtigungen als virtuelle Gastcomputer hat.  Das Stammpartition bietet die Management-Dienste, die alle virtuellen Gastcomputern zu steuern, bietet Unterstützung für virtuelle Geräte für Gäste und alle Geräte-e/a für virtuelle Gastcomputer verwaltet.  Microsoft empfiehlt dringend, keine arbeitsauslastungen von Anwendungen in einer Hostpartition ausgeführt werden.

* Jeder virtuelle Prozessor (VP) von der Stammpartition wird zugeordneten 1:1 für einen zugrunde liegenden logischen Prozessor (LP).  Ein Host VP wird immer ausgeführt werden, auf dem gleichen zugrunde liegenden LP – es ist keine Migration von der Stammpartition VPs.  

* Standardmäßig können die auf dem Host VPs ausgeführt LPs auch Gast VPs ausführen.

* Ein Gast VP möglicherweise vom Hypervisor zur Ausführung auf einem beliebigen verfügbaren logischen Prozessor geplant.  Während der Hypervisor-Planer kümmert Ort des temporären Caches, NUMA-Topologie und viele andere Faktoren zu berücksichtigen, bei der Planung einer Gast-VP, konnte auf einem Host LP letztlich die VP geplant werden.

## <a name="the-minimum-root-or-minroot-configuration"></a>Die minimale Stamm oder "Minroot"-Konfiguration

Frühe Versionen von Hyper-V mussten eine Architektur Höchstgrenze von 64 VPs pro Partition.  Dies ist die Stamm- und die Gast-Partitionen angewendet.  Wie Systeme mit mehr als 64 logischen Prozessoren auf High-End-Server angezeigt wurden, sich Hyper-V auch seine Kapazitätsgrenzen der Host zur Unterstützung dieser größere Systeme an einem Punkt, die Unterstützung von eines Hosts mit bis zu 320 LPs entwickelt.  Allerdings unterbrechen die 64 VP pro Partition zu diesem Zeitpunkt präsentiert verschiedene Herausforderungen und Komplexität, die Unterstützung von mehr als 64 VPs pro Partition unerschwinglich eingeführt.  Um dieses Problem zu beheben, beschränkt Hyper-V die Anzahl der VPs übergeben, um die Stammpartition auf 64, selbst wenn die zugrunde liegende Computer viele logische Prozessoren zur Verfügung haben.  Der Hypervisor würde weiterhin alle verfügbaren LPs für die Ausführung von Gast VPs nutzen, aber künstliche Obergrenze die rootpartition auf 64.  Diese Konfiguration als "minimale Root" oder "Minroot"-Konfiguration bezeichnet.  Testen der Leistung bestätigt, dass, auch auf Systemen mit mehr als 64 LPs umfangreiche der Stamm nicht mehr als 64 Stamm VPs ausreichend-Support, um eine große Anzahl von virtuellen Gastcomputern sowie Gast VPs – tatsächlich bereitstellen erforderlich viel weniger als 64 Stamm VPs häufig geeignet war. , natürlich auf die Anzahl und Größe von Gast-VMs, die bestimmte Workloads, die ausgeführt wird usw. abhängig.

Dieses Konzept "Minroot" weiterhin heute verwendet werden.  In der Tat wie auch Windows Server 2016 Hyper-V die Begrenzung der maximalen architektursupport Host LPs 512 LPs erhöht, wird das Stammpartition auf bis zu 320 LPs noch begrenzt.

## <a name="using-minroot-to-constrain-and-isolate-host-compute-resources"></a>Verwenden Minroot und Isolieren der Host Compute-Ressourcen
Mit der hohen Standardschwellenwert von 320 LPs in Windows Server 2016 Hyper-V werden die Minroot-Konfiguration nur auf die sehr größten Server-Systemen verwendet.  Allerdings kann diese Funktion mit einem viel niedriger Schwellenwert der Hyper-V-Host-Administrator konfiguriert und daher genutzt wird, um die Menge der verfügbaren Host CPU-Ressourcen erheblich auf der Stammpartition zu beschränken werden.  Die angegebene Anzahl von Stamm LPs nutzen muss natürlich sorgfältig ausgewählt werden, für die Unterstützung der maximalen Anforderungen von der virtuellen Computer und arbeitsauslastungen, die dem Host zugeordnet.  Allerdings können geeignete Werte für die Anzahl der Hosts-LPs bestimmt über sorgfältig zu bewerten und Überwachung von Workloads für die Produktion und überprüfte in nicht produktiven Umgebungen vor der umfassenden Bereitstellung sein.

## <a name="enabling-and-configuring-minroot"></a>Aktivieren und Konfigurieren von Minroot

Die Minroot-Konfiguration wird über den Hypervisor BCD-Einträge gesteuert. So aktivieren Sie Minroot, über eine Eingabeaufforderung mit Administratorrechten aus:

```
    bcdedit /set hypervisorrootproc n
```
Wobei n die Anzahl der Stamm VPs ist. 

Das System muss neu gestartet werden, und die neue Anzahl von Prozessoren für Stamm bleiben für die Lebensdauer der Start-Betriebssystem.  Die Minroot-Konfiguration kann nicht dynamisch zur Laufzeit geändert werden.

Wenn mehrere NUMA-Knoten vorhanden sind, kann jeder Knoten erhalten `n/NumaNodeCount` Prozessoren.

Beachten Sie, dass mit mehreren NUMA-Knoten, Sie, dass die VM Topologie ist so sicherstellen müssen, dass genügend freier LPs (d. h. LPs ohne Root VPs) vorhanden sind, für jeden NUMA-Knoten zum Ausführen der entsprechenden VM VPs NUMA-Knoten.

## <a name="verifying-the-minroot-configuration"></a>Überprüfen der Minroot-Konfiguration

Sie können die Konfiguration des Hosts Minroot mithilfe des Task-Manager überprüfen, wie unten dargestellt.

![](./media/minroot-taskman.png)

Wenn Minroot aktiv ist, wird die Task-Manager die Anzahl der logischen Prozessoren, die derzeit zugewiesen an den Host zusätzlich zu die Gesamtzahl der logischen Prozessoren im System angezeigt.
 
