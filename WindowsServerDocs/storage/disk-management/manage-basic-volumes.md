---
title: Verwalten von Basisvolumes
description: Dieser Artikel beschreibt die Vorgehensweise beim Verwalten von Basisvolumes.
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c75d887a6427673319999522b890d523f4276871
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="manage-basic-volumes"></a>Verwalten von Basisvolumes

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

Ein Basisdatenträger ist ein physischer Datenträger, der primäre Partitionen, erweiterte Partitionen und logische Laufwerke enthält. Partitionen und logische Laufwerke auf Basisdatenträgern werden als Basisvolumes bezeichnet. Basisvolumes können nur auf Basisdatenträgern erstellt werden.

Sie können vorhandenen primären Partitionen und logischen Laufwerken mehr Platz hinzufügen, indem sie diese auf den angrenzenden, zusammenhängende verfügbaren Speicherplatz auf dem gleichen Datenträger erweitern. Um ein Basisvolume zu erweitern, muss es mit dem NTFS-Dateisystem formatiert ist. Sie können ein logisches Laufwerk innerhalb einem fortlaufendem, freiem Speicherplatz in der erweiterten Partition erweitern, die es enthält. Wenn Sie ein logisches Laufwerk über den freien Speicherplatz in der erweiterten Partition erweitern, erhöht die erweiterte Partition die Größe, um das logische Laufwerk zu enthalten, solange ein zusammenhängender Speicherplatz der erweiterten Partition folgt.

## <a name="see-also"></a>Weitere Informationen

-   [Einem Laufwerk einen Ordnerpfad mit Bereitstellungspunkt zuweisen](assign-a-mount-point-folder-path-to-a-drive.md)
-   [Erweitern eines Basisvolumes](extend-a-basic-volume.md)
-   [Verkleinern eines Basisvolumes](shrink-a-basic-volume.md)