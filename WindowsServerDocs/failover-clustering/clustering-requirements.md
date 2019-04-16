---
title: Failover clustering hardwareanforderungen und Speicheroptionen
description: Hardware- und Speicheroptionen für das Erstellen eines Failoverclusters.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4706372b06d0554196b692c3ddcda145dee5bae5
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082195"
---
# <a name="failover-clustering-hardware-requirements-and-storage-options"></a>Failover clustering hardwareanforderungen und Speicheroptionen

Betrifft: Windows Server 2012 R2, WindowsServer 2012 und WindowsServer 2016

Sie benötigen die folgenden Hardware zum Erstellen eines Failoverclusters. Von Microsoft unterstützt wird, muss die gesamte Hardware zertifiziert werden für die Version von Windows Server, auf dem Sie ausgeführt werden, und die vollständige Failoverlösung Cluster muss alle Tests unter Überprüfen einen Konfigurations-Assistenten übergeben. Weitere Informationen zu einen Failovercluster überprüfen finden Sie unter [Überprüfen der Hardware für einen Failovercluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>).

- **Server**: Es wird empfohlen, dass Sie eine Reihe von Computern, die mit den gleichen oder ähnlichen Komponenten verwenden.
- **Netzwerkadapter und Kabel (für die Netzwerkkommunikation)**: Wenn Sie iSCSI verwenden, jeden Netzwerkadapter sollte die dedizierte Netzwerkkommunikation oder iSCSI, nicht beides.

    Vermeiden Sie in der Netzwerkinfrastruktur, die die Clusterknoten verbindet einzelne Fehlerquellen. Sie können beispielsweise die Clusterknoten verbinden, von mehreren unterschiedlichen Netzwerken. Alternativ können Sie Ihre Knoten im Cluster mit einem einzelnen Netzwerk, das erstellt wird verbinden, mit Netzwerkadaptern, redundante Switches, redundante Router oder ähnliche Hardware, mit der einzelne Fehlerquellen entfernt.

    >[!NOTE]
    >Wenn Sie den Knoten im Cluster mit einem einzelnen Netzwerk verbinden, wird im Netzwerk in die Gültigkeit einer Konfigurations-Assistenten für die Redundanz-Anforderung übergeben. Der Bericht über den Assistenten wird jedoch eine Warnung enthalten, die im Netzwerk nicht einzelne Fehlerquellen verfügen soll.

- **Gerätecontroller oder entsprechende Adapter für den Speicher**:

  - **Serial Attached SCSI oder Fibre Channel**: Wenn Sie alle gruppierten Server Serial Attached SCSI oder Fibre Channel verwenden, sollten alle Elemente des Stapels Speicher identisch sein. Es ist, die Multipfad e/a (MPIO) Software identisch sein und die Software Gerät bestimmten Modul (DSM) identisch ist erforderlich. Es wird empfohlen, die die Massenspeichergerät Controller – der Host-Bus-Adapter (HBA), HBA-Treiber und HBA Firmware – zugeordnet sind Cluster-Speicher identisch sein. Wenn Sie unterschiedliche HBAs verwenden, sollten Sie mit der Speicheranbieter sicherstellen, dass Sie ihre unterstützten oder empfohlenen Konfigurationen folgen.
  - **iSCSI**: Wenn Sie iSCSI verwenden, sollte jeder gruppierter Server verfügen, eine oder mehrere Netzwerkadapter oder, den für den Clusterspeicher vorgesehen sind. Das Netzwerk, das Sie für iSCSI verwenden sollte nicht für die Kommunikation verwendet werden. Alle gruppierten Server die Netzwerkadapter, die Sie für die Verbindung an das Ziel des iSCSI-Speicher verwenden sollten übereinstimmen, und es wird empfohlen, für die Verwendung von Gigabit-Ethernet- oder höher.
- **Speicher**: Sie müssen [Speicher Leerzeichen direkte](../storage/storage-spaces/storage-spaces-direct-overview.md) verwenden oder gemeinsam genutzter Speicher, die mit Windows Server 2012 R2 oder Windows Server 2012 kompatibel ist. Freigegebenen Speicher, der angefügt werden können, und Sie können auch Dateifreigaben SMB 3.0 als freigegebener Speicher für Server, auf dem Hyper-V ausgeführt werden, die in einem Failovercluster konfiguriert sind. Weitere Informationen finden Sie unter [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>).

    In den meisten Fällen sollten angeschlossenen Speicher enthalten mehrere, separate Datenträger (logische Gerätenummern oder LUNs), die auf Hardware-Ebene konfiguriert sind. Für einige Cluster fungiert ein Datenträger als Datenträger Zeuge (am Ende dieses Unterabschnitts beschrieben). Weitere Festplatten enthalten erforderlichen Dateien für die gruppierten Rollen (früher als geclusterten Diensten oder Anwendungen bezeichnet). Speicheranforderungen umfassen Folgendes:

  - Verwenden Sie Basisdatenträger, keine dynamischen Datenträgern, für die Verwendung die systemeigenen Unterstützung in der Failover-Clusterunterstützung enthalten.
  - Es wird empfohlen, dass Sie die Partitionen mit NTFS formatieren. Wenn Sie Cluster Shared Volumes (CSV) verwenden, muss die Partition für jede dieser NTFS sein.

    >[!NOTE]
    >Wenn Sie ein Zeuge Datenträger für Ihre Quorumkonfiguration verfügen, können Sie den Datenträger mit entweder NTFS oder ausfallsichere File System (ReFS) formatieren.

  - Für die Partition Formatvorlage des Datenträgers können Sie entweder MBR (MBR) oder GUID-Partitionstabelle (GPT).

    Ein Zeuge Datenträger ist ein Datenträger im Cluster, die zum Speichern einer Kopie der Datenbank mit der Clusterkonfiguration festgelegt wurde. Ein Failovercluster hat ein Zeuge Datenträger nur, wenn dies als Teil der Quorumkonfiguration angegeben wird. Weitere Informationen finden Sie unter [Grundlegendes zu Quorum im Speicher Leerzeichen Direct](../storage/storage-spaces/understand-quorum.md).

