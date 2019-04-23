---
title: Der Status-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5fff31c91b4d267011f2d738b4fc3acb3f0f2377
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832701"
---
# <a name="the-progress-command"></a>Der Status-Befehl



Zeigt Status an, während ein Befehl ausgeführt wird. Sie können **/progress** mit andere WDSUTIL-Befehle, die Sie ausführen. Beachten Sie, den Sie angeben, müssen **/ verbose** und **/progress** direkt nach **WDSUTIL**.

## <a name="syntax"></a>Syntax

```
WDSUTIL /progress <commands>
```

## <a name="examples"></a>Beispiele

Um den Server zu initialisieren und Anzeigen des Fortschritts, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Progress /Initialize-Server /Server:MyWDSServer /RemInst:"C:\RemoteInstall"
```