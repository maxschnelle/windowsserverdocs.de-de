---
title: bdehdcfg DriveInfo
description: Windows-Befehls Thema für **bdehdcfg DriveInfo**, das den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c598ea2d1d140090d623b3b48dbcc1be51ee66c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851063"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: DriveInfo

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale an. Nur gültige Partitionen sind aufgeführt. Verfügbarer Speicher ist nicht aufgeführt, wenn bereits vier primäre oder erweiterte Partitionen vorhanden sind.

Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -driveinfo <DriveLetter>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| <DriveLetter> | Gibt einen Laufwerk Buchstaben gefolgt von einem Doppelpunkt an. |

## <a name="remarks"></a>Hinweise

Der Befehl dient nur zu Informationszwecken und führt keine Änderungen am Laufwerk aus.

## <a name="example"></a><a name=BKMK_Examples></a>Beispiel

Im folgenden Beispiel werden die Laufwerks Informationen für Laufwerk C angezeigt.

```
bdehdcfg  driveinfo C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
