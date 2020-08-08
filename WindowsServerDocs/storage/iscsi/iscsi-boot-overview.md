---
ms.assetid: 134840f3-c416-4a10-ad73-ef7855b206f7
title: iSCSI-Zielstart (Übersicht)
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: f3f2ce63afa3e75b6d2f55789866c1872504c8eb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957417"
---
# <a name="iscsi-target-boot-overview"></a>iSCSI-Zielstart (Übersicht)

> Gilt für: Windows Server 2016

Mit einem iSCSI-Zielserver in Windows Server können Sie Hunderte von Computern aus einem einzelnen, zentral gespeicherten Betriebssystemimage starten. Dies führt zu einer Verbesserung von Effizienz, Verwaltbarkeit, Verfügbarkeit und Sicherheit.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Featurebeschreibung
Mithilfe differenzierender virtueller Festplatten ( \( VHDs) \) können Sie ein einzelnes Betriebssystem \( Abbild des Master Abbilds verwenden, \) um bis zu 256 Computer zu starten. Angenommen, Sie haben Windows Server mit einem Betriebssystem Abbild von ungefähr 20 GB bereitgestellt, und Sie haben zwei gespiegelte Laufwerke verwendet, die als Start Volume fungieren. Sie würden ca. 10 TB Speicher allein dafür benötigen, dass das Betriebssystemimage die 256 Computer starten kann. Mit dem iSCSI-Zielserver benötigen Sie 40 GB für das Basisimage des Betriebssystems und 2 GB für differenzierende virtuelle Festplatten pro Serverinstanz, also insgesamt 552 GB für die Betriebssystemimages. Das stellt allein bei den Betriebssystemimages eine Speicherersparnis von über 90 % dar.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
Ein kontrolliertes Betriebssystemimage bietet die folgenden Vorteile:

**Mehr Sicherheit und einfachere Verwaltung.** In einigen Unternehmen ist die Sicherung von Daten durch physisch gesperrten Speicher an einem zentralen Standort erforderlich. Bei diesem Szenario greifen Server remote auf die Daten zu, auch auf das Betriebssystemimage. Mit dem iSCSI-Zielserver können Administratoren die Betriebssystem-Startimage zentral verwalten und steuern, welche Anwendungen in das Masterimage aufgenommen werden sollen.

**Schnelle Bereitstellung.** Da es sich beim Masterimage um ein mit Sysprep vorbereitetes Betriebssystemimage handelt, überspringen Computer beim Starten aus dem Masterimage die Phase bei Windows Setup, in der Dateien kopiert und installiert werden, und beginnen direkt mit der Anpassungsphase. Auf diese Weise konnten bei internen Tests von Microsoft 256 Computer innerhalb von 34 Minuten bereitgestellt werden.

**Schnelle Wiederherstellung.** Da die Betriebssystemimages auf dem Computer gehostet sind, auf dem der iSCSI-Zielserver ausgeführt wird, kann bei einem Austausch eines datenträgerlosen Clients der neue Computer auf das Betriebssystemimage verweisen und direkt starten.

> [!NOTE]
> Verschiedene Hersteller stellen eine Storage Area Network \(SAN\)-Startlösung zur Verfügung, die vom iSCSI-Zielserver unter Windows Server in Verbindung mit handelsüblicher Hardware verwendet werden kann.

## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>Hardwareanforderungen
Der iSCSI-Zielserver erfordert keine spezielle Hardware für die funktionale Überprüfung. In Rechenzentren mit großen Bereitstellungen sollte das Design mit der jeweiligen Hardware abgestimmt werden. Als Referenz haben interne Tests von Microsoft ergeben, dass eine 256-Computer Bereitstellung rund \- um die Uhr in einer RAID 10-Konfiguration für den Speicher rund um die Uhr benötigte Datenträger Eine Netzwerkbandbreite von 10 GB ist optimal. Die allgemeine Schätzung liebt bei 60 iSCSI-Startservern pro 1-GB-Netzwerkadapter.

Für dieses Szenario ist kein Netzwerkadapter erforderlich; ein Software-Startladeprogramm kann verwendet werden \(z.B. Open Source-Startfirmware wie iPXE\).

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Softwareanforderungen
Der iSCSI-Zielserver kann im Server-Manager als Teil der Datei- und iSCSI-Dienste-Rolle verwendet werden.

> [!NOTE]
> Das Starten von Nano Server über iSCSI (entweder von Windows iSCSI Target Server oder von einer Drittanbieter-Zielimplementierung) wird nicht unterstützt.

## <a name="additional-references"></a>Weitere Verweise
* [iSCSI-Zielserver](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh848272(v=ws.11))
* [iSCSI initiator cmdlets (Cmdlets des iSCSI-Intitiators)](/powershell/module/iscsi/?view=win10-ps)
* [iSCSI Target Server cmdlets (Cmdlets des iSCSI-Zielservers)](/powershell/module/iscsi/?view=win10-ps)
