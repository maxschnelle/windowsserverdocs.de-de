---
title: break
description: Windows-Befehle Thema für break_1, das die erweiterte STRG + C-Überprüfung auf MS-DOS-Systemen festlegt oder löscht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c89b7357-d69e-4141-826e-73c9ba0fc630
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 809a9321b8b4f8b2d201582f767da132076826d4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848363"
---
# <a name="break"></a>break

Legt die erweiterte STRG + C-Überprüfung auf MS-DOS-Systemen fest oder löscht sie. Bei Verwendung ohne Parameter zeigt **break** die aktuelle Einstellung an.

> [!NOTE]
> Dieser Befehl wird nicht mehr verwendet. Er ist nur zur Wahrung der Kompatibilität mit vorhandenen MS-DOS-Dateien enthalten, hat aber in der Befehlszeile keine Wirkung, da die Funktionalität automatisch sichergestellt ist.

## <a name="syntax"></a>Syntax

```
break=[on|off]
```

## <a name="remarks"></a>Hinweise

Wenn Befehls Erweiterungen auf der Windows-Plattform aktiviert sind und ausgeführt werden, wird der **break** -Befehl in eine Batchdatei eingefügt, wenn der Debugger von einem Debugger debuggt wird.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)