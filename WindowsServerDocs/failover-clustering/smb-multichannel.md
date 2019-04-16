---
ms.assetid: a6343f1c-e9dd-4a02-91ad-39bd519d66cd
title: Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: RobHindman
ms.author: robhind
ms.date: 09/15/2016
ms.openlocfilehash: 45d8364adf9d3db24a8e6d8f7bc91178ce7d1551
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a>Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke

> Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Vereinfachte SMB Multichannel- und Multi -<abbr title="Network Interface Card">NIC</abbr> Clusternetzwerke ist ein neues Feature in Windows Server2016, die die Verwendung mehrerer Netzwerkkarten innerhalb desselben clusternetzwerksubnetzes ermöglicht und SMB Multichannel automatisch aktiviert.  

Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke bietet die folgenden Vorteile:  
- Failover-Clusterunterstützung automatisch alle Netzwerkkarten auf Knoten, die den gleichen Switch verwenden, erkennt / demselben Subnetz - benötigen keine zusätzliche Konfiguration.  
- SMB Multichannel ist automatisch aktiviert.  
- Netzwerke, die nur über IPv6 Link lokale (fe80) IP-Adressen-Ressourcen verfügen, werden in nur-Cluster (privat) Netzwerken erkannt.  
- Eine einzelne IP-Adresse Ressource ist standardmäßig auf jedem (Cluster Access Point, CAP) Netzwerk Name (NN) konfiguriert.  
- Clusterüberprüfung nicht mehr gibt Warnmeldungen, wenn mehrere NICs im gleichen Subnetz befinden.  

## <a name="requirements"></a>Anforderungen  
-   Mehrere NICs pro Server, mit dem gleichen Switch / Subnetz.  

## <a name="how-to-take-advantage-of-multi-nic-clusters-networks-and-simplified-smb-multichannel"></a>Nutzen von Multi-NIC-Hostclustern Netzwerke und vereinfachte SMB Multichannel-  
In diesem Abschnittwird beschrieben, wie Sie den neuen Cluster-Netzwerken, Multi-NIC und vereinfachte SMB multichannel-Features in Windows Server2016 nutzen.  

### <a name="use-at-least-two-networks-for-failover-clustering"></a>Verwenden Sie mindestens zwei Netzwerke für die Failover-Clusterunterstützung   
Ist, Netzwerkswitches können fehlschlagen – es wird weiterhin empfohlen, mindestens zwei Netzwerke für die Failover-Clusterunterstützung verwenden. Alle Netzwerke, die gefunden werden, werden für Cluster-Signale verwendet. Vermeiden Sie mit einem einzigen Netzwerk für den Failovercluster, um einen einzelnen Fehlerpunkt zu vermeiden. Im Idealfall sollte sein mehrere physische Kommunikationspfade zwischen den Knoten im Cluster und keine einzelnen Fehlerpunkt.  

![Abbildungvon zwei Netzwerke für die Failover-Clusterunterstützung](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig1.png)  
**Abbildung1: Verwenden Sie mindestens zwei Netzwerke für die Failover-Clusterunterstützung**  

### <a name="use-multiple-nics-across-clusters"></a>Verwenden Sie mehrere NICs für mehrere Cluster  

Maximale Vorteil, dass die vereinfachte SMB Multichannel wird erreicht, wenn mehrere NICs für mehrere Cluster - Speicher und speichercluster Workload verwendet werden. Dadurch werden die Arbeitslast-Cluster (Hyper-V, SQL Server-Failoverclusterinstanz, Speicherreplikate, usw.), mithilfe von SMB Multichannel und die Ergebnisse in eine effizientere Nutzung des Netzwerks. Cluster-Konfiguration, bei denen ein Dateiservercluster mit horizontaler Skalierung wird zum Speichern von Arbeitsauslastungsdaten für einen Hyper-V oder SQL Server-Failoverclusterinstanz Cluster dieses Netzwerk wird häufig als "Nord-Süd-Subnetz" bezeichnet / Netzwerk, in einer zusammengeführten (konvergenten). Viele Kunden maximieren Durchsatz von diesem Netzwerk durch die Investition in die Lage RDMA-Netzwerkkarten und Switches.  

