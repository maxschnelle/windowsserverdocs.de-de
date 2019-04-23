---
title: Failover-clustering hardwareanforderungen und Speicheroptionen
description: Hardwareanforderungen und Speicheroptionen für das Erstellen eines Failoverclusters.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4706372b06d0554196b692c3ddcda145dee5bae5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848171"
---
# <a name="failover-clustering-hardware-requirements-and-storage-options"></a>Failover-clustering hardwareanforderungen und Speicheroptionen

Gilt für: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

Zum Erstellen eines Failoverclusters benötigen Sie die folgende Hardware. Die Unterstützung durch Microsoft setzt voraus, dass alle Hardware für die ausgeführte Version von Windows Server zertifiziert ist und die komplette Failoverclusterlösung alle Tests im Konfigurationsüberprüfungs-Assistenten besteht. Weitere Informationen zum Überprüfen eines Failoverclusters finden Sie unter [Überprüfen der Hardware für einen Failovercluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>).

- **Server**: Es wird empfohlen, eine Reihe übereinstimmender Computer mit identischen oder ähnlichen Komponenten zu verwenden.
- **Netzwerkadapter und Kabel (für die Netzwerkkommunikation)**: Wenn Sie iSCSI verwenden, sollten alle Netzwerkadapter entweder für die Netzwerkkommunikation oder für iSCSI, nicht jedoch für beides verwendet werden.

    Vermeiden Sie in der Netzwerkinfrastruktur, über die die Clusterknoten verbunden sind, die Verwendung von Komponenten, deren Ausfall einen Ausfall des Gesamtsystems zur Folge hätte. Sie können die Clusterknoten z. B. durch mehrere unterschiedliche Netzwerke verbinden. Alternativ können Sie die Clusterknoten mit einem Netzwerk, das erstellt wird, verbinden, mit Netzwerkadapterteams, redundanten Switches, redundanten Routern oder ähnlicher Hardware besteht, der einzelne Fehlerpunkte beseitigt.

    >[!NOTE]
    >Wenn Sie Clusterknoten nur mit einem Netzwerk verbinden, erfüllt das Netzwerk die Redundanzanforderung des Konfigurationsüberprüfungs-Assistenten. Der Bericht des Assistenten enthält aber eine Warnung, dass das Netzwerk keine einzelnen Fehlerpunkte enthalten sollte.

- **Gerätecontroller oder entsprechende Adapter für den Speicher**:

  - **SAS (Serial Attached SCSI) oder Fibre Channel**: Wenn Sie SAS oder Fibre Channel verwenden, sollten alle Elemente des Speicherstapels aller geclusterten Server identisch sein. Er verlangt, dass das Multipfad e/a (MPIO)-Software identisch sein und die Software für Geräte bestimmten Modul (DSM) identisch sein. Es wird empfohlen, die Massenspeicher-Gerätecontroller: der Host bus Hostbusadapter (HBA), HBA-Treiber und HBA-Firmware, zugeordnet sind Clusterspeicher identisch sein. Wenn Sie unterschiedliche HBAs verwenden, sollten Sie gemeinsam mit dem Speicheranbieter überprüfen, ob die unterstützten oder empfohlenen Konfigurationen eingehalten werden.
  - **iSCSI**: Wenn Sie iSCSI verwenden, sollte jeder Clusterserver über mindestens einen Netzwerkadapter oder HBA verfügen, der dem Clusterspeicher zugewiesen ist. Das für iSCSI verwendete Netzwerk sollte nicht für die Netzwerkkommunikation verwendet werden. Die zum Herstellen von Verbindungen mit dem iSCSI-Speicherziel verwendeten Netzwerkadapter müssen für alle Clusterserver identisch sein, und es empfiehlt sich, Gigabit Ethernet oder höher zu verwenden.
- **Speicher**: Verwenden Sie ["direkte Speicherplätze"](../storage/storage-spaces/storage-spaces-direct-overview.md) oder freigegebenen Speicher, die mit Windows Server 2012 R2 oder Windows Server 2012 kompatibel ist. Sie können angeschlossenen freigegebenen Speicher verwenden, und Sie können auch SMB 3.0-Dateifreigaben als freigegebener Speicher für Server, auf dem Hyper-V ausgeführt werden, die in einem Failovercluster konfiguriert sind. Weitere Informationen finden Sie unter [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>).

    In den meisten Fällen sollte der angeschlossene Speicher mehrere separate, auf Hardwareebene konfigurierte Datenträger (logische Gerätenummern bzw. LUNs) enthalten. In einigen Clustern fungiert ein Datenträger als Datenträgerzeuge (siehe Beschreibung am Ende dieses Unterabschnitts). Andere Datenträger enthalten die erforderlichen Dateien für die Clusterrollen (früher bezeichnet als Clusterdienste oder -anwendungen). Die Speicheranforderungen beinhalten Folgendes:

  - Um die systemeigene, im Failoverclustering enthaltene Datenträgerunterstützung verwenden zu können, müssen anstelle von dynamischen Datenträgern Basisdatenträger verwendet werden.
  - Es wird empfohlen, die Partitionen mit NTFS zu formatieren. Wenn Sie freigegebene Clustervolumes (CSVs) verwenden, müssen diese jeweils über NTFS-Partitionen verfügen.

    >[!NOTE]
    >Wenn Sie für Ihre Quorumkonfiguration über einen Datenträgerzeugen verfügen, können Sie den Datenträger entweder mit NTFS oder ReFS (Resilient File System) formatieren.

  - Als Partitionsstil des Datenträgers können Sie entweder MBR (Master Boot Record) oder GPT (GUID-Partitionstabelle) verwenden.

    Ein Zeugendatenträger ist ein Datenträger im Clusterspeicher, auf dem eine Kopie der Clusterkonfigurationsdatenbank gespeichert ist. Ein Failovercluster besitzt nur dann einen Zeugendatenträger, wenn dies als Teil der Quorumkonfiguration angegeben ist. Weitere Informationen finden Sie unter [Understanding Quorum in "direkte Speicherplätze"](../storage/storage-spaces/understand-quorum.md).

