---
title: Verwenden des Befehls Get-DriverPackage
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: f3d31d9a02454b0f7fca06b28a4df27174f7b02e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363191"
---
# <a name="using-the-get-driverpackage-command"></a>Verwenden des Befehls Get-DriverPackage



Zeigt Informationen zu einem Treiber Paket auf dem Server an.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>Parameter

|        Parameter         |                                                                           Beschreibung                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: \<Server Name >] |              Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.               |
| [/DriverPackage: \<name >] |                                                        Gibt den Namen des anzuzeigenden Treiber Pakets an.                                                         |
|    [/PackageId: \<ID >]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an, das angezeigt werden soll. Sie müssen die ID angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. |
|     [/Show: {Drivers     |                                                                              Dateien                                                                               |

## <a name="BKMK_examples"></a>Beispiele

Wenn Sie Informationen zu einem Treiber Paket anzeigen möchten, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)