---
title: list
description: Referenz Thema für den List-Befehl, der eine Liste von Datenträgern, von Partitionen auf einem Datenträger, von Volumes auf einem Datenträger oder von virtuellen Festplatten (VHDs) anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 69b105a1-9710-4a06-8102-38cc9e475ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53914468ddee4a8930fc05c677c94be700a89021
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724495"
---
# <a name="list"></a>list

Zeigt eine Liste von Datenträgern, von Partitionen auf einem Datenträger, von Volumes auf einem Datenträger oder von virtuellen Festplatten (VHDs) an.

## <a name="syntax"></a>Syntax

```
list { disk | partition | volume | vdisk }
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|disk|Zeigt eine Liste der Datenträger und Informationen dazu an, z. b. die Größe, die Menge des verfügbaren freien Speicherplatzes, ob es sich um einen einfachen oder dynamischen Datenträger handelt und ob der Datenträger den Partitions Stil Master Boot Record (MBR) oder GUID-Partitionstabelle (GPT) verwendet.|
|partition|Zeigt die Partitionen an, die in der Partitionstabelle des aktuellen Datenträgers aufgeführt sind.|
|Volume|Zeigt eine Liste der Basisvolumes und dynamischen Volumes auf allen Datenträgern an.|
|Vdisk|Zeigt eine Liste der VHDs an, die angefügt und/oder ausgewählt sind. Dieser Befehl listet getrennte VHDs auf, wenn Sie aktuell ausgewählt sind. der Datenträgertyp wird jedoch auf "unknown" festgelegt, bis die VHD angefügt ist. Die mit einem Sternchen (*) markierte VHD hat den Fokus.</br>Hinweis: Dieser Befehl ist nur für Windows 7 und Windows Server 2008 R2 verfügbar.|

## <a name="remarks"></a>Bemerkungen

-   Beim Auflisten von Partitionen auf einem dynamischen Datenträger entsprechen die Partitionen möglicherweise nicht den dynamischen Volumes auf dem Datenträger. Diese Diskrepanz tritt auf, weil dynamische Datenträger Einträge in der Partitionstabelle für das System Volume oder Start Volume (sofern auf dem Datenträger vorhanden) enthalten. Sie enthalten außerdem eine Partition, die den Rest des Datenträgers einnimmt, um den Speicherplatz zu reservieren, der von dynamischen Volumes verwendet werden soll.
-   Das mit einem Sternchen (*) markierte Objekt hat den Fokus.
-   Wenn beim Auflisten von Datenträgern ein Datenträger fehlt, wird die zugehörige Datenträger Nummer mit "M" vorangestellt. Beispielsweise ist der erste fehlende Datenträger mit der Nummerierung M0.

## <a name="examples"></a>Beispiele

```
list disk
list partition
list volume
list vdisk
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

