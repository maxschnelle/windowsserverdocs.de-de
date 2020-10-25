---
title: Add-drivergroupfilter
description: Referenz Artikel für den Befehl "Add-drivergroupfilter", mit dem einer Treiber Gruppe auf einem Server ein Filter hinzugefügt wird.
ms.topic: reference
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bd9e26e7bdf6b1a03d01b2993c969bbbcf5b8754
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524605"
---
# <a name="add-drivergroupfilter"></a>Add-drivergroupfilter

Fügt einer Treiber Gruppe auf einem Server einen Filter hinzu.

## <a name="syntax"></a>Syntax

```
wdsutil /Add-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /DriverGroup:`<Groupname>` | Gibt den Namen der neuen Treiber Gruppe an. |
| Servers`<Servername>` | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| Filter Type`<Filtertype>` | Gibt den Typ des Filters an, der der Gruppe hinzugefügt werden soll. Sie können mehrere Filtertypen in einem einzelnen Befehl angeben. Auf jeden Filtertyp muss **/Policy** und mindestens ein **/value**folgen. Gültige Werte:<ul><li>Biosvendor</li><li>Biosversion</li><li>Chassistype</li><li>Hersteller</li><li>Uuid</li><li>OSVersion</li><li>Odition</li><li>OSLanguage</li></ul> Informationen zum erhalten von Werten für alle anderen Filtertypen finden Sie unter [Treiber Gruppen Filter](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759191(v=ws.11)). |
| [/Policy: `{Include|Exclude}` ] | Gibt die Richtlinie an, die für den Filter festgelegt werden soll. Wenn **/Policy** auf **include**festgelegt ist, können Client Computer, die dem Filter entsprechen, die Treiber in dieser Gruppe installieren. Wenn **/Policy** auf **Exclude**festgelegt ist, sind Client Computer, die dem Filter entsprechen, nicht berechtigt, die Treiber in dieser Gruppe zu installieren. |
| [/Value: `<Value>` ] | Gibt den Client Wert an, der **/FilterType**entspricht. Sie können mehrere Werte für einen einzelnen Typ angeben. Informationen zu zulässigen Filtertyp Werten finden Sie unter [Treiber Gruppen Filter](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759191(v=ws.11)). |

## <a name="examples"></a>Beispiele

Wenn Sie einer Treiber Gruppe einen Filter hinzufügen möchten, geben Sie Folgendes ein:

```
wdsutil /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```

```
wdsutil /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl "Add-drivergrouppackage"](wdsutil-add-drivergrouppackage.md)

- [WDSUTIL-Befehl "Add-drivergrouppackages"](wdsutil-add-drivergrouppackages.md)

- [WDSUTIL-Befehl "Add-drivergroup"](wdsutil-add-drivergroup.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
