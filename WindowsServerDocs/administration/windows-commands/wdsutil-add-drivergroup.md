---
title: WDSUTIL Add-drivergroup
description: Referenz Artikel für den Befehl "WDSUTIL Add-drivergroup", durch den dem Server eine Treiber Gruppe hinzugefügt wird.
ms.topic: reference
ms.assetid: 2a92fe8f-03f9-462a-b99e-f23275259807
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 68583ba35c141df03cbc5e351da6c4dc8ea4e161
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524615"
---
# <a name="wdsutil-add-drivergroup"></a>WDSUTIL Add-drivergroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt dem Server eine Treiber Gruppe hinzu.

## <a name="syntax"></a>Syntax

```
wdsutil /add-DriverGroup /DriverGroup:<Groupname>\n\ [/Server:<Servername>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}] [/Filtertype:<Filtertype> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /DriverGroup:`<Groupname>` | Gibt den Namen der neuen Treiber Gruppe an. |
| Servers`<Servername>` | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| Wodurch`{Yes|No}` | Aktiviert oder deaktiviert das Paket. |
| Barkeits`{Matched|All}` | Gibt an, welche Pakete installiert werden sollen, wenn die Filterkriterien erfüllt sind. **Übereinstimmende** bedeutet, dass nur die Treiber Pakete installiert werden, die mit einer Client-e- **Alle** bedeutet, dass alle Pakete unabhängig von Ihrer Hardware auf Clients installiert werden. |
| Filter Type`<Filtertype>` | Gibt den Typ des Filters an, der der Gruppe hinzugefügt werden soll. Sie können mehrere Filtertypen in einem einzelnen Befehl angeben. Auf jeden Filtertyp muss **/Policy** und mindestens ein **/value**folgen. Gültige Werte:<ul><li>Biosvendor</li><li>Biosversion</li><li>Chassistype</li><li>Hersteller</li><li>Uuid</li><li>OSVersion</li><li>Odition</li><li>OSLanguage</li></ul> Informationen zum erhalten von Werten für alle anderen Filtertypen finden Sie unter [Treiber Gruppen Filter](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759191(v=ws.11)). |
| [/Policy: `{Include|Exclude}` ] | Gibt die Richtlinie an, die für den Filter festgelegt werden soll. Wenn **/Policy** auf **include**festgelegt ist, können Client Computer, die dem Filter entsprechen, die Treiber in dieser Gruppe installieren. Wenn **/Policy** auf **Exclude**festgelegt ist, sind Client Computer, die dem Filter entsprechen, nicht berechtigt, die Treiber in dieser Gruppe zu installieren. |
| [/Value: `<Value>` ] | Gibt den Client Wert an, der **/FilterType**entspricht. Sie können mehrere Werte für einen einzelnen Typ angeben. Informationen zu zulässigen Filtertyp Werten finden Sie unter [Treiber Gruppen Filter](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759191(v=ws.11)). |

## <a name="examples"></a>Beispiele

Zum Hinzufügen einer Treiber Gruppe geben Sie Folgendes ein:

```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```

```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Applicability:All /Filtertype:Manufacturer /Policy:Include /Value:Name1 /Filtertype:Chassistype /Policy:Exclude /Value:Tower /Value:MiniTower
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl "Add-drivergrouppackage"](wdsutil-add-drivergrouppackage.md)

- [WDSUTIL-Befehl "Add-drivergrouppackages"](wdsutil-add-drivergrouppackages.md)

- [WDSUTIL-Befehl "Add-drivergroupfilter"](wdsutil-add-drivergroupfilter.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
