---
title: Wiederherstellung simulieren
description: Windows-Befehls Artikel zum Simulieren der Wiederherstellung, bei dem die Writer-Beteiligung in Wiederherstellungs Sitzungen auf dem Computer getestet wird, ohne vorab-oder postrestore-Ereignisse an Writer auszugeben.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d883d94c-3cb1-4848-9d74-1b4378044b31
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 024d654864c000e44bccb9ddb167c6147444cc00
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834103"
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