![Abbildungeines Subnetzes Nord-Süd SMB](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig2.png)  
**Abbildung2: Um maximale Netzwerkdurchsatz zu erzielen, verwenden Sie mehrere NICs auf sowohl Dateiserver mit horizontaler Skalierung und Hyper-V oder SQL Server-Failoverclusterinstanz-Cluster -, die das Subnetz Nord-Süd gemeinsam nutzen.**  

![ScreenCap von zwei Clustern mit mehreren NICs im gleichen Subnetz SMB Multichannel nutzen](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig3.png)  
**Abbildung3: Zwei Clustern (Dateiserver mit horizontaler Skalierung, für die Speicherung, SQL Server <abbr title="Failover-Clusterunterstützung Instanz">FCI</abbr> für Workload) beide mehrere NICs im gleichen Subnetz verwenden, um SMB Multichannel nutzen und besser Netzwerkdurchsatz erreichen.** 

## <a name="automatic-recognition-of-ipv6-link-local-private-networks"></a>Automatische Erkennung von IPv6-Link lokalen privaten Netzwerken  
Wenn Private (nur Cluster)-Netzwerke mit mehreren NICs erkannt werden, wird der Cluster automatisch IPv6 Link lokalen (fe80) IP-Adressen für jede Netzwerkkarte in jedem Subnetz erkennen. Diese speichert Administratoren Zeit, da sie nicht mehr Ressourcen IPv6 Link lokale (fe80) IP-Adresse manuell konfiguriert haben.  

Wenn Sie mehrere VPN-(nur Cluster) verwenden, überprüfen Sie die IPv6-Routing-Konfiguration, um sicherzustellen, dass Routing nicht konfiguriert ist, dass Subnetze, überschreiten, da dadurch die Leistung des Netzwerks verringert wird.  

![ScreenCap automatische Netzwerkkonfiguration in der Failovercluster-Manager-UI](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig4.png)  
**Abbildung4: Automatische IPv6 Link lokale (fe80) Adresse Ressourcenkonfiguration**  

## <a name="throughput-and-fault-tolerance"></a>Durchsatz und Fehlertoleranz  
Windows Server2016 erkennt NIC-Funktionen und versucht, jede Netzwerkkarte in der Konfiguration der schnellsten Möglichkeit zu verwenden. Netzwerkkarten, die zusammengeschlossen sind NICs mit RSS- und NICs mit RDMA-Funktion können alle verwendet werden. In der folgenden Tabelle werden die vor- und Nachteile zusammengefasst, wenn Sie diese Technologien verwenden. Maximaler Durchsatz wird erreicht, wenn Sie mehrere RDMA-fähige NICs verwenden. Weitere Informationen finden Sie unter [die Grundlagen der SMB-Mutlichannel](https://blogs.technet.microsoft.com/josebda/2012/06/28/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0/).

![Eine Darstellung der Durchsatz und mehr Fehlertoleranz für verschiedene NIC-Konfigurationen](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig5.png)  
**Abbildung5: Durchsatz und mehr Fehlertoleranz für verschiedene NIC conifigurations**   

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen  
**Werden alle Netzwerkkarten in einem Multi-NIC-Netzwerk werden für die Cluster-Takt verwendet?**  
    Ja.  

**Kann ein Multi-NIC-Netzwerk für Clusterkommunikation werden verwendet? Oder kann es nur zum Client und die Clusterkommunikation?**  
    Entweder Konfiguration funktioniert – alle Clusterrollen Netzwerk auf einem Multi-NIC-Netzwerk genutzt werden.  

**Wird SMB Multichannel auch für CSV und Clusterdatenverkehr verwendet?**  
    Ja, werden standardmäßig alle Cluster und CSV-Datenverkehr verwenden verfügbaren Multi-NIC-Netzwerken. Administratoren können die Failover-Clusterunterstützung PowerShell-Cmdlets oder den Failovercluster-Manager UI so ändern Sie die Netzwerkrolle verwenden.  

**Wie kann ich die SMB Multichannel-Einstellungen anzeigen?**  
    Verwenden der **Get-SMBServerConfiguration** -Cmdlet, suchen Sie nach dem Wert der Eigenschaft EnableMultiChannel.  

**Ist die allgemeine Clustereigenschaft, die plumballcrosssubnetroutes berücksichtigt, in einem Multi-NIC-Netzwerk?**  
     Ja.  

## <a name="see-also"></a>Siehe auch  
- [Neues beim Failoverclustering in Windows Server](whats-new-in-failover-clustering.md)  
