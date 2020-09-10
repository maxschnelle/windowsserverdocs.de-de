---
title: bcdboot
description: Referenz Artikel für den BCDboot-Befehl, der schnell eine Systempartition einrichten oder die in der Systempartition befindliche Start Umgebung reparieren kann.
ms.topic: reference
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b7cc67c47093686882f0a7bfa1fcc47f8c444210
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632979"
---
# <a name="bcdboot"></a>bcdboot

Ermöglicht es Ihnen, schnell eine Systempartition einzurichten oder die Start Umgebung zu reparieren, die sich auf der Systempartition befindet. Die Systempartition wird eingerichtet, indem ein einfacher Satz von Startkonfigurationsdaten Dateien (BCD) in eine vorhandene leere Partition kopiert wird.

## <a name="syntax"></a>Syntax

```
bcdboot <source> [/l] [/s]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| source | Gibt den Speicherort des Windows-Verzeichnisses an, das als Quelle zum Kopieren von Start Umgebungs Dateien verwendet werden soll. |
| /l | Gibt das Gebiets Schema an. Das Standard Gebiets Schema ist US-Englisch. |
| /s | Gibt den volumenbuchstabe der Systempartition an. Der Standardwert ist die von der Firmware identifizierte Systempartition. |

## <a name="examples"></a>Beispiele

Informationen dazu, wo Sie BCDboot finden, sowie Beispiele zur Verwendung dieses Befehls finden Sie im Thema [BCDboot-Befehlszeilenoptionen](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824874(v=win.10)) .

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
