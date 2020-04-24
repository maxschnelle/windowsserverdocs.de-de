---
title: Verwalten von Datenträgern
description: Dieser Artikel beschreibt die Vorgehensweise beim Verwalten von Datenträgern.
ms.date: 06/07/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 0aac0b78e79949de94ebd20912b8c2b2db167339
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "71385871"
---
# <a name="manage-disks"></a>Verwalten von Datenträgern

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema und seine Unterthemen behandeln die Verwaltung von Datenträgern eines Computers mithilfe der Datenträgerverwaltung. Darüber hinaus enthalten sie Informationen zum Initialisieren neuer Datenträger, zum Konvertieren von Datenträgern zwischen unterschiedlichen Partitionsstilen und zur Behandlung des Onlinestatus neuer Datenträger durch Windows.

## <a name="online-and-offline-status"></a>Online- und Offlinestatus

In der Datenträgerverwaltung wird angezeigt, ob ein Datenträger online (verfügbar) oder offline ist.

Unter Windows werden alle neu entdeckten Datenträger standardmäßig mit Lese- und Schreibzugriff online geschaltet. Unter Windows Server werden neu entdeckte Datenträger standardmäßig mit Lese- und Schreibzugriff online geschaltet, wenn sie sich auf einem freigegebenen Bus (z. B. SCSI, iSCSI, Serial Attached SCSI oder Fibre Channel) befinden. Datenträger auf einem freigegebenen Bus sind bei ihrer ersten Erkennung offline.

Ist ein Datenträger offline, musst du ihn online schalten, bevor du ihn initialisieren oder Volumes darauf erstellen kannst.

Wenn du einen Datenträger online oder offline schalten möchtest, klicke mit der rechten Maustaste auf den Datenträgernamen, und wähle dann die entsprechende Aktion aus.

## <a name="see-also"></a>Weitere Informationen

-   [Initialisieren neuer Datenträger](initialize-new-disks.md)
-   [Verschieben des Datenträgers auf einen anderen Computer](move-disks-to-another-computer.md)
-   [Zurückkonvertieren eines dynamischen Datenträgers in einer Basisfestplatte](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [Change a Master Boot Record disk into a GUID Partition Table disk](change-an-mbr-disk-into-a-gpt-disk.md) (Ändern eines MBR-Datenträgers in einen Datenträger mit GUID-Partitionstabelle)
-   [Change a GUID Partition Table disk into a Master Boot Record disk](change-a-gpt-disk-into-an-mbr-disk.md) (Ändern eines Datenträgers mit GUID-Partitionstabelle in einen MBR-Datenträger)
-   [Verwalten virtueller Festplatten](manage-virtual-hard-disks.md)