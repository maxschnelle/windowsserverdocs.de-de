---
title: Verwenden des Fortschritts Befehls
description: Referenz Artikel zum Fortschritt, in dem der Fortschritt angezeigt wird, während ein Befehl ausgeführt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9284c7330adfbad0115b5b7f6bbab034b42fda4
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519629"
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