---
ms.assetid: a6343f1c-e9dd-4a02-91ad-39bd519d66cd
title: Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke
ms.topic: article
author: RobHindman
ms.author: robhind
ms.date: 09/15/2016
ms.openlocfilehash: 1abaf439a25e5175aba7290c0600c0f5b56db0d4
ms.sourcegitcommit: 6c53a7d37b4884212469c38dc97c192cd767e49b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/19/2020
ms.locfileid: "94919382"
---
# <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a>Vereinfachte SMB Multichannel- und Multi-NIC-Clusternetzwerke

> Gilt für: Windows Server 2019, Windows Server 2016

Vereinfachtes SMB Multichannel und Multi-<abbr title="Netzwerkschnittstellenkarte">NIC</abbr> Cluster Netzwerke sind ein Feature, das die Verwendung mehrerer NICs im gleichen clusternetzwerksubnetz ermöglicht und SMB Multichannel automatisch aktiviert.

Vereinfachte SMB Multichannel-und Multi-NIC-Cluster Netzwerke bieten folgende Vorteile:
- Failoverclustering erkennt automatisch alle NICs auf Knoten, die denselben Switch/dasselbe Subnetz verwenden. es ist keine zusätzliche Konfiguration erforderlich.
- SMB Multichannel wird automatisch aktiviert.
- Netzwerke, die nur über IPv6-Verbindungs lokale (FE80) IP-Adress Ressourcen verfügen, werden in reinen Cluster Netzwerken (private Netzwerke) erkannt.
- Standardmäßig wird für jeden Netzwerknamen (Cap) des Cluster Zugriffs Punkts eine einzelne IP-Adress Ressource konfiguriert.
- Die Cluster Überprüfung gibt keine Warnmeldungen mehr aus, wenn mehrere NICs im selben Subnetz gefunden werden.

## <a name="requirements"></a>Requirements (Anforderungen)
-   Mehrere NICs pro Server mit demselben Switch/Subnetz.

## <a name="how-to-take-advantage-of-multi-nic-clusters-networks-and-simplified-smb-multichannel"></a>Nutzen von multinic-Cluster Netzwerken und vereinfachtem SMB Multichannel
In diesem Abschnitt wird beschrieben, wie Sie die neuen multinic-Cluster Netzwerke und die vereinfachten SMB Multichannel-Features nutzen können.

### <a name="use-at-least-two-networks-for-failover-clustering"></a>Verwenden von mindestens zwei Netzwerken für Failoverclustering
Obwohl es selten vorkommt, können Netzwerk Switches fehlschlagen. es wird immer noch empfohlen, mindestens zwei Netzwerke für das Failoverclustering zu verwenden. Alle gefundenen Netzwerke werden für Cluster Takte verwendet. Vermeiden Sie die Verwendung eines einzelnen Netzwerks für den Failovercluster, um eine Single Point of Failure zu vermeiden. Im Idealfall sollten mehrere physische Kommunikations Pfade zwischen den Knoten im Cluster und keine Single Point of Failure vorhanden sein.

![Darstellung von zwei Netzwerken für Failoverclustering ](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig1.png)
 **Abbildung 1: Verwenden von mindestens zwei Netzwerken für Failoverclustering**

### <a name="use-multiple-nics-across-clusters"></a>Cluster übergreifende Verwendung mehrerer NICs

Der größte Vorteil des vereinfachten SMB Multichannel wird erzielt, wenn mehrere NICs Cluster übergreifend in Speicher-und Speicher-Arbeits Auslastungs Clustern verwendet werden. Dadurch können Arbeits Auslastungs Cluster (Hyper-V, SQL Server-Failoverclusterinstanz, Speicher Replikat usw.) SMB Multichannel verwenden und eine effizientere Verwendung des Netzwerks erzielen. In einer konvergenten (auch disaggregierten) Cluster Konfiguration, in der ein Datei Server Cluster mit horizontaler Skalierung zum Speichern von Arbeits Auslastungs Daten für einen Hyper-V-oder SQL Server failoverclusterinstanzcluster verwendet wird, wird dieses Netzwerk häufig als "das North-South Subnetz"/Netzwerk bezeichnet. Viele Kunden maximieren den Durchsatz dieses Netzwerks, indem Sie in RDMA-fähige NIC-Karten und-Switches investieren.

