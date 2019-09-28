---
title: break
description: 'Windows-Befehls Thema für **break_1** -Sets oder löscht erweiterte STRG + C-Überprüfung auf MS-DOS-Systemen. Bei Verwendung ohne Parameter zeigt **break** die aktuelle Einstellung an. '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c89b7357-d69e-4141-826e-73c9ba0fc630
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73afdac29efbfd9efec88d297cf4185ca1b92d62
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380489"
---
# <a name="break"></a>break



Legt die erweiterte STRG + C-Überprüfung auf MS-DOS-Systemen fest oder löscht sie. Bei Verwendung ohne Parameter zeigt **break** die aktuelle Einstellung an.

> [!NOTE]
> Dieser Befehl wird nicht mehr verwendet. Er soll lediglich die Kompatibilität mit vorhandenen MS-DOS-Dateien gewährleisten. In der Befehlszeile ist er jedoch ohne Auswirkungen, da die Funktionalität automatisch ausgeführt wird.

## <a name="syntax"></a>Syntax

```
break=[on|off]
```

## <a name="remarks"></a>Hinweise

Wenn Befehls Erweiterungen auf der Windows-Plattform aktiviert sind und ausgeführt werden, wird der **break** -Befehl in eine Batchdatei eingefügt, wenn der Debugger von einem Debugger debuggt wird.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)