---
title: Unterbefehls Satz-DriverPackage
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11804bb6-ca29-4461-8c63-5131748cd742
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65751cf6e03baa87c7734b318a26111652bee0a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370822"
---
# <a name="subcommand-set-driverpackage"></a>Unterbefehl: Set-DriverPackage



Benennt ein Treiber Paket auf einem Server um und/oder aktiviert oder deaktiviert dieses.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Set-DriverPackage [/Server:<Server name>] {/DriverPackage:<Name> | /PackageId:<ID>} [/Name:<New Name>] [/Enabled:{Yes | No}
```

## <a name="parameters"></a>Parameter

|        Parameter         |                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: \<Server Name >] |                                                                                                                                                 Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                 |
| [/DriverPackage: \<name >] |                                                                                                                                                                                       Gibt den aktuellen Namen des zu ändernden Treiber Pakets an.                                                                                                                                                                                        |
|    [/PackageId: \<ID >]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. Um diese ID für ein Paket zu finden, klicken Sie auf die Treiber Gruppe, in der sich das Paket befindet (oder den Knoten **alle Pakete** ), klicken Sie mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID ist auf der Registerkarte **Allgemein** aufgeführt. Beispiel: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}. |
|   [/Name: \<new Name >]    |                                                                                                                                                                                              Gibt den neuen Namen für das Treiber Paket an.                                                                                                                                                                                              |
|      [/Enabled: {Ja      |                                                                                                                                                                                                                   gar                                                                                                                                                                                                                    |

## <a name="BKMK_examples"></a>Beispiele

Um die Einstellungen für ein Paket zu ändern, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Set-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318} /Name:MyDriverPackage
```
```
WDSUTIL /Set-DriverPackage /DriverPackage:MyDriverPackage /Name:NewName /Enabled:Yes
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)