## <a name="hardware-requirements-for-hyper-v"></a>Hardwareanforderungen für Hyper-V

Wenn Sie einen Failovercluster erstellen, der virtuelle Clustercomputer einbezieht, müssen die Clusterserver die Hardwareanforderungen für die Hyper-V-Rolle unterstützen. Für Hyper-V ist ein 64-Bit-Prozessor erforderlich, der Folgendes einschließt:

- Hardwareunterstützte Virtualisierung. Diese ist für Prozessoren mit Virtualisierungsoption verfügbar, insbesondere für Prozessoren mit Intel VT (Intel Virtualization Technology)- oder AMD-V (AMD Virtualization)-Technologie.
- Von der Hardware erzwungene Datenausführungsverhinderung (DEP) muss verfügbar und aktiviert sein. Das heißt, Sie müssen Intel XD-Bit (Execute Disable Bit) oder AMD NX-Bit (No Execute Bit) aktivieren.

Weitere Informationen über die Hyper-V-Rolle finden Sie unter [Hyper-V: Übersicht](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831531(v%3dws.11)>).

## <a name="deploying-storage-area-networks-with-failover-clusters"></a>Bereitstellen von SANs (Storage Area Networks) mit Failoverclustern

Befolgen Sie die folgenden Richtlinien, wenn Sie ein SAN mit einem Failovercluster bereitstellen:

- **Stellen Sie die Kompatibilität des Speichers sicher**: Stellen Sie gemeinsam mit den Herstellern und Anbietern sicher, dass der Speicher einschließlich der für den Speicher verwendeten Treiber, Firmware und Software mit Failoverclustern mit der von Ihnen ausgeführten Windows Server-Version kompatibel ist.
- **Isolieren Sie Speichergeräte, jeweils ein Cluster pro Gerät**: Server unterschiedlicher Cluster dürfen nicht auf dieselben Speichergeräte zugreifen. In den meisten Fällen muss eine LUN, die für eine Gruppe mit Clusterservern verwendet wird, durch LUN-Masking oder -Zonen von allen anderen Servern isoliert werden.
- **Verwenden Sie ggf. Multipfad-E/A-Software oder ein Netzwerkadapterteam**: In einem Speicherfabric mit hoher Verfügbarkeit können Sie Failovercluster mithilfe von Multipfad-E/A-Software oder eines Netzwerkadapterteams (auch als Lastenausgleich und Failover oder LBFO bezeichnet) mit mehreren Hostbusadaptern bereitstellen. Auf diese Weise erhalten Sie den höchsten Grad an Redundanz und Verfügbarkeit. Für Windows Server 2012 R2 oder Windows Server 2012 muss die multipfadlösung auf Microsoft Multipfad-e/a (MPIO) basieren. Die meisten Hardwarehersteller stellen ein gerätespezifisches MPIO-Modul (DSM) für die Hardware bereit, obwohl Windows Server mindestens ein DSM als Bestandteil des Betriebssystems enthält.

    Weitere Informationen zu LBFO finden Sie unter [NIC-Teamvorgang: Übersicht](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming) in der technischen Bibliothek für Windows Server.

    >[!IMPORTANT]
    >Bei Hostbusadaptern und der MPIO-Software muss möglicherweise genau auf die Version geachtet werden. Wenn Sie für Ihren Cluster eine Multipfadlösung implementieren, sollten Sie die richtigen Adapter sowie die Firm- und Software für die von Ihnen ausgeführte Version von Windows Server in enger Zusammenarbeit mit dem Hardwarehersteller auswählen.

- **Verwenden Sie ggf. "Speicherplätze"**: Wenn Sie planen, bereitzustellen, Serial angefügten Speicher SCSI (SAS) gruppiert, die mithilfe von Speicherplätzen konfiguriert ist, finden Sie unter [Bereitstellen von Clusterspeicherplätzen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>) für die Anforderungen.

## <a name="more-information"></a>Weitere Informationen

- [Failover-Clusterunterstützung](failover-clustering.md)
- [Speicherplätze](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831739(v%3dws.11)>)
- [Verwenden von Gastclustering für hohe Verfügbarkeit](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)