---
title: Anpassen des Baselinenetzwerk-Schwellenwerts für das Failover
description: In diesem Artikel werden Lösungen zum Anpassen des Schwellenwerts von failoverclusternetzwerken vorgestellt.
ms.prod: windows-server
ms.technology: server-general
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 86a7023f6480e68f917cb8cdd9d0c69c417d3145
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409791"
---
# <a name="iaas-with-sql-alwayson---tuning-failover-cluster-network-thresholds"></a>IaaS mit SQL Always On: Optimieren der Failovercluster-Netzwerkschwellenwerte

In diesem Artikel werden Lösungen zum Anpassen des Schwellenwerts von failoverclusternetzwerken vorgestellt.

## <a name="symptom"></a>Symptom

Wenn Sie Windows-Failoverclusterknoten in IaaS mit SQL Server AlwaysOn ausführen, wird empfohlen, die Cluster Einstellung in einen stärker gelockerten Überwachungs Status zu ändern. Standardmäßig sind die Cluster Einstellungen restriktiv und können zu nicht benötigten Ausfällen führen. Die Standardeinstellungen sind für hochoptimierte lokale Netzwerke konzipiert und berücksichtigen nicht die Möglichkeit der durch eine mehr Instanzen fähigen Umgebung, wie z. b. Windows Azure (IaaS), verursachten Latenz.

Das Windows Server-Failoverclustering überwacht ständig die Netzwerkverbindungen und die Integrität der Knoten in einem Windows-Cluster.  Wenn ein Knoten über das Netzwerk nicht erreichbar ist, wird eine Wiederherstellungsaktion ausgeführt, um die Anwendungen und Dienste auf einem anderen Knoten im Cluster wieder online zu schalten. Die Latenz bei der Kommunikation zwischen Cluster Knoten kann zu folgendem Fehler führen:

> Fehler 1135 (System Ereignisprotokoll)

Der Cluster Knoten **Node1** wurde aus der aktiven failoverclustermitgliedschaft entfernt. Die Clusterdienst auf diesem Knoten wurde möglicherweise beendet. Dies kann auch darauf zurückzuführen sein, dass der Knoten die Kommunikation mit anderen aktiven Knoten im Failovercluster verloren hat. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Wenn die Bedingung weiterhin besteht, prüfen Sie, ob Hardware-oder Softwarefehler im Zusammenhang mit den Netzwerkadaptern auf diesem Knoten vorliegen. Überprüfen Sie auch, ob in anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler.

Beispiel für Cluster. log:

```console
0000ab34.00004e64::2014/06/10-07:54:34.099 DBG   [NETFTAPI] Signaled NetftRemoteUnreachable event, local address 10.xx.x.xxx:3343 remote address 10.x.xx.xx:3343
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] got event: Remote endpoint 10.xx.xx.xxx:~3343~ unreachable from 10.xx.x.xx:~3343~
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Marking Route from 10.xxx.xxx.xxxx:~3343~ to 10.xxx.xx.xxxx:~3343~ as down
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [NDP] Checking to see if all routes for route (virtual) local fexx::xxx:5dxx:xxxx:3xxx:~0~ to remote xxx::cxxx:xxxd:xxx:dxxx:~0~ are down
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [NDP] All routes for route (virtual) local fxxx::xxxx:5xxx:xxxx:3xxx:~0~ to remote fexx::xxxx:xxxx:xxxx:xxxx:~0~ are down
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [CORE] Node 8: executing node 12 failed handlers on a dedicated thread
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: Cleaning up connections for n12.
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [Nodename] Clearing 0 unsent and 15 unacknowledged messages.
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: n12 node object is closing its connections
0000ab34.00008b68::2014/06/10-07:54:34.099 INFO  [DCM] HandleNetftRemoteRouteChange
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 1: Old: 05.936, Message: Response, Route sequence: 150415, Received sequence: 150415, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:28.000, Ticks since last sending: 4
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: closing n12 node object channels
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 2: Old: 06.434, Message: Request, Route sequence: 150414, Received sequence: 150402, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:27.665, Ticks since last sending: 36
0000ab34.0000a8ac::2014/06/10-07:54:34.099 INFO  [DCM] HandleRequest: dcm/netftRouteChange
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 3: Old: 06.934, Message: Response, Route sequence: 150414, Received sequence: 150414, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:27.165, Ticks since last sending: 4
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 4: Old: 07.434, Message: Request, Route sequence: 150413, Received sequence: 150401, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:26.664, Ticks since last sending: 36
```

