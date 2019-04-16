---
title: "Verwalten von Datenträgern"
description: "Dieser Artikel beschreibt die Vorgehensweise beim Verwalten von Datenträgern."
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ae96071733b961fbe65551120894c21c633db83e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="manage-disks"></a>Verwalten von Datenträgern

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema und seine Unterthemen behandeln die Verwendung der Datenträgerverwaltung, um die Datenträger in einem Computer zu verwalten, und enthalten Informationen zum Konvertieren von Datenträgern zwischen unterschiedlichen Partitionsstilen und wie Windows den Online-Status der neue Datenträger behandelt.

## <a name="converting-disk-types"></a>Konvertieren von Datenträgertypen

Auch wenn die Datenträgerverwaltung die Änderung zwischen verschiedenen Partitionstypen und -Stilen ermöglicht, können einige Vorgänge nicht rückgängig gemacht werden (es sei denn, Sie formatieren das Laufwerk neu). Sie sollten sorgfältig den Datenträgertyp und den Partitionsstil erwägen, die für Ihre Anwendung am besten geeignet sind.

Die folgende Tabelle zeigt die Optionen zum Konvertieren von Datenträgern zwischen den verschiedenen Partitionstypen:

| Datenträgertyp | Konvertieren in MBR  | Konvertieren in GPT| In dynamischen Datenträger konvertieren |
| ---- | --- | --- |--- |
| <p>Master Boot Record (MBR)</p> | <p>--</p> | <p>Zugelassen (wenn keine Volumes auf dem Datenträger vorhanden sind).</p> | <p>Zugelassen, aber der Datenträger kann möglicherweise nicht mehr gestartet werden. Siehe Hinweis.</p> |
| <p>GUID-Partitionstabelle (GPT)</p> | <p>Zugelassen (wenn keine Volumes auf dem Datenträger vorhanden sind).</p> | <p>--</p>  | <p>Zugelassen, aber der Datenträger kann möglicherweise nicht mehr gestartet werden. Siehe Hinweis.</p> |


> [!NOTE]
> Wenn Sie mit einem Betriebssystem begonnen haben und einen MBR-Basisdatenträger mit einem alternativen Betriebssystem in einen dynamischen Datenträger konvertieren, können Sie in einem Multibootszenario nicht mehr mit dem alternativen Betriebssystem starten.

## <a name="online-and-offline-status"></a>Online- und Offlinestatus

„Datenträgerverwaltung” zeigt den Online- und Offlinestatus der Datenträger an. 

In Windows sind standardmäßig alle neu entdeckten Datenträger mit Lese- und Schreibzugriff Online. In Windows Server sind in der Standardeinstellung neu entdeckten Datenträger mit Lese- und Schreibzugriff Online, wenn sie auf einem freigegebenen Bus (z.B. SCSI, iSCSI, Serial Attached SCSI oder Fibre Channel) sind. Datenträger auf einem freigegebenen Bus sind offline, wenn sie zuerst erkannt werden.

Wenn ein Datenträger offline ist, müssen Sie ihn online schalten, bevor Sie ihn initialisieren und Volumes erstellen können. 

-  Schalten Sie einen Datenträger online oder offline, indem Sie mit der rechten Maustaste auf den Namen des Datenträgers klicken, und wählen Sie dann die entsprechende Aktion aus.

## <a name="see-also"></a>Weitere Informationen

-   [Initialisieren neuer Datenträger](initialize-new-disks.md)
-   [Den Datenträger einen anderen Computer verschieben](move-disks-to-another-computer.md)
-   [Zurückkonvertieren eines dynamischen Datenträgers in einen Basisdatenträger](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [Ändern einer MBR-Festplatte auf einen GPT-Datenträgers mit GUID-Partitionstabelle](change-an-mbr-disk-into-a-gpt-disk.md)
-   [Ändern eines GPT-Datenträgers mit GUID-Partitionstabelle in eine MBR-Festplatte](change-a-gpt-disk-into-an-mbr-disk.md)
-   [Verwalten virtueller Festplatten](manage-virtual-hard-disks.md)