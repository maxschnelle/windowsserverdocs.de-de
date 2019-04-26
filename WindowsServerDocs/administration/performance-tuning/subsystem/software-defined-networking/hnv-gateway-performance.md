---
title: In der Software Optimierung der Leistung von hnv-Gateway definierten Netzwerken
description: Hnv-Gateway Richtlinien zur leistungsoptimierung in Softwaredefinierten Netzwerken
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 217428b84a00b2e2231a15cb3878d0abcec1d9ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827321"
---
# <a name="hnv-gateway-performance-tuning-in-software-defined-networks"></a>In der Software Optimierung der Leistung von hnv-Gateway definierten Netzwerken

Dieses Thema enthält die Hardwarespezifikationen und konfigurationsempfehlungen für Server, auf denen Hyper-V ausführen und Hosten von Windows Server-Gateway-VMs, neben Konfigurationsparametern für Windows Server-Gateway-VMs (VMs) . Um optimale Leistung von Windows Server-Gateway-VMs zu extrahieren, wird davon ausgegangen, dass diese Richtlinien beachtet werden.
Die folgenden Abschnitte enthalten Hardware- und Konfigurationsanforderungen für die Bereitstellung von Windows Server-Gateway.
1. Hardwareempfehlungen für Hyper-V
2. Hyper-V-Hostkonfiguration
3. Windows Server-Gateway-VM-Konfiguration

## <a name="hyper-v-hardware-recommendations"></a>Hardwareempfehlungen für Hyper-V

Es folgt die empfohlene Mindesthardwarekonfiguration für jeden Server, auf denen Windows Server 2016 und Hyper-V ausgeführt wird.

| Serverkomponente               | Spezifikation                                                                                                                                                                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Zentralprozessor (CPU)  | Non-Uniform Memory Architecture (NUMA)-Knoten: 2 <br> Wenn es mehrere Windows Server Gateway-VMs auf dem Host für eine optimale Leistung sind müssen jeden Gateway-VM vollen Zugriff auf einem NUMA-Knoten. Und es muss sich von den NUMA-Knoten, die von dem physischen Host-Adapter verwendet. |
| Kerne pro NUMA-Knoten            | 2                                                                                                                                                                                                                                                                               |
| Hyper-Threading                | Deaktiviert. Hyperthreading verbessert die Leistung von Windows Server-Gateway nicht.                                                                                                                                                                                           |
| Arbeitsspeicher (RAM)     | 48 GB                                                                                                                                                                                                                                                                           |
| Netzwerkschnittstellenkarten (NICs) | Zwei 10-GB-Netzwerkkarten, die Gateway-Leistung hängt die Rate der Zeile ab. Wenn die Rate der Zeile weniger als 10 Gbit/s ist, werden die Gateway-Tunnel Durchsatzzahlen auch durch den gleichen Faktor ausfallen.                                                                                          |

Stellen Sie sicher, dass die Anzahl virtueller Prozessoren, die einer Windows Server-Gateway-VM zugewiesen sind, die Anzahl von Prozessoren auf dem NUMA-Knoten nicht übersteigt. Bei einem NUMA-Knoten mit acht Kernen sollten z. B. maximal acht virtuelle Prozessoren verwendet werden. Für eine optimale Leistung sollte 8 sein. Führen Sie das folgende Windows PowerShell-Skript auf jedem Hyper-V-Host aus, um die Anzahl von NUMA-Knoten und die Anzahl von Kernen pro NUMA-Knoten zu ermitteln:

```PowerShell
$nodes = [object[]] $(gwmi –Namespace root\virtualization\v2 -Class MSVM_NumaNode)
$cores = ($nodes | Measure-Object NumberOfProcessorCores -sum).Sum
$lps = ($nodes | Measure-Object NumberOfLogicalProcessors -sum).Sum


Write-Host "Number of NUMA Nodes: ", $nodes.count
Write-Host ("Total Number of Cores: ", $cores)
Write-Host ("Total Number of Logical Processors: ", $lps)
```

>[!Important]
> Die Zuordnung von virtuellen Prozessoren zu NUMA-Knoten kann sich negativ auf die Leistung von Windows Server-Gateway auswirken. Die Ausführung mehrerer VMs, denen jeweils Prozessoren von einem NUMA-Knoten zugewiesen sind, bietet wahrscheinlich eine höhere Gesamtleistung als eine einzige VM, der alle virtuellen Prozessoren zugewiesen sind.

