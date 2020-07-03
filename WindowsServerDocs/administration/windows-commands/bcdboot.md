---
title: bcdboot
description: Referenz Artikel für den BCDboot-Befehl, der schnell eine Systempartition einrichten oder die in der Systempartition befindliche Start Umgebung reparieren kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: def4052e8aaa4f1e32216b5de837706b5cde3d04
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923503"
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

Informationen dazu, wo Sie BCDboot finden, sowie Beispiele zur Verwendung dieses Befehls finden Sie im Thema [BCDboot-Befehlszeilenoptionen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824874(v=win.10)) .

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
