---
title: Verwenden des Befehls "ausführliche"
description: Referenz Artikel zu "ausführliche", in dem die ausführliche Ausgabe für einen angegebenen Befehl angezeigt wird.
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a96e3dde7291f839a0a53a5e8a851ff1ca88c1e3
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881446"
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