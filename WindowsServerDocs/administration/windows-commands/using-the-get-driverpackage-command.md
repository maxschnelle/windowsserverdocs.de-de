---
title: Get-DriverPackage
description: Windows-Befehls Thema für Get-DriverPackage, das Informationen zu einem Treiber Paket auf dem Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 94d231e4-ff01-48e7-9bc8-7b0d97a4339e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1906a109d22b24b5a44227d56c726996e6532bd6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831053"
---
# <a name="get-driverpackage"></a>Get-DriverPackage

Zeigt Informationen zu einem Treiber Paket auf dem Server an.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>} [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>Parameter

|        Parameter         |                                                                           Beschreibung                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server Name >] |              Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.               |
| [/DriverPackage:\<Name >] |                                                        Gibt den Namen des anzuzeigenden Treiber Pakets an.                                                         |
|    [/PackageId:\<ID >]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an, das angezeigt werden soll. Sie müssen die ID angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. |
|     [/Show: {Drivers     |                                                                              Dateien                                                                               |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn Sie Informationen zu einem Treiber Paket anzeigen möchten, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Get-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Get-DriverPackage /DriverPackage:MyDriverPackage /Show:All
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)