---
title: Bdehdcfg Größe
description: Windows-Befehle-Thema – gibt die Größe der Systempartition beim Erstellen ein neuen Systemlaufwerks erstellt wird.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d024bb4092f93782300d6afb9053cee1da32629a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817521"
---
# <a name="bdehdcfg-size"></a>Bdehdcfg: Größe



Gibt die Größe der Systempartition, beim Erstellen ein neuen Systemlaufwerks erstellt wird. Ein Beispiel, wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink} -size <SizeinMB>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<SizeinMB>|Gibt die Anzahl der Megabytes (MB) an, die für die neue Partition verwendet werden soll.|

## <a name="remarks"></a>Hinweise

Wenn Sie keine Größe angeben, verwendet das Tool den Standardwert von 300 MB. Die minimale Größe des Systemlaufwerks beträgt 100 MB. Wenn Sie die Systemwiederherstellung oder andere Systemtools auf der Systempartition speichern, sollten Sie die Größe entsprechend anpassen.

> [!NOTE]
> Die **Größe** Befehl kann nicht kombiniert werden, mit der **Ziel** \<DriveLetter > **Merge** Befehl.

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **Größe** Befehl aus, um das System-Standardlaufwerk 500 MB zuweisen.
```
bdehdcfg -target default -size 500
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)