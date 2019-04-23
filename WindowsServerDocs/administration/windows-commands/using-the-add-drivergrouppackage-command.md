---
title: Mithilfe des Befehls Add-DriverGroupPackage
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b32d72a1317683e4c1bbeb2d6101d1315b69148e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862641"
---
# <a name="using-the-add-drivergrouppackage-command"></a>Mithilfe des Befehls Add-DriverGroupPackage

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

eine Treibergruppe wird einem Treiberpaket hinzugefügt.
## <a name="syntax"></a>Syntax
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/DriverGroup:<Group Name>|Gibt den Namen der Gruppe "Treiber".|
|/ Server:<Server name>|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|/DriverPackage:<Name>|Gibt den Namen des Treiberpakets der Gruppe hinzugefügt werden. Sie müssen diese Option angeben, wenn das Treiberpaket eindeutig anhand des Namens identifiziert werden kann.|
|/PackageId:<ID>|Gibt die ID für ein Paket. Um die Paket-ID zu suchen, klicken Sie auf die Treibergruppe gewährt wird, der das Paket wird (oder die **alle Pakete** Knoten) mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID finden Sie auf die **allgemeine** Registerkarte, z. B.: **{DD098D20-1850-4fc8-8E35-EA24A1BEFF5E}**.|
## <a name="BKMK_examples"></a>Beispiele für
Um ein Treiberpaket hinzufügen möchten, geben Sie eine der folgenden:
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Add-DriverGroupPackages](using-the-add-drivergrouppackages-command.md)
[mithilfe des Befehls Add-DriverPackage /](using-the-add-driverpackage-command.md) 
 [Mit dem Add-AllDriverPackages Unterbefehl](using-the-add-alldriverpackages-subcommand.md)
