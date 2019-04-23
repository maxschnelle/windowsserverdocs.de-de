---
title: Verwenden den Befehl Remove-DriverGroupPackage
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e48616d-d6a4-45f0-a5c6-efe62bf6a0ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 82a8fb8fbe9e713c3e22c08839bc4bc22fe900db
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883991"
---
# <a name="using-the-remove-drivergrouppackage-command"></a>Verwenden den Befehl Remove-DriverGroupPackage



Entfernt ein Treiberpaket aus einer Treibergruppe auf einem Server an.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn ein Servername nicht angegeben ist, wird der lokale Server verwendet.|
|[/ DriverPackage /:\<Name >]|Gibt den Namen des Treiberpakets zu entfernen.|
|[/PackageId:\<ID>]|Gibt an, die Windows Deployment Services-ID des Treiberpakets zu entfernen. Sie müssen diese Option angeben, wenn das Treiberpaket eindeutig anhand des Namens identifiziert werden kann.|

## <a name="BKMK_examples"></a>Beispiele für

```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318}
```
```
WDSUTIL /Remove-DriverGroupPackage /DriverGroup:PrinterDrivers /DriverPackage:XYZ
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)