---
title: bcdboot
description: Windows-Befehls Thema für **BCDboot**, das schnell eine Systempartition einrichten oder die Start Umgebung auf der Systempartition reparieren kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 637170cbd8ee4f3c11ee1dc77a0cd49b5dfa3038
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851083"
---
# <a name="bcdboot"></a>bcdboot

Ermöglicht es Ihnen, schnell eine Systempartition einzurichten oder die Start Umgebung zu reparieren, die sich auf der Systempartition befindet. Die Systempartition wird eingerichtet, indem ein einfacher Satz von Startkonfigurationsdaten Dateien (BCD) in eine vorhandene leere Partition kopiert wird.

## <a name="syntax"></a>Syntax

```
bcdboot <source> [/l] [/s]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| source | Gibt den Speicherort des Windows-Verzeichnisses an, das als Quelle zum Kopieren von Start Umgebungs Dateien verwendet werden soll. |
| /l | Gibt das Gebietsschema an. Das Standard Gebiets Schema ist US-Englisch. |
| /s | Gibt den Volumebuchstaben der Systempartition an. Der Standardwert ist die von der Firmware identifizierte Systempartition. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Informationen dazu, wo Sie BCDboot finden, sowie Beispiele zur Verwendung dieses Befehls finden Sie im Thema [BCDboot-Befehlszeilenoptionen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824874(v=win.10)x) .

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)