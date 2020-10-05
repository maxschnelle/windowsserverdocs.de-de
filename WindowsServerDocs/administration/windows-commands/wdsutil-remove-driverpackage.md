---
title: WDSUTIL Remove-DriverPackage
description: Referenz Artikel zu "Remove-DriverPackage" von WDSUTIL, mit dem ein Treiber Paket von einem Server entfernt wird.
ms.topic: reference
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fe40c9a1dbbf4a5f0bd09e61f39e6b9314a09337
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730113"
---
# <a name="wdsutil-remove-driverpackage"></a>WDSUTIL Remove-DriverPackage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt ein Treiber Paket von einem Server.

## <a name="syntax"></a>Syntax
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>Parameter

|        Parameter        |                                                                            BESCHREIBUNG                                                                             |
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL Remove-driverpackages-Befehl](wdsutil-remove-driverpackages.md)
