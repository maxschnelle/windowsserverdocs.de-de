---
title: Ausführlich
description: Windows-Befehls Thema für ausführlich, das eine ausführliche Ausgabe für einen angegebenen Befehl anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f67a4fe99a5051e8844e6386d87911946a808c1e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832843"
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