![Abbildung 2: Verwenden eines North-South SMB-Subnetzes ](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig2.png)
 **: um einen maximalen Netzwerk Durchsatz zu erreichen, verwenden Sie mehrere Netzwerkkarten im Datei Server Cluster mit horizontaler Skalierung und den Hyper-V-oder SQL Server failoverclusterinstanzcluster, die das North-South Subnetz gemeinsam verwenden** .

![ScreenCap von zwei Clustern mit mehreren Netzwerkkarten im gleichen Subnetz zum Nutzen von SMB Multichannel ](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig3.png)
 **Abbildung 3: zwei Cluster (Datei Server mit horizontaler Skalierung für Speicher, SQL Server <abbr title=" Failoverclusterinstanz- "> FCI </abbr> für die Arbeitsauslastung) verwenden beide mehrere NICs im gleichen Subnetz, um SMB Multichannel zu nutzen und einen besseren Netzwerk Durchsatz zu erzielen.**

## <a name="automatic-recognition-of-ipv6-link-local-private-networks"></a>Automatische Erkennung von IPv6-Link-lokalen privaten Netzwerken
Wenn private Netzwerke (nur Cluster) mit mehreren Netzwerkkarten erkannt werden, erkennt der Cluster automatisch IPv6-Link Local (FE80)-IP-Adressen für jede NIC in jedem Subnetz. Dies spart Administratoren Zeit, da Sie IPv6-Verknüpfungs lokale (FE80) IP-Adress Ressourcen nicht mehr manuell konfigurieren müssen.

Wenn Sie mehr als ein privates Netzwerk (nur Cluster) verwenden, überprüfen Sie die IPv6-Routing Konfiguration, um sicherzustellen, dass das Routing nicht für Subnetze konfiguriert ist, da dadurch die Netzwerkleistung reduziert wird.

![ScreenCap der automatischen Netzwerkkonfiguration in der Failovercluster-Manager-Benutzeroberfläche ](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig4.png)
 **Abbildung 4: automatische IPv6-Verbindungs Konfiguration (FE80) Adress Ressourcen Konfiguration**

## <a name="throughput-and-fault-tolerance"></a>Durchsatz und Fehlertoleranz
Mit Windows Server 2019 und Windows Server 2016 werden NIC-Funktionen automatisch erkannt, und es wird versucht, jede NIC in der schnellstmöglichen Konfiguration zu verwenden. NICs, die kombiniert werden, NICs mit RSS und NICs mit RDMA-Funktion können verwendet werden. In der folgenden Tabelle werden die Kompromisse bei der Verwendung dieser Technologien zusammengefasst. Maximaler Durchsatz wird erzielt, wenn mehrere RDMA-fähige NICs verwendet werden. Weitere Informationen finden Sie [Untergrund lagen von SMB Multichannel](/archive/blogs/josebda/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0).

![Eine Abbildung des Durchsatzes und der Fehlertoleranz für verschiedene NIC-Konfigurationen ](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig5.png)
 **Abbildung 5: Durchsatz und Fehlertoleranz für verschiedene NIC-Konfigurationen**

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen
**Befinden sich alle NICs in einem Netzwerk mit mehreren Netzwerkkarten, die für Cluster-Herzschläge verwendet werden?**
Ja.

**Kann ein Netzwerk mit mehreren NIC nur für die Cluster Kommunikation verwendet werden? Oder kann Sie nur für die Kommunikation zwischen Client und Cluster verwendet werden?**
Beide Konfigurationen funktionieren. alle Cluster Netzwerk Rollen funktionieren in einem Netzwerk mit mehreren NIC.

**Wird SMB Multichannel auch für CSV-und Cluster Datenverkehr verwendet?**
Ja, standardmäßig werden für den gesamten Cluster-und CSV-Datenverkehr verfügbare multinic-Netzwerke verwendet. Administratoren können die PowerShell-Cmdlets für Failoverclustering oder Failovercluster-Manager-Benutzeroberfläche verwenden, um die Netzwerk Rolle zu ändern.

**Wie kann ich die SMB Multichannel-Einstellungen sehen?**
Verwenden Sie das Cmdlet **Get-smbserverconfiguration** , und suchen Sie nach dem Wert der **enablemultichannel** -Eigenschaft.

**Wird die allgemeine Cluster Eigenschaft "plumballcrosssubnettrotroutes" in einem Netzwerk mit mehreren NIC beachtet?**
Ja.

## <a name="additional-references"></a>Weitere Verweise
- [Neues beim Failoverclustering unter Windows Server](whats-new-in-failover-clustering.md)