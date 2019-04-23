---
title: Planen der Verwendung von vRSS
description: Sie können in diesem Thema verwenden, So bereiten Sie Ihre virtuellen Computer und Hyper-V-Host für die Verwendung von vRSS in Windows Server 2016 vor.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850441"
---
# <a name="plan-the-use-of-vrss"></a>Planen der Verwendung von vRSS

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In Windows Server 2016 ist vRSS standardmäßig aktiviert, jedoch muss die Umgebung zu vRSS auf einem virtuellen Computer ordnungsgemäß vorbereitet \(VM\) oder auf einen virtuellen Host-Adapter \(vNIC\). In Windows Server 2012 R2 wurde vRSS standardmäßig deaktiviert.

Wenn Sie planen und der Verwendung von vRSS vorbereiten, stellen Sie sicher, dass:

- Der physische Netzwerkadapter ist kompatibel mit Virtual Machine Queue \(VMQ\) und eine verbindungsgeschwindigkeit von 10 Gbit/s oder mehr.
- VMQ aktiviert ist, auf die physische NIC und die Hyper\-V Virtual Switch Port
- Es gibt keine Single Root Input\-Output Virtualization \(SR\-IOV\) für den virtuellen Computer konfiguriert.
- NIC-Teamvorgang ist ordnungsgemäß konfiguriert.
- Der virtuelle Computer kann mehrere logische Prozessoren \(LPs\).

>[!NOTE]
>vRSS ist standardmäßig für alle Host-vNICs, die RSS aktiviert haben, ebenfalls aktiviert.

Im folgenden sehen zusätzliche Informationen, dass Sie die folgenden Vorbereitungsschritte zur ausführen müssen.
  
1. **Adapter Netzwerkkapazität**. Stellen Sie sicher, dass der Netzwerkadapter mit Virtual Machine Queue kompatibel ist \(VMQ\) und eine verbindungsgeschwindigkeit von 10 Gbit/s oder mehr. Wenn die verbindungsgeschwindigkeit von weniger als 10 Gbit/s, die Hyper wird\-V-Switches VMQ standardmäßig deaktiviert, auch wenn es weiterhin VMQ zeigt, wie in den Ergebnissen der Windows PowerShell-Befehle aktiviert **Get-NetAdapterVmq**. Eine Methode, können Sie überprüfen, ob VMQ aktiviert oder deaktiviert ist, den Befehl ist **Get-NetAdapterVmqQueue**.  Wenn VMQ deaktiviert ist, zeigen die Ergebnisse dieses Befehls an, dass keine QueueID, die den virtuellen Computer oder Hosts virtuellen Netzwerkadapter zugewiesen ist. 
  
2. **Aktivieren Sie VMQ**. Überprüfen, Sie ob VMQ auf dem Hostcomputer aktiviert ist. vRSS funktioniert nicht, wenn der Host VMQ nicht unterstützt wird. Sie können überprüfen, ob VMQ, indem Sie Ausführung aktiviert ist **Get-VMSwitch** und suchen den Adapter, der der virtuelle Switch verwendet wird. Führen Sie als Nächstes **Get-NetAdapterVmq** aus, und stellen Sie sicher, dass der Adapter in den Ergebnissen angezeigt wird und dass VMQ für den Adapter aktiviert ist.
  
3. **Fehlen von SR\-IOV**. Stellen Sie sicher, dass ein einziger Stammknoten Eingabe\-Output Virtualization \(SR\-IOV\) virtuelle Funktion \(VF\) Treiber nicht an die VM-Netzwerkschnittstelle angefügt ist. Sie können dies überprüfen, mit der **Get-NetAdapterSriov** Befehl. Wenn ein VF-Treiber geladen wird, verwendet RSS die skalierungseinstellungen aus diesem Treiber die dafür konfigurierten vRSS an. Wenn der VF-Treiber keine RSS unterstützt, ist vRSS deaktiviert.
  
4. **NIC-Teaming-Konfiguration**. Wenn Sie NIC-Teamvorgang verwenden, ist es wichtig, dass Sie ordnungsgemäß VMQ für die Arbeit mit den NIC-Teamvorgang-Einstellungen konfigurieren. Ausführliche Informationen zur NIC-Teamvorgang-Bereitstellung und Verwaltung finden Sie unter [NIC-Teamvorgang](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming).

5. **Anzahl der LPs**. Stellen Sie sicher, dass der virtuelle Computer mehr als ein logischen Prozessor kann \(LP\). vRSS basiert auf RSS auf dem virtuellen Computer oder auf dem Hyper-V-Host, den Lastenausgleich für empfangenen Datenverkehr auf mehrere LPs für die parallele Verarbeitung. Sie können beobachten, wie viele Ihr virtueller Computer verfügt, mit dem Windows PowerShell-Befehl LPs **Get-VMProcessor** auf dem Host. Nachdem Sie den Befehl ausführen können Sie die Anzahl der Eintrag in der Spalte für die Anzahl der LPs beobachten.

Die Host-vNIC hat immer Zugriff auf alle von der physischen Prozessoren; um die Host-vNIC zur Verwendung von einer bestimmten Anzahl von Prozessoren zu konfigurieren, verwenden Sie die Einstellungen **- BaseProcessorNumber** und **- MaxProcessors** beim Ausführen der **Set-NetAdapterRss** Windows PowerShell-Befehl.

---