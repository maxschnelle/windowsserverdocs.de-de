---
ms.assetid: a6343f1c-e9dd-4a02-91ad-39bd519d66cd
title: Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: RobHindman
ms.author: robhind
ms.date: 09/15/2016
ms.openlocfilehash: 1b9271ceac99ac9b21cbfac902ba133d66815df4
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476117"
---
# <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a>Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke

> Gilt für: Windows Server 2019, Windows Server 2016

Vereinfachte SMB Multichannel- und Multi -<abbr title="Netzwerkschnittstellenkarte">NIC</abbr> Clusternetzwerke ist ein Feature, das die Verwendung von mehreren NICs auf den desselben clusternetzwerksubnetzes ermöglicht und SMB Multichannel automatisch aktiviert.

Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke bietet die folgenden Vorteile:  
- Failover-Clusterunterstützung automatisch alle NICs auf Knoten, die den gleichen Switch verwenden, erkennt / demselben Subnetz – keine zusätzliche Konfiguration erforderlich.  
- SMB Multichannel wird automatisch aktiviert.  
- Netzwerke, die nur IPv6-Link lokalen (fe80) IP-Adressen-Ressourcen werden in nur Cluster-(privat) Netzwerken erkannt.  
- Eine einzelne IP-Adressressource ist auf jeden (Cluster Access Point, CAP) Network Name (NN) standardmäßig konfiguriert.  
- Nicht mehr die clustervalidierung Warnmeldungen, wenn mehrere NICs im selben Subnetz gefunden werden.  

## <a name="requirements"></a>Anforderungen  
-   Mehrere NICs pro Server, mit dem gleichen Switch / Subnetz.  

## <a name="how-to-take-advantage-of-multi-nic-clusters-networks-and-simplified-smb-multichannel"></a>Nutzen von Multi-NIC-Netzwerken und vereinfachte SMB Multichannel--Clustern  
Dieser Abschnitt beschreibt, wie Sie das neue Multi-NIC-Cluster-Netzwerke und vereinfachte SMB multichannel-Features nutzen.  

### <a name="use-at-least-two-networks-for-failover-clustering"></a>Verwenden Sie mindestens zwei Netzwerke für Failover-Clusterunterstützung   
Obwohl es nur selten auftritt, Netzwerkswitches können ein Fehler auftreten – weiterhin empfohlen, mindestens zwei Netzwerke für Failover-Clusterunterstützung zu verwenden. Alle Netzwerke, die gefunden wurden, werden für clustertakte verwendet. Verwenden Sie ein einzelnes Netzwerk, für den Failovercluster, um eine einzelne Fehlerquelle zu vermeiden. Im Idealfall, dürfen sich mehrere physische Kommunikationspfade zwischen Knoten im Cluster, und keine einzelne Fehlerquelle.  

![Abbildung zwei Netzwerke für Failover-Clusterunterstützung](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig1.png)  
**Abbildung 1: Verwenden Sie mindestens zwei Netzwerke für Failover-Clusterunterstützung**  

### <a name="use-multiple-nics-across-clusters"></a>Verwenden mehrerer NICs für Cluster  

Maximalen Nutzen aus den vereinfachten SMB Multichannel wird erreicht, wenn mehrere NICs für Cluster - in Speicher- und speichercluster-Workload verwendet werden. Dadurch wird die arbeitsauslastung-Cluster (Hyper-V, SQL Server-Failoverclusterinstanz, Funktion "Speicherreplikat", usw.), verwenden Sie SMB Multichannel und Ergebnisse in eine effizientere Nutzung des Netzwerks. Klicken Sie in einem zusammengeführten (auch bekannt als getrennte) Clusterkonfiguration, in denen ein Dateiservercluster mit horizontaler dient zum Speichern von Arbeitsauslastungsdaten für Hyper-V oder SQL Server-Failoverclusterinstanz Cluster dieses Netzwerk wird häufig als "die Nord-Süd-Subnetz" bezeichnet, / Netzwerk . Viele Kunden Maximieren des Durchsatzes des Netzwerks durch eine Investition in die RDMA-fähige Netzwerkkarten und Switches.  

![Abbildung eines Nord-Süd-SMB-Subnetzes](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig2.png)  
**Abbildung 2: Um maximale Netzwerk-Durchsatz zu erzielen, verwenden Sie mehrere NICs auf dem Dateiservercluster mit horizontaler und die Hyper-V- oder SQL Server-Failoverclusterinstanz-Clusters – die die Nord-Süd-Subnetz freigeben**  

