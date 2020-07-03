---
title: Remove-DriverPackage
description: Referenz Artikel zu Remove-DriverPackage, mit dem ein Treiber Paket von einem Server entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c39f34d1556e6ad0f61f3f1cc3cf0aac36b18ee5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933452"
---
# <a name="remove-driverpackage"></a>Remove-DriverPackage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt ein Treiber Paket von einem Server.

## <a name="syntax"></a>Syntax
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>Parameter

|        Parameter        |                                                                            Beschreibung                                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |              Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.              |
| [/DriverPackage: <Name> ] |                                                        Gibt den Namen des zu entfernenden Treiber Pakets an.                                                         |
|    [/PackageId: <ID> ]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an, das entfernt werden soll. Sie müssen die ID angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. |

## <a name="examples"></a>Beispiele
Wenn Sie Informationen zu den Bildern anzeigen möchten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Remove-DriverPackages-Befehls](using-the-remove-driverpackages-command.md)
