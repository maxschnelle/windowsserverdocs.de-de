---
title: bitsadmin nowrap
description: 'Windows-Befehls Thema für **bizadmin NoWrap** : abgeschnitten jede Zeile von Ausgabetext, der über den äußersten rechten Rand des Befehls Fensters hinausgeht.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3806ec51161eeae498e3c9b367b2aacf0bd32c99
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381049"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

Verkürzt jede Zeile von Ausgabetext, die über den rechten Rand des Befehls Fensters hinausgeht.

## <a name="syntax"></a>Syntax

```
bitsadmin /NoWrap
```

## <a name="remarks"></a>Hinweise

Standardmäßig wird die Ausgabe durch alle Switches außer dem **Monitor** Switch umschlossen. Geben Sie den Schalter " **nowrap** " vor anderen Switches an.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Status für den Auftrag mit dem Namen *mydownloadjob* abgerufen, und die Ausgabe wird nicht eingeschlossen.
```
C:\>bitsadmin /NoWrap /GetState myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)