---
ms.assetid: 134840f3-c416-4a10-ad73-ef7855b206f7
title: iSCSI-Zielstart (Übersicht)
ms.prod: windows-server-threshold
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: b3ec6dad0b3fcc9ef595350c7df09505beba1103
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838801"
---
# <a name="iscsi-target-boot-overview"></a>iSCSI-Zielstart (Übersicht)

> Gilt für: Windows Server 2016

Mit einem iSCSI-Zielserver in Windows Server können Sie Hunderte von Computern aus einem einzelnen, zentral gespeicherten Betriebssystemimage starten. Dies führt zu einer Verbesserung von Effizienz, Verwaltbarkeit, Verfügbarkeit und Sicherheit.  
  
## <a name="BKMK_OVER"></a>Featurebeschreibung  
Mithilfe differenzierender virtueller Festplatten \(VHDs\), können Sie ein einzelnes Betriebssystemabbild \(des "masterimages"\) bis zu 256 Computer starten. Nehmen wir beispielsweise an, dass Sie Windows Server mit einem Betriebssystemimage von ca. 20 GB bereitgestellt und zwei gespiegelte Laufwerke verwenden, die als Startvolume fungieren. Sie würden ca. 10 TB Speicher allein dafür benötigen, dass das Betriebssystemimage die 256 Computer starten kann. Mit dem iSCSI-Zielserver benötigen Sie 40 GB für das Basisimage des Betriebssystems und 2 GB für differenzierende virtuelle Festplatten pro Serverinstanz, also insgesamt 552 GB für die Betriebssystemimages. Das stellt allein bei den Betriebssystemimages eine Speicherersparnis von über 90 % dar.  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Ein kontrolliertes Betriebssystemimage bietet die folgenden Vorteile:  
  
**Mehr Sicherheit und einfachere Verwaltung.** In einigen Unternehmen ist die Sicherung von Daten durch physisch gesperrten Speicher an einem zentralen Standort erforderlich. Bei diesem Szenario greifen Server remote auf die Daten zu, auch auf das Betriebssystemimage. Mit dem iSCSI-Zielserver können Administratoren die Betriebssystem-Startimage zentral verwalten und steuern, welche Anwendungen in das Masterimage aufgenommen werden sollen.  
  
**Schnelle Bereitstellung.** Da es sich beim Masterimage um ein mit Sysprep vorbereitetes Betriebssystemimage handelt, überspringen Computer beim Starten aus dem Masterimage die Phase bei Windows Setup, in der Dateien kopiert und installiert werden, und beginnen direkt mit der Anpassungsphase. Auf diese Weise konnten bei internen Tests von Microsoft 256 Computer innerhalb von 34 Minuten bereitgestellt werden.  
  
**Schnelle Wiederherstellung.** Da die Betriebssystemimages auf dem Computer gehostet sind, auf dem der iSCSI-Zielserver ausgeführt wird, kann bei einem Austausch eines datenträgerlosen Clients der neue Computer auf das Betriebssystemimage verweisen und direkt starten.  
  
> [!NOTE]  
> Verschiedene Hersteller stellen eine Storage Area Network \(SAN\)-Startlösung zur Verfügung, die vom iSCSI-Zielserver unter Windows Server in Verbindung mit handelsüblicher Hardware verwendet werden kann.  
  
## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Der iSCSI-Zielserver erfordert keine spezielle Hardware für die funktionale Überprüfung. In Rechenzentren mit großen\-Bereitstellungen, das Design mit der jeweiligen Hardware überprüft werden soll. Zu Referenzzwecken interne Tests von Microsoft, dass eine Bereitstellung für 256 Computer 24x15k erforderlichen angegeben\-u/min in einer RAID 10-Konfiguration für den Speicher. Eine Netzwerkbandbreite von 10 GB ist optimal. Die allgemeine Schätzung liebt bei 60 iSCSI-Startservern pro 1-GB-Netzwerkadapter.  
  
Für dieses Szenario ist kein Netzwerkadapter erforderlich; ein Software-Startladeprogramm kann verwendet werden \(z.B. Open Source-Startfirmware wie iPXE\).  
  
## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Der iSCSI-Zielserver kann im Server-Manager als Teil der Datei- und iSCSI-Dienste-Rolle verwendet werden.

> [!NOTE]
> Das Starten von Nano Server über iSCSI (entweder von Windows iSCSI Target Server oder von einer Drittanbieter-Zielimplementierung) wird nicht unterstützt.

## <a name="see-also"></a>Siehe auch
* [iSCSI-Zielserver](https://technet.microsoft.com/library/hh848272(v=ws.11).aspx)
* [iSCSI-Initiator-cmdlets](https://technet.microsoft.com/library/hh826099(v=wps.640).aspx)
* [iSCSI Target Server cmdlets](https://technet.microsoft.com/library/jj612803(v=wps.630).aspx)