---
ms.assetid: 134840f3-c416-4a10-ad73-ef7855b206f7
title: iSCSI-Zielstart (Übersicht)
ms.prod: windows-server
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 9c359c7929ff90968d16e92b1128f4fc8ebde37c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402990"
---
# <a name="iscsi-target-boot-overview"></a>iSCSI-Zielstart (Übersicht)

> Gilt für: Windows Server 2016

Mit einem iSCSI-Zielserver in Windows Server können Sie Hunderte von Computern aus einem einzelnen, zentral gespeicherten Betriebssystemimage starten. Dies führt zu einer Verbesserung von Effizienz, Verwaltbarkeit, Verfügbarkeit und Sicherheit.  
  
## <a name="BKMK_OVER"></a>Funktionsbeschreibung  
Mithilfe differenzierender virtueller Festplatten \(vhds @ no__t-1 können Sie ein einzelnes Betriebssystem Abbild \(The "Master Image" \) verwenden, um bis zu 256 Computer zu starten. Angenommen, Sie haben Windows Server mit einem Betriebssystem Abbild von ungefähr 20 GB bereitgestellt, und Sie haben zwei gespiegelte Laufwerke verwendet, die als Start Volume fungieren. Sie würden ca. 10 TB Speicher allein dafür benötigen, dass das Betriebssystemimage die 256 Computer starten kann. Mit dem iSCSI-Zielserver benötigen Sie 40 GB für das Basisimage des Betriebssystems und 2 GB für differenzierende virtuelle Festplatten pro Serverinstanz, also insgesamt 552 GB für die Betriebssystemimages. Das stellt allein bei den Betriebssystemimages eine Speicherersparnis von über 90 % dar.  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Ein kontrolliertes Betriebssystemimage bietet die folgenden Vorteile:  
  
**Mehr Sicherheit und einfachere Verwaltung.** In einigen Unternehmen ist die Sicherung von Daten durch physisch gesperrten Speicher an einem zentralen Standort erforderlich. Bei diesem Szenario greifen Server remote auf die Daten zu, auch auf das Betriebssystemimage. Mit dem iSCSI-Zielserver können Administratoren die Betriebssystem-Startimage zentral verwalten und steuern, welche Anwendungen in das Masterimage aufgenommen werden sollen.  
  
**Schnelle Bereitstellung.** Da es sich beim Masterimage um ein mit Sysprep vorbereitetes Betriebssystemimage handelt, überspringen Computer beim Starten aus dem Masterimage die Phase bei Windows Setup, in der Dateien kopiert und installiert werden, und beginnen direkt mit der Anpassungsphase. Auf diese Weise konnten bei internen Tests von Microsoft 256 Computer innerhalb von 34 Minuten bereitgestellt werden.  
  
**Schnelle Wiederherstellung.** Da die Betriebssystemimages auf dem Computer gehostet sind, auf dem der iSCSI-Zielserver ausgeführt wird, kann bei einem Austausch eines datenträgerlosen Clients der neue Computer auf das Betriebssystemimage verweisen und direkt starten.  
  
> [!NOTE]  
> Verschiedene Hersteller stellen eine Storage Area Network \(SAN\)-Startlösung zur Verfügung, die vom iSCSI-Zielserver unter Windows Server in Verbindung mit handelsüblicher Hardware verwendet werden kann.  
  
## <a name="BKMK_HARD"></a>Hardware Anforderungen  
Der iSCSI-Zielserver erfordert keine spezielle Hardware für die funktionale Überprüfung. In Rechenzentren mit großen bereit Stellungen mit no__t-0scale sollte der Entwurf anhand bestimmter Hardware überprüft werden. Als Referenz haben interne Tests von Microsoft ergeben, dass eine 256-Computer Bereitstellung rund um die Uhr in einer RAID 10-Konfiguration, die für den Speicher erforderlich ist, rund um die Uhr no__t. Eine Netzwerkbandbreite von 10 GB ist optimal. Die allgemeine Schätzung liebt bei 60 iSCSI-Startservern pro 1-GB-Netzwerkadapter.  
  
Für dieses Szenario ist kein Netzwerkadapter erforderlich; ein Software-Startladeprogramm kann verwendet werden \(z.B. Open Source-Startfirmware wie iPXE\).  
  
## <a name="BKMK_SOFT"></a>Software Anforderungen  
Der iSCSI-Zielserver kann im Server-Manager als Teil der Datei- und iSCSI-Dienste-Rolle verwendet werden.

> [!NOTE]
> Das Starten von Nano Server über iSCSI (entweder von Windows iSCSI Target Server oder von einer Drittanbieter-Zielimplementierung) wird nicht unterstützt.

## <a name="see-also"></a>Siehe auch
* [iSCSI-Zielserver](https://technet.microsoft.com/library/hh848272(v=ws.11).aspx)
* [iSCSI-Initiator-Cmdlets](https://technet.microsoft.com/library/hh826099(v=wps.640).aspx)
* [Cmdlets für iSCSI-Ziel Server](https://technet.microsoft.com/library/jj612803(v=wps.630).aspx)