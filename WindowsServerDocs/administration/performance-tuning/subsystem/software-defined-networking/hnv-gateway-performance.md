---
title: Leistungsoptimierung des HNV-Gateways in Software definierten Netzwerken
description: Richtlinien zur Leistungsoptimierung des HNV-Gateways für Software definierte Netzwerke
ms.topic: article
ms.author: grcusanz
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: de6a83d883efbdf592c7a21524c36b9d9086b7cc
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077967"
---
# <a name="hnv-gateway-performance-tuning-in-software-defined-networks"></a>Leistungsoptimierung des HNV-Gateways in Software definierten Netzwerken

Dieses Thema enthält die Hardware Spezifikationen und Konfigurations Empfehlungen für Server, auf denen Hyper-V ausgeführt wird und die virtuelle Computer des Windows Server-Gateways hosten, zusätzlich zu den Konfigurationsparametern für virtuelle Windows Server-Gatewaycomputer (Virtual Machines, VMS). Um die beste Leistung von Windows Server-Gateway-VMS zu extrahieren, wird erwartet, dass diese Richtlinien befolgt werden.
Die folgenden Abschnitte enthalten Hardware- und Konfigurationsanforderungen für die Bereitstellung von Windows Server-Gateway.
1. Hardwareempfehlungen für Hyper-V
2. Hyper-V-Hostkonfiguration
3. VM-Konfiguration des Windows Server-Gateways

## <a name="hyper-v-hardware-recommendations"></a>Hardwareempfehlungen für Hyper-V

Im folgenden finden Sie die empfohlene Mindesthardwarekonfiguration für jeden Server, auf dem Windows Server 2016 und Hyper-V ausgeführt wird.

| Serverkomponente               | Spezifikation                                                                                                                                                                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Zentralprozessor (CPU)  | Non-Uniform Memory Architecture (NUMA)-Knoten: 2 <br> Wenn auf dem Host mehrere Windows Server-Gateway-VMS vorhanden sind, sollte für eine optimale Leistung jede Gateway-VM über Vollzugriff auf einen NUMA-Knoten verfügen. Dies sollte sich von dem NUMA-Knoten unterscheiden, der vom physischen Host Adapter verwendet wird. |
| Kerne pro NUMA-Knoten            | 2                                                                                                                                                                                                                                                                               |
| Hyperthreading                | Deaktiviert. Hyperthreading verbessert die Leistung von Windows Server-Gateway nicht.                                                                                                                                                                                           |
| Arbeitsspeicher (RAM)     | 48 GB                                                                                                                                                                                                                                                                           |
| Netzwerkschnittstellenkarten (NICs) | 2 10 GB NICs, die Gatewayleistung hängt von der Zeilen Rate ab. Wenn die zeilenate weniger als 10 Gbit/s ist, werden die Durchsatz Zahlen des gatewaytunnels ebenfalls um denselben Faktor gesenkt.                                                                                          |

Stellen Sie sicher, dass die Anzahl virtueller Prozessoren, die einer Windows Server-Gateway-VM zugewiesen sind, die Anzahl von Prozessoren auf dem NUMA-Knoten nicht übersteigt. Bei einem NUMA-Knoten mit acht Kernen sollten z. B. maximal acht virtuelle Prozessoren verwendet werden. Die beste Leistung erzielen Sie, wenn Sie 8 ist. Führen Sie das folgende Windows PowerShell-Skript auf jedem Hyper-V-Host aus, um die Anzahl von NUMA-Knoten und die Anzahl von Kernen pro NUMA-Knoten zu ermitteln:

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

Eine Gateway-VM mit acht virtuellen Prozessoren und mindestens 8 GB RAM wird empfohlen, wenn Sie die Anzahl der Gateway-VMS auswählen, die auf jedem Hyper-V-Host installiert werden sollen, wenn jeder NUMA-Knoten über acht Kerne verfügt. In diesem Fall ist ein NUMA-Knoten für den Host Computer dediziert.

## <a name="hyper-v-host-configuration"></a>Hyper-V-Host Konfiguration

