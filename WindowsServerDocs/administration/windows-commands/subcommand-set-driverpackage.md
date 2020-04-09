---
title: Unterbefehls Satz-DriverPackage
description: Windows-Befehls Thema für den Unterbefehl set-DriverPackage, das ein Treiber Paket auf einem Server umbenennt und/oder aktiviert oder deaktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11804bb6-ca29-4461-8c63-5131748cd742
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68d282b3338e67a33a55481658f55db69930b10e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834018"
---
# <a name="subcommand-set-driverpackage"></a>Unterbefehl: Set-DriverPackage

Benennt ein Treiber Paket auf einem Server um und/oder aktiviert oder deaktiviert dieses.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Set-DriverPackage [/Server:<Server name>] {/DriverPackage:<Name> | /PackageId:<ID>} [/Name:<New Name>] [/Enabled:{Yes | No}
```

### <a name="parameters"></a>Parameter

|        Parameter         |                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server Name >] |                                                                                                                                                 Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                 |
| [/DriverPackage:\<Name >] |                                                                                                                                                                                       Gibt den aktuellen Namen des zu ändernden Treiber Pakets an.                                                                                                                                                                                        |
|    [/PackageId:\<ID >]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. Um diese ID für ein Paket zu finden, klicken Sie auf die Treiber Gruppe, in der sich das Paket befindet (oder den Knoten **alle Pakete** ), klicken Sie mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID ist auf der Registerkarte **Allgemein** aufgeführt. Beispiel: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}. |
|   [/Name:\<neuer Name >]    |                                                                                                                                                                                              Gibt den neuen Namen für das Treiber Paket an.                                                                                                                                                                                              |
|      [/Enabled: {Ja      |                                                                                                                                                                                                                   gar                                                                                                                                                                                                                    |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um die Einstellungen für ein Paket zu ändern, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Set-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318} /Name:MyDriverPackage
```
```
WDSUTIL /Set-DriverPackage /DriverPackage:MyDriverPackage /Name:NewName /Enabled:Yes
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)