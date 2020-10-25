---
title: Get-DriverPackage
description: Referenz Artikel zu Get-DriverPackage, in dem Informationen zu einem Treiber Paket auf dem Server angezeigt werden.
ms.topic: reference
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 86f8b2cdc7a0bc62f42c02c9ff7c6852e9b159f0
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524435"
---
# <a name="get-driverpackage"></a>Get-DriverPackage

Zeigt Informationen zu einem Treiber Paket auf dem Server an.

## <a name="syntax"></a>Syntax

```
wdsutil /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>Parameter

|        Parameter         |                                                                           BESCHREIBUNG                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server name>] |              Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.               |
| [/DriverPackage: \<Name> ] |                                                        Gibt den Namen des anzuzeigenden Treiber Pakets an.                                                         |
|    [/PackageId: \<ID> ]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an, das angezeigt werden soll. Sie müssen die ID angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. |
|     [/Show: {Drivers     |                                                                              Dateien                                                                               |

## <a name="examples"></a>Beispiele

Wenn Sie Informationen zu einem Treiber Paket anzeigen möchten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
wdsutil /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)