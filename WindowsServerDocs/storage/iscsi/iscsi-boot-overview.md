---
ms.assetid: 134840f3-c416-4a10-ad73-ef7855b206f7
title: "iSCSI-Zielstart (Übersicht)"
ms.prod: windows-server-threshold
ms.technology: storage-iscsi
ms.topic: article
author: MicGray-MS
manager: dongill
ms.author: micgray
ms.date: 10/11/2016
ms.openlocfilehash: 958d8a71e6fe62ec9d256be132aef4edf00942db
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="iscsi-target-boot-overview"></a>iSCSI-Zielstart (Übersicht)

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mit einem iSCSI-Zielserver in Windows Server können Sie Hunderte von Computern aus einem einzelnen, zentral gespeicherten Betriebssystemimage starten. Dies führt zu einer Verbesserung von Effizienz, Verwaltbarkeit, Verfügbarkeit und Sicherheit.  
  
## <a name="BKMK_OVER"></a>Featurebeschreibung  
Durch differenzierende virtuelle Festplatten \(Virtual Hard Disks, VHDs\) können Sie mithilfe eines einzelnen Betriebssystemimages \(„Masterimage“\) bis zu 256 Computer starten. Angenommen, Sie haben z.B. Windows Server mit einem Betriebssystemimage von ca. 20 GB bereitgestellt und verwenden zwei gespiegelte Laufwerke, die als Startvolume fungieren. Sie würden ca. 10 TB Speicher allein dafür benötigen, dass das Betriebssystemimage die 256 Computer starten kann. Mit dem iSCSI-Zielserver benötigen Sie 40 GB für das Basisimage des Betriebssystems und 2 GB für differenzierende virtuelle Festplatten pro Serverinstanz, also insgesamt 552 GB für die Betriebssystemimages. Das stellt allein bei den Betriebssystemimages eine Speicherersparnis von über 90% dar.  
  
## <a name="BKMK_APP"></a>Praktische Anwendung  
Ein kontrolliertes Betriebssystemimage bietet die folgenden Vorteile:  
  
**Mehr Sicherheit und einfachere Verwaltung.** In einigen Unternehmen ist die Sicherung von Daten durch physisch gesperrten Speicher an einem zentralen Standort erforderlich. Bei diesem Szenario greifen Server remote auf die Daten zu, auch auf das Betriebssystemimage. Mit dem iSCSI-Zielserver können Administratoren die Betriebssystem-Startimage zentral verwalten und steuern, welche Anwendungen in das Masterimage aufgenommen werden sollen.  
  
**Schnelle Bereitstellung.** Da es sich beim Masterimage um ein mit Sysprep vorbereitetes Betriebssystemimage handelt, überspringen Computer beim Starten aus dem Masterimage die Phase bei Windows Setup, in der Dateien kopiert und installiert werden, und beginnen direkt mit der Anpassungsphase. Auf diese Weise konnten bei internen Tests von Microsoft 256 Computer innerhalb von 34 Minuten bereitgestellt werden.  
  
**Schnelle Wiederherstellung.** Da die Betriebssystemimages auf dem Computer gehostet sind, auf dem der iSCSI-Zielserver ausgeführt wird, kann bei einem Austausch eines datenträgerlosen Clients der neue Computer auf das Betriebssystemimage verweisen und direkt starten.  
  
> [!NOTE]  
> Verschiedene Hersteller stellen eine SAN-Startlösung \(Storage Area Network\) zur Verfügung, die vom iSCSI-Zielserver unter Windows Server in Verbindung mit handelsüblicher Hardware verwendet werden kann.  
  
## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Der iSCSI-Zielserver erfordert keine spezielle Hardware für die funktionale Überprüfung. In Rechenzentren mit großen Bereitstellungen sollte das Design mit der jeweiligen Hardware abgestimmt werden. So ergaben interne Tests von Microsoft, dass bei einer Bereitstellung für 256 Computer 24 Datenträger mit 15.000 U/Min in einer RAID 10-Konfiguration als Speicher erforderlich sind. Eine Netzwerkbandbreite von 10 GB ist optimal. Die allgemeine Schätzung liegt bei 60 iSCSI-Startservern pro 1-GB-Netzwerkadapter.  
  
Für dieses Szenario ist kein Netzwerkadapter erforderlich. Ein Software-Startladeprogramm kann verwendet werden, z.B. Open Source-Startfirmware wie iPXE.  
  
## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Der iSCSI-Zielserver kann im Server-Manager als Teil des Datei- und iSCSI-Dienste-Rollendiensts verwendet werden.

> [!NOTE]
> Das Starten von Nano Server über iSCSI (entweder von Windows iSCSI Target Server oder von einer Drittanbieter-Zielimplementierung) wird nicht unterstützt.

## <a name="see-also"></a>Siehe auch
* [iSCSI Target Server](https://technet.microsoft.com/library/hh848272(v=ws.11).aspx)
* [iSCSI initiator cmdlets (Cmdlets des iSCSI-Intitiators)](https://technet.microsoft.com/library/hh826099(v=wps.640).aspx)
* [iSCSI Target Server cmdlets (Cmdlets des iSCSI-Zielservers)](https://technet.microsoft.com/library/jj612803(v=wps.630).aspx)