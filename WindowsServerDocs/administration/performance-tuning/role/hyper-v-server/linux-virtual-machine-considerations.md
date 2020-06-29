---
title: Überlegungen zu virtuellen Linux-Computern
description: Virtueller Linux-und BSD-Computer
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 1109eb50bbe052b39fe7a91903fa0aea58b6e4f1
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471385"
---
# <a name="linux-virtual-machine-considerations"></a>Überlegungen zu virtuellen Linux-Computern

Bei virtuellen Linux-und BSD-Computern müssen im Vergleich zu virtuellen Windows-Computern in Hyper-V zusätzliche Aspekte berücksichtigt werden.

Der erste Aspekt ist, ob Integration Services vorhanden sind oder ob der virtuelle Computer nur auf emulierten Hardware ohne Aufklärung ausgeführt wird. Eine Tabelle mit Linux-und BSD-Releases, die über integrierte oder herunterladbare Integration Services verfügen, ist [unter Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows)verfügbar. Diese Seiten enthalten Raster verfügbarer Hyper-V-Features, die für Linux-Verteilungs Releases verfügbar sind, sowie Hinweise zu diesen Features, sofern zutreffend.

Auch wenn der Gast Integration Services ausgeführt wird, kann er mit Legacy Hardware konfiguriert werden, die nicht die beste Leistung aufweist. Konfigurieren und verwenden Sie z. b. einen virtuellen Ethernet-Adapter für den Gast, anstatt einen Legacy-Netzwerkadapter zu verwenden. Mit Windows Server 2016 sind auch erweiterte Netzwerke wie SR-IOV verfügbar.

## <a name="linux-network-performance"></a>Linux-Netzwerkleistung

Linux aktiviert standardmäßig Hardwarebeschleunigung und-Abladungen. Wenn vrss in den Eigenschaften einer NIC auf dem Host aktiviert ist und der Linux-Gast die Funktion zur Verwendung von vrss hat, wird die Funktion aktiviert. In PowerShell kann derselbe Parameter mit dem Befehl geändert werden `EnableNetAdapterRSS` .

Ebenso kann die vmmq-Funktion (Virtual Switch RSS) auf der physischen NIC aktiviert werden, die von den Gast **Eigenschaften**  >  **konfiguriert wird...**  >  Die Registerkarte **erweitert** > den **virtuellen Switch RSS** auf **aktiviert** festlegen oder vmmq in PowerShell aktivieren, indem Sie Folgendes verwenden:

```PowerShell
 Set-VMNetworkAdapter -VMName **$VMName** -VmmqEnabled $True
 ```

Im Gast kann zusätzliche TCP-Optimierung durch Erhöhung der Limits durchgeführt werden. Um die beste Leistung für die Leistungsverteilung für mehrere CPUs zu erzielen und umfassende Workloads zu erzielen, wird der beste Durchsatz erzielt, da virtualisierte Arbeits Auslastungen eine höhere Latenz als "Bare-Metal" aufweisen.

Beispiele für Optimierungsparameter, die in den Netzwerk Benchmarks nützlich waren:

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

Ein nützliches Tool für Netzwerk-Mikrobenchmarks ist ntttcp, das unter Linux und Windows verfügbar ist. Die Linux-Version ist Open Source und ist [über ntttcp-for-Linux auf GitHub.com](https://github.com/Microsoft/ntttcp-for-linux)verfügbar. Die Windows-Version finden [Sie im Download Center](https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769). Beim Optimieren von Arbeits Auslastungen empfiehlt es sich, möglichst viele Streams zu verwenden, um den besten Durchsatz zu erzielen. Durch die Verwendung von ntttcp zum Modellieren von Datenverkehr legt der- `-P` Parameter die Anzahl der verwendeten parallelen Verbindungen fest.

## <a name="linux-storage-performance"></a>Linux-Speicherleistung

Einige bewährte Methoden, wie z. b. die folgenden, werden unter Empfohlene [Vorgehensweisen für die Ausführung von Linux unter Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/best-practices-for-running-linux-on-hyper-v)aufgeführt. Der Linux-Kernel verfügt über unterschiedliche e/a-Planer, um Anforderungen mit unterschiedlichen Algorithmen neu anzuordnen. NOOP ist eine First-in-First-Out-Warteschlange, die die vom Hypervisor vorgenommene Zeit Plan Entscheidung übergibt. Es wird empfohlen, NOOP als Scheduler zu verwenden, wenn Sie virtuelle Linux-Computer unter Hyper-V ausführen. Um den Scheduler für ein bestimmtes Gerät zu ändern, fügen Sie in der Konfiguration des Start Laders (z. b./etc/grub.conf) `elevator=noop` die Kernel Parameter hinzu, und starten Sie dann neu.

Ähnlich wie bei Netzwerken profitiert die Leistung der Linux-gastleistung mit dem Speicher am meisten von mehreren Warteschlangen mit ausreichender Tiefe, um den Host ausgelastet zu halten. Die Speicherleistung von Mikro Benchmarks ist wahrscheinlich am besten mit dem fio-Benchmark-Tool mit der libaio-Engine.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)
