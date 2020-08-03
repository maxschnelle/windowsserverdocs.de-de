---
title: Verwenden des Befehls "ausführliche"
description: Referenz Artikel zu "ausführliche", in dem die ausführliche Ausgabe für einen angegebenen Befehl angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b53defe143ab9a5c068d5012ed60b66e29398004
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519609"
---
# <a name="using-the-verbose-command"></a>Verwenden des Befehls "ausführliche"

Zeigt die ausführliche Ausgabe für einen angegebenen Befehl an. Sie können **/verbose** mit allen anderen WDSUTIL-Befehlen verwenden, die Sie ausführen. Beachten Sie, dass Sie **/verbose** und **/Progress** direkt nach " **WDSUTIL**" angeben müssen.

## <a name="syntax"></a>Syntax

```
WDSUTIL /verbose <commands>
```

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um genehmigte Computer aus der Datenbank zum automatischen Hinzufügen zu löschen und ausführliche Ausgabe anzuzeigen:

```
WDSUTIL /Verbose /progress /Delete-AutoAddDevices /Server:MyWDSServer /DeviceType:ApprovedDevices
```