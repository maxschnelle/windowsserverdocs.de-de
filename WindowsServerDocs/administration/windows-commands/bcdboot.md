---
title: bcdboot
description: Referenz Artikel für den BCDboot-Befehl, der schnell eine Systempartition einrichten oder die in der Systempartition befindliche Start Umgebung reparieren kann.
ms.topic: reference
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fedbd771efb3d2bba63f906b446632114fa91858
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031618"
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
| /l | Gibt das Gebiets Schema an. Das Standard Gebiets Schema ist US-Englisch. |
| /s | Gibt den volumenbuchstabe der Systempartition an. Der Standardwert ist die von der Firmware identifizierte Systempartition. |

## <a name="examples"></a>Beispiele

Informationen dazu, wo Sie BCDboot finden, sowie Beispiele zur Verwendung dieses Befehls finden Sie im Thema [BCDboot-Befehlszeilenoptionen](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824874(v=win.10)) .

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
