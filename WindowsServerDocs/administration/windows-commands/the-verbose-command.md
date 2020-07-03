---
title: Ausführlich
description: Referenz Artikel zu "ausführliche", in dem die ausführliche Ausgabe für einen angegebenen Befehl angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 079e441ba4a932e23493e7e37fbe36cab4c4971f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935238"
---
# <a name="verbose"></a>Ausführlich

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