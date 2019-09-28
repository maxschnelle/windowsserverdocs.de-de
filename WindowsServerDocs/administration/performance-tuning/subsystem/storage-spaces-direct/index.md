---
title: Leistungsoptimierung für „Direkte Speicherplätze“
description: „Direkte Speicherplätze“ optimiert seine Leistung automatisch basierend auf der Cachekonfiguration der Hardware, die Sie verwenden, wie in diesem Thema beschrieben.
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.assetid: 15a519fa-37cc-4d84-a9fe-097d33bb71ea
author: phstee
ms.author: Vshankar; DanLo; clausjor; StevenEk
ms.date: 4/14/2017
ms.openlocfilehash: dabfadb30666ec93aa36985e2bc55a3f496e6d34
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383470"
---
# <a name="performance-tuning-for-storage-spaces-direct"></a>Leistungsoptimierung für „Direkte Speicherplätze“

„Direkte Speicherplätze“, eine softwaredefinierte Speicherlösung auf Windows Server-Basis, optimiert ihre Leistung automatisch, sodass die manuelle Angabe der Anzahl der Spalten, der von Ihnen verwendeten Cachekonfiguration der Hardware sowie anderer Faktoren, die bei freigegebenen SAS-Speicherlösungen manuell festgelegt werden müssen, überflüssig ist. Hintergrundinformationen finden Sie unter [Direkte Speicherplätze – Übersicht](../../../../storage/storage-spaces/storage-spaces-direct-overview.md).

Der Softwarespeicherbus-Cache von „Direkte Speicherplätze“ wird automatisch basierend auf den im System vorhandenen Typen von Speicher konfiguriert. Drei Typen werden erkannt: **HDD**, **SSD** und **NVMe**. Der Cache beansprucht den schnellsten Speicher je nach Bedarf für Lese- und/oder Schreibzwischenspeichern und verwendet den langsameren Speicher für die dauerhafte Speicherung von Daten.

Die folgende Tabelle enthält eine Zusammenfassung der Standards:

| Speichertypen | Cachekonfiguration |
| --- | --- |
| Beliebiger einzelner Typ | Wenn nur eine Art von Speicher vorhanden ist, wird der Softwarespeicherbus-Cache nicht konfiguriert. |
| SSD+HDD oder NVMe+HDD | Der schnellste Speicher wird als Cacheebene konfiguriert und speichert sowohl Lese- als auch Schreibvorgänge zwischen. |
| SSD+SSD oder NVMe+NVMe | Diese „Schnell+Schnell“-Optionen sind für Kombinationen von höherem und niedrigerem Permanentspeicher vorgesehen, z.B. 10-DWPD-NAND-Flash-SSD (Drive Writes Per Day, Laufwerkschreibvorgänge täglich) für den Cache und 1,5-DWPD-NAND-Flash-SSD für Kapazität. Sie werden aktiviert, indem „Direkte Speicherplätze“ eine Reihe von Modellzeichenfolgen zum Identifizieren von Cachegeräten erhalten. Weitere Informationen finden Sie in der Referenz zum Cmdlet [Enable-StorageSpacesDirect](https://technet.microsoft.com/library/mt589697.aspx) (`CacheDeviceModel`). <br><br>In einem „Schnell+Schnell“-System werden nur Schreibvorgänge zwischengespeichert. Lesevorgänge werden nicht zwischengespeichert. |

Beachten Sie, dass Zwischenspeichern über ein SSD- oder NVMe-Gerät standardmäßig nur bei Schreibvorgängen durchgeführt wird. Der Grund ist: Da das Kapazitätsgerät schnell ist, ist es nur begrenzt von Vorteil, Leseinhalt auf die Cachegeräte zu verschieben. Es gibt Fälle, in denen dies vielleicht nicht gilt, trotzdem sollte darauf geachtet werden, da das Aktivieren des Lesecaches unnötigerweise Cachegerätkapazität ohne Zunahme der Leistung verbrauchen kann. Zu den Beispielen können zählen:

* **NVme+SSD**: Aktivieren des Lesecaches ermöglicht Lese-E/A die Nutzung der PCIe-Konnektivität und/oder im Vergleich mit aggregiertem SSD höheren IOPS-Leistung der NVMe-Geräte. <br>Dies _kann_ aufgrund der relativen Bandbreitenkapazitäten der NVMe-Geräte im Vergleich zu mit dem SSD verbundenen HBA auf bandbreitenorientierte Szenarien zutreffen. Es trifft _möglicherweise nicht_ auf IOPS-orientierte Szenarien zu, in denen IOPS-CPU-Kosten Systeme einschränken können, bevor die höhere Leistung realisiert werden kann.
* **NVMe+NVMe**: In ähnlicher Weise kann, wenn die Lesefähigkeit des Cache-NVMe größer als die kombinierte NVMe-Kapazität ist, die Aktivierung des Lesecaches von Vorteil sein. <br>Gute Gründe für den Lesecache sind in diesen Konfigurationen eher unwahrscheinlich.

Verwenden Sie zum Anzeigen und Ändern der Cachekonfiguration das [Get-ClusterStorageSpacesDirect](https://technet.microsoft.com/library/mt634616.aspx)- und [Set-ClusterStorageSpacesDirect](https://technet.microsoft.com/library/mt763265.aspx)-Cmdlet. Die Eigenschaften `CacheModeHDD` und `CacheModeSSD` definieren, wie der Cache bei Kapazitätsmedien des angegeben Typs funktioniert.

## <a name="see-also"></a>Weitere Informationen

- [Grundlegendes zu „Direkte Speicherplätze“](../../../../storage/storage-spaces/understand-storage-spaces-direct.md)
- [Planen für „Direkte Speicherplätze“](../../../../storage/storage-spaces/plan-storage-spaces-direct.md)
- [Leistungsoptimierung für Dateiserver](../../role/file-server/index.md)
- [Handbuch zu Entwurfsüberlegungen für softwaredefinierten Speicher](https://technet.microsoft.com/library/mt243829.aspx) (für Windows Server 2012 R2 und freigegebenen SAS-Speicher)
