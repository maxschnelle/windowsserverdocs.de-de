---
title: Offline-Volume
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 71e507bde827233ce1f15aacd5e13523236a080e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372571"
---
# <a name="offline-volume"></a>Offline-Volume



Schaltet das Online Volume mit dem Fokus in den Offline Zustand.

> [!IMPORTANT]
> Dieser Diskpart-Befehl ist in keiner Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
offline volume [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Ein Volume muss ausgewählt werden, damit es erfolgreich ist. Wählen Sie mit dem Befehl **Volume auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="BKMK_examples"></a>Beispiele

Wenn Sie den Fokus offline schalten möchten, geben Sie Folgendes ein:
```
offline volume
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

