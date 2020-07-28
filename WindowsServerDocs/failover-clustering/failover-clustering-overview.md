---
ms.assetid: c9844427-27cf-4d76-b5bb-e06368b092f7
title: Failoverclusterunterstützung
ms.prod: windows-server
ms.topic: landing-page
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 06/06/2019
ms.localizationpriority: high
ms.openlocfilehash: 657cf161086047ca87ca7dbd2adcd2b8e6bde892
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87177886"
---
# <a name="failover-clustering-in-windows-server"></a>Failoverclustering in Windows Server

> Gilt für: Windows Server 2019, Windows Server 2016

Ein Failovercluster ist eine Gruppe aus unabhängigen Computern, die miteinander interagieren, um die Verfügbarkeit und Skalierbarkeit von Clusterrollen (früher Clusteranwendungen und -dienste genannt) zu erhöhen. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn auf einem oder mehreren der Clusterknoten ein Fehler auftritt, werden seine Aufgaben sofort von anderen Knoten übernommen. Dieser Vorgang wird als Failover bezeichnet. Zusätzlich werden die Clusterrollen proaktiv überwacht, um sicherzustellen, dass sie ordnungsgemäß funktionieren. Funktionieren sie nicht, werden sie neu gestartet oder auf einen anderen Knoten verschoben.

Failovercluster stellen darüber hinaus Funktionen für freigegebene Clustervolumes (Cluster Shared Volume, CSV) mit einem konsistenten verteilten Namespace bereit, mit dem Clusterrollen von allen Knoten aus auf den freigegebenen Speicher zugreifen können. Das Failoverclusteringfeature sorgt dafür, dass die Unterbrechung auf Benutzerseite nur minimal ist.

Für Failoverclustering gibt es viele praktische Anwendungsfälle, einschließlich:

* Hoch verfügbarer oder fortlaufend verfügbarer Dateifreigabespeicher für Anwendungen wie Microsoft SQL Server und Hyper-V-basierte virtuelle Computer
* Hoch verfügbare Clusterrollen, die auf physischen Servern oder virtuellen Computern ausgeführt werden, die auf Servern mit Hyper-V installiert sind

| **Grundlegende Informationen**                                                               |  **Planung**                          |  **Bereitstellung**       |
| -------------                                                                |  --------------                        | --------------------- |
| [Neues beim Failoverclustering](whats-new-in-failover-clustering.md)    | [Planen der Hardwareanforderungen und Speicheroptionen für Failoverclustering](clustering-requirements.md)  | [Erstellen eines Failoverclusters](create-failover-cluster.md) |
| [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](sofs-overview.md)               | [Verwenden von freigegebenen Clustervolumes (CSVs)](failover-cluster-csvs.md) | [Bereitstellen eines Dateiservers mit zwei Knoten](deploy-two-node-clustered-file-server.md) |
|  [Cluster- und Poolquorum](../storage/storage-spaces/understand-quorum.md)   |  [Verwenden von virtuellen Gastcomputerclustern mit direkten Speicherplätzen](../storage/storage-spaces/storage-spaces-direct-in-vm.md)       | [Vorabbereitstellen von Clustercomputerobjekten in Active Directory Domain Services](prestage-cluster-adds.md) |
| [Fehlerdomänenunterstützung](fault-domains.md)                                 |                                 | [Konfigurieren von Clusterkonten in Active Directory](configure-ad-accounts.md) |
| [Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke](smb-multichannel.md) |                       | [Verwalten des Quorums und von Zeugen](manage-cluster-quorum.md) |
| [VM-Lastenausgleich](vm-load-balancing-overview.md)                         |                             | [Bereitstellen eines Cloudzeugen](deploy-cloud-witness.md) |
| [Clustergruppen](../storage/storage-spaces/cluster-sets.md)                  |                             |[Bereitstellen eines Dateifreigabezeugen](file-share-witness.md) |
| [Clusteraffinität](cluster-affinity.md)                                     |                            | [Paralleles Upgrade für Clusterbetriebssystem](cluster-operating-system-rolling-upgrade.md) |
|                                                                             |                            | [Upgrade eines Failoverclusters auf derselben Hardware](upgrade-option-same-hardware.md) |
|                                                                            |                             | [Bereitstellen eines von Active Directory getrennten Clusters](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\))

|**Verwalten**  |  **Tools und Einstellungen**  |  **Communityressourcen**       |
| ------------- |  -------------- | --------------------- |
| [Clusterfähiges Aktualisieren](cluster-aware-updating.md)    |   [PowerShell-Cmdlets für Failoverclustering](https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps)      |  [Forum für hohe Verfügbarkeit (Clustering)](https://go.microsoft.com/fwlink/p/?LinkId=230641)       |
|  [Integritätsdienst](health-service-overview.md)   |   [PowerShell-Cmdlets für das clusterfähige Aktualisieren](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)      | [Teamblog zu Failoverclustering und Netzwerklastenausgleich](https://blogs.msdn.com/b/clustering/)        |
|  [Clusterdomänenmigration](cluster-domain-migration.md)   |         |         |
|  [Problembehandlung mit der Windows-Fehlerberichterstattung](troubleshooting-using-wer-reports.md)   |         |         |
