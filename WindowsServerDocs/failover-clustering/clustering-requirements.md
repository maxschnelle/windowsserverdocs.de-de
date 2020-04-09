---
title: Hardwareanforderungen und Speicheroptionen für Failoverclustering
description: Hardware Anforderungen und Speicheroptionen zum Erstellen eines Failoverclusters.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
manager: lizross
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: dec242282b0d7a07b8f244a1044134bd8af03f6f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827853"
---
# <a name="failover-clustering-hardware-requirements-and-storage-options"></a>Hardwareanforderungen und Speicheroptionen für Failoverclustering

Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zum Erstellen eines Failoverclusters benötigen Sie die folgende Hardware. Die Unterstützung durch Microsoft setzt voraus, dass alle Hardware für die ausgeführte Version von Windows Server zertifiziert ist und die komplette Failoverclusterlösung alle Tests im Konfigurationsüberprüfungs-Assistenten besteht. Weitere Informationen zum Überprüfen eines Failoverclusters finden Sie unter [Überprüfen der Hardware für einen Failovercluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>).

- **Server**: Wir empfehlen, eine Reihe übereinstimmender PCs mit identischen oder ähnlichen Komponenten zu verwenden.
- **Netzwerkadapter und -kabel (für die Netzwerkkommunikation)** : Wenn Sie iSCSI verwenden, sollte jeder Netzwerkadapter entweder für die Netzwerkkommunikation oder für iSCSI zugewiesen werden, aber nicht für beides.

    Vermeiden Sie in der Netzwerkinfrastruktur, über die die Clusterknoten verbunden sind, die Verwendung von Komponenten, deren Ausfall einen Ausfall des Gesamtsystems zur Folge hätte. Sie können die Clusterknoten z. B. durch mehrere unterschiedliche Netzwerke verbinden. Alternativ können Sie Ihre Cluster Knoten mit einem Netzwerk verbinden, das mit kombinierten Netzwerkadaptern, redundanten Switches, redundanten Routern oder ähnlicher Hardware erstellt wird, die einzelne Fehlerquellen entfernt.

    >[!NOTE]
    >Wenn Sie Clusterknoten nur mit einem Netzwerk verbinden, erfüllt das Netzwerk die Redundanzanforderung des Konfigurationsüberprüfungs-Assistenten. Der Bericht des Assistenten enthält aber eine Warnung, dass das Netzwerk keine einzelnen Fehlerpunkte enthalten sollte.

- **Gerätecontroller oder entsprechende Adapter für den Speicher**:

  - **Serial Attached SCSI oder Fibre Channel**: Wenn Sie Serial Attached SCSI oder Fibre Channel verwenden, sollten alle Elemente des Speicherstapels in allen Clusterservern identisch sein. Es ist erforderlich, dass die Multipfad-e/a-Software (MPIO) identisch ist und dass die DSM-Software (Device Specific Module) identisch ist. Es wird empfohlen, dass die Massenspeichergeräte-Controller – der Hostbus Adapter (HBA), HBA-Treiber und HBA-Firmware – identisch sind, die an den Cluster Speicher angefügt sind. Wenn Sie unterschiedliche HBAs verwenden, sollten Sie gemeinsam mit dem Speicheranbieter überprüfen, ob die unterstützten oder empfohlenen Konfigurationen eingehalten werden.
  - **iSCSI**: Wenn Sie iSCSI verwenden, sollte jeder Clusterserver über mindestens einen Netzwerkadapter oder HBA verfügen, der dem Clusterspeicher zugewiesen ist. Das für iSCSI verwendete Netzwerk sollte nicht für die Netzwerkkommunikation verwendet werden. Die zum Herstellen von Verbindungen mit dem iSCSI-Speicherziel verwendeten Netzwerkadapter müssen für alle Clusterserver identisch sein, und es empfiehlt sich, Gigabit Ethernet oder höher zu verwenden.
- **Speicher**: Sie müssen [direkte Speicherplätze](../storage/storage-spaces/storage-spaces-direct-overview.md) oder freigegebenen Speicher verwenden, der mit Windows Server 2012 R2 oder Windows Server 2012 kompatibel ist. Sie können freigegebenen Speicher verwenden, der angefügt ist, und Sie können auch SMB 3,0-Dateifreigaben als freigegebenen Speicher für Server verwenden, die Hyper-V ausführen und in einem Failovercluster konfiguriert sind. Weitere Informationen finden Sie unter [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>).

    In den meisten Fällen sollte der angeschlossene Speicher mehrere separate, auf Hardwareebene konfigurierte Datenträger (logische Gerätenummern bzw. LUNs) enthalten. In einigen Clustern fungiert ein Datenträger als Datenträgerzeuge (siehe Beschreibung am Ende dieses Unterabschnitts). Andere Datenträger enthalten die erforderlichen Dateien für die Clusterrollen (früher bezeichnet als Clusterdienste oder -anwendungen). Die Speicheranforderungen beinhalten Folgendes:

  - Um die systemeigene, im Failoverclustering enthaltene Datenträgerunterstützung verwenden zu können, müssen anstelle von dynamischen Datenträgern Basisdatenträger verwendet werden.
  - Es wird empfohlen, die Partitionen mit NTFS zu formatieren. Wenn Sie freigegebene Clustervolumes (CSVs) verwenden, müssen diese jeweils über NTFS-Partitionen verfügen.

    >[!NOTE]
    >Wenn Sie für Ihre Quorumkonfiguration über einen Datenträgerzeugen verfügen, können Sie den Datenträger entweder mit NTFS oder ReFS (Resilient File System) formatieren.

  - Als Partitionsstil des Datenträgers können Sie entweder MBR (Master Boot Record) oder GPT (GUID-Partitionstabelle) verwenden.

    Ein Datenträger Zeuge ist ein Datenträger im Cluster Speicher, der eine Kopie der Cluster Konfigurations Datenbank enthalten soll. Ein Failovercluster besitzt nur dann einen Zeugendatenträger, wenn dies als Teil der Quorumkonfiguration angegeben ist. Weitere Informationen finden Sie Untergrund Legendes zu [Quorum in direkte Speicherplätze](../storage/storage-spaces/understand-quorum.md).

