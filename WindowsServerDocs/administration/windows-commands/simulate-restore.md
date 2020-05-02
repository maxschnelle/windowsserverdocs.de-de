---
title: Wiederherstellung simulieren
description: Referenz Thema zum Simulieren der Wiederherstellung, bei dem die Writer-Beteiligung in Wiederherstellungs Sitzungen auf dem Computer getestet wird, ohne vorab-oder postrestore-Ereignisse an Writer auszugeben.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d883d94c-3cb1-4848-9d74-1b4378044b31
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bab6c56cddc1d2ac95dc70205b0990b82fbfd12
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721776"
---
# <a name="simulate-restore"></a>Wiederherstellung simulieren

Testet die Beteiligung von Writer in Wiederherstellungs Sitzungen auf dem Computer ohne Ausgabe von **vorab** -oder **postrestore** -Ereignissen an Writer.

## <a name="syntax"></a>Syntax

```
simulate restore
```

## <a name="remarks"></a>Bemerkungen

-   Mit " **Wiederherstellung simulieren** " können Sie testen, ob die Wiederherstellung mit Writer erfolgreich sein kann.
-   Bevor Sie die **Wiederherstellung simulieren**verwenden können, müssen Sie mithilfe des Befehls " **Metadaten laden** " eine DiskShadow-Metadatendatei laden. Hierdurch werden die ausgewählten Writer und Komponenten für die Wiederherstellung geladen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)