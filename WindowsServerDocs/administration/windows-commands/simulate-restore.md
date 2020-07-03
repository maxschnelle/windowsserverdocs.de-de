---
title: simulate restore
description: Referenz Artikel zum Simulieren der Wiederherstellung, bei dem die Writer-Beteiligung in Wiederherstellungs Sitzungen auf dem Computer getestet wird, ohne vorab-oder postrestore-Ereignisse an Writer auszugeben.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d883d94c-3cb1-4848-9d74-1b4378044b31
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7cc247848ef4fac1e3a6537247f640f3533c2bcd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936348"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)