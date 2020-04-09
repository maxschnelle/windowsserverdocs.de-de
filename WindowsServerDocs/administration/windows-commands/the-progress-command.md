---
title: Progress
description: Thema für Windows-Befehle für den Fortschritt, der den Fortschritt anzeigt, während ein Befehl ausgeführt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9957174203df8f2f5c02bf3ab8a4f3406701a8da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833123"
---
# <a name="progress"></a>Progress

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