```console
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <realLocal>10.xxx.xx.xxx:~3343~</realLocal>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <realRemote>10.xxx.xx.xxx:~3343~</realRemote>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <virtualLocal>fexx::xxxx:xxxx:xxxx:xxxx:~0~</virtualLocal>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <virtualRemote>fexx::xxxx:xxxx:xxxx:xxxx:~0~</virtualRemote>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Delay>1000</Delay>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Threshold>5</Threshold>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Priority>140481</Priority>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Attributes>2147483649</Attributes>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO  </struct mscs::FaultTolerantRoute>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO   removed
```

```console
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   [QUORUM] Node 8: Lost quorum (3 4 5 6 7 8)
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   [QUORUM] Node 8: goingAway: 0, core.IsServiceShutdown: 0
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   lost quorum (status = 5925)
```

## <a name="cause"></a>Ursache

Zum Konfigurieren der konnektivitätsintegrität des Clusters werden zwei Einstellungen verwendet.

**Delay** – definiert die Häufigkeit, mit der Cluster Takte zwischen Knoten gesendet werden.  Die Verzögerung ist die Anzahl der Sekunden, bevor der nächste Takt gesendet wird.  Innerhalb desselben Clusters kann es unterschiedliche Verzögerungen zwischen Knoten im gleichen Subnetz und zwischen Knoten geben, die sich in unterschiedlichen Subnetzen befinden.

**Threshold** – definiert die Anzahl von Takten, die übersehen werden, bevor der Cluster eine Wiederherstellungs Aktion durchführt.  Der Schwellenwert ist eine Anzahl von Takten.  Innerhalb desselben Clusters können unterschiedliche Schwellenwerte zwischen Knoten im gleichen Subnetz und zwischen Knoten in unterschiedlichen Subnetzen vorhanden sein.

Standardmäßig legt Windows Server 2016 **samesubnetthreshold** auf 10 und **samesubnetdelay** auf 1000 ms fest. Wenn beispielsweise die Verbindungsüberwachung 10 Sekunden lang ausfällt, wird der failoverschwellen Wert erreicht, was dazu führt, dass der Knoten aus der Cluster Mitgliedschaft entfernt wurde. Dies führt dazu, dass die Ressourcen auf einen anderen verfügbaren Knoten im Cluster verschoben werden. Cluster Fehler werden gemeldet, einschließlich des Cluster Fehlers 1135 (oben).

## <a name="resolution"></a>Auflösung

Lockern Sie in einer IaaS-Umgebung die Konfigurationseinstellungen des Cluster Netzwerks.

### <a name="steps-to-verify-current-configuration"></a>Schritte zum Überprüfen der aktuellen Konfiguration

Überprüfen Sie die aktuellen Cluster Netzwerk-Konfigurationseinstellungen, indem Sie den Befehl Get-Cluster verwenden:

```powershell
C:\Windows\system32> get-cluster | fl *subnet*
```

Standard-, minimal-, höchst-und empfohlene Werte für jedes Support Betriebssystem

