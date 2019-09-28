---
title: Der Status Befehl
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 841d9103354e3162489492ba7dd97e726b37d37d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370176"
---
# <a name="the-progress-command"></a>Der Status Befehl



Zeigt den Fortschritt während der Ausführung eines Befehls an. Sie können **/Progress** mit allen anderen WDSUTIL-Befehlen verwenden, die Sie ausführen. Beachten Sie, dass Sie **/verbose** und **/Progress** direkt nach " **WDSUTIL**" angeben müssen.

## <a name="syntax"></a>Syntax

```
WDSUTIL /progress <commands>
```

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Server zu initialisieren und Fortschritt anzuzeigen:
```
WDSUTIL /Verbose /Progress /Initialize-Server /Server:MyWDSServer /RemInst:"C:\RemoteInstall"
```