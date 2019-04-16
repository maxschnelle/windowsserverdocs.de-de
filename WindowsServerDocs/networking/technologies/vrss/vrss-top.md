---
title: Virtual Receive Side Scaling (vRSS)
description: Erfahren Sie, Virtual Receive Side Scaling (vRSS) in Windows Server und wie Sie einen virtuellen Netzwerkadapter zum Laden des Saldo eingehende Netzwerkverkehr über mehrere logische Prozessorkerne auf einem virtuellen Computer zu konfigurieren. Sie können auch mehrere physischen Kernen für einen Host konfigurieren virtuelle Netzwerkkarte (vNIC).
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 9be477b3-f81d-4e84-a6b0-ac4c1ea97715
ms.date: 09/05/2018
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0c1cb11cb8ce69463a31cfa5061290f79d8dda91
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133686"
---
# Virtuelle Side Scaling \(vRSS\) erhalten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie Virtual Receive Side Scaling (vRSS) und wie Sie einen virtuellen Netzwerkadapter zum Laden des Saldo eingehende Netzwerkverkehr über mehrere logische Prozessorkerne auf einem virtuellen Computer zu konfigurieren. Sie können auch vRSS verwenden, um physischen Kernen für einen Host-virtuelle Netzwerkkarte \(vNIC\) zu konfigurieren.

Diese Konfiguration ermöglicht das Laden von einem virtuellen Netzwerkadapter auf mehreren virtuellen Prozessoren auf einem virtuellen Computer verteilt werden \(VM\), sodass weitere Netzwerkdatenverkehr verarbeitet schneller als mit einem einzigen logischen Prozessor möglich den virtuellen Computer.

>[!TIP]
>Können vRSS in virtuellen Computern auf Hyper-V-Hosts, die mehrere Prozessoren, eine einzelne mehrere Core-Prozessor verfügen oder mehr als eine mehrere Core-Prozessoren installiert und für die VM-Verwendung konfiguriert.

vRSS ist mit allen anderen Hyper-V-netzwerktechnologien kompatibel. vRSS ist \(VMQ\) Warteschlange des virtuellen Computers auf dem Hyper-V-Host und RSS auf dem virtuellen Computer oder auf die Host-vNIC abhängig.

Standardmäßig Windows Server ermöglicht vRSS, aber Sie können Sie mithilfe von Windows PowerShell auf einem virtuellen Computer deaktivieren. Weitere Informationen finden Sie unter [Verwalten vRSS](vrss-manage.md) und [Windows PowerShell-Befehlen für RSS- und vRSS](vrss-wps.md).



## Betriebssystem-Kompatibilität

RSS können auf jedem Computer mit mehreren Prozessoren oder Steuerung- oder vRSS auf eine beliebige VM mit mehreren Prozessoren oder Steuerung -, auf denen Windows Server 2016 ausgeführt wird.

Mit mehreren Prozessoren oder Multicore virtuellen Computern, die die folgenden Microsoft-Betriebssysteme ausgeführt werden auch unterstützen vRSS.

- Windows Server 2016
- Windows 10 Pro oder Enterprise
- Windows Server 2012 R2
- Windows 8.1 Pro oder Enterprise
- Windows Server 2012 mit der Windows Server 2012 R2-Integrationskomponenten installiert.
- Windows 8 mit der Windows Server 2012 R2-Integrationskomponenten installiert.

Informationen zur vRSS-Unterstützung für virtuelle Computer FreeBSD oder Linux als Gastbetriebssystem auf Hyper-V finden Sie unter [unterstützte Linux- und FreeBSD virtuellen Computer für Hyper-V unter Windows](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows).
  
## Hardwareanforderungen

Im folgenden werden die hardwareanforderungen für vRSS.
 
- Physischen Netzwerkadaptern müssen Warteschlange des virtuellen Computers \(VMQ\) unterstützen. Wenn VMQ deaktiviert oder nicht unterstützt, ist vRSS für den Hyper-V-Host und alle virtuellen Computer auf dem Host konfiguriert wurde deaktiviert.
- Netzwerkadapter müssen mindestens eine Verknüpfung Geschwindigkeit von 10 Gbit/s ist.
- Hyper-V-Hosts müssen mit mehreren Prozessoren oder mindestens eine Multi\-Core-Prozessor mit vRSS konfiguriert werden.
- Virtuelle Computer \(VMs\) muss konfiguriert werden, um zwei oder mehr logischen Prozessoren verwenden.


## Anwendungsfälle

Die folgenden zwei Anwendungsfälle dargestellt übliche Verwendung von vRSS für Prozessor-Lastenausgleich und Software Load balancing.

### Prozessor-Lastenausgleich
  
Anthony, Netzwerkadministrator, einen neuen Hyper-V-Host mit zwei Netzwerkadapter zum Einrichten von, die einzelnen Stamm ein-/ Ausgabe-Virtualisierung \(SR\-IOV\) unterstützt. Er stellt Windows Server 2016 um einen VM-Dateiserver zu hosten.

Nach der Installation von Hardware und Software, konfiguriert Anthony acht virtuelle Prozessoren verwenden einen virtuellen Computer und 4.096 MB Arbeitsspeicher. Leider verfügt Anthony nicht die Möglichkeit, SR\-IOV einschalten, da seine VMs auf Durchsetzen von Richtlinien über den virtuellen Switch angewiesen, die er mit dem Hyper-V Virtual Switch-Manager erstellt haben. Aus diesem Grund entscheidet Anthony vRSS anstelle SR\-IOV verwenden.

Zunächst weist Anthony vier virtuelle Prozessoren mithilfe von Windows PowerShell für die Verwendung mit vRSS verfügbar sein. Die Verwendung des Dateiservers nach einer Woche schien ziemlich beliebte sein, damit Anthony die Leistung des virtuellen Computers überprüft.  Er ermittelt vollständige Nutzung der vier virtuellen Prozessoren.

Aus diesem Grund entscheidet Anthony des virtuellen Computers für die Verwendung von vRSS Prozessoren hinzu.  Er weist zwei weitere virtuellen Prozessoren auf dem virtuellen Computer, die automatisch für vRSS zu behandeln die Last großen Netzwerk verfügbar sind. Seine bemühungen führen eine bessere Leistung für die VM-Dateiserver, die sechs Prozessoren effizient behandeln die Netzwerk-Datenverkehr geladen.


### Softwarelastenausgleich

Sandra, Netzwerkadministrator Einrichten einer einzigen High-End-VM auf einem der ihre Systeme, die als eine Software Load Balancers fungieren. Er verfügt über alle verfügbaren logischen Prozessoren mit diesem einzelnen virtuellen Computer zugewiesen.

Nach der Installation von Windows Server wird mit seiner vRSS parallel Netzwerkdatenverkehr Verarbeitung auf mehreren logischen Prozessoren auf dem virtuellen Computer. Da Windows Server vRSS ermöglicht, keinen Sandra keine konfigurationsänderungen vornehmen.


## Verwandte Themen

- [Planen der Verwendung von vRSS](vrss-plan.md)
- [Aktivieren Sie vRSS auf einem virtuellen Netzwerkadapter](vrss-enable.md)
- [Verwalten von vRSS](vrss-manage.md)
- [vRSS häufig gestellte Fragen](vrss-faq.md)
- [Windows PowerShell-Befehlen für RSS- und vRSS](vrss-wps.md)

---
