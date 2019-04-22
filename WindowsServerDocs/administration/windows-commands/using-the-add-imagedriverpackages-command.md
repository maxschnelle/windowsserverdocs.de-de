---
title: Mithilfe des Befehls Add-ImageDriverPackages
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9dc78909-a4d1-42a2-af8f-21ebcbfe8302
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55b26acf9c4006db3d64e27be8a10e158876ddc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817361"
---
# <a name="using-the-add-imagedriverpackages-command"></a>Mithilfe des Befehls Add-ImageDriverPackages

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

ein Startimage hinzugefügt Treiberpakete aus dem Treiberspeicher. Die Version des Images muss Windows 7 oder Windows Server 2008 R2 oder höher.
Beispiele, wie Sie diesen Befehl verwenden können, finden Sie unter [Beispiele](#BKMK_examples).
## <a name="syntax"></a>Syntax
```
wdsutil /add-ImageDriverPackages [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64} 
[/Filename:<File name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ Server:<Server name>|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
Medien:<Image name>|Gibt den Namen des Bildes, das die Treiber hinzufügen.|
mediatype:Boot|Gibt den Typ des Bilds, das die Treiber hinzufügen. Treiberpakete können um nur zu Startabbildern hinzugefügt werden.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Startabbilds. Da es möglich, dass der gleiche ImageName für Startabbilder in verschiedenen Architekturen handelt, sollten Sie angeben, die Architektur, um sicherzustellen, dass das richtige Image verwendet wird.|
|/ Filename:<File name>|Gibt den Dateinamen an. Wenn das Bild nach Namen eindeutig identifiziert werden kann, muss der Dateiname angegeben werden.|
|/Filtertype:<Filter type>|Gibt das Attribut des zu suchenden Treiberpakets. Sie können mehrere Attribute in einem einzigen Befehl angeben. Sie müssen auch angeben, **/Operator** und **-Wert-** mit dieser Option.<br /><br /><Filter type> Dabei kann es sich um eine der folgenden sein:<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/Operator:{Equal &#124; NotEqual &#124; GreaterOrEqual &#124; LessOrEqual &#124; Contains}|Die Beziehung zwischen dem Attribut und die Werte. Sie können nur angeben **Contains** mit Zeichenfolgenattributen. Sie können nur angeben **grösser oder gleich** und **kleiner oder gleich** mit Datum und die Version-Attribute.|
|Wert:<Value>|Gibt den Wert für die Suche, relativ zum angegebenen <attribute>. Sie können angeben, mehrere Werte für ein einzelnes **/Filtertype**. Der folgenden Liste werden die Attribute, die Sie für jeden Filter geben können. Weitere Informationen zu diesen Attributen finden Sie unter [Treiber und Paket-Attribute](https://go.microsoft.com/fwlink/?LinkId=166895) (https://go.microsoft.com/fwlink/?LinkId=166895).<br /><br />-PackageId - Geben Sie eine gültige GUID. Zum Beispiel: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-Geben Sie Paketname jeder string-Wert.<br />-Geben Sie PackageEnabled - **Ja** oder **keine**.<br />-Packagedateadded - Geben Sie das Datum im folgenden Format: JJJJ/MM/TT<br />-Geben Sie PackageInfFilename jeder string-Wert.<br />-PackageClass - Geben Sie einen gültigen Klassennamen oder den Klassen-GUID. Zum Beispiel: **Laufwerk**, **Net**, oder {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-Geben Sie PackageProvider jeder string-Wert.<br />-Geben Sie PackageArchitecture - **X86**, **X64**, oder **ia64**.<b /> -PackageLocale - Geben Sie einen gültiger Sprachbezeichner. Zum Beispiel: **En-US** oder **es-ES**.<br />-Geben Sie PackageSigned - **Ja** oder **keine**.<br />-PackagedatePublished - Geben Sie das Datum im folgenden Format: JJJJ/MM/TT<br />-Packageversion - Geben Sie die Version im folgenden Format: a.b.x.y. Zum Beispiel: 6.1.0.0<br />-Geben Sie Driverdescription jeder string-Wert.<br />-Geben Sie DriverManufacturer jeder string-Wert.<br />-DriverHardwareId - Geben Sie einen beliebigen Zeichenfolgenwert.<br />-DrivercompatibleId - Geben Sie einen beliebigen Zeichenfolgenwert.<br />-DriverExcludeId - Geben Sie einen beliebigen Zeichenfolgenwert.<br />-DriverGroupId - Geben Sie eine gültige GUID. Zum Beispiel: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-Geben Sie DriverGroupName jeder string-Wert.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, um ein Startimage Treiberpakete hinzuzufügen:
```
wdsutil /add-ImageDriverPackagemedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86 /Filtertype:DriverGroupName /Operator:Equal /Value:x86Bus /Filtertype:PackageProvider /Operator:Contains /Value:Provider1 /Filtertype:Packageversion /Operator:GreaterOrEqual /Value:6.1.0.0
```
```
wdsutil /verbose /add-ImageDriverPackagemedia: "WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```
```
wdsutil /verbose /add-ImageDriverPackagemedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filtertype:PackageClass /Operator:Equal /Value:Net /Value:System /Value:DiskDrive /Value:HDC /Value:SCSIAdapter
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Add-ImageDriverPackage](using-the-add-imagedriverpackage-command.md)
[mit dem Add-AllDriverPackages Unterbefehl](using-the-add-alldriverpackages-subcommand.md)
