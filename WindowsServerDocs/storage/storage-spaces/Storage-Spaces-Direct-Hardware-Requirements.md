---
title: Hardwareanforderungen für „Direkte Speicherplätze“
ms.prod: windows-server-threshold
description: Mindesthardwareanforderungen zum Testen von „Direkte Speicherplätze“.
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 84d10ab3e25500720dd13e2ba057dc3c5bf05a6f
ms.sourcegitcommit: 515b4fd5c40fcbae0e12a2c30090384533972353
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/29/2018
ms.locfileid: "8232529"
---
# Hardwareanforderungen für „Direkte Speicherplätze“

> Gilt für: WindowsServer 2016, Windows Server Insider Preview

Dieses Thema beschreibt die mindesthardwareanforderungen zum "direkte Speicherplätze".

Für die Produktion empfiehlt Microsoft diese [Windows Server Software-Defined](https://microsoft.com/wssd) Hardware und Software-Angebote von unseren Partnern, die Tools für die Bereitstellung und Verfahren enthalten. Sie sind entworfen, zusammengesetzt und unsere Referenzarchitektur, um sicherzustellen, dass Kompatibilität und Zuverlässigkeit, so Sie nach oben erhalten und schnell überprüft. Weitere Informationen zu [https://microsoft.com/wssd](https://microsoft.com/wssd).

![Logos unserer Partner Windows Server Software-Defined](media/hardware-requirements/wssd-partners.png)

   > [!TIP]
   > "Direkte Speicherplätze" evaluieren möchten Sie jedoch nicht Hardware? Verwenden Sie Hyper-V oder virtuellen Azure-Computern als unter [Verwendung von "direkte Speicherplätze" im virtuellen Computer gastcluster](storage-spaces-direct-in-vm.md)beschrieben.

## Grundlegende Anforderungen

Systeme, Komponenten, Geräte und Treiber müssen pro der [Windows Server-Katalog](https://www.windowsservercatalog.com) **Windows Server 2016 zertifiziert** sein. Darüber hinaus empfehlen wir die Server, Laufwerke, Host Busadapter und Netzwerkadapter **Software-Defined Data Center (SDDC) Standard** und/oder **Software-Defined Data Center (SDDC) Premium** erhöhte (AQs), als Symbole unten. Es gibt 1.000 Komponenten mit der SDDC-AQs.

![Screenshot des Windows Server-Katalogs mit der SDDC-AQs](media/hardware-requirements/sddc-aqs.png)

Der vollständig konfigurierte Cluster (Server, Netzwerk und Speicher) muss für alle erfolgreich [Clustervalidierungstests](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx) des Assistenten im Failovercluster-Manager oder mit der `Test-Cluster` PowerShell- [Cmdlet](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) .

Darüber hinaus gelten folgende Anforderungen:

## Server

- Mindestens zwei, maximal 16Server
- Empfohlen, alle Server gleichen Hersteller und Modell aufweisen.

## CPU

- Intel Nehalem oder kompatibler Prozessor; oder
- AMD EPYC oder kompatibler Prozessor

## Arbeitsspeicher

- Arbeitsspeicher, um Windows Server, VMs und anderen apps oder Arbeitslasten. Plus
- 4 GB RAM pro Terabyte (TB) cachelaufwerkkapazität auf jedem Server für "direkte Speicherplätze"-Metadaten

## Boot

- Alle von Windows Server, welche [SATADOM enthält nun u. a.](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/) unterstützten Startgerät
- RAID 1 Spiegelung ist **nicht** erforderlich, jedoch wird für den Start unterstützt
- Empfohlen: 200 GB minimale Größe

## Networking

Minimum (für kleine Skalierung 2 bis 3-Knoten)
- 10 Gbit/s Netzwerk-Schnittstelle
- Direct-Verbindung (switchless) wird unterstützt, mit 2-Knoten

Empfohlen (für hohe Leistung und einer Skalierung oder Bereitstellungen von 4 + Knoten)
- Netzwerkkarten, die Remote Direct Memory Access (RDMA) kann, sind (empfohlen) iWARP oder RoCE
- Mindestens zwei NICs für Redundanz und Leistung
- 25 Gbit/s Netzwerkschnittstelle oder höher

## Laufwerke

"Direkte Speicherplätze" funktioniert mit direkt angeschlossene SATA-, SAS- oder NVMe-Laufwerke, die physisch mit nur einem Server verbunden sind. Weitere Hilfe zum Auswählen von Laufwerken finden Sie im Thema [Auswählen von Laufwerken](choosing-drives.md).

- SATA, SAS und NVMe-Laufwerke (M.2 U.2 und Add-In-Karte) werden alle unterstützt.
- Um 512n, 512e und 4K native Laufwerke werden alle unterstützt.
- Solid State Drives müssen [Stromausfall Schutz](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/) zu bieten
- Dieselbe Anzahl und Typen von Laufwerken auf jedem Server – finden Sie unter [Laufwerk Symmetrie Aspekte](drive-symmetry-considerations.md)
- NVMe-Treiber ist Microsofts mitgelieferte oder NVMe-Treiber aktualisiert.
- Empfohlen: Anzahl der kapazitätslaufwerke ist ein ganzes Vielfaches der Anzahl der Cache-Laufwerke
- Empfohlen: Sollten Cachelaufwerke hohe schreibbelastung haben: mindestens 3 Laufwerk-datenträgerbeschreibungen pro Tag (DWPD) oder mindestens 4 Terabyte-Beschreibungen (TBW) pro Tag – finden Sie unter [datenträgerbeschreibungen pro Tag (DWPD), Terabyte-Beschreibungen (TBW), und der empfohlene Mindestwert für Speicher Speicherplätze](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)

Hier sehen Sie, wie Laufwerke für "direkte Speicherplätze" verbunden werden können:

1. Direkt angeschlossene SATA-Laufwerke
2. Direkt angeschlossene NVMe-Laufwerke
3. SAS-Hostbusadapter (HBA) mit SAS-Laufwerke
4. SAS-Hostbusadapter (HBA) mit SATA-Laufwerke
5. **Nicht unterstützt:** RAID-Controller-Karten oder SAN (Fibre Channel, iSCSI, FCoE) Speicher. Host-Bus Adapter (HBA) Karten müssen einfachen Pass-Through-Modus implementieren.

![Diagramm der unterstützten Laufwerk sind](media/hardware-requirements/drive-interconnect-support-1.png)

Laufwerken können es sich um interne an den Server, oder in einem externen Gehäuse ist, die Verbindung mit nur einem Server. SCSI Enclosure Services (SES) ist erforderlich für Steckplatz-Zuordnung und Identifikation besteht. Jede externe Gehäuse muss eine eindeutige Kennung (eindeutige ID) vorhanden.

1. Server-internen Laufwerke
2. In einem externen Gehäuse ("JBOD"), die mit einem Server verbunden Laufwerke
3. **Nicht unterstützt:** Freigegebene SAS-Gehäusen verbunden, mehrere Server oder eine beliebige Form der Multi-Path e/a (MPIO), in denen Laufwerken über mehrere Pfade zugänglich sind.

![Diagramm der unterstützten Laufwerk sind](media/hardware-requirements/drive-interconnect-support-2.png)

### Mindestanzahl von Laufwerken (schließt Startlaufwerk)

- Wenn Laufwerke als Cache verwendet werden, sind mindestens zwei pro Server erforderlich.
- Pro Server müssen mindestens vier Kapazitätslaufwerke vorhanden sein, die nicht als Cache fungieren.

| Vorhandene Laufwerktypen   | Erforderliche Mindestanzahl |
|-----------------------|-------------------------|
| Alle NVMe (gleiches Modell) | 4x NVMe                  |
| Alle SSD (gleiches Modell)  | 4x SSD                   |
| NVMe und SSD            | 2x NVMe und 4x SSD          |
| NVMe und HDD            | 2x NVMe und 4x HDD          |
| SSD und HDD             | 2x SSD und 4x HDD           |
| NVMe und SSD und HDD      | 2x NVMe und vier andere       |

   >[!NOTE]
   > Diese Tabelle enthält die minimale für Hardware-Bereitstellungen. Wenn Sie mit virtuellen Computern bereitstellen und Speicher, z. B. in Microsoft Azure virtualisiert, finden Sie unter [Verwendung von "direkte Speicherplätze" in gastcluster virtuellen Computer](storage-spaces-direct-in-vm.md).

### Maximale Kapazität

- Empfohlen: Maximal 100 Terabyte (TB) reine Speicherkapazität pro server
- Maximal 1 Petabyte (1.000 TB) Gesamtkapazität im Speicherpool