Im folgenden finden Sie die empfohlene Konfiguration für jeden Server, auf dem Windows Server 2016 und Hyper-V ausgeführt wird und dessen Arbeitsauslastung das Ausführen von virtuellen Windows Server-Gateway-VMS ist. Die Konfigurationsanweisungen beinhalten Windows PowerShell-Befehlsbeispiele. Die Beispiele enthalten Platzhalter für die tatsächlichen Werte, die Sie beim Ausführen der Befehle in Ihrer Umgebung angeben müssen. Beispielsweise sind die Platzhalter für Netzwerkadapter Namen "NIC1" und "NIC2". Wenn Sie Befehle mit diesen Platzhaltern ausführen, verwenden Sie anstelle der Platzhalter die tatsächlichen Namen der Netzwerkadapter auf Ihren Servern. Andernfalls schlagen die Befehle fehl.

>[!Note]
> Zum Ausführen der folgenden Windows PowerShell-Befehle müssen Sie ein Mitglied der lokalen Gruppe %%amp;quot;Administratoren%%amp;quot; sein.

| Konfigurationselement                          | Windows PowerShell-Konfiguration                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Switch Embedded Teaming                     | Wenn Sie einen Vswitch mit mehreren Netzwerkadaptern erstellen, wird der Switch Embedded Team Vorgang automatisch für diese Adapter aktiviert. <br> ```New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"``` <br> Herkömmliches Team Vorgang über LBFO wird mit Sdn in Windows Server 2016 nicht unterstützt. Mit Switch Embedded Teaming können Sie denselben Satz von NICs für den virtuellen und RDMA-Datenverkehr verwenden. Dies wurde beim NIC-Team Vorgang, das auf LBFO basiert, nicht unterstützt.                                                        |
| Interruptüberprüfung für physische NICs       | Verwenden Sie die Standardeinstellungen. Um die Konfiguration zu überprüfen, können Sie den folgenden Windows PowerShell-Befehl verwenden: ```Get-NetAdapterAdvancedProperty```                                                                                                                                                                                                                                                                                                                                                                    |
| Empfangspuffer (Größe) für physische NICs       | Sie können überprüfen, ob die physischen NICs die Konfiguration dieses Parameters unterstützen, indem Sie den Befehl ausführen  ```Get-NetAdapterAdvancedProperty``` . Wenn Sie diesen Parameter nicht unterstützen, enthält die Ausgabe des Befehls nicht die Eigenschaft "Empfangs Puffer". Unterstützen die NICs den Parameter, können Sie die Empfangspuffergröße mit dem folgenden Windows PowerShell-Befehl festlegen: <br>```Set-NetAdapterAdvancedProperty "NIC1" –DisplayName "Receive Buffers" –DisplayValue 3000``` <br>                          |
| Sendepuffer (Größe) für physische NICs          | Sie können überprüfen, ob die physischen NICs die Konfiguration dieses Parameters unterstützen, indem Sie den Befehl ausführen ```Get-NetAdapterAdvancedProperty``` . Wenn die NICs diesen Parameter nicht unterstützen, enthält die Ausgabe des Befehls nicht die Eigenschaft "Sendepuffer". Unterstützen die NICs den Parameter, können Sie die Sendepuffergröße mit dem folgenden Windows PowerShell-Befehl festlegen: <br> ```Set-NetAdapterAdvancedProperty "NIC1" –DisplayName "Transmit Buffers" –DisplayValue 3000``` <br>                           |
| Empfangsseitige Skalierung (Receive Side Scaling, RSS) für physische NICs | Sie können überprüfen, ob RSS für die physischen NICs aktiviert ist, indem Sie den Windows PowerShell-Befehl Get-NetAdapterRss ausführen. Sie können die folgenden Windows PowerShell-Befehle verwenden, um RSS auf ihren Netzwerkadaptern zu aktivieren und zu konfigurieren: <br> ```Enable-NetAdapterRss "NIC1","NIC2"```<br> ```Set-NetAdapterRss "NIC1","NIC2" –NumberOfReceiveQueues 16 -MaxProcessors``` <br> Hinweis: Wenn vmmq oder VMQ aktiviert ist, muss RSS auf den physischen Netzwerkadaptern nicht aktiviert werden. Sie können Sie auf den virtuellen Netzwerkadaptern des Hosts aktivieren. |
| Vmmq                                        | Um vmmq für eine VM zu aktivieren, führen Sie den folgenden Befehl aus: <br> ```Set-VmNetworkAdapter -VMName <gateway vm name>,-VrssEnabled $true -VmmqEnabled $true``` <br> Hinweis: vmmq wird nicht von allen Netzwerkadaptern unterstützt. Derzeit wird Sie von Chelsio T5 und T6, Mellanox CX-3 und CX-4 und QLogic 45xxx-Serie unterstützt.                                                                                                                                                                                                                                      |
| Warteschlange für virtuelle Computer (Virtual Machine Queue, VMQ) für das NIC-Team | Sie können VMQ mit dem folgenden Windows PowerShell-Befehl für Ihr Set-Team aktivieren: <br>```Enable-NetAdapterVmq``` <br> Hinweis: diese Option sollte nur aktiviert werden, wenn die HW vmmq nicht unterstützt. Wenn unterstützt, sollte vmmq aktiviert werden, um eine bessere Leistung zu erzielen.                                                                                                                                                                                                                                                               |
>[!Note]
> VMQ und vrss sind nur dann in Frage, wenn die Auslastung des virtuellen Computers hoch ist und die CPU bis zum Maximum ausgelastet ist. Nur dann wird mindestens ein Prozessorkern max. VMQ und vrss werden dann von Vorteil sein, um die Verarbeitungs Last auf mehrere Kerne zu verteilen. Dies gilt nicht für IPSec-Datenverkehr, da der IPSec-Datenverkehr auf einen einzelnen Kern beschränkt ist.

