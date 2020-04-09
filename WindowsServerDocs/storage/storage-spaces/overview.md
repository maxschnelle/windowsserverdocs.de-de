---
title: Übersicht über Speicherplätze
ms.prod: windows-server
ms.author: jgerend
manager: dougkim
ms.technology: storage-file-systems
ms.topic: article
author: jasongerend
ms.date: 05/22/2018
ms.openlocfilehash: 6785508704ff1eebcfd9b70a529ba9d615e5ce11
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858803"
---
# <a name="storage-spaces-overview"></a>Übersicht über Speicherplätze

Speicherplätze sind eine Technologie in Windows und Windows Server, mit der Sie Ihre Daten vor Laufwerk Fehlern schützen können. Es ist konzeptionell vergleichbar mit RAID, das in Software implementiert ist. Sie können Speicherplätze verwenden, um drei oder mehr Laufwerke in einem Speicherpool zu gruppieren und dann die Kapazität aus diesem Pool zum Erstellen von Speicherplätzen zu verwenden. Diese speichern in der Regel zusätzliche Kopien Ihrer Daten, sodass Sie, wenn eines Ihrer Laufwerke ausfällt, immer noch über eine intakte Kopie Ihrer Daten verfügen. Wenn die Kapazität erschöpft ist, fügen Sie einfach weitere Laufwerke zum Speicherpool hinzu.

Es gibt vier Hauptmöglichkeiten für die Verwendung von Speicherplätzen:

- **Auf einem Windows-PC** : Weitere Informationen finden Sie unter [Speicherplätze in Windows 10](https://windows.microsoft.com/windows-10/storage-spaces-windows-10).
- **Auf einem eigenständigen Server mit dem gesamten Speicher auf einem einzelnen Server** : Weitere Informationen finden Sie unter [Bereitstellen von Speicherplätzen auf einem eigenständigen Server](deploy-standalone-storage-spaces.md).
- **Auf einem gruppierten Server mithilfe von direkte Speicherplätze mit lokalem direkt angeschlossenem Speicher in jedem Cluster Knoten** . Weitere Informationen finden Sie unter [direkte Speicherplätze Übersicht](storage-spaces-direct-overview.md).
- **Auf einem gruppierten Server mit einem oder mehreren freigegebenen SAS-Speicher Gehäusen, die alle Laufwerke** enthalten. Weitere Informationen finden Sie unter [Speicherplätze in einem Cluster mit frei gegebener SAS (Übersicht](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831739(v%3dws.11))).