Eine Gateway-VM mit acht virtuellen Prozessoren und mindestens 8GB RAM wird bei der Auswahl der Anzahl der Gateway-VMs empfohlen, um auf jedem Hyper-V-Host zu installieren, wenn jeder NUMA-Knoten über acht Kerne verfügt. In diesem Fall dient einem NUMA-Knoten auf den Hostcomputer.

## <a name="hyper-v-host-configuration"></a>Hyper-V-Hostkonfiguration

Folgendes ist die empfohlene Konfiguration für jeden Server mit Windows Server 2016 und Hyper-V und deren arbeitsauslastung Windows Server-Gateway-VMs ausgeführt wird. Die Konfigurationsanweisungen beinhalten Windows PowerShell-Befehlsbeispiele. Die Beispiele enthalten Platzhalter für die tatsächlichen Werte, die Sie beim Ausführen der Befehle in Ihrer Umgebung angeben müssen. Platzhalter für den Netzwerkadapternamen sind z. B. "NIC1? und "NIC2.? Wenn Sie Befehle mit diesen Platzhaltern ausführen, verwenden Sie anstelle der Platzhalter die tatsächlichen Namen der Netzwerkadapter auf Ihren Servern. Andernfalls schlagen die Befehle fehl.

>[!Note]
> Zum Ausführen der folgenden Windows PowerShell-Befehle müssen Sie ein Mitglied der lokalen Gruppe %%amp;quot;Administratoren%%amp;quot; sein.

| Konfigurationselement                          | Windows Powershell-Konfiguration                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Switch Embedded Teaming                     | Bei der Erstellung eines Vswitch mit mehreren Netzwerkadaptern aktiviert Switch embedded teaming für diese Adapter automatisch. <br> ```New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"``` <br> Herkömmliche über LBFO-Teamvorgang ist mit SDN in Windows Server 2016 nicht unterstützt. Switch Embedded Teaming können Sie den gleichen Satz von NICs für Ihre virtuellen und RDMA-Datenverkehr verwenden. Dies wurde nicht mit NIC-Teamvorgang basierend auf LBFO unterstützt.                                                        |
| Interruptüberprüfung für physische NICs       | Verwenden Sie die Standardeinstellungen. Um die Konfiguration zu überprüfen, können Sie den folgenden Windows PowerShell-Befehl: ```Get-NetAdapterAdvancedProperty```                                                                                                                                                                                                                                                                                                                                                                    |
| Empfangspuffer (Größe) für physische NICs       | Sie können überprüfen, ob die physischen NICs die Konfiguration dieses Parameters unterstützen, mithilfe des Befehls ```Get-NetAdapterAdvancedProperty```. Wenn sie diesen Parameter nicht unterstützen, die Ausgabe des Befehls enthält keine Eigenschaft "Empfangspuffer.? Unterstützen die NICs den Parameter, können Sie die Empfangspuffergröße mit dem folgenden Windows PowerShell-Befehl festlegen: <br>```Set-NetAdapterAdvancedProperty “NIC1�? –DisplayName “Receive Buffers�? –DisplayValue 3000``` <br>                          |
| Sendepuffer (Größe) für physische NICs          | Sie können überprüfen, ob die physischen NICs die Konfiguration dieses Parameters unterstützen, mithilfe des Befehls ```Get-NetAdapterAdvancedProperty```. Wenn die NICs den Parameter nicht unterstützen, die Ausgabe des Befehls enthält keine Eigenschaft "Puffer zu senden.? Unterstützen die NICs den Parameter, können Sie die Sendepuffergröße mit dem folgenden Windows PowerShell-Befehl festlegen: <br> ```Set-NetAdapterAdvancedProperty “NIC1�? –DisplayName “Transmit Buffers�? –DisplayValue 3000``` <br>                           |
| Empfangsseitige Skalierung (Receive Side Scaling, RSS) für physische NICs | Sie können überprüfen, ob die physischen NICs RSS mit dem Windows PowerShell-Befehl Get-NetAdapterRss aktiviert haben. Sie können die folgenden Windows PowerShell-Befehle zum Aktivieren und Konfigurieren von RSS für Ihre Netzwerkadapter verwenden: <br> ```Enable-NetAdapterRss “NIC1�?,�?NIC2�?```<br> ```Set-NetAdapterRss “NIC1�?,�?NIC2�? –NumberOfReceiveQueues 16 -MaxProcessors``` <br> HINWEIS: Wenn VMMQ oder VMQ aktiviert ist, muss RSS nicht auf die physischen Netzwerkadapter aktiviert werden. Sie können sie auf die virtuellen Netzwerkadapter des Hosts aktivieren. |
| VMMQ                                        | Um VMMQ für einen virtuellen Computer zu aktivieren, führen Sie den folgenden Befehl aus: <br> ```Set-VmNetworkAdapter -VMName <gateway vm name>,-VrssEnabled $true -VmmqEnabled $true``` <br> HINWEIS: Nicht alle Netzwerkadapter unterstützen VMMQ. Derzeit ist es Chelsio T5 und T6 Mellanox CX-3 und CX-4 und QLogic 45xxx-Serie unterstützt                                                                                                                                                                                                                                      |
| Warteschlange für virtuelle Computer (Virtual Machine Queue, VMQ) für das NIC-Team | Sie können VMQ mit dem folgenden Windows PowerShell-Befehl in Ihrem Team Satz aktivieren: <br>```Enable-NetAdapterVmq``` <br> HINWEIS: Dies sollte aktiviert werden, nur dann, wenn die HW VMMQ nicht unterstützt. Wenn unterstützt, sollte die VMMQ für eine bessere Leistung aktiviert werden.                                                                                                                                                                                                                                                               |
>[!Note]
> VMQ und vRSS kommen in Abbildung nur, wenn die Last auf dem virtuellen Computer hoch ist, und die CPU bis zum Maximum genutzt wird wird. Mindestens ein Prozessor wird erst dann max, wichtige. VMQ und vRSS werden vorteilhaft, die helfen, die Verarbeitungslast auf mehrere Kerne verteilt. Dies gilt nicht für die IPsec-Datenverkehr als IPsec-Datenverkehr an einen einzelnen Kern beschränkt ist.

