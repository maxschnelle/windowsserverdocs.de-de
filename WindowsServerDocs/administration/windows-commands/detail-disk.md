---
title: Detail Festplatte
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff78a3f9e27cde35a7e19bdf1565c515a127261b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378583"
---
# <a name="detail-disk"></a>Detail Festplatte



Zeigt die Eigenschaften des ausgewählten Datenträgers und das Volume auf der Festplatte an.

## <a name="syntax"></a>Syntax

```
detail disk
```

## <a name="remarks"></a>Hinweise

-   Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.
-   Wenn es sich bei der ausgewählten Festplatte um eine virtuelle Festplatte (VHD) handelt, meldet der **Detail** Datenträger den Bustyp des Datenträgers als virtuell

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die Eigenschaften des ausgewählten Datenträgers und Informationen zu den Volumes auf dem Datenträger anzuzeigen:
```
detail disk
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