## <a name="windows-server-gateway-vm-configuration"></a>Konfiguration der Windows Server-Gateway-VM

Auf beiden Hyper-V-Hosts können Sie mehrere VMS konfigurieren, die als Gateways mit dem Windows Server-Gateway konfiguriert sind. Mit dem Manager für virtuelle Switches können Sie einen virtuellen Hyper-V-Switch erstellen, der an das NIC-Team auf dem Hyper-V-Host gebunden ist. Beachten Sie, dass Sie für eine optimale Leistung eine einzelne Gateway-VM auf einem Hyper-V-Host bereitstellen sollten.
Folgende Konfiguration wird für jede Windows Server-Gateway-VM empfohlen.

| Konfigurationselement                 | Windows PowerShell-Konfiguration                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Arbeitsspeicher                             | 8 GB                                                                                                                                                                                                                                                                                                                                                                                           |
| Anzahl virtueller Netzwerkadapter | 3 NICs mit den folgenden spezifischen Verwendungszwecken: 1 für die Verwaltung, die vom Verwaltungs Betriebssystem verwendet wird, 1 extern, das den Zugriff auf externe Netzwerke ermöglicht, d. h. ein interner, der nur den Zugriff auf interne Netzwerke ermöglicht.                                                                                                                                                            |
| Empfangsseitige Skalierung (RSS)         | Sie können die standardmäßigen RSS-Einstellungen für die Verwaltungs-NIC beibehalten. Im Folgenden sehen Sie eine Beispielkonfiguration für eine VM mit acht virtuellen Prozessoren. Für externe und interne NICs können Sie RSS aktivieren, wenn baseprocnumber auf 0 festgelegt ist und maxrssprocken auf 8 festgelegt ist. verwenden Sie dazu den folgenden Windows PowerShell-Befehl: <br> ```Set-NetAdapterRss "Internal","External" –BaseProcNumber 0 –MaxProcessorNumber 8``` <br> |
| Sende seitiger Puffer                   | Sie können die Standardeinstellungen für den Sende seitigen Puffer für die Verwaltungs-NIC beibehalten. Für die internen und externen NICs können Sie den Sende seitigen Puffer mit 32 MB RAM konfigurieren, indem Sie den folgenden Windows PowerShell-Befehl verwenden: <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Send Buffer Size" –DisplayValue "32MB"``` <br>                                                       |
| Empfangs seitiger Puffer                | Sie können die Standardeinstellungen für den Empfangs seitigen Puffer für die Verwaltungs-NIC beibehalten. Für die internen und externen NICs können Sie den Empfangs seitigen Puffer mit 16 MB RAM konfigurieren, indem Sie den folgenden Windows PowerShell-Befehl verwenden: <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Receive Buffer Size" –DisplayValue "16MB"``` <br>                                            |
| Weiterleitungsoptimierung               | Sie können die Standardeinstellungen für die vorwärts Optimierung für die Verwaltungs-NIC beibehalten. Für die internen und externen NICs können Sie die vorwärts Optimierung mit dem folgenden Windows PowerShell-Befehl aktivieren: <br> ```Set-NetAdapterAdvancedProperty "Internal","External" –DisplayName "Forward Optimization" –DisplayValue "1"``` <br>                                                                      |
