---
title: Unterbefehls Satz-DriverPackage
description: Referenz Artikel für den Unterbefehl set-DriverPackage, der ein Treiber Paket auf einem Server umbenennt und/oder aktiviert oder deaktiviert.
ms.topic: reference
ms.assetid: 11804bb6-ca29-4461-8c63-5131748cd742
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a4b0b3154f6cc7cee34e6fdcc91f332295164541
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640860"
---
# <a name="subcommand-set-driverpackage"></a>Unterbefehl: Set-DriverPackage

Benennt ein Treiber Paket auf einem Server um und/oder aktiviert oder deaktiviert dieses.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Set-DriverPackage [/Server:<Server name>] {/DriverPackage:<Name> | /PackageId:<ID>} [/Name:<New Name>] [/Enabled:{Yes | No}
```

### <a name="parameters"></a>Parameter

|        Parameter         |                                                                                                                                                                                                               BESCHREIBUNG                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server name>] |                                                                                                                                                 Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                 |
| [/DriverPackage: \<Name> ] |                                                                                                                                                                                       Gibt den aktuellen Namen des zu ändernden Treiber Pakets an.                                                                                                                                                                                        |
|    [/PackageId: \<ID> ]    | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. Um diese ID für ein Paket zu finden, klicken Sie auf die Treiber Gruppe, in der sich das Paket befindet (oder den Knoten **alle Pakete** ), klicken Sie mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID ist auf der Registerkarte **Allgemein** aufgeführt. Beispiel: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}. |
|   [/Name: \<New Name> ]    |                                                                                                                                                                                              Gibt den neuen Namen für das Treiber Paket an.                                                                                                                                                                                              |
|      [/Enabled: {Ja      |                                                                                                                                                                                                                   Gar                                                                                                                                                                                                                    |

## <a name="examples"></a>Beispiele

Um die Einstellungen für ein Paket zu ändern, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /Set-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318} /Name:MyDriverPackage
```
```
WDSUTIL /Set-DriverPackage /DriverPackage:MyDriverPackage /Name:NewName /Enabled:Yes
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)