---
ms.assetid: c9844427-27cf-4d76-b5bb-e06368b092f7
title: Failoverclustering
ms.prod: windows-server-threshold
layout: LandingPage
ms.topic: landing-page
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 03/08/2019
ms.localizationpriority: high
ms.openlocfilehash: 9e4184e52ef48e758ebc80e63d3d6f952a09cc2c
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222455"
---
# <a name="failover-clustering-in-windows-server"></a>Failoverclustering in Windows Server

> Gilt für: Windows Server 2019, Windows Server 2016

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf „docs.microsoft.com“ an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<hr />

Ein Failovercluster ist eine Gruppe aus unabhängigen Computern, die miteinander interagieren, um die Verfügbarkeit und Skalierbarkeit von Clusterrollen (früher Clusteranwendungen und -dienste genannt) zu erhöhen. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn auf einem oder mehreren der Clusterknoten ein Fehler auftritt, werden seine Aufgaben sofort von anderen Knoten übernommen. Dieser Vorgang wird als Failover bezeichnet. Zusätzlich werden die Clusterrollen proaktiv überwacht, um sicherzustellen, dass sie ordnungsgemäß funktionieren. Funktionieren sie nicht, werden sie neu gestartet oder auf einen anderen Knoten verschoben.

Failovercluster stellen darüber hinaus Funktionen für freigegebene Clustervolumes (Cluster Shared Volume, CSV) mit einem konsistenten verteilten Namespace bereit, mit dem Clusterrollen von allen Knoten aus auf den freigegebenen Speicher zugreifen können. Das Failoverclusteringfeature sorgt dafür, dass die Unterbrechung auf Benutzerseite nur minimal ist.

Für Failoverclustering gibt es viele praktische Anwendungsfälle, einschließlich:
* Hoch verfügbarer oder fortlaufend verfügbarer Dateifreigabespeicher für Anwendungen wie Microsoft SQL Server und Hyper-V-basierte virtuelle Computer
* Hoch verfügbare Clusterrollen, die auf physischen Servern oder virtuellen Computern ausgeführt werden, die auf Servern mit Hyper-V installiert sind


|  |  |
|---------|---------|
|![Neuigkeiten:](../media/i-whats-new.svg)  | [**Neues beim Failoverclustering**](whats-new-in-failover-clustering.md) |


|  |  |  |
|---------|---------|---------|
|![Verstehen](../media/i-cluster.svg)**verstehen**  |  ![Planen der](../media/i-cluster.svg)**planen**  |  ![Bereitstellung](../media/i-cluster.svg)**Bereitstellung**       |
| [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](sofs-overview.md)    |   [Planen der Failoverclustering-Hardwareanforderungen und Speicheroptionen](clustering-requirements.md)      |  [Bereitstellung vorab bereitgestellten Clustercomputerobjekten in Active Directory-Domänendienste](prestage-cluster-adds.md)  |
|  [Cluster- und Poolquorum](../storage/storage-spaces/understand-quorum.md)   |   [Verwenden von freigegebenen Clustervolumes (CSVs)](failover-cluster-csvs.md)      | [Erstellen eines Failoverclusters](create-failover-cluster.md)        |
|  [Fehlerdomänenunterstützung](fault-domains.md)   |  [Verwenden von gastclustern für virtuelle Computer mit "direkte Speicherplätze"](../storage/storage-spaces/storage-spaces-direct-in-vm.md)       | [Bereitstellen eines Dateiservers mit zwei Knoten](../storage/storage-spaces/storage-spaces-direct-in-vm.md)        |
| [Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke](smb-multichannel.md)    |         |  [Verwalten des Quorums und Zeugen](manage-cluster-quorum.md)       |
|   [VM-Lastenausgleich](vm-load-balancing-overview.md)  |         |   [Bereitstellen eines cloudzeugen](deploy-cloud-witness.md)      |
|   [Clustergruppen](../storage/storage-spaces/cluster-sets.md)  |         |     [Bereitstellen eines Dateifreigabezeugen](file-share-witness.md)    |
|   [Clusteraffinität](cluster-affinity.md)  |         |    [Paralleles Upgrade für Clusterbetriebssystem]()     |
|     |         |     [Upgrade eines Failoverclusters auf derselben Hardware](upgrade-option-same-hardware.md)    |
|     |         |     [Bereitstellen eines Active Directory getrennten Clusters](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\))    |


|  |  |  |
|---------|---------|---------|
|![Verwalten von](../media/i-cluster.svg)**verwalten**  |  ![Tools und Einstellungen](../media/i-cluster.svg)**Tools und Einstellungen**  |  ![Community-Ressourcen](../media/i-cluster.svg)**Community-Ressourcen**       |
| [Clusterfähiges Aktualisieren](cluster-aware-updating.md)    |   [Failoverclustering PowerShell-Cmdlets](https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps)      |  [Forum für hohe Verfügbarkeit (Clustering)](https://go.microsoft.com/fwlink/p/?LinkId=230641)       |
|  [Integritätsdienst](health-service-overview.md)   |   [Beachten Sie PowerShell-Cmdlets aktualisieren-Cluster](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)      | [Laden von Failoverclustering und Netzwerklastenausgleichs-Teamblog](http://blogs.msdn.com/b/clustering/)        |
|  [Clusterdomänenmigration](cluster-domain-migration.md)   |         |         |
|  [Problembehandlung mit der Windows-Fehlerberichterstattung](troubleshooting-using-wer-reports.md)   |         |         |
