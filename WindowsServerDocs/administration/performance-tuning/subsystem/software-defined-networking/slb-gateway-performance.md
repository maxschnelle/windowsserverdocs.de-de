---
title: In der Software Optimierung der Leistung von SLB-Gateway definierten Netzwerken
description: SLB-Gateway Richtlinien zur leistungsoptimierung für SDN-Netzwerke
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fede7d404ddbb4f465eff435cc340db1907ce9d2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829931"
---
# <a name="slb-gateway-performance-tuning-in-software-defined-networks"></a>In der Software Optimierung der Leistung von SLB-Gateway definierten Netzwerken

Softwarelastenausgleich wird durch eine Kombination aus einem Load Balancer-Manager in die Netzwerkcontroller-VMs, die den virtuellen Hyper-V-Switch und eine Gruppe von VMs mit Laden von Lastenausgleich Multixplexor (Mux) bereitgestellt.

Keine zur weiteren leistungsoptimierung ist erforderlich, um den Netzwerkcontroller konfigurieren oder der Hyper-V-Host für den Lastenausgleich hinausgehen wird beschrieben, in der [Software Defined Networking](index.md) Abschnitt, es sei denn, Sie SR-IOV für verwenden die MUX ab, wie unten beschrieben.

## <a name="slb-mux-vm-configuration"></a>SLB/Mux-VM-Konfiguration

Virtuellen SLB Mux-Maschinen werden in einer Aktiv / Aktiv-Konfiguration bereitgestellt.  Dies bedeutet, dass jede Mux-VM, die bereitgestellt und hinzugefügt, die dem Netzwerkcontroller eingehende Anforderungen verarbeiten kann.  Daher wird der gesamte aggregierte Durchsatz aller Verbindungen nur durch Mux-VM-Anzahl beschränkt, die Sie bereitgestellt haben.  

Eine einzelne Verbindung zu einer virtuellen IP (VIP) werden immer gesendet, die gleichen MUX-Instanz, vorausgesetzt, die Anzahl der MUX konstant bleibt, und daher der Durchsatz kann auf den Durchsatz einer einzelnen Mux-VM beschränkt.  MUX verarbeiten nur eingehenden Datenverkehr, der für eine VIP-Adresse bestimmt ist.  Antwortpaketen wechseln Sie direkt von den virtuellen Computer, die die Antwort auf physischen Switch gesendet wird, der sie sich an den Client weiterleitet.

In einigen Fällen, wenn die Quelle der Anforderung vom SDN-Host stammt, die den gleichen Netzwerkcontroller hinzugefügt wird, die verwaltet die VIP-Adresse, eine weitere Optimierung der eingehenden Pfad für die Anforderung auch erfolgt dadurch können die meisten Pakete direkt über .NET-Remotegrenzen übertragen der der Client auf dem Server, der Mux-VM vollständig umgehen.  Keine zusätzliche Konfiguration ist erforderlich, für die Optimierung erfolgen soll.

Jede SLB/Mux-VM muss gemäß den Richtlinien in SDN VM-Rolle Anforderungen im Abschnitt zur Infrastruktur der Größe angepasst werden die [Planen einer Software Defined Networking-Infrastruktur](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md) Thema.

## <a name="single-root-io-virtualization-sr-iov"></a>Einzelne Root-e/a-Virtualisierung (SR-IOV)

Wenn Sie 40 Ethernet verwenden zu können, wird die Möglichkeit für den virtuellen Switch zum Verarbeiten von Paketen für die Mux-VM der einschränkende Faktor Mux-VM-Durchsatz.  Aus diesem Grund empfiehlt es sich, dass SR-IOV auf dem SLB VMs VM-Netzwerkadapter aktiviert werden, um sicherzustellen, dass der virtuelle Switch nicht zum Engpass wird.

Um SR-IOV aktivieren möchten, müssen Sie es auf dem virtuellen Switch aktivieren, wenn der virtuelle Switch erstellt wird.  In diesem Beispiel erstellen wir einen virtuellen Switch mit dem Switch embedded teaming (SET) und SR-IOV:
``` syntax
    new-vmswitch -Name SDNSwitch -EnableEmbeddedTeaming $true -NetAdapterName @("NIC1", "NIC2") -EnableIOV $true
```
Anschließend muss aktiviert sein, auf dem virtuellen Netzwerkadapter von der SLB/Mux-VM, der den Datenverkehr zu verarbeiten.  In diesem Beispiel wird auf allen Netzwerkkarten SR-IOV aktiviert:
``` syntax
    get-vmnetworkadapter -VMName SLBMUX1 | set-vmnetworkadapter -IovWeight 50
```