## <a name="hardware-requirements-for-hyper-v"></a>Hardwareanforderungen für Hyper-V

Wenn Sie einen Failovercluster erstellen, der virtuelle Clustercomputer einbezieht, müssen die Clusterserver die Hardwareanforderungen für die Hyper-V-Rolle unterstützen. Für Hyper-V ist ein 64-Bit-Prozessor erforderlich, der Folgendes einschließt:

- Hardwareunterstützte Virtualisierung. Diese ist für Prozessoren mit Virtualisierungsoption verfügbar, insbesondere für Prozessoren mit Intel VT (Intel Virtualization Technology)- oder AMD-V (AMD Virtualization)-Technologie.
- Von der Hardware erzwungene Datenausführungsverhinderung (DEP) muss verfügbar und aktiviert sein. Das heißt, Sie müssen Intel XD-Bit (Execute Disable Bit) oder AMD NX-Bit (No Execute Bit) aktivieren.

Weitere Informationen zur Hyper-v-Rolle finden Sie unter [Hyper-v Overview (Übersicht über Hyper-v](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831531(v%3dws.11)>)).

## <a name="deploying-storage-area-networks-with-failover-clusters"></a>Bereitstellen von SANs (Storage Area Networks) mit Failoverclustern

Befolgen Sie die folgenden Richtlinien, wenn Sie ein SAN mit einem Failovercluster bereitstellen:

- Überprüfen Sie **die Kompatibilität des Speichers**: Vergewissern Sie sich bei Herstellern und Anbietern, dass der Speicher einschließlich der für den Speicher verwendeten Treiber, Firmware und Software mit Failoverclustern in der Windows Server-Version kompatibel ist, die Sie ausführen.
- **Isolieren Sie Speichergeräte – ein Cluster pro Gerät**: Server aus unterschiedlichen Clustern dürfen keinen Zugriff auf die gleichen Speichergeräte haben. In den meisten Fällen muss eine LUN, die für eine Gruppe mit Clusterservern verwendet wird, durch LUN-Masking oder -Zonen von allen anderen Servern isoliert werden.
- **Verwenden Sie ggf. Multipfad-E/A-Software oder ein Netzwerkadapterteam**: In einem Speicherfabric mit hoher Verfügbarkeit können Sie Failovercluster mithilfe von Multipfad-E/A-Software oder eines Netzwerkadapterteams (auch als Lastenausgleich und Failover oder LBFO bezeichnet) mit mehreren Hostbusadaptern bereitstellen. Auf diese Weise erhalten Sie den höchsten Grad an Redundanz und Verfügbarkeit. Für Windows Server 2012 R2 oder Windows Server 2012 muss die Multipfadlösung auf Microsoft Multipfad-e/a (MPIO) basieren. Die meisten Hardwarehersteller stellen ein gerätespezifisches MPIO-Modul (DSM) für die Hardware bereit, obwohl Windows Server mindestens ein DSM als Bestandteil des Betriebssystems enthält.

    Weitere Informationen zu LBFO finden Sie unter [NIC Teaming Overview](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming) in der technischen Bibliothek für Windows Server.

    >[!IMPORTANT]
    >Bei Hostbusadaptern und der MPIO-Software muss möglicherweise genau auf die Version geachtet werden. Wenn Sie für Ihren Cluster eine Multipfadlösung implementieren, sollten Sie die richtigen Adapter sowie die Firm- und Software für die von Ihnen ausgeführte Version von Windows Server in enger Zusammenarbeit mit dem Hardwarehersteller auswählen.

- **Verwenden Sie die Verwendung von Speicherplätzen**: Wenn Sie planen, den mit Speicherplätzen konfigurierten SAS-Cluster Speicher (Serial Attached SCSI) bereitzustellen, finden Sie unter Bereitstellen von [Cluster Speicherplätzen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>) die Anforderungen.

## <a name="more-information"></a>Weitere Informationen

- [Failoverclustering](failover-clustering.md)
- [Speicherplätze](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831739(v%3dws.11)>)
- [Verwenden von Gastclustering für hohe Verfügbarkeit](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)