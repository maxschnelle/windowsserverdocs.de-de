---
title: Hardwareanforderungen für Direkte Speicherplätze
ms.prod: windows-server-threshold
description: Mindesthardwareanforderungen zum Testen von „Direkte Speicherplätze“.
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 08/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2f3f8bff39550108b0417b9513bee4a248dca432
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546371"
---
# <a name="storage-spaces-direct-hardware-requirements"></a>Hardwareanforderungen für „Direkte Speicherplätze“

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema werden die Mindesthardwareanforderungen für direkte Speicherplätze beschrieben.

In der Produktionsumgebung empfiehlt Microsoft, eine überprüfte Hardware-/Softwarelösung unserer Partner zu erwerben, die Bereitstellungs Tools und-Verfahren umfasst. Diese Lösungen wurden mit unserer Referenzarchitektur entworfen, zusammengestellt und überprüft, um Kompatibilität und Zuverlässigkeit sicherzustellen, sodass Sie schnell loslegen können. Informationen zu Windows Server 2019-Lösungen finden Sie auf der [Azure Stack HCI Solutions-Website](https://azure.microsoft.com/overview/azure-stack/hci). Informationen zu Windows Server 2016-Lösungen finden Sie unter [Windows Server-Software definiert](https://microsoft.com/wssd).

   > [!TIP]
   > Möchten Sie direkte Speicherplätze auswerten, aber keine Hardware? Verwenden Sie Hyper-V oder Azure Virtual Machines, wie in [Verwenden von direkte Speicherplätze in virtuellen Gastcomputer Clustern](storage-spaces-direct-in-vm.md)beschrieben.

## <a name="base-requirements"></a>Grundvoraussetzungen

Systeme, Komponenten, Geräte und Treiber müssen gemäß dem [Windows Server-Katalog](https://www.windowsservercatalog.com) **Windows Server 2016-zertifiziert** sein. Außerdem wird empfohlen, dass Server, Laufwerke, Hostbus Adapter und Netzwerkadapter über das **Software-Defined Data Center (SDDC) Standard** und/oder das **Software-Defined Data Center (SDDC) Premium** -Standard Qualifizierungen (AQS) wie dargestellt verfügen. untenstehende. Es sind mehr als 1.000 Komponenten mit dem SDDC AQS vorhanden.

![Screenshot des Windows Server-Katalogs mit dem SDDC-AQS](media/hardware-requirements/sddc-aqs.png)

Der vollständig konfigurierte Cluster (Server, Netzwerk und Speicher) muss alle [Cluster Validierungstests](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx) gemäß dem Assistenten in Failovercluster-Manager oder mit dem `Test-Cluster` [Cmdlet](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) in PowerShell bestehen.

Außerdem gelten die folgenden Anforderungen:

## <a name="servers"></a>Server

- Mindestens zwei, maximal 16 Server
- Es wird empfohlen, dass alle Server den gleichen Hersteller und das gleiche Modell aufweisen

## <a name="cpu"></a>CPU

- Intel Nehalem oder höher kompatibler Prozessor; noch
- Mit AMD epyc oder höher kompatibler Prozessor

## <a name="memory"></a>Arbeitsspeicher

- Arbeitsspeicher für Windows Server, VMS und andere apps oder Arbeits Auslastungen; ZZ
- 4 GB RAM pro Terabyte (TB) der Cache Laufwerks Kapazität auf jedem Server, für direkte Speicherplätze-Metadaten

## <a name="boot"></a>Starten

- Alle Start Geräte, die von Windows Server unterstützt werden und [nun SATADOM enthalten](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/)
- RAID 1-Spiegel ist **nicht** erforderlich, wird jedoch für den Start unterstützt.
- Empfohlen: Mindestgröße von 200 GB

## <a name="networking"></a>Netzwerk

Direkte Speicherplätze erfordert eine zuverlässige Netzwerkverbindung mit hoher Bandbreite und geringer Latenz zwischen den einzelnen Knoten.  

Minimale Verbindungs Verbindung für kleinen 2-3-Knoten
- Netzwerkschnittstellenkarte (NIC) mit 10 Gbit/s oder schneller
- Zwei oder mehr Netzwerkverbindungen von jedem Knoten, der für Redundanz und Leistung empfohlen wird

Empfohlene Interverbindung für hohe Leistung, Skalierbarkeit oder bereit Stellungen von 4 und höher 
- NICs, die RDMA (Remote Direct Memory Access), IWarp (empfohlen) oder ROCE sind
- Zwei oder mehr Netzwerkverbindungen von jedem Knoten, der für Redundanz und Leistung empfohlen wird
- Netzwerkkarte mit 25 Gbit/s oder schneller

Umgeschaltete oder switchlose Knoten Verbindungen
- Einschalten Netzwerk Switches müssen ordnungsgemäß für die Handhabung der Bandbreite und des Netzwerk Typs konfiguriert werden.  Wenn Sie RDMA verwenden, das das ROCE-Protokoll implementiert, ist die Netzwerkgeräte-und Switchkonfiguration noch wichtiger. 
- Switchlos: Knoten können mithilfe direkter Verbindungen miteinander verbunden werden, sodass die Verwendung eines Schalters vermieden wird.  Es ist erforderlich, dass jeder Knoten über eine direkte Verbindung mit allen anderen Knoten des Clusters verfügt.


## <a name="drives"></a>Laufwerke

Direkte Speicherplätze funktioniert mit direkt angeschlossenen SATA-, SAS-oder nvme-Laufwerken, die physisch an jeweils nur einen Server angeschlossen sind. Weitere Hilfe zum Auswählen von Laufwerken finden Sie im Thema [Auswählen von Laufwerken](choosing-drives.md).

- SATA-, SAS-und nvme-Laufwerke (M. 2, U. 2 und Add-in-Card) werden unterstützt.
- 512 n, 512 e und 4K Native Laufwerke werden unterstützt.
- Solid-State-Laufwerke müssen den [Schutz von Energieverlusten](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/) bereitstellen.
- Gleiche Anzahl und Arten von Laufwerken auf jedem Server – siehe [Überlegungen zur Laufwerk Symmetrie](drive-symmetry-considerations.md)
- Cache Geräte müssen 32 GB oder größer sein.
- Wenn Sie persistente Speichergeräte als Cache Geräte verwenden, müssen Sie nvme-oder SSD-Kapazitäts Geräte verwenden (HDDs können nicht verwendet werden).
- Der nvme-Treiber ist der von Microsoft bereitgestellte, der in Windows enthalten ist. (stornvme. sys)
- Empfohlen: Die Anzahl der Kapazitäts Laufwerke ist ein gesamtes Vielfaches der Anzahl von Cache Laufwerken.
- Empfohlen: Cache Laufwerke sollten eine hohe Schreib Ausdauer aufweisen: mindestens 3 Laufwerk-Schreibvorgänge pro Tag (dwpd) oder mindestens 4 Terabyte (TBW) pro Tag – Siehe Grundlegendes zu [Laufwerks Schreibvorgängen pro Tag (dwpd), Terabyte (TBW) und die empfohlene Mindestanzahl für direkte Speicherplätze ](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)

So können Laufwerke für direkte Speicherplätze verbunden werden:

- Direkt angeschlossene SATA-Laufwerke
- Direkt angeschlossene nvme-Laufwerke
- SAS-Hostbus Adapter (HBA) mit SAS-Laufwerken
- SAS-Hostbus Adapter (HBA) mit SATA-Laufwerken
- **NICHT UNTERSTÜTZT:** RAID-Controller-Karten oder SAN-Speicher (Fibre Channel, iSCSI, FCoE). HBA-Karten (Hostbus Adapter) müssen den einfachen Pass-Through-Modus implementieren.

![Diagramm der unterstützten Laufwerk-Verbindungen](media/hardware-requirements/drive-interconnect-support-1.png)

Laufwerke können für den Server oder ein externes Gehäuse, das mit nur einem Server verbunden ist, intern sein. SCSI-Gehäuse Dienste (SES) sind für die slotzuordnung und-Identifikation erforderlich. Jedes externe Gehäuse muss einen eindeutigen Bezeichner (eindeutige ID) enthalten.

- Interne Laufwerke für den Server
- Laufwerke in einem externen Gehäuse ("JBOD"), die mit einem Server verbunden sind
- **NICHT UNTERSTÜTZT:** Freigegebene SAS-Gehäuse, die mit mehreren Servern oder einer beliebigen Form von Multipfad-e/a (MPIO) verbunden sind

![Diagramm der unterstützten Laufwerk-Verbindungen](media/hardware-requirements/drive-interconnect-support-2.png)

### <a name="minimum-number-of-drives-excludes-boot-drive"></a>Mindestanzahl von Laufwerken (durch das Start Laufwerk ausgeschlossen)

- Wenn Laufwerke als Cache verwendet werden, sind mindestens zwei pro Server erforderlich.
- Pro Server müssen mindestens vier Kapazitätslaufwerke vorhanden sein, die nicht als Cache fungieren.

| Vorhandene Laufwerktypen   | Erforderliche Mindestanzahl |
|-----------------------|-------------------------|
| Alle persistenten Speicher (Gleiches Modell) | 4 persistenter Speicher |
| Alle NVMe (gleiches Modell) | 4x NVMe                  |
| Alle SSD (gleiches Modell)  | 4x SSD                   |
| Persistenter Arbeitsspeicher + nvme oder SSD | 2 persistenter Arbeitsspeicher + 4 nvme oder SSD |
| NVMe und SSD            | 2x NVMe und 4x SSD          |
| NVMe und HDD            | 2x NVMe und 4x HDD          |
| SSD und HDD             | 2x SSD und 4x HDD           |
| NVMe und SSD und HDD      | 2x NVMe und vier andere       |

   >[!NOTE]
   > Diese Tabelle enthält die Mindestanforderungen für Hardware Bereitstellungen. Wenn Sie mit virtuellen Computern und virtualisiertem Speicher wie z. b. in Microsoft Azure bereitstellen, finden Sie weitere Informationen unter [Verwenden von direkte Speicherplätze in Clustern virtueller Gastcomputer](storage-spaces-direct-in-vm.md).

### <a name="maximum-capacity"></a>Maximale Kapazität

| Höchstwerte                | Windows Server 2019  | Windows Server 2016  |
| ---                     | ---------            | ---------            |
| Rohkapazität pro Server | 400 TB               | 100 TB               |
| Pool Kapazität           | 4 PB (4.000 TB)      | 1 PB                 |
