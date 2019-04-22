---
title: bitsadmin nowrap
description: Windows-Befehle Thema **Bitsadmin Nowrap** -schneidet jede Zeile der Ausgabe Text erweitern, über die rechte Rand des Befehlsfensters.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4130f606a6b1874e1ea31952160de44d6e09c6b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822921"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

Schneidet jede Zeile der Ausgabe Text erweitern, über die rechte Rand des Befehlsfensters ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /NoWrap
```

## <a name="remarks"></a>Hinweise

Standardmäßig wird für alle Switches, mit Ausnahme der **Monitor** wechseln, und Packen Sie die Ausgabe. Geben Sie die **NoWrap** wechseln, bevor Sie anderen Schaltern.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft den Status des Auftrags namens *MyDownloadJob* und die Ausgabe wird nicht umbrochen
```
C:\>bitsadmin /NoWrap /GetState myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)