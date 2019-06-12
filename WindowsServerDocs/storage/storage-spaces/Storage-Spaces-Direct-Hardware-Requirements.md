---
title: Hardwareanforderungen für Direkte Speicherplätze
ms.prod: windows-server-threshold
description: Mindesthardwareanforderungen zum Testen von „Direkte Speicherplätze“.
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: f2031afada302c0f73621a75f572c8547620db16
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501661"
---
# <a name="storage-spaces-direct-hardware-requirements"></a>Hardwareanforderungen für „Direkte Speicherplätze“

> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema beschreibt die minimalen hardwareanforderungen für "direkte Speicherplätze".

Für die Produktion, Microsoft empfiehlt, die eine überprüfte Hardware/Software-Lösung von unseren Partnern kaufen, umfassen, die die von Bereitstellungstools und Verfahren. Diese Lösungen werden entworfen, zusammengesetzt und für unsere Referenzarchitektur, um sicherzustellen, dass Kompatibilität und Zuverlässigkeit, damit Sie Sie nutzen und schnell überprüft. 2019 für Windows Server-Lösungen finden Sie auf die [Solutions-Website für Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci). Für Windows Server 2016-Lösungen, erfahren Sie mehr unter [Windows Server-Software-Defined](https://microsoft.com/wssd).

![Logos unserer Windows Server-Software-Defined-Partner](media/hardware-requirements/wssd-partners.png)

   > [!TIP]
   > "Direkte Speicherplätze" ausgewertet werden soll, aber keine Hardware? Hyper-V oder Azure-Computer verwenden, siehe [mithilfe von "direkte Speicherplätze" in VM-gastclustern](storage-spaces-direct-in-vm.md).

## <a name="base-requirements"></a>Grundanforderungen

Systeme, Komponenten, Geräte und Treiber muss **Windows Server 2016-zertifizierten** pro der [Windows Server-Katalog](https://www.windowsservercatalog.com). Darüber hinaus wird empfohlen, dass der Server, Laufwerke, Hostbusadapter und Netzwerkadapter verfügen die **softwaredefinierten Data Center (SDDC)-Standard** und/oder **softwaredefinierten Data Center (SDDC) Premium** zusätzliche Bedingungen (AQs), wie unten gezeigt. Es gibt mehr als 1.000 Komponenten mit der SDDC-AQs.

![Screenshot der Windows Server-Katalog, die mit der SDDC-AQs](media/hardware-requirements/sddc-aqs.png)

Vollständig konfigurierte Cluster (Server, Netzwerk und Speicher), muss alle übergeben [Clustervalidierungstests](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx) pro des Assistenten im Failovercluster-Manager oder mit der `Test-Cluster` [Cmdlet](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) in PowerShell.

Darüber hinaus gelten die folgenden Anforderungen:

## <a name="servers"></a>Server

- Mindestens zwei, maximal 16 Server
- Empfohlen, dass alle Server der Hersteller und Modell

## <a name="cpu"></a>CPU

- Intel Nehalem oder höher kompatible Prozessoren; oder
- AMD EPYC oder höher kompatible Prozessoren

## <a name="memory"></a>Arbeitsspeicher

- Arbeitsspeicher, um Windows Server, virtuellen Computern und anderen apps oder arbeitsauslastungen. Plus
- 4 GB RAM pro Terabyte (TB) Laufwerk Cachekapazität auf jedem Server für "direkte Speicherplätze"-Metadaten

## <a name="boot"></a>Start

- Alle Startgerät von Windows Server unterstützt die [enthält jetzt SATADOM](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/)
- RAID 1 Spiegel **nicht** erforderlich, aber für den Start unterstützt wird
- Empfohlen: Minimale Größe von 200 GB

## <a name="networking"></a>Netzwerk

Minimum (für kleinen 2 und 3 Knoten)
- 10 Gbit/s-Netzwerkschnittstelle
- Direkt verbinden (switchless) wird unterstützt, mit 2-Knoten

Empfohlen (für hohe Leistung, Skalierung oder Bereitstellungen von Knoten 4 +)
- NICs, die Remote Direct Memory Access (RDMA) fähig ist, sind (empfohlen) iWARP oder RoCE
- Mindestens zwei NICs für Redundanz und Leistung
- 25 Gbit/s-Netzwerkschnittstelle oder höher

## <a name="drives"></a>Laufwerke

"Direkte Speicherplätze" arbeitet mit direkt angeschlossener SATA, SAS oder NVMe-Laufwerke, die physisch mit nur einem Server verbunden sind. Weitere Hilfe zum Auswählen von Laufwerken finden Sie im Thema [Auswählen von Laufwerken](choosing-drives.md).

- SATA, SAS und NVMe-Laufwerke (M.2 U.2 und Add-In-Karte) werden alle unterstützt.
- 512n, 512e und systemeigenen 4-KB-Laufwerke werden alle unterstützt.
- Solid State Drives müssen bereitstellen [Stromausfall Schutz](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/)
- Dieselbe Anzahl und Arten von Laufwerken in jedem Server – finden Sie unter [Laufwerk Symmetrie Überlegungen](drive-symmetry-considerations.md)
- Cachegeräte muss 32 GB oder größer
- Bei persistenten Speichergeräte als cachegeräte verwenden zu können, müssen Sie NVMe oder SSD-Kapazität-Geräte verwenden (Sie können keine HDDs verwenden)
- NVMe-Treiber ist Microsofts integrierte oder NVMe-Treiber aktualisiert.
- Empfohlen: Anzahl der Laufwerke, die Kapazität ist ein ganzes Vielfaches der Anzahl von Cachelaufwerken
- Empfohlen: Cachelaufwerken müssen hohem Endurance: mindestens 3 Laufwerk schreibt – pro Tag (DWPD) oder über mindestens 4 Terabyte (TBW) pro Tag – geschriebene finden Sie unter [Verständnis Laufwerk schreibt pro Tag (DWPD), Terabyte geschrieben (TBW) und das Minimum für Speicher empfohlen "Direkte Speicherplätze"](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)

Hier ist, wie die Laufwerke für "direkte Speicherplätze" verbunden werden können:

- Direkt angeschlossener SATA-Laufwerke
- Direkt angeschlossener NVMe-Laufwerke
- SAS-Hostbusadapter (HBA) mit SAS-Laufwerke
- SAS-Hostbusadapter (HBA) mit SATA-Laufwerke
- **NICHT UNTERSTÜTZT:** RAID-Controller-Karten oder SAN (Fibre Channel, iSCSI, FCoE) Speicher. Hostbus-Hostbusadapter (HBA) Karten müssen einfache Pass-Through-Modus implementieren.

![Diagramm der unterstützten Laufwerk miteinander verbindet.](media/hardware-requirements/drive-interconnect-support-1.png)

Laufwerke auf dem Server intern sein können, oder in externe Gehäuse ist mit nur einem Server. SCSI Enclosure Services (SES) ist für die Zuordnung und Identifikation erforderlich. Jedes externe Gehäuse muss einen eindeutigen Bezeichner (eindeutige ID) darstellen.

- Laufwerke, die in den server
- Laufwerke, die in einem externen Gehäuse ("JBOD"), die mit einem Server verbunden
- **NICHT UNTERSTÜTZT:** Freigegebener SAS-Gehäuse mit mehreren Servern oder jede andere Form von Multipfad e/a (MPIO), in denen Laufwerke zugegriffen werden kann, indem Sie mehrere Pfade sind, verbunden ist.

![Diagramm der unterstützten Laufwerk miteinander verbindet.](media/hardware-requirements/drive-interconnect-support-2.png)

### <a name="minimum-number-of-drives-excludes-boot-drive"></a>Minimale Anzahl von Laufwerken (ausgenommen Startlaufwerk)

- Wenn Laufwerke als Cache verwendet werden, sind mindestens zwei pro Server erforderlich.
- Pro Server müssen mindestens vier Kapazitätslaufwerke vorhanden sein, die nicht als Cache fungieren.

| Vorhandene Laufwerktypen   | Erforderliche Mindestanzahl |
|-----------------------|-------------------------|
| Alle persistenten Speicher (demselben Modell) | 4 persistenten Speicher |
| Alle NVMe (gleiches Modell) | 4x NVMe                  |
| Alle SSD (gleiches Modell)  | 4x SSD                   |
| Persistenten Speicher + NVMe oder SSD | 2 persistenten Speicher + 4 NVMe oder SSD |
| NVMe und SSD            | 2x NVMe und 4x SSD          |
| NVMe und HDD            | 2x NVMe und 4x HDD          |
| SSD und HDD             | 2x SSD und 4x HDD           |
| NVMe und SSD und HDD      | 2x NVMe und vier andere       |

   >[!NOTE]
   > Diese Tabelle enthält das Minimum für Hardware-Bereitstellungen. Wenn Sie mit virtuellen Computern bereitstellen und virtualisierten sind z. B. in Microsoft Azure-Speicher finden Sie unter [mithilfe von "direkte Speicherplätze" in VM-gastclustern](storage-spaces-direct-in-vm.md).

### <a name="maximum-capacity"></a>Maximale Kapazität

| Maximalwerte                | Windows Server 2019  | Windows Server 2016  |
| ---                     | ---------            | ---------            |
| Raw-Kapazität pro server | 100 TB               | 100 TB               |
| Pool-Kapazität           | 4 PB (4.000 TB)      | 1 PB                 |