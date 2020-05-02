---
title: bdehdcfg DriveInfo
description: Referenz Thema für den Befehl bdehdcfg DriveInfo, der den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b18b4c3e128cd17353d369b418a049d0208cb654
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718687"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: DriveInfo

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale an. Nur gültige Partitionen sind aufgeführt. Verfügbarer Speicher ist nicht aufgeführt, wenn bereits vier primäre oder erweiterte Partitionen vorhanden sind.

>[!NOTE]
> Dieser Befehl dient nur zu Informationszwecken und führt keine Änderungen am Laufwerk aus.

## <a name="syntax"></a>Syntax

```
bdehdcfg -driveinfo <drive_letter>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| <drive_letter> | Gibt einen Laufwerk Buchstaben gefolgt von einem Doppelpunkt an. |

## <a name="example"></a>Beispiel

So zeigen Sie die Laufwerk Informationen für das Laufwerk "C:" an:

```
bdehdcfg  driveinfo C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
