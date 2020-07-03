---
title: Remove-drivergrouppackage
description: Referenz Artikel zu Remove-drivergrouppackage, mit dem ein Treiber Paket aus einer Treiber Gruppe auf einem Server entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2e48616d-d6a4-45f0-a5c6-efe62bf6a0ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8f4177a9e4a3abfa41eb3db094dc5d6e481678f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933481"
---
# <a name="remove-drivergrouppackage"></a>Remove-drivergrouppackage



Entfernt ein Treiber Paket aus einer Treiber Gruppe auf einem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
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