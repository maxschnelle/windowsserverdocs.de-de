---
title: Mithilfe des Befehls Get-DriverPackage /
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0f123d281625140b3c4ba46316cb9b773bf5fee
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440517"
---
# <a name="using-the-get-driverpackage-command"></a>Mithilfe des Befehls Get-DriverPackage /



Zeigt Informationen zu einem Treiberpaket auf dem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>Parameter

|        Parameter         |                                                                           Beschreibung                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/ Server:\<Servername >] |              Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.               |
| [/ DriverPackage /:\<Name >] |                                                        Gibt den Namen des Treiberpakets angezeigt.                                                         |
|    [/PackageId:\<ID>]    | Gibt an, die Windows Deployment Services-ID des Treiberpakets angezeigt. Sie müssen die ID angeben, wenn das Treiberpaket eindeutig anhand des Namens identifiziert werden kann. |
|     [/Show: {Drivers     |                                                                              Dateien                                                                               |

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie einen der folgenden Schritte aus, zum Anzeigen von Informationen zu einem Treiberpaket:
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)