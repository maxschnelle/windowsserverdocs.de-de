---
title: Mithilfe des Befehls Add-ImageDriverPackage
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c2a4833-6427-47f8-9ffb-20b3786cb406
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38d6c032f347f9945701f17b9289f3e3ff474031
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440620"
---
# <a name="using-the-add-imagedriverpackage-command"></a>Mithilfe des Befehls Add-ImageDriverPackage

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt ein Treiberpaket, das im Driver Store auf ein vorhandenes Startabbild auf dem Server ist. Die Version des Images muss Windows 7 oder Windows Server 2008 R2 oder höher.
## <a name="syntax"></a>Syntax
```
wdsutil /add-ImageDriverPackage [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64} 
```
```
[/Filename:<File name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>Parameter

|                 Parameter                  |                                                                                                                                                                                                            Beschreibung                                                                                                                                                                                                             |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           [/ Server:<Server name>           |                                                                                                                                               Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.                                                                                                                                                |
|             Medien:<Image name>             |                                                                                                                                                                                       Gibt den Namen des Bildes, das die Treiber hinzufügen.                                                                                                                                                                                        |
|               mediatype:Boot               |                                                                                                                                                                Gibt den Typ des Bilds, das die Treiber hinzufügen. Treiberpakete können nur um zu Startabbildern hinzugefügt werden.                                                                                                                                                                 |
| /Architecture:{x86 &#124; ia64 &#124; x64} |                                                                                                       Gibt die Architektur des Startabbilds. Da es möglich, dass der gleiche ImageName für Startabbilder in verschiedenen Architekturen handelt, sollten Sie angeben, die Architektur, um sicherzustellen, dass das richtige Image verwendet wird.                                                                                                        |
|           / Filename:<File name>]           |                                                                                                                                                        Gibt den Namen der Datei. Wenn das Bild nach Namen eindeutig identifiziert werden kann, muss der Dateiname angegeben werden.                                                                                                                                                        |
|           [/ DriverPackage /:<Name>           |                                                                                                                                                                                   Gibt den Namen des Treiberpakets auf das Bild hinzufügen.                                                                                                                                                                                    |
|             [/PackageId:<ID>]              | Gibt die Windows Deployment Services-ID des Treiberpakets an. Sie müssen diese Option angeben, wenn das Treiberpaket eindeutig anhand des Namens identifiziert werden kann. Um die Paket-ID zu suchen, klicken Sie auf die Treibergruppe gewährt wird, der das Paket wird (oder die **alle Pakete** Knoten) mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID finden Sie auf die **allgemeine** Registerkarte. Zum Beispiel: {DD098D20-1850-4fc8-8E35-EA24A1BEFF5E}. |

## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, zum Hinzufügen eines Treiberpakets zu einem Startabbild:
```
wdsutil /add-ImageDriverPackagmedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86 /DriverPackage:XYZ
```
```
wdsutil /verbose /add-ImageDriverPackagmedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Add-ImageDriverPackages](using-the-add-imagedriverpackages-command.md)