## <a name="windows-server-gateway-vm-configuration"></a>Konfiguration der Windows Server-Gateway-VM

Auf beiden Hyper-V-Hosts können Sie mehrere virtuelle Computer konfigurieren, die als Gateways mit Windows Server-Gateway konfiguriert sind. Mit dem Manager für virtuelle Switches können Sie einen virtuellen Hyper-V-Switch erstellen, der an das NIC-Team auf dem Hyper-V-Host gebunden ist. Beachten Sie, dass für eine optimale Leistung Sie ein einzelnes Gateway-VM auf einem Hyper-V-Host bereitstellen soll.
Folgende Konfiguration wird für jede Windows Server-Gateway-VM empfohlen.

| Konfigurationselement                 | Windows Powershell-Konfiguration                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Arbeitsspeicher                             | 8 GB                                                                                                                                                                                                                                                                                                                                                                                           |
| Anzahl virtueller Netzwerkadapter | 3 NICs für folgende verwendet: 1 für die Verwaltung, die durch das Verwaltungsbetriebssystem, 1 extern verwendet wird, die Zugriff auf externe Netzwerke, 1 bereitstellt, die intern ist, die nur Zugriff auf interne Netzwerke bietet.                                                                                                                                                            |
| Receive Side Scaling (RSS)         | Sie können die standardmäßigen übernehmen RSS-Einstellungen für die Management-NIC. Im Folgenden sehen Sie eine Beispielkonfiguration für eine VM mit acht virtuellen Prozessoren. Für die externen und internen NICs können Sie RSS mit dem BaseProcNumber-Wert auf 0 und dem MaxRssProcessors auf 8, die mit dem folgenden Windows PowerShell-Befehl aktivieren: <br> ```Set-NetAdapterRss “Internal�?,�?External�? –BaseProcNumber 0 –MaxProcessorNumber 8``` <br> |
| Sendeseitiger Puffer                   | Sie können die standardmäßigen übernehmen Sendeseitigen Puffer-Einstellungen für die Management-NIC. Für die interne und externe NIC können Sie den Sendeseitigen Puffer mit 32 MB RAM konfigurieren, mit dem folgenden Windows PowerShell-Befehl: <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Send Buffer Size�? –DisplayValue “32MB�?``` <br>                                                       |
| Empfangsseitiger Puffer                | Sie können die standardmäßigen übernehmen empfangsseitigen Puffer-Einstellungen für die Management-NIC. Für die interne und externe NIC können Sie den empfangsseitigen Puffer mit mindestens 16 MB RAM konfigurieren, mit dem folgenden Windows PowerShell-Befehl: <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Receive Buffer Size�? –DisplayValue “16MB�?``` <br>                                            |
| Weiterleitungsoptimierung               | Sie können die standardmäßigen übernehmen Weiterleitungsoptimierung-Einstellungen für die Management-NIC. Für die interne und externe NIC können Sie die Weiterleitungsoptimierung mit dem folgenden Windows PowerShell-Befehl aktivieren: <br> ```Set-NetAdapterAdvancedProperty “Internal�?,�?External�? –DisplayName “Forward Optimization�? –DisplayValue “1�?``` <br>                                                                      |
