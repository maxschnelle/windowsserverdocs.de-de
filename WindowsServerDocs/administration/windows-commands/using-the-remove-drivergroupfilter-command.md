---
title: Remove-drivergroupfilter
description: Referenz Artikel zu Remove-drivergroupfilter, mit dem eine Filterregel aus einer Treiber Gruppe auf einem Server entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98d2253cc5148ba4581399d688b74cd426a649fb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936328"
---
# <a name="remove-drivergroupfilter"></a>Remove-drivergroupfilter



Entfernt eine Filterregel aus einer Treiber Gruppe auf einem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/DriverGroup:\<Group Name>|Gibt den Namen der Treiber Gruppe an.|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/FILTERTYPE: \<FilterType> ]|Gibt den Typ des Filters an, der aus der Gruppe entfernt werden soll. \<FilterType>kann eines der folgenden sein:</br>**Biosvendor**</br>**Biosversion**</br>**ChassisType**</br>**Hersteller**</br>**UUID**</br>**OsVersion**</br>**Odition**</br>**OSLanguage**|

## <a name="examples"></a>Beispiele

Um einen Filter zu entfernen, geben Sie einen der folgenden Informationen ein:
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)