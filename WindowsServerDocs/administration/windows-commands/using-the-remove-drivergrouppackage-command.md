---
title: Remove-drivergrouppackage
description: Referenz Artikel zu Remove-drivergrouppackage, mit dem ein Treiber Paket aus einer Treiber Gruppe auf einem Server entfernt wird.
ms.topic: reference
ms.assetid: 2e48616d-d6a4-45f0-a5c6-efe62bf6a0ed
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2cddeca84ba4993d8d77a4b55062d6ba4255abf9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635060"
---
# <a name="remove-drivergrouppackage"></a>Remove-drivergrouppackage



Entfernt ein Treiber Paket aus einer Treiber Gruppe auf einem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/DriverPackage: \<Name> ]|Gibt den Namen des zu entfernenden Treiber Pakets an.|
|[/PackageId: \<ID> ]|Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an, das entfernt werden soll. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann.|

## <a name="examples"></a>Beispiele

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /DriverPackage:XYZ
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)