---
title: WDSUTIL Add-drivergrouppackages
description: Referenz Artikel für den Befehl "WDSUTIL Add-drivergrouppackages", mit dem Treiber GRUPPENPAKETE hinzugefügt werden.
ms.topic: reference
ms.assetid: 29022f53-ce14-4b2d-a81a-679c18e022b2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 67e211207f2c715053d734d659d511c61337e393
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524535"
---
# <a name="wdsutil-add-drivergrouppackages"></a>WDSUTIL Add-drivergrouppackages

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt Treiber GRUPPENPAKETE hinzu.

## <a name="syntax"></a>Syntax

```
wdsutil /add-DriverGroupPackages /DriverGroup:<Group Name> [/Server:<Server Name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /DriverGroup:`<Groupname>` | Gibt den Namen der neuen Treiber Gruppe an. |
| Servers`<Servername>` | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| Filter Type`<Filtertype>` | Gibt den Typ des Treiber Pakets an, nach dem gesucht werden soll. Sie können mehrere Attribute in einem einzelnen Befehl angeben. Sie müssen auch **/Operator** und **/value** mit dieser Option angeben. Gültige Werte:<ul><li>PackageId</li><li>PackageName</li><li>Packageaktivierte</li><li>Packagedateadded</li><li>Packageingeffilename</li><li>Packageclass<p>PackageProvider</li><li>PackageArchitecture</li><li>Packagelocale</li><li>Packagesigned</li><li>Packagedateveröffentlicht</li><li>Packageversion</li><li>Driverdescription</li><li>Driverhersteller</li><li>Driverhardwareid</li><li>Drivercompatibleid</li><li>Driverexcludeid</li><li>Drivergroupid</li><li>Drivergroupname * *</li></ul>. |
| KOM`{Equal|NotEqual|GreaterOrEqual|LessOrEqual|Contains}` | Gibt die Beziehung zwischen dem Attribut und den Werten an. Sie können nur " **enthält** "-Attribute mit Zeichen folgen Attributen angeben. Sie können nur " **EQUAL**", " **NotEqual**", " **greaterOrEqual** " und " **lessOrEqual** " mit Datums-und Versions Attributen angeben. |
| Wert`<Value>` | Gibt den Client Wert an, der **/FilterType**entspricht. Sie können mehrere Werte für ein einzelnes **/FilterType**angeben. Für jeden Filter sind die folgenden Werte verfügbar:<ul><li>**PackageID** : Geben Sie eine gültige GUID an. Beispiel: {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**PackageName** -geben Sie einen beliebigen Zeichen folgen Wert an</li><li>**Packageaktiviert** : Geben Sie **Ja** oder **Nein** an.</li><li>**Packagedateadded** -geben Sie das Datum im folgenden Format an: yyyy/mm/dd</li><li>**Packageinffilename** : Geben Sie einen beliebigen Zeichen folgen Wert an.</li><li>**Packageclass** : Geben Sie einen gültigen Klassennamen oder eine Klassen-GUID an. Beispiel: **diskdrive**, **net**oder {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**Packageprovider** -geben Sie einen beliebigen Zeichen folgen Wert an</li><li>**Packagearchitecture** : Angeben von **x86**, **x64**oder **ia64**</li><li>**Packagelocale** : Geben Sie einen gültigen sprach Bezeichner an. Beispiel: **en-US** oder **es-es**</li><li>**Packagesigned** -geben Sie **Ja** oder **Nein** an.</li><li>**Packagedatepublished** -geben Sie das Datum im folgenden Format an: yyyy/mm/dd</li><li>**Packageversion** : Geben Sie die Version im folgenden Format an: a.b.x.y. Beispiel: 6.1.0.0</li><li>**Driverdescription** : Geben Sie einen beliebigen Zeichen folgen Wert an</li><li>**Drivermanufacturer** -geben Sie einen beliebigen Zeichen folgen Wert an</li><li>**Driverhardwareid** : Geben Sie einen beliebigen Zeichen folgen Wert an.</li><li>**Drivercompatibleid** : Geben Sie einen beliebigen Zeichen folgen Wert an.</li><li>**Driverexcludeid** -geben Sie einen beliebigen Zeichen folgen Wert an.</li><li>**Drivergroupid** : Geben Sie eine gültige GUID an. Beispiel: {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**Drivergroupname** : Geben Sie einen beliebigen Zeichen folgen Wert an.</li></ul> Weitere Informationen zu diesen Werten finden Sie unter [Treiber-und Paket Attribute](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759262(v=ws.11)). |

## <a name="examples"></a>Beispiele

Zum Hinzufügen eines Treiber Gruppen Pakets geben Sie Folgendes ein:

```
wdsutil /verbose /add-DriverGroupPackages /DriverGroup:printerdrivers /Filtertype:PackageClass /Operator:Equal /Value:printer /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2
```

```
wdsutil /verbose /add-DriverGroupPackages /DriverGroup:DisplayDriversX86 /Filtertype:PackageClass /Operator:Equal /Value:Display /Filtertype:PackageArchitecture /Operator:Equal /Value:x86 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl "Add-DriverPackage"](wdsutil-add-driverpackage.md)

- [WDSUTIL-Befehl "Add-drivergrouppackage"](wdsutil-add-drivergrouppackage.md)

- [WDSUTIL-Befehl "Add-AllDriverPackages"](wdsutil-add-alldriverpackages.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
