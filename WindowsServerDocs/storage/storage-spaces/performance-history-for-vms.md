---
title: Leistungsverlauf für virtuelle Computer
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/07/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: f8072ab5fc853248f2eedd26019956ec864a891d
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239217"
---
# Leistungsverlauf für virtuelle Computer

> Gilt für: Windows Server Insider Preview

Untergeordnete in diesem Thema von ["direkte Speicherplätze" Verlauf](performance-history.md) beschreibt ausführlich der Verlauf für virtuelle Computer (VM) erfasst. Leistungsverlauf ist für jede ausgeführt, gruppierten virtuellen Computer verfügbar.

   > [!NOTE]
   > Es kann mehrere Minuten Sammlung für neu erstellte oder umbenannt VMs beginnen.

## Seriennamen und Einheiten

Diese Serie werden für alle berechtigten VM erfasst:

| Serie                            | Einheit             |
|-----------------------------------|------------------|
| `vm.cpu.usage`                    | Prozent          |
| `vm.memory.assigned`              |  Bytes            |
| `vm.memory.available`             |  Bytes            |
| `vm.memory.maximum`               |  Bytes            |
| `vm.memory.minimum`               |  Bytes            |
| `vm.memory.pressure`              | -                |
| `vm.memory.startup`               |  Bytes            |
| `vm.memory.total`                 |  Bytes            |
| `vmnetworkadapter.bandwidth.inbound`  | Bits pro Sekunde |
| `vmnetworkadapter.bandwidth.outbound` | Bits pro Sekunde |
| `vmnetworkadapter.bandwidth.total`    | Bits pro Sekunde |

Darüber hinaus werden alle virtuelle Festplatte (VHD)-Serie, z. B. `vhd.iops.total`, aggregiert werden, für jede virtuelle Festplatte für die VM angefügt.

## Zum Interpretieren


| Serie                            | Beschreibung                                                                                                  |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------|
| `vm.cpu.usage`                    | Prozentsatz der virtuelle Computer wird mit dem Host-Server-Prozessoren verwendet.                                   |
| `vm.memory.assigned`              | Die Menge von Arbeitsspeicher, die mit dem virtuellen Computer zugewiesen.                                                      |
| `vm.memory.available`             | Die Menge des Speichers, der zur Verfügung, die Größe zugewiesen bleibt.                                       |
| `vm.memory.maximum`               | Bei Verwendung von dynamischem Arbeitsspeicher, ist dies die maximale Menge an Arbeitsspeicher, die mit dem virtuellen Computer zugewiesen werden kann. |
| `vm.memory.minimum`               | Bei Verwendung von dynamischem Arbeitsspeicher, ist dies die Mindestmenge des Speichers, der mit dem virtuellen Computer zugewiesen werden kann. |
| `vm.memory.pressure`              | Das Verhältnis von Speicher, die vom virtuellen Computer über den Speicher für den virtuellen Computer reserviert angefordert.            |
| `vm.memory.startup`               | Die Menge der erforderlichen Speicher für den virtuellen Computer zu starten.                                            |
| `vm.memory.total`                 | Gesamter Speicher. |
| `vmnetworkadapter.bandwidth.inbound`  | Die Anzahl der vom virtuellen Computer über dessen virtuellen Netzwerkadapter empfangenen Daten.                        |
| `vmnetworkadapter.bandwidth.outbound` | Die Anzahl der vom virtuellen Computer über dessen virtuellen Netzwerkadapter gesendeten Daten.                            |
| `vmnetworkadapter.bandwidth.total`    | Gesamtanzahl der Daten empfangen oder vom virtuellen Computer über dessen virtuellen Netzwerkadapter gesendet.          |

   > [!NOTE]
   > Leistungsindikatoren werden über das gesamte Intervall nicht gesampelt gemessen. Wenn die VM für 9 Sekunden jedoch Spitzen mit 50 % der Host CPU in der zweiten 10. im Leerlauf ist z. B. seine `vm.cpu.usage` aufgezeichnet als 5 % durchschnittlich während dieses Intervalls 10 Sekunden. Dadurch wird sichergestellt, dessen Leistungsverlauf alle Aktivität erfasst und robust, um Rauschen ist.

## Verwendung in PowerShell

Verwenden Sie das Cmdlet [Get-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) :

```PowerShell
Get-VM <Name> | Get-ClusterPerf
```

   > [!NOTE]
   > Das Cmdlet Get-VM gibt nur virtuellen Computern auf dem lokalen (oder angegeben)-Server nicht über den Cluster zurück.

## Weitere Informationen:

- ["Direkte Speicherplätze" Verlauf](performance-history.md)