| BESCHREIBUNG | OS | Min | Max | Standard | Empfohlen |
|--|--|--|--|--|--|
| CrossSubnetThreshold | 2008 R2 | 3 | 20 | 5 | 20 |
| Crosssubnet-Schwellenwert | 2012 | 3 | 120 | 5 | 20 |
| Crosssubnet-Schwellenwert | 2012 R2 | 3 | 120 | 5 | 20 |
| Crosssubnet-Schwellenwert | 2016 | 3 | 120 | 20 | 20 |
| Samesubnet-Schwellenwert | 2008 R2 | 3 | 10 | 5 | 10 |
| Samesubnet-Schwellenwert | 2012 | 3 | 120 | 5 | 10 |
| Samesubnet-Schwellenwert | 2012 R2 | 3 | 120 | 5 | 10 |
| SameSubnetThreshold | 2016 | 3 | 120 | 10 | 10 |

Die Werte für Schwellenwert entsprechen den aktuellen Empfehlungen in Bezug auf den Umfang der Bereitstellung, wie im folgenden Artikel beschrieben:

[Optimieren der Netzwerk Schwellenwerte für Failovercluster in Windows Server 2012 R2](https://support.microsoft.com/en-us/help/3153887/fine-tuning-failover-cluster-network-thresholds-in-windows-server-2012)

Der **Schwellenwert** definiert die Anzahl der Takte, die übersehen werden, bevor der Cluster eine Wiederherstellungs Aktion durchführt.  Der Schwellenwert ist eine Anzahl von Takten.  Innerhalb desselben Clusters können unterschiedliche Schwellenwerte zwischen Knoten im gleichen Subnetz und zwischen Knoten vorhanden sein, die sich in unterschiedlichen Subnetzen befinden.

## <a name="recommendations-for-changing-to-more-relaxed-settings-for-multi-tenant-environments-like-azure-iaas"></a>Empfehlungen für die Umstellung auf die Einstellungen für mehr Instanzen fähige Umgebungen wie Azure (IaaS)

> [!NOTE]
> Das Erhöhen der Resilienz ihrer Cluster Umgebung durch die Anpassung der Cluster Netzwerk-Konfigurationseinstellungen kann zu einer längeren Ausfallzeit führen. Weitere Informationen finden Sie unter [Optimieren der Netzwerk Schwellenwerte für Failovercluster](https://techcommunity.microsoft.com/t5/failover-clustering/tuning-failover-cluster-network-thresholds/ba-p/371834).

1. Ändern Sie die Einstellungen in den Einstellungen:

    > [!NOTE]
    > Das Ändern des Cluster Schwellenwerts wird sofort wirksam. Sie müssen den Cluster oder die Ressourcen nicht neu starten.

    Die folgenden Einstellungen werden sowohl für das gleiche Subnetz als auch für Regions übergreifende bereit Stellungen von AlwaysOn-Verfügbarkeits Gruppen empfohlen.

    ```powershell
    C:\Windows\system32> (get-cluster).SameSubnetThreshold = 20
    ```

    ```powershell
    C:\Windows\system32> (get-cluster).CrossSubnetThreshold = 20
    ```

2. Überprüfen Sie die Änderungen:

    ```powershell
    C:\Windows\system32> get-cluster | fl *subnet*
    ```

    :::image type="content" source="media/iaas-sql-failover-cluster/cmd.png" alt-text="cmd" border="false":::

## <a name="references"></a>Referenzen

Weitere Informationen zum Optimieren der Netzwerk Konfigurationseinstellungen für Windows-Cluster finden Sie unter [Optimieren der Netzwerk Schwellenwerte für Failovercluster](https://techcommunity.microsoft.com/t5/failover-clustering/tuning-failover-cluster-network-thresholds/ba-p/371834).

Informationen zum Verwenden von cluster.exe zum Optimieren der Netzwerk Konfigurationseinstellungen für Windows-Cluster finden Sie unter [Konfigurieren von Cluster Netzwerken für einen Failovercluster](/previous-versions/office/exchange-server-2007/bb690953(v=exchg.80)?redirectedfrom=MSDN).
