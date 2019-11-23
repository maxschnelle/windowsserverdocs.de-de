---
title: Verwenden des Remove-DriverPackage-Befehls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 923a86805134c4162b36cdade98c2122b3cb7ccd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362808"
---
# <a name="using-the-remove-driverpackage-command"></a>Verwenden des Remove-DriverPackage-Befehls

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> 
> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

entfernt ein Treiber Paket von einem Server.
## <a name="syntax"></a>Syntax
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>Parameter

|        Parameter        |                                                                            Beschreibung                                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |              Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.              |
| [/DriverPackage:<Name>] |                                                        Gibt den Namen des zu entfernenden Treiber Pakets an.                                                         |
|    [/PackageId:<ID>]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an, das entfernt werden soll. Sie müssen die ID angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. |

## <a name="BKMK_examples"></a>Beispiele
Wenn Sie Informationen zu den Bildern anzeigen möchten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Befehl "Remove-DriverPackages](using-the-remove-driverpackages-command.md) "
