---
title: Verwalten von Basisvolumes
description: Dieser Artikel beschreibt die Vorgehensweise beim Verwalten von Basisvolumes.
ms.date: 10/12/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e97672e7ceceaa5eea83752169ccfd46bd910ed4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961574"
---
# <a name="manage-basic-volumes"></a>Verwalten von Basisvolumes

> **Gilt für:** Windows 10, Windows 8.1, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ein Basisdatenträger ist ein physischer Datenträger, der primäre Partitionen, erweiterte Partitionen oder logische Laufwerke enthält. Partitionen und logische Laufwerke auf Basisdatenträgern werden als Basisvolumes bezeichnet. Basisvolumes können nur auf Basisdatenträgern erstellt werden.

Sie können vorhandenen primären Partitionen und logischen Laufwerken mehr Platz hinzufügen, indem sie diese auf den angrenzenden, zusammenhängenden und nicht zugewiesenen Speicherplatz auf dem gleichen Datenträger erweitern. Um ein Basisvolume zu erweitern, muss es mit dem NTFS-Dateisystem formatiert sein. Ein logisches Laufwerk kann innerhalb des zusammenhängenden freien Speicherplatzes in der erweiterten Partition erweitert werden, die es enthält. Wenn Sie ein logisches Laufwerk über den in der erweiterten Partition verfügbaren freien Speicherplatz hinaus erweitern, erhöht die erweiterte Partition die Größe, um das logische Laufwerk zu beinhalten, solange sich an die erweiterte Partition zusammenhängender, nicht zugewiesener Speicherplatz anschließt.

## <a name="see-also"></a>Weitere Informationen

-   [Zuweisen eines Ordnerpfads mit Bereitstellungspunkt zu einem Laufwerk](assign-a-mount-point-folder-path-to-a-drive.md)
-   [Erweitern eines Basisvolumes](extend-a-basic-volume.md)
-   [Verkleinern eines Basisvolumes](shrink-a-basic-volume.md)