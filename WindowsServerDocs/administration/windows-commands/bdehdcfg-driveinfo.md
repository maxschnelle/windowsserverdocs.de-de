---
title: bdehdcfg driveinfo
description: Referenz Artikel für den Befehl bdehdcfg DriveInfo, der den Laufwerk Buchstaben, die Gesamtgröße, den maximalen freien Speicherplatz und die Partitions Merkmale anzeigt.
ms.topic: reference
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fb474e40e92979f5f2cf73d90a553bbf785c0312
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632964"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