## <a name="hardware-requirements-for-hyper-v"></a>Hardwareanforderungen für Hyper-V

Wenn Sie einen Failovercluster erstellen, der gruppierte virtuelle Computer enthält, müssen der Cluster-Server die hardwareanforderungen für Hyper-V-Rolle unterstützen. Hyper-V erfordert einen 64-Bit-Prozessor, der Folgendes umfasst:

- Hardwareunterstützte Virtualisierung Diese Option ist verfügbar in Prozessoren, die eine Virtualisierungsoption enthalten – speziell Prozessoren mit Intel Virtualization Technology (Intel VT) oder AMD Virtualization (AMD-V)-Technologie.
- Hardwaregestützte Daten Datenausführungsverhinderung (DEP) muss verfügbar und aktiviert sein. Sie müssen insbesondere aktivieren Intel XD-bit (execute Disable Bit) oder AMD NX-Bit (keine Execute-Bit).

Weitere Informationen zu Hyper-V-Rolle finden Sie unter [Übersicht über Hyper-V](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831531(v%3dws.11)>).

## <a name="deploying-storage-area-networks-with-failover-clusters"></a>Bereitstellen von Storage Area Networks mit Failoverclustern

Wenn Sie ein Storage Area Network (SAN) mit einem Failovercluster bereitstellen, folgen Sie diesen Richtlinien:

- **Kompatibilität des Speichers bestätigen**: Confirm mit Hersteller und Softwarehersteller, die der Speicher, einschließlich Treiber, Firmware und Software für den Speicher sind kompatibel mit Failoverclustern in der Version von Windows Server, auf dem Sie ausgeführt werden.
- **Isolieren von Speichergeräten, einem Cluster pro Gerät**: verschiedene Cluster-Server muss nicht auf die gleichen Speichergeräten zugreifen. In den meisten Fällen sollte eine LUN für eine Gruppe von Cluster-Servern verwendet von allen anderen Servern durch LUN-Maskierung oder-Zonen isoliert werden.
- **Berücksichtigen Sie dabei Multipfad-e/a-Software verwendet oder Netzwerkadapter gearbeitet**: In einer hochverfügbaren Speicher Fabric können Failovercluster mit mehreren Hostbusadapter mithilfe von Multipfad-e/a-Software bereitstellen oder Netzwerk-Adapter teaming (so genannte laden Lastenausgleich und Failover oder LBFO =). Dies bietet den höchsten Grad an Redundanz und Verfügbarkeit. Für Windows Server 2012 R2 oder Windows Server 2012 muss Ihre Multipfad-Lösung auf Microsoft e/a Multipfad-basieren. Hardwarehersteller wird in der Regel ein MPIO gerätespezifische Modul (DSM) für Ihre Hardware angeben, obwohl Windows Server eine oder mehrere DSM als Teil des Betriebssystems enthält.

    Weitere Informationen zu LBFO = finden Sie unter [Übersicht über die NIC-Teaming](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming) in der technischen Bibliothek für Windows Server.

    >[!IMPORTANT]
    >Hostbusadapter und Multipfad-e/a-Software kann sehr vertrauliche Version sein. Wenn Sie für den Cluster Multipfad-Lösung implementieren, arbeiten Sie eng mit Ihren Hardwarehersteller Auswählen der richtigen Adapter, Firmware und Software für die Version von Windows Server, auf dem Sie ausgeführt werden.

- **Berücksichtigen Sie dabei Speicherplätze verwenden**: Wenn Sie planen, serial-attached SCSI (SAS) gruppiert Storage bereitstellen, die mit Speicherplätze konfiguriert ist, finden Sie unter [Bereitstellen gruppierte Speicherplätze](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>) die Anforderungen.

## <a name="more-information"></a>Weitere Informationen

- [Failoverclusterunterstützung](failover-clustering.md)
- [Speicherplätze](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831739(v%3dws.11)>)
- [Hohe Verfügbarkeit durch Gastclustering](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)