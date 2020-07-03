---
title: Fortschritt
description: Referenz Artikel zum Fortschritt, in dem der Fortschritt angezeigt wird, während ein Befehl ausgeführt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e9650a980d74f15bc0ec5c88d8df2dc93a3d8b0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934597"
---
# <a name="progress"></a>Fortschritt

Zeigt den Fortschritt an, während ein Befehl ausgeführt wird. Sie können **/Progress** mit allen anderen WDSUTIL-Befehlen verwenden, die Sie ausführen. Beachten Sie, dass Sie **/verbose** und **/Progress** direkt nach " **WDSUTIL**" angeben müssen.

## <a name="syntax"></a>Syntax

```
WDSUTIL /progress <commands>
```

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Server zu initialisieren und Fortschritt anzuzeigen:
```
WDSUTIL /Verbose /Progress /Initialize-Server /Server:MyWDSServer /RemInst:C:\RemoteInstall
```