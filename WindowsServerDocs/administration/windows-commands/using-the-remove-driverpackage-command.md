---
title: Verwenden den Befehl Remove-DriverPackage /
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 217ff23b8724464670520d0b2d5b196df5a4af47
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440302"
---
# <a name="using-the-remove-driverpackage-command"></a>Verwenden den Befehl Remove-DriverPackage /

> Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012
> 
> 
> Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Entfernt ein Treiberpaket von einem Server an.
## <a name="syntax"></a>Syntax
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>Parameter

|        Parameter        |                                                                            Beschreibung                                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |              Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn ein Servername nicht angegeben ist, wird der lokale Server verwendet.              |
| [/DriverPackage:<Name>] |                                                        Gibt den Namen des Treiberpakets zu entfernen.                                                         |
|    [/PackageId:<ID>]    | Gibt an, die Windows Deployment Services-ID des Treiberpakets zu entfernen. Sie müssen die ID angeben, wenn das Treiberpaket eindeutig anhand des Namens identifiziert werden kann. |

## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, zum Anzeigen von Informationen zu den Images:
```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Remove-DriverPackages-Befehl](using-the-remove-driverpackages-command.md)
