---
title: list
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69b105a1-9710-4a06-8102-38cc9e475ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef9262a04f469f54e43cf3a83efe30fac7ad8580
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854671"
---
# <a name="list"></a>list



Zeigt eine Liste von Datenträgern, von Partitionen auf einem Datenträger, Volumes auf einem Datenträger oder von virtuellen Festplatten (VHDs).

## <a name="syntax"></a>Syntax

```
list { disk | partition | volume | vdisk }
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Datenträger|Zeigt eine Liste der Datenträger und Informationen dazu, wie z. B. ihre Größe, der verfügbare freie Speicherplatz, gibt an, ob der Datenträger für einen einfachen oder dynamischen Datenträger ist und ob der Datenträger der master Boot Record (MBR) oder den Partitionsstil GUID-Partitionstabelle (GPT) verwendet.|
|mit der Bezeichnung|Zeigt die Partitionen, die in der Partitionstabelle den aktuellen Datenträger aufgeführt.|
|Volume|Zeigt eine Liste der Basis- und dynamischen Volumes auf allen Festplatten an.|
|vdisk|Zeigt eine Liste der virtuellen Festplatten, die angefügt bzw. ausgewählt werden. Dieser Befehl listet die getrennten VHDs, wenn sie derzeit aktiviert sind; Allerdings wird der Datenträgertyp in unbekanntes Element festgelegt, bis die virtuelle Festplatte angefügt ist. Die virtuelle Festplatte mit einem Sternchen (*) gekennzeichnet werden den Fokus besitzt.</br>Hinweis: Dieser Befehl ist nur für Windows 7 und Windows Server 2008 R2 verfügbar.|

## <a name="remarks"></a>Hinweise

-   Beim Auflisten von Partitionen auf einem dynamischen Datenträger können die dynamischen Volumes auf dem Datenträger keine Partitionen entsprechen. Diese Abweichung tritt auf, da dynamische Datenträger Einträge in der Partitionstabelle für die System- oder Startvolume (falls vorhanden, auf dem Datenträger) enthalten. Es enthält auch eine Partition, die den Rest des Datenträgers belegt wird, um den Speicherplatz für die Verwendung von dynamischen Volumes zu reservieren.
-   Das Objekt, das mit einem Sternchen (*) gekennzeichnet werden den Fokus besitzt.
-   Beim Auflisten von Datenträgern, wenn ein Datenträger nicht vorhanden ist wird die Anzahl der Datenträger mit M vorangestellt. Beispielsweise ist der erste fehlende Datenträger nummeriert M0.

## <a name="BKMK_examples"></a>Beispiele für

```
list disk
list partition
list volume
list vdisk
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

