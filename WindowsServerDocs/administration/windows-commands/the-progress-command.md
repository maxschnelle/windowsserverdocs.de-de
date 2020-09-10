---
title: Verwenden des Fortschritts Befehls
description: Referenz Artikel zum Fortschritt, in dem der Fortschritt angezeigt wird, während ein Befehl ausgeführt wird.
ms.topic: reference
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 51f127cd9d707652e43a5cae2a2e0bfd7a573b69
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640792"
---
# <a name="using-the-progress-command"></a>Verwenden des Fortschritts Befehls

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