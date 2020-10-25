---
title: WDSUTIL Add-imagedriverpackage
description: Referenz Artikel für den Befehl "WDSUTIL Add-imagedriverpackage", mit dem ein Treiber Paket im Treiber Speicher einem vorhandenen Start Abbild auf dem Server hinzugefügt wird.
ms.topic: reference
ms.assetid: 6c2a4833-6427-47f8-9ffb-20b3786cb406
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5d441007f673a194799e245bb704d31add81a483
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524505"
---
# <a name="wdsutil-add-imagedriverpackage"></a>WDSUTIL Add-imagedriverpackage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem vorhandenen Start Abbild auf dem-Server ein Treiber Paket hinzu, das sich im Treiber Speicher befindet.

## <a name="syntax"></a>Syntax

```
wdsutil /add-ImageDriverPackage [/Server:<Servername>] [media:<Imagename>] [mediatype:Boot] [/Architecture:{x86 | ia64 | x64}] [/Filename:<Filename>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| [Medien: `<Imagename>` ] | Gibt den Namen des Bilds an, dem der Treiber hinzugefügt werden soll. |
| [MediaType: Boot] | Gibt den Typ des Bilds an, dem der Treiber hinzugefügt wird. Treiber Pakete können nur zu Start Abbildern hinzugefügt werden. |
| [/Architecture: `{x86 | ia64 | x64}` ] | Gibt die Architektur des Start Abbilds an. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass das richtige Image verwendet wird. |
| [/Filename:`<Filename>`] | Gibt den Namen der Datei an. Wenn das Bild nicht anhand des Namens eindeutig identifiziert werden kann, muss der Dateiname angegeben werden. |
| [/DriverPackage:`<Name>` | Gibt den Namen des Treiber Pakets an, das dem Abbild hinzugefügt werden soll. |
| [/PackageId: `<ID>` ] | Gibt die ID der Windows-Bereitstellungs Dienste des Treiber Pakets an. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. Wählen Sie zum Ermitteln der Paket-ID die Treiber Gruppe aus, in der sich das Paket befindet (oder den Knoten **alle Pakete** ), klicken Sie mit der rechten Maustaste auf das Paket, und wählen Sie dann **Eigenschaften**aus. Die Paket-ID ist auf der Registerkarte **Allgemein** aufgeführt. Beispiel: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}. |

## <a name="examples"></a>Beispiele

Wenn Sie einem Start Abbild ein Treiber Paket hinzufügen möchten, geben Sie Folgendes ein:

```
wdsutil /add-ImageDriverPackagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /DriverPackage:XYZ
```

```
wdsutil /verbose /add-ImageDriverPackagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl "Add-imagedriverpackages"](wdsutil-add-imagedriverpackages.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
