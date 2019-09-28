---
title: bdehdcfg DriveInfo
description: 'Thema Windows-Befehle für * * bdehdcfg: DriveInfo * *-zeigt den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale an.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0f4541bfd71fb7639d18e6e548559ed02918815
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382267"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: DriveInfo

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale an. Nur gültige Partitionen sind aufgeführt. Verfügbarer Speicher ist nicht aufgeführt, wenn bereits vier primäre oder erweiterte Partitionen vorhanden sind. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).
## <a name="syntax"></a>Syntax
```
bdehdcfg -driveinfo <DriveLetter>
```
### <a name="parameters"></a>Parameter

|   Parameter   |                  Beschreibung                  |
|---------------|-----------------------------------------------|
| <DriveLetter> | Gibt einen Laufwerk Buchstaben gefolgt von einem Doppelpunkt an. |

## <a name="remarks"></a>Hinweise
Der Befehl dient nur zu Informationszwecken und führt keine Änderungen am Laufwerk aus.
## <a name="BKMK_Examples"></a>Beispiel
Im folgenden Beispiel werden die Laufwerks Informationen für Laufwerk C angezeigt.
```
bdehdcfg  driveinfo C:
```
## <a name="additional-references"></a>Weitere Verweise
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [bdehdcfg](bdehdcfg.md)
