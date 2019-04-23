---
title: Verwalten von Datenträgern
description: Dieser Artikel beschreibt die Vorgehensweise beim Verwalten von Datenträgern.
ms.date: 12/21/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f4698dac683ff3769eb4403ae2750ad38a301022
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846191"
---
# <a name="manage-disks"></a>Verwalten von Datenträgern

> **Gilt für:** Windows 10, Windows 8.1, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

In diesem Thema und seine Unterthemen besprechen, mit der Datenträgerverwaltung zum Verwalten der Datenträger auf einem Computer, und enthält Informationen zum Initialisieren der neuen Datenträger, Konvertieren von Datenträgern zwischen verschiedenen Partitionstypen und Behandlung von Windows auf den Onlinestatus des neuen Datenträger aus.

## <a name="online-and-offline-status"></a>Online- und Offlinestatus

Die Datenträgerverwaltung anzeigt, ob ein Datenträger online ist (verfügbar) oder offline.

In Windows sind standardmäßig alle neu entdeckten Datenträger mit Lese- und Schreibzugriff Online. In Windows Server sind in der Standardeinstellung neu entdeckten Datenträger mit Lese- und Schreibzugriff Online, wenn sie auf einem freigegebenen Bus (z. B. SCSI, iSCSI, Serial Attached SCSI oder Fibre Channel) sind. Datenträger auf einem freigegebenen Bus sind offline beim ersten sie erkannt werden.

Wenn ein Datenträger offline ist, müssen Sie ihn online schalten, bevor Sie ihn initialisieren und Volumes erstellen können.

Schalten Sie einen Datenträger online oder offline schalten zu können, mit der rechten Maustaste den Datenträgernamen und dann die entsprechende Aktion aus.





## <a name="see-also"></a>Siehe auch

-   [Neuen Datenträger initialisieren](initialize-new-disks.md)
-   [Datenträger auf einen anderen Computer verschieben](move-disks-to-another-computer.md)
-   [Ändern Sie einen dynamischen Datenträger in einen Basisdatenträger](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [Ändern Sie einen MBR-Datenträger in einen Datenträger (GUID-Partitionstabelle)](change-an-mbr-disk-into-a-gpt-disk.md)
-   [Ändern Sie einen GUID-Partitionstabelle Datenträger in einen MBR-Datenträger](change-a-gpt-disk-into-an-mbr-disk.md)
-   [Verwalten virtueller Festplatten](manage-virtual-hard-disks.md)