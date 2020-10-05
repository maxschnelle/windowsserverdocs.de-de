---
title: WDSUTIL Add-imagedriverpackage
description: Referenz Artikel zu WDSUTIL Add-imagedriverpackage, mit dem ein Treiber Paket im Treiber Speicher einem vorhandenen Start Abbild auf dem Server hinzugefügt wird.
ms.topic: reference
ms.assetid: 6c2a4833-6427-47f8-9ffb-20b3786cb406
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5a85e64f39b360b5e970a15bd0da85326d67b06a
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730444"
---
# <a name="wdsutil-add-imagedriverpackage"></a>WDSUTIL Add-imagedriverpackage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem vorhandenen Start Abbild auf dem-Server ein Treiber Paket hinzu, das sich im Treiber Speicher befindet. Die Image Version muss Windows 7 oder Windows Server 2008 R2 oder höher sein.

## <a name="syntax"></a>Syntax
```
wdsutil /add-ImageDriverPackage [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64}
```
```
[/Filename:<File name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>Parameter

|                 Parameter                  |                                                                                                                                                                                                            BESCHREIBUNG                                                                                                                                                                                                             |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /Server<Server name>           |                                                                                                                                               Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                |
|             Medien<Image name>             |                                                                                                                                                                                       Gibt den Namen des Bilds an, dem der Treiber hinzugefügt werden soll.                                                                                                                                                                                        |
|               MediaType: Boot               |                                                                                                                                                                Gibt den Typ des Bilds an, dem der Treiber hinzugefügt wird. Treiber Pakete können nur zu Start Abbildern hinzugefügt werden.                                                                                                                                                                 |
| /Architecture: {x86 &#124; ia64 &#124; x64} |                                                                                                       Gibt die Architektur des Start Abbilds an. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass das richtige Image verwendet wird.                                                                                                        |
|           /Filename: <File name> ]           |                                                                                                                                                        Gibt den Namen der Datei an. Wenn das Bild nicht anhand des Namens eindeutig identifiziert werden kann, muss der Dateiname angegeben werden.                                                                                                                                                        |
|           [/DriverPackage:<Name>           |                                                                                                                                                                                   Gibt den Namen des Treiber Pakets an, das dem Abbild hinzugefügt werden soll.                                                                                                                                                                                    |
|             [/PackageId: <ID> ]              | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. Klicken Sie zum Ermitteln der Paket-ID auf die Treiber Gruppe, in der sich das Paket befindet (oder auf den Knoten **alle Pakete** ), klicken Sie mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID ist auf der Registerkarte **Allgemein** aufgeführt. Beispiel: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}. |

## <a name="examples"></a>Beispiele
Wenn Sie einem Start Abbild ein Treiber Paket hinzufügen möchten, geben Sie einen der folgenden Schritte ein:
```
wdsutil /add-ImageDriverPackagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /DriverPackage:XYZ
```
```
wdsutil /verbose /add-ImageDriverPackagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-imagedriverpackages"](wdsutil-add-imagedriverpackages.md)
