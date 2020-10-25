---
title: WDSUTIL Add-imagedriverpackages
description: Referenz Artikel für den Befehl WDSUTIL Add-imagedriverpackages, mit dem Treiber Pakete aus dem Treiber Speicher einem Start Abbild hinzugefügt werden.
ms.topic: reference
ms.assetid: 9dc78909-a4d1-42a2-af8f-21ebcbfe8302
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 74029ca7b2243603c832b74f59a9248353cea911
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524475"
---
# <a name="wdsutil-add-imagedriverpackages"></a>WDSUTIL Add-imagedriverpackages

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hinzufügen von Treiber Paketen aus dem Treiber Speicher zu einem Start Abbild.

## <a name="syntax"></a>Syntax

```
wdsutil /add-ImageDriverPackages [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| [Medien: `<Imagename>` ] | Gibt den Namen des Bilds an, dem der Treiber hinzugefügt werden soll. |
| [MediaType: Boot] | Gibt den Typ des Bilds an, dem der Treiber hinzugefügt wird. Treiber Pakete können nur zu Start Abbildern hinzugefügt werden. |
| [/Architecture: `{x86 | ia64 | x64}` ] | Gibt die Architektur des Start Abbilds an. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass das richtige Image verwendet wird. |
| [/Filename:`<Filename>`] | Gibt den Namen der Datei an. Wenn das Bild nicht anhand des Namens eindeutig identifiziert werden kann, muss der Dateiname angegeben werden. |
| Filter Type`<Filtertype>` | Gibt das Attribut des Treiber Pakets an, nach dem gesucht werden soll. Sie können mehrere Attribute in einem einzelnen Befehl angeben. Sie müssen auch **/Operator** und **/value** mit dieser Option angeben. Gültige Werte:<ul><li>PackageId</li><li>PackageName</li><li>Packageaktivierte</li><li>Packagedateadded</li><li>Packageingeffilename</li><li>Packageclass<p>PackageProvider</li><li>PackageArchitecture</li><li>Packagelocale</li><li>Packagesigned</li><li>Packagedateveröffentlicht</li><li>Packageversion</li><li>Driverdescription</li><li>Driverhersteller</li><li>Driverhardwareid</li><li>Drivercompatibleid</li><li>Driverexcludeid</li><li>Drivergroupid</li><li>Drivergroupname * *</li></ul>. |
| KOM`{Equal|NotEqual|GreaterOrEqual|LessOrEqual|Contains}` | Gibt die Beziehung zwischen dem Attribut und den Werten an. Sie können nur " **enthält** "-Attribute mit Zeichen folgen Attributen angeben. Sie können nur " **greaterOrEqual** " und " **lessOrEqual** " mit Datums-und Versions Attributen angeben. |
| Wert`<Value>` | Gibt den Wert an, der relativ zum angegebenen gesucht werden soll `<attribute>` . Sie können mehrere Werte für ein einzelnes **/FilterType**angeben. Für jeden Filter sind die folgenden Werte verfügbar:<ul><li>**PackageID** : Geben Sie eine gültige GUID an. Beispiel: {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**PackageName** -geben Sie einen beliebigen Zeichen folgen Wert an</li><li>**Packageaktiviert** : Geben Sie **Ja** oder **Nein** an.</li><li>**Packagedateadded** -geben Sie das Datum im folgenden Format an: yyyy/mm/dd</li><li>**Packageinffilename** : Geben Sie einen beliebigen Zeichen folgen Wert an.</li><li>**Packageclass** : Geben Sie einen gültigen Klassennamen oder eine Klassen-GUID an. Beispiel: **diskdrive**, **net**oder {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**Packageprovider** -geben Sie einen beliebigen Zeichen folgen Wert an</li><li>**Packagearchitecture** : Angeben von **x86**, **x64**oder **ia64**</li><li>**Packagelocale** : Geben Sie einen gültigen sprach Bezeichner an. Beispiel: **en-US** oder **es-es**</li><li>**Packagesigned** -geben Sie **Ja** oder **Nein** an.</li><li>**Packagedatepublished** -geben Sie das Datum im folgenden Format an: yyyy/mm/dd</li><li>**Packageversion** : Geben Sie die Version im folgenden Format an: a.b.x.y. Beispiel: 6.1.0.0</li><li>**Driverdescription** : Geben Sie einen beliebigen Zeichen folgen Wert an</li><li>**Drivermanufacturer** -geben Sie einen beliebigen Zeichen folgen Wert an</li><li>**Driverhardwareid** : Geben Sie einen beliebigen Zeichen folgen Wert an.</li><li>**Drivercompatibleid** : Geben Sie einen beliebigen Zeichen folgen Wert an.</li><li>**Driverexcludeid** -geben Sie einen beliebigen Zeichen folgen Wert an.</li><li>**Drivergroupid** : Geben Sie eine gültige GUID an. Beispiel: {4D36E972-E325-11CE-BFC1-08002BE10318}</li><li>**Drivergroupname** : Geben Sie einen beliebigen Zeichen folgen Wert an.</li></ul> Weitere Informationen zu diesen Werten finden Sie unter [Treiber-und Paket Attribute](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759262(v=ws.11)). |

## <a name="examples"></a>Beispiele

Zum Hinzufügen von Treiber Paketen zu einem Start Abbild geben Sie eine der folgenden Informationen ein:

```
wdsutil /add-ImageDriverPackagemedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /Filtertype:DriverGroupName /Operator:Equal /Value:x86Bus /Filtertype:PackageProvider /Operator:Contains /Value:Provider1 /Filtertype:Packageversion /Operator:GreaterOrEqual /Value:6.1.0.0
```

```
wdsutil /verbose /add-ImageDriverPackagemedia: WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```

```
wdsutil /verbose /add-ImageDriverPackagemedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Value:System /Value:DiskDrive /Value:HDC /Value:SCSIAdapter
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-
- [WDSUTIL-Befehl "Add-imagedriverpackage"](wdsutil-add-imagedriverpackage.md)
-
- [WDSUTIL-Befehl "Add-AllDriverPackages"](wdsutil-add-alldriverpackages.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
