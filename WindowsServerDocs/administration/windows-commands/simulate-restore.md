---
title: Wiederherstellung simulieren
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: d6652fea4e74c706fcc03b8a547fab771a7c0191
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370884"
---
# <a name="simulate-restore"></a>Wiederherstellung simulieren



Testet die Beteiligung von Writer in Wiederherstellungs Sitzungen auf dem Computer ohne Ausgabe von **vorab** -oder **postrestore** -Ereignissen an Writer.

## <a name="syntax"></a>Syntax

```
simulate restore
```

## <a name="remarks"></a>Hinweise

-   Mit " **Wiederherstellung simulieren** " können Sie testen, ob die Wiederherstellung mit Writer erfolgreich sein kann.
-   Bevor Sie die **Wiederherstellung simulieren**verwenden können, müssen Sie mithilfe des Befehls " **Metadaten laden** " eine DiskShadow-Metadatendatei laden. Hierdurch werden die ausgewählten Writer und Komponenten für die Wiederherstellung geladen.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)