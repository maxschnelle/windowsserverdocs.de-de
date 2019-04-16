---
title: Planen der Verwendung von vRSS
description: In diesem Thema können Sie Ihre virtuellen Computer und Hyper-V-Host Vorbereiten für die Verwendung von vRSS in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 695e6192-5e84-4ab4-b33e-8ebf6b8f5cbb
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: e6558b00e87721d8ab81c84946a14745c4faa812
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133386"
---
# Planen der Verwendung von vRSS

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In Windows Server 2016 vRSS ist standardmäßig aktiviert, aber Sie Vorbereiten der Umgebung vRSS auf einem virtuellen Computer ordnungsgemäß zulassen müssen \(VM\) oder auf einem Host virtuellen Adapter \(vNIC\). VRSS wurde in Windows Server 2012 R2 standardmäßig deaktiviert.

Wenn Sie die Verwendung von vRSS vorbereiten und möchten, stellen Sie sicher, dass:

- Der physischen Netzwerkadapter ist kompatibel mit virtuellen Computer Warteschlange \(VMQ\) und verfügt über eine Verknüpfung Geschwindigkeit von 10 Gbit/s oder mehr.
- VMQ ist auf der physischen NIC und auf dem Hyper-V Virtual Switch-Port aktiviert.
- Es gibt keine einzelnen Stamm Input\-Ausgabe-Virtualisierung \(SR\-IOV\) für den virtuellen Computer konfiguriert.
- NIC-Teamvorgang ist ordnungsgemäß konfiguriert.
- Der virtuelle Computer verfügt über mehrere logischen Prozessoren \(LPs\).

>[!NOTE]
>vRSS ist auch für alle Host-vNICs standardmäßig aktiviert, die RSS aktiviert haben.

Es folgt zusätzliche Informationen, die Sie benötigen die folgenden Vorbereitungsschritte zur ausführen.
  
1. **Netzwerk-Adapter Kapazität**. Stellen Sie sicher, dass der Netzwerkadapter kompatibel mit virtuellen Computer Warteschlange \(VMQ\) ist und verfügt über eine Verknüpfung Geschwindigkeit von mindestens 10 Gbit/s. Ist der Übertragungsrate weniger als 10 Gbit/s, wird der Hyper-V Virtual Switch VMQ standardmäßig deaktiviert, obwohl es weiterhin VMQ zeigt, wie in den Ergebnissen des Windows PowerShell-Befehl **Get-NetAdapterVmq**aktiviert. Eine Methode, die Sie verwenden können, um sicherzustellen, dass VMQ aktiviert oder deaktiviert ist, ist den Befehl **Get-NetAdapterVmqQueue**verwendet.  Wenn VMQ deaktiviert ist, zeigen die Ergebnisse dieses Befehls, dass es keine QueueID dem virtuellen Computer oder Host virtuelles Netzwerk-Adapter zugewiesen gibt. 
  
2. **VMQ aktivieren**. Stellen Sie sicher, dass VMQ auf dem Hostcomputer aktiviert ist. vRSS funktioniert nicht, wenn der Host VMQ nicht unterstützt. Sie können überprüfen, ob VMQ aktiviert ist, durch Ausführen von **Get-VM-Switch** und suchen den Adapter, den der virtuelle Switch verwendet wird. Als Nächstes führen Sie **Get-NetAdapterVmq** , und stellen Sie sicher, dass der Adapter, in den Ergebnissen angezeigt wird und VMQ aktiviert hat.
  
3. **SR\-IOV fehlen**. Überprüfen Sie, ob eine einzelne Stamm Input\-Ausgabe-Virtualisierung \(SR\-IOV\) virtuelle Funktion \(VF\) Treiber nicht an der VM-Schnittstelle angefügt ist. Sie können dies mithilfe des Befehls **Get-NetAdapterSriov** überprüfen. Wenn ein VF Treiber geladen wird, verwendet RSS die Skalierung Einstellungen aus dieser Treiber anstelle von vRSS konfiguriert. Wenn der Treiber VF RSS nicht unterstützt, ist die vRSS deaktiviert.
  
4. **NIC-Teaming-Konfiguration**. Wenn Sie NIC-Teamvorgang verwenden, ist es wichtig, dass Sie ordnungsgemäß VMQ funktioniert mit den NIC-Teaming-Einstellungen konfigurieren. Ausführliche Informationen zur NIC-Teamvorgang Bereitstellung und Verwaltung finden Sie in der [NIC-Teamvorgang](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming).

5. **Anzahl der LPs**. Stellen Sie sicher, dass der virtuelle Computer mehr als einen logischen Prozessor hat \(LP\). vRSS basiert auf RSS auf dem virtuellen Computer oder auf dem Hyper-V-Host zum Lastenausgleich empfangen des Datenflusses auf mehrere LPs für parallele Verarbeitung. Sie können feststellen, wie viele LPs Ihre virtuellen Computer mit dem Windows PowerShell-Befehl **Get-VMProcessor** auf dem Host hat. Nach dem Ausführen des Befehls können Sie den Anzahl der Eintrag in der Spalte für die Anzahl der LPs beobachten.

Die Host-vNIC hat immer den Zugriff auf alle physischen Prozessoren. um die Host-vNIC zur Verwendung einer bestimmten Anzahl von Prozessoren zu konfigurieren, verwenden Sie die Einstellungen **- BaseProcessorNumber** und **-MaxProcessors** , wenn Sie den **Satz-NetAdapterRss** Windows PowerShell-Befehl ausführen.

---