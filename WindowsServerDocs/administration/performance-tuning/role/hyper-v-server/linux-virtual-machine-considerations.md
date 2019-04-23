---
title: Überlegungen zur Linux-VM
description: Linux und BSD-VM
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: cc6aab7825754579269eb05e591ca2a3cf5a561b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869681"
---
# <a name="linux-virtual-machine-considerations"></a>Überlegungen zur Linux-VM

Linux- und BSD-Computer sind noch weitere Aspekte im Vergleich zu Windows-VMs in Hyper-V.

Der erste Aspekt ist, ob Integration Services vorhanden sind oder wenn der virtuelle Computer mit keine Erleuchtung lediglich auf emulierte Hardware ausgeführt wird. Eine Tabelle mit Linux und BSD-Versionen, die integrierte oder durch Herunterladen-Integrationsdiensten finden Sie in [unterstützt Linux und FreeBSD-VMs für Hyper-V unter Windows](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows). Diese Seiten enthalten Raster verfügbare Hyper-V-Features, die für Linux verteilungsversionen und Hinweise zu dieser Funktionen verfügbar, falls zutreffend.

Selbst wenn der Gast Integration Services ausgeführt wird, kann es bei älterer Hardware konfiguriert werden, die nicht die optimale Leistung aufweist. Beispielsweise konfigurieren Sie und verwenden Sie einen virtuellen Ethernetadapter für das Gastbetriebssystem, anstatt eine ältere Netzwerkkarte. Mit Windows Server 2016 können Sie erweiterte Netzwerk wie SR-IOV sind ebenfalls verfügbar.

## <a name="linux-network-performance"></a>Linux-Netzwerkleistung

Linux in der Standardeinstellung wird die Hardwarebeschleunigung aktiviert und standardmäßig verlagert. Wenn vRSS in den Eigenschaften einer NIC auf dem Host aktiviert ist, und Linux-Gast die Möglichkeit zum Verwenden von vRSS bietet wird die Funktion aktiviert werden. In Powershell diese denselben Parameter geändert werden kann, mit der `EnableNetAdapterRSS` Befehl.

Auf ähnliche Weise kann die VMMQ (virtuellen Switch, RSS)-Funktion aktiviert werden, auf die physische Netzwerkkarte vom Gastbetriebssystem **Eigenschaften** > **konfigurieren...**   >  **Erweitert** Registerkarte > festgelegt **RSS für virtuelle Switches** zu **aktiviert** oder VMMQ in Powershell mithilfe des folgenden aktivieren:

```PowerShell
 Set-VMNetworkAdapter -VMName **$VMName** -VmmqEnabled $True
 ```

Auf dem Gast kann zusätzliche TCP-Optimierungen erfolgen durch Erhöhen der Grenzwerte. Die beste Leistung Verteilen von Arbeitslast über mehrere CPUs und Tiefe von Workloads generiert den besten Durchsatz, wie für virtualisierte arbeitsauslastungen sind höhere Latenz als "bare-Metal" hat die.

Einige Beispiel-Optimierung-Parameter, die insbesondere für die Netzwerk-Benchmarks wurden gehören:

```PowerShell
net.core.netdev_max_backlog = 30000
net.core.rmem_max = 67108864
net.core.wmem_max = 67108864
net.ipv4.tcp_wmem = 4096 12582912 33554432
net.ipv4.tcp_rmem = 4096 12582912 33554432
net.ipv4.tcp_max_syn_backlog = 80960
net.ipv4.tcp_slow_start_after_idle = 0
net.ipv4.tcp_tw_reuse = 1
net.ipv4.ip_local_port_range = 10240 65535
net.ipv4.tcp_abort_on_overflow = 1
```

Ein nützliches Tool für die Netzwerk-Microbenchmarks ist Ntttcp, die auf Linux- und Windows verfügbar ist. Die Linux-Version ist open Source und verfügbar [Ntttcp-for-Linux auf github.com](https://github.com/Microsoft/ntttcp-for-linux). Die Windows-Version finden Sie in der [Downloadcenter](https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769). Beim Optimieren von Workloads ist es am besten, so viele Streams nach Bedarf zu verwenden, um den besten Durchsatz zu erhalten. Mithilfe der Ntttcp für den Modell-Verkehr, der `-P` Parameter legt fest, die Anzahl von parallelen Verbindungen verwendet.

## <a name="linux-storage-performance"></a>Linux-Speicherleistung

Finden Sie einige bewährten Methoden, wie folgt aus, auf [bewährte Methoden für die Ausführung von Linux auf Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/best-practices-for-running-linux-on-hyper-v). Der Linux-Kernel verfügt über verschiedene e/a-Planer, Anforderungen mit unterschiedlichen Algorithmen neu anzuordnen. NOOP ist einer First in First Out-Warteschlange, die die Entscheidung Zeitplan vom Hypervisor getroffen werden übergeben. Es wird empfohlen, NOOP als Planer zu verwenden, bei der Ausführung von virtuellen Linux-Computer auf Hyper-V. So ändern Sie den Planer für ein bestimmtes Gerät, in der Konfiguration für das Startladeprogramm (/ etc/grub.conf, z. B.), fügen `elevator=noop` die Kernel-Parameter, und klicken Sie dann erneut starten.

Ähnlich wie Netzwerke, profitiert auch Linux-Gast-Anwendungsleistung mit Storage Nutzung von mehreren Warteschlangen mit ausreichende Tiefe um den Host ausgelastet. Speicherleistung Microbenchmarking ist wahrscheinlich am besten mit dem Fio Benchmark-Tool, mit der Libaio-Engine.

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Server-Konfiguration](configuration.md)

-   [Hyper-V, prozessorbezogene Leistungsdaten](processor-performance.md)

-   [Hyper-V-Memory-Leistung](memory-performance.md)

-   [Hyper-V-Speicher-e/a-Leistung](storage-io-performance.md)

-   [Hyper-V-Netzwerk-e/a-Leistung](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)
