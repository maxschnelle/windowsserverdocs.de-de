---
title: Virtual Receive Side Scaling (vRSS)
description: Erfahren Sie mehr über die virtuelle empfangsseitige Skalierung (vRSS), in Windows Server und zum Laden von Lastenausgleich für eingehenden Netzwerk-Datenverkehr über mehrere logische Prozessorkerne auf einem virtuellen Computer einen virtuellen Netzwerkadapter zu konfigurieren. Sie können auch mehrere physische CPU-Kerne für einen Host konfigurieren virtuelle Netzwerkkarte (vNIC).
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875231"
---
# <a name="virtual-receive-side-scaling-vrss"></a>Virtuelle empfangsseitige Skalierung \(vRSS\)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erfahren Sie, über die virtuelle empfangsseitige Skalierung (vRSS) und wie Sie einen virtuellen Netzwerkadapter zum Laden von Lastenausgleich für eingehenden Netzwerk-Datenverkehr über mehrere logische Prozessorkerne auf einem virtuellen Computer zu konfigurieren. Sie können auch vRSS verwenden, so konfigurieren Sie mehrere physische Kerne für einen Host virtual Network Interface Card \(vNIC\).

Diese Konfiguration mit die Last einem virtuellen Netzwerkadapters auf mehrere virtuelle Prozessoren auf einem virtuellen Computer verteilt werden \(VM\), damit die virtuelle Maschine mehr Netzwerkverkehr schneller als mit einem einzelnen möglich verarbeiten. Logischer Prozessor.

>[!TIP]
>Können Sie vRSS auf virtuellen Computern auf Hyper\-V-Hosts, die mehrere Prozessoren, ein einzelnes mehrere Core-Prozessor oder mehrere Mehrkernprozessoren installiert und konfiguriert Sie für die Verwendung des virtuellen Computers.

vRSS ist kompatibel mit allen anderen Hyper\-V netzwerktechnologien. vRSS ist abhängig von der Warteschlange für virtuelle Maschinen \(VMQ\) auf den virtuellen Hyper\-V-Host und RSS auf dem virtuellen Computer oder auf die Host-vNIC.

Standardmäßig Windows Server ermöglicht vRSS, aber Sie können Sie mithilfe von Windows PowerShell auf einem virtuellen Computer deaktivieren. Weitere Informationen finden Sie unter [verwalten vRSS](vrss-manage.md) und [Windows PowerShell-Befehle für RSS und vRSS](vrss-wps.md).



## <a name="operating-system-compatibility"></a>Betriebssystemkompatibilität

Sie können RSS verwenden, auf einem Multiprozessor- oder multicore-Computer- oder die vRSS auf jeder Multiprozessor- oder multicore-VM -, auf denen Windows Server 2016 ausgeführt wird.

Unterstützung von Multiprozessor- oder Multicore-VMs, die folgenden Microsoft-Betriebssysteme ausgeführt werden, auch vRSS.

- Windows Server 2016
- Windows 10 Pro oder Enterprise
- Windows Server 2012 R2
- Windows 8.1 Pro oder Enterprise
- Windows Server 2012 mit installierten Komponenten des Windows Server 2012 R2.
- Windows 8 mit Komponenten des Windows Server 2012 R2 installiert.

Weitere Informationen zu vRSS-Unterstützung für virtuelle Maschinen von FreeBSD oder Linux als Gastbetriebssystem auf Hyper-V, finden Sie unter [unterstützt Linux und FreeBSD-VMs für Hyper-V unter Windows](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows).
  
## <a name="hardware-requirements"></a>Hardwareanforderungen

Es folgen die hardwareanforderungen für vRSS.
 
- Physische Netzwerkadapter müssen die Warteschlange für virtuelle Computer unterstützen \(VMQ\). Wenn VMQ deaktiviert ist, oder nicht unterstützt, ist vRSS deaktiviert, für die Hyper\-V-Host und alle virtuellen Computer, auf dem Host konfiguriert.
- Netzwerkadapter müssen mindestens eine verbindungsgeschwindigkeit von 10 Gbit/s haben.
- Hyper\-V-Hosts müssen konfiguriert werden, mit mehreren Prozessoren oder mindestens mit mehreren\-core-Prozessor vRSS verwenden.
- Virtuelle Computer \(VMs\) muss zur Verwendung von zwei oder mehreren logischer Prozessoren konfiguriert werden.


## <a name="use-case-scenarios"></a>Anwendungsszenarien

Die folgenden zwei Szenarien zu Anwendungsfällen darzustellen übliche Nutzung vRSS prozessorlastenausgleich und softwarelastenausgleich.

### <a name="processor-load-balancing"></a>Prozessorlastenausgleich
  
Michael, ein Netzwerkadministrator, Einrichten von einen neuen Hyper-V-Host mit zwei Netzwerkadapter, Single Root Input-Output Vortualization unterstützt \(SR\-IOV\). Er stellt Windows Server 2016, um einen Dateiserver für die virtuellen Computer zu hosten.

Nach der Installation von Hardware und Software, konfiguriert Michael an einen virtuellen Computer mit acht virtuellen Prozessoren und 4096 MB Arbeitsspeicher. Anthony haben leider nicht die Möglichkeit, SR einschalten\-IOV da seiner VMs auf dem richtlinienerzwingung über den virtuellen Switch basieren er, mit Hyper erstellt\-V Virtual Switch-Manager. Aus diesem Grund entscheidet, Anthony mit vRSS statt SR\-IOV.

Zunächst weist Michael vier virtuelle Prozessoren mithilfe von Windows PowerShell für die Verwendung mit vRSS verfügbar sein. Die Verwendung des Dateiservers nach einer Woche erschien sehr beliebt ist, damit Michael die Leistung des virtuellen Computers überprüft.  Er stellt die vollständige Nutzung der vier virtuellen Prozessoren.

Aus diesem Grund entscheidet, Anthony Prozessoren mit dem virtuellen Computer für die Verwendung von vRSS hinzufügen.  Er weist zwei weitere virtuellen Prozessoren der VM, die vRSS können von der hohen Netzwerklast behandelt automatisch zur Verfügung stehen. Seine bemühungen führen eine bessere Leistung für den Dateiserver des virtuellen Computers mit den sechs Prozessoren effiziente Behandlung der Datenverkehrslast im Netzwerk.


### <a name="software-load-balancing"></a>Softwarelastenausgleich

Stefan, ein Netzwerkadministrator, ist eine einzelne Hochleistungs-VM auf eines seiner Systeme einrichten, die als eines Software Load Balancer fungiert. Er verfügt über alle verfügbaren logischen Prozessoren auf diese einzelnen virtuellen Computer zugewiesen.

Nach der Installation von Windows Server, verwendet sie vRSS auf um parallele Verarbeitung auf mehreren logischen Prozessoren auf dem virtuellen Computer Netzwerkdatenverkehr zu erhalten. Da Windows Server vRSS ermöglicht, keine Stefan konfigurationsänderungen vornehmen.


## <a name="related-topics"></a>Verwandte Themen

- [Planen der Verwendung von vRSS](vrss-plan.md)
- [Aktivieren Sie vRSS auf einem virtuellen Netzwerkadapter](vrss-enable.md)
- [Verwalten Sie vRSS](vrss-manage.md)
- [vRSS häufig gestellte Fragen](vrss-faq.md)
- [Windows PowerShell-Befehle für RSS und vRSS](vrss-wps.md)

---
