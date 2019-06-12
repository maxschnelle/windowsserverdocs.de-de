---
title: Verwalten von Datenträgern
description: Dieser Artikel beschreibt die Vorgehensweise beim Verwalten von Datenträgern.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 344dd363e970b195abe20fcb69e741c450fc7a21
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812409"
---
# <a name="manage-disks"></a>Verwalten von Datenträgern

> **Gilt für:** Windows 10, Windows 8.1, WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

In diesem Thema und seine Unterthemen besprechen, mit der Datenträgerverwaltung zum Verwalten der Datenträger auf einem Computer, und enthält Informationen zum Initialisieren der neuen Datenträger, Konvertieren von Datenträgern zwischen verschiedenen Partitionstypen und Behandlung von Windows auf den Onlinestatus des neuen Datenträger aus.

## <a name="online-and-offline-status"></a>Online- und Offlinestatus

Die Datenträgerverwaltung anzeigt, ob ein Datenträger online ist (verfügbar) oder offline.

In Windows sind standardmäßig alle neu entdeckten Datenträger mit Lese- und Schreibzugriff Online. In Windows Server sind in der Standardeinstellung neu entdeckten Datenträger mit Lese- und Schreibzugriff Online, wenn sie auf einem freigegebenen Bus (z. B. SCSI, iSCSI, Serial Attached SCSI oder Fibre Channel) sind. Datenträger auf einem freigegebenen Bus sind offline beim ersten sie erkannt werden.

Wenn ein Datenträger offline ist, müssen Sie ihn online schalten, bevor Sie ihn initialisieren und Volumes erstellen können.

Schalten Sie einen Datenträger online oder offline schalten zu können, mit der rechten Maustaste den Datenträgernamen und dann die entsprechende Aktion aus.

## <a name="see-also"></a>Siehe auch

-   [Initialisieren neuer Datenträger](initialize-new-disks.md)
-   [Datenträger auf einen anderen Computer verschieben](move-disks-to-another-computer.md)
-   [Zurückkonvertieren eines dynamischen Datenträgers in einer Basisfestplatte](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [Ändern Sie einen MBR-Datenträger in einen Datenträger (GUID-Partitionstabelle)](change-an-mbr-disk-into-a-gpt-disk.md)
-   [Ändern Sie einen GUID-Partitionstabelle Datenträger in einen MBR-Datenträger](change-a-gpt-disk-into-an-mbr-disk.md)
-   [Verwalten virtueller Festplatten](manage-virtual-hard-disks.md)