![Abbildung von zwei Clustern mit mehreren Netzwerkkarten im gleichen Subnetz, SMB Multichannel nutzen](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig3.png)  
**Abbildung 3: Zwei Cluster (Scale-Out File Server für SQL Server-Speicher <abbr title="Clustering Failoverinstanz">FCI</abbr> für die arbeitsauslastung) beide mehrere NICs im selben Subnetz verwenden, um SMB Multichannel nutzen und erzielen bessere Netzwerk Durchsatz.** 

## <a name="automatic-recognition-of-ipv6-link-local-private-networks"></a>Automatische Erkennung von IPv6-Link lokale private Netzwerke  
Wenn Private (nur Cluster)-Netzwerke mit mehreren Netzwerkkarten erkannt werden, erkennt der Cluster automatisch IPv6 Link-Local (fe80) IP-Adressen für jede NIC, die in jedem Subnetz. Dieser Zeitaufwand der Administratoren, da sie nicht mehr manuell konfigurieren, IPv6-Link lokalen (fe80) IP-Adressressourcen müssen.  

Wenn Sie mehr als ein privates (nur Cluster)-Netzwerk zu verwenden, überprüfen Sie die IPv6-routing-Konfiguration, um sicherzustellen, dass das routing nicht konfiguriert ist Subnetze überschreiten, da dadurch die Leistung des Netzwerks verringert wird.  

![Abbildung der automatische Netzwerkkonfiguration in der Failovercluster-Manager-UI](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig4.png)  
**Abbildung 4: Automatische IPv6-Link lokale (fe80) Adresse Ressourcenkonfiguration**  

## <a name="throughput-and-fault-tolerance"></a>Durchsatz und Fehlertoleranz  
2019 für Windows Server und Windows Server 2016 automatisch erkennen NIC-Funktionen, und versucht, jeder NIC in der Konfiguration der schnellste Möglichkeit verwenden. Netzwerkkarten, die in einem Team verwendet werden, Netzwerkkarten mithilfe von RSS und NICs mit RDMA-Funktion können alle verwendet werden. Der Tabelle unten sind die vor-und Nachteile der Verwendung dieser Technologien. Maximaler Durchsatz wird erreicht, wenn Sie mehrere RDMA-fähige NICs verwenden. Weitere Informationen finden Sie unter [die Grundlagen der SMB-Mutlichannel](https://blogs.technet.microsoft.com/josebda/2012/06/28/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0/).

![Eine Abbildung der Durchsatz und mehr Fehlertoleranz für verschiedene NIC-Konfigurationen](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig5.png)  
**Abbildung 5: Durchsatz und mehr Fehlertoleranz für verschiedene NIC conifigurations**   

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen  
**Werden alle NICs in einem Netzwerk mit mehreren NICs werden für die Cluster-Takt verwendet?**  
    Ja.  

**Kann ein Netzwerk mit mehreren Netzwerkkarten für Clusterkommunikation werden verwendet? Oder kann es nur verwendet werden für die Kommunikation zwischen Client und -Cluster?**  
    Entweder Konfiguration funktioniert – alle clusterrollen Netzwerk werden in einem Netzwerk mit mehreren Netzwerkkarten arbeiten.  

**Wird für den Datenverkehr für CSV und -Cluster auch SMB Multichannel verwendet?**  
    Ja, werden standardmäßig alle Cluster und CSV-Datenverkehr verfügbar Multi-NIC-Netzwerke verwenden. Administratoren können die Failover-Clustering-PowerShell-Cmdlets oder der Failovercluster-Manager UI verwenden, ändern die Netzwerkrolle.  

**Wie kann ich die SMB Multichannel-Einstellungen anzeigen?**  
    Verwenden der **Get-SMBServerConfiguration** -Cmdlet, suchen Sie nach dem Wert der Eigenschaft EnableMultiChannel.  

**Ist der allgemeine Clustereigenschaft, die PlumbAllCrossSubnetRoutes berücksichtigt in einem Netzwerk mit mehreren Netzwerkkarten?**  
     Ja.  

## <a name="see-also"></a>Siehe auch  
- [Neues beim Failoverclustering in WindowsServer](whats-new-in-failover-clustering.md)  
