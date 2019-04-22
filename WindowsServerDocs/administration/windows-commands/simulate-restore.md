---
title: Simulieren der Wiederherstellung
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d883d94c-3cb1-4848-9d74-1b4378044b31
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09b626939c13d4e38a983435b45d8c47ee2b93a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817251"
---
# <a name="simulate-restore"></a>Simulieren der Wiederherstellung



Testet Writer Beteiligung in der Restore-Sitzungen auf dem Computer nur durch Ausstellung **PreRestore** oder **PostRestore** Ereignisse auf Writer.

## <a name="syntax"></a>Syntax

```
simulate restore
```

## <a name="remarks"></a>Hinweise

-   **Simulieren der Wiederherstellung** wird verwendet, um zu testen, und zwar unabhängig davon, ob die Wiederherstellung mit Writer erfolgreich sein kann.
-   Vor der Verwendung **simulieren der Wiederherstellung**, Sie müssen eine DiskShadow-Metadatendatei laden, indem Sie mit der **Laden von Metadaten** Befehl. Dies lädt die ausgewählten Writer und die Komponenten für die Wiederherstellung.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)