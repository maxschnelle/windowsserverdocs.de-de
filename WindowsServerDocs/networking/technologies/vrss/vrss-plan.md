---
title: Planen der Verwendung von vrss
description: Sie können dieses Thema verwenden, um den virtuellen Computer und den Hyper-V-Host für die Verwendung von vrss in Windows Server 2016 vorzubereiten.
ms.topic: article
ms.assetid: 695e6192-5e84-4ab4-b33e-8ebf6b8f5cbb
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/04/2018
ms.openlocfilehash: 9457a1763f92e7f2571040c1c6e8e323d96ee598
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951939"
---
# <a name="plan-the-use-of-vrss"></a>Planen der Verwendung von vrss

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In Windows Server 2016 ist vrss standardmäßig aktiviert. Sie müssen jedoch Ihre Umgebung vorbereiten, damit vrss ordnungsgemäß auf einem virtuellen Computer mit einem virtuellen Computer \( \) oder auf einer vNIC des virtuellen Host Adapters funktioniert \( \) . In Windows Server 2012 R2 war vrss standardmäßig deaktiviert.

Wenn Sie die Verwendung von vrss planen und vorbereiten, stellen Sie Folgendes sicher:

- Der physische Netzwerkadapter ist mit Warteschlange für virtuelle Computer \( VMQ kompatibel \) und weist eine Verbindungsgeschwindigkeit von 10 Gbit/s oder mehr auf.
- VMQ ist auf der physischen NIC und dem virtuellen Hyper- \- V-Switchport aktiviert.
- Es ist keine Single root input \- Output Virtualization \( SR \- IOV \) für den virtuellen Computer konfiguriert.
- Der NIC-Team Vorgang ist ordnungsgemäß konfiguriert.
- Der virtuelle Computer verfügt über mehrere logische Prozessoren \( LPs \) .

>[!NOTE]
>vrss ist standardmäßig auch für alle Host-vNICs aktiviert, für die RSS aktiviert ist.

Im folgenden finden Sie weitere Informationen, die Sie benötigen, um diese Vorbereitungsschritte abzuschließen.

1. **Kapazität des Netzwerkadapters**. Vergewissern Sie sich, dass der Netzwerkadapter mit Warteschlange für virtuelle Computer \( VMQ kompatibel ist \) und eine Verbindungsgeschwindigkeit von 10 Gbit/s oder mehr aufweist. Wenn die Verbindungsgeschwindigkeit weniger als 10 Gbit/s beträgt, \- deaktiviert der virtuelle Hyper-V-Switch standardmäßig VMQ, obwohl VMQ weiterhin in den Ergebnissen des Windows PowerShell-Befehls **Get-netadaptervmq**als aktiviert angezeigt wird. Eine Methode, die Sie verwenden können, um zu überprüfen, ob VMQ aktiviert oder deaktiviert ist, besteht darin, den Befehl **Get-netadaptervmqqueue**zu verwenden.  Wenn VMQ deaktiviert ist, zeigen die Ergebnisse dieses Befehls, dass dem virtuellen Computer oder dem virtuellen Netzwerkadapter des Hosts keine QueueId zugewiesen ist.

2. **Aktivieren Sie VMQ**. Überprüfen, Sie ob VMQ auf dem Hostcomputer aktiviert ist. vrss funktioniert nicht, wenn VMQ vom Host nicht unterstützt wird. Sie können überprüfen, ob VMQ aktiviert ist, indem Sie **Get-VMSwitch** ausführen und den Adapter suchen, der vom virtuellen Switch verwendet wird. Führen Sie als Nächstes **Get-NetAdapterVmq** aus, und stellen Sie sicher, dass der Adapter in den Ergebnissen angezeigt wird und dass VMQ für den Adapter aktiviert ist.

3. **Abwesenheit von SR \- IOV**. Vergewissern Sie sich, dass \- \( \- \) der virtuelle Computer \( \) mit der VM-Netzwerkschnittstelle nicht an die VM-Netzwerkschnittstelle angefügt ist. Dies können Sie mit dem Befehl **Get-netadaptersriov** überprüfen. Wenn ein VF-Treiber geladen wird, verwendet RSS die Skalierungs Einstellungen aus diesem Treiber anstelle der von vrss konfigurierten. Wenn der VF-Treiber RSS nicht unterstützt, wird vrss deaktiviert.

4. **Konfiguration des NIC**-Team Vorgangs. Wenn Sie NIC-Team Vorgänge verwenden, ist es wichtig, dass Sie VMQ ordnungsgemäß konfigurieren, damit Sie mit den NIC-Team Vorgangs Einstellungen arbeiten können. Ausführliche Informationen zur Bereitstellung und Verwaltung von NIC-Teaming finden Sie unter [NIC](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)-Team Vorgang.

5. **Anzahl der LPs**. Vergewissern Sie sich, dass der virtuelle Computer über mehr als eine logische Prozessor- \( LP verfügt \) . vrss basiert auf RSS auf dem virtuellen Computer oder auf dem Hyper-V-Host, um einen Lastenausgleich für den empfangenen Datenverkehr auf mehrere LPs zur parallelen Verarbeitung durchzusetzen. Sie können die Anzahl der LPs Ihres virtuellen Computers beobachten, indem Sie den Windows PowerShell-Befehl **Get-vmprocessor** auf dem Host ausführen. Nachdem Sie den Befehl ausgeführt haben, können Sie den Eintrag für die Anzahl der-Spalten in der Anzahl der LPs beobachten.

Die Host-vNIC hat immer Zugriff auf alle physischen Prozessoren. um die Host-vNIC für die Verwendung einer bestimmten Anzahl von Prozessoren zu konfigurieren, verwenden Sie die Einstellungen **-baseprocessornumber** und **-maxprocessor** , wenn Sie den Windows PowerShell-Befehl **Set-netadapterrss** ausführen.

---