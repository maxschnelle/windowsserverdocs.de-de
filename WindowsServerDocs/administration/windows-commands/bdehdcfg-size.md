---
title: bdehdcfg-Größe
description: 'Windows-Befehls Thema: gibt die Größe der Systempartition an, wenn ein neues Systemlaufwerk erstellt wird.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6ec42cdb5716c63c7210ea6cfde8ce8884833b45
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382198"
---
# <a name="bdehdcfg-size"></a>bdehdcfg: Größe



Gibt die Größe der Systempartition an, wenn ein neues Systemlaufwerk erstellt wird. Ein Beispiel für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink} -size <SizeinMB>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<sizeinmb >|Gibt die Anzahl der Megabytes (MB) an, die für die neue Partition verwendet werden soll.|

## <a name="remarks"></a>Hinweise

Wenn Sie keine Größe angeben, verwendet das Tool den Standardwert von 300 MB. Die minimale Größe des Systemlaufwerks beträgt 100 MB. Wenn Sie die Systemwiederherstellung oder andere Systemtools auf der Systempartition speichern, sollten Sie die Größe entsprechend anpassen.

> [!NOTE]
> Der **size** -Befehl kann nicht mit dem **Ziel** \<driveletter > **Merge** -Befehl kombiniert werden.

## <a name="BKMK_Examples"></a>Beispiele

Im folgenden Beispiel wird die Verwendung des Befehls **size** zum Zuordnen von 500 MB zum Standardsystem Laufwerk veranschaulicht.
```
bdehdcfg -target default -size 500
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)