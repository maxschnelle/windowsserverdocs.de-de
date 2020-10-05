---
title: WDSUTIL-Status
description: Referenz Artikel für "WDSUTIL Progress", in dem der Fortschritt während der Ausführung eines Befehls angezeigt wird.
ms.topic: reference
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4a7ddc18db35b110c8b5c513f798e3408aafd93f
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730164"
---
# <a name="wdsutil-progress"></a>WDSUTIL/Progress

Zeigt den Fortschritt an, während ein Befehl ausgeführt wird. Sie können **/Progress** mit allen anderen WDSUTIL-Befehlen verwenden, die Sie ausführen. Wenn Sie die ausführliche Protokollierung für diesen Befehl aktivieren möchten, müssen Sie " **/verbose** " und " **/Progress** " direkt nach " **WDSUTIL**" angeben.

## <a name="syntax"></a>Syntax

```
wdsutil /progress <commands>
```

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Server zu initialisieren und Fortschritt anzuzeigen:

```
wdsutil /verbose /progress /Initialize-Server /Server:MyWDSServer /RemInst:C:\RemoteInstall
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)