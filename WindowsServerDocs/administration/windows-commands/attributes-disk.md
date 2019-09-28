---
title: Attribute-Datenträger
description: 'Themen zu Windows-Befehlen für **Attribut** Datenträger: zeigt die Attribute eines Datenträgers an, legt Sie fest oder löscht sie.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eed57071-c1c6-4394-9542-62b52a878c92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 415125208b13d82adeed736107f59fda9489a953
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382566"
---
# <a name="attributes-disk"></a>Attribute-Datenträger



Hiermit werden die Attribute eines Datenträgers angezeigt, festgelegt oder gelöscht.

> [!IMPORTANT]
> Dieser Parameter ist in keiner Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
attributes disk [{set | clear}] [readonly] [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|set|Legt das angegebene Attribut des Datenträgers mit dem Fokus fest.|
|clear|Löscht das angegebene Attribut des Datenträgers mit dem Fokus.|
|ReadOnly|Gibt an, dass der Datenträger schreibgeschützt ist.|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Wenn **Attribute Disk** verwendet wird, um die aktuellen Attribute eines Datenträgers anzuzeigen, gibt das Attribut des Start Datenträgers den Datenträger an, der zum Starten des Computers verwendet wird. Bei einer dynamischen Spiegelung wird diese für den Datenträger angezeigt, der den Start-Plex des Start Volume enthält.
-   Ein Datenträger muss ausgewählt werden, damit der Befehl Datenträger für **Attribute** erfolgreich ist. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die Attribute des ausgewählten Datenträgers anzuzeigen:
```
attributes disk
```
Geben Sie Folgendes ein, um den ausgewählten Datenträger als schreibgeschützt festzulegen:
```
attributes disk set readonly
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

