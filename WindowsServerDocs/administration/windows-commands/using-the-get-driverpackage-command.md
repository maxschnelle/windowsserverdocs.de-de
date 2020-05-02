---
title: Get-DriverPackage
description: Referenz Thema zu Get-DriverPackage, das Informationen zu einem Treiber Paket auf dem Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4fc6bc327b46f8219a7c40fa47e85cc94b6fc749
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719937"
---
# <a name="get-driverpackage"></a>Get-DriverPackage

Zeigt Informationen zu einem Treiber Paket auf dem Server an.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>Parameter

|        Parameter         |                                                                           BESCHREIBUNG                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server Name>] |              Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.               |
| [/DriverPackage:\<Name>] |                                                        Gibt den Namen des anzuzeigenden Treiber Pakets an.                                                         |
|    [/PackageId:\<ID->]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an, das angezeigt werden soll. Sie müssen die ID angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. |
|     [/Show: {Drivers     |                                                                              Dateien                                                                               |

## <a name="examples"></a>Beispiele

Wenn Sie Informationen zu einem Treiber Paket anzeigen möchten, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)