---
title: Bdehdcfg driveinfo
description: 'Windows-Befehle Thema ** Bdehdcfg: Driveinfo **: der Buchstabe des Laufwerks, beträgt die Gesamtgröße, der maximale freie Speicherplatz und die Partitionseigenschaften angezeigt.'
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b2dd62e34f8205e0b5d395ba759fff4b4937b0ad
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435042"
---
# <a name="bdehdcfg-driveinfo"></a>Bdehdcfg: Driveinfo

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt an, der Buchstabe des Laufwerks, beträgt die Gesamtgröße, der maximale freie Speicherplatz und die Partitionseigenschaften. Nur gültige Partitionen sind aufgeführt. Verfügbarer Speicher ist nicht aufgeführt, wenn bereits vier primäre oder erweiterte Partitionen vorhanden sind. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).
## <a name="syntax"></a>Syntax
```
bdehdcfg -driveinfo <DriveLetter>
```
### <a name="parameters"></a>Parameter

|   Parameter   |                  Beschreibung                  |
|---------------|-----------------------------------------------|
| <DriveLetter> | Gibt einen Laufwerkbuchstaben an, gefolgt von einem Doppelpunkt an. |

## <a name="remarks"></a>Hinweise
Der Befehl dient nur zu Informationszwecken und ist keine Änderungen auf das Laufwerk.
## <a name="BKMK_Examples"></a>Beispiel
Das folgende Beispiel zeigt die Laufwerkinformationen für Laufwerk c:.
```
bdehdcfg  driveinfo C:
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [bdehdcfg](bdehdcfg.md)
