---
title: Verwenden des Befehls "ausführliche"
description: Referenz Artikel zu "ausführliche", in dem die ausführliche Ausgabe für einen angegebenen Befehl angezeigt wird.
ms.topic: reference
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2335ef8bf3e3b231851d424f99f0a7e878218c4b
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524875"
---
# <a name="using-the-verbose-command"></a>Verwenden des Befehls "ausführliche"

Zeigt die ausführliche Ausgabe für einen angegebenen Befehl an. Sie können **/verbose** mit allen anderen WDSUTIL-Befehlen verwenden, die Sie ausführen. Beachten Sie, dass Sie **/verbose** und **/Progress** direkt nach " **WDSUTIL**" angeben müssen.

## <a name="syntax"></a>Syntax

```
wdsutil /verbose <commands>
```

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um genehmigte Computer aus der Datenbank zum automatischen Hinzufügen zu löschen und ausführliche Ausgabe anzuzeigen:

```
wdsutil /Verbose /progress /Delete-AutoAddDevices /Server:MyWDSServer /DeviceType:ApprovedDevices
```