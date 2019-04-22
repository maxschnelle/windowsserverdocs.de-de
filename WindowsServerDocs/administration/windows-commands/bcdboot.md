---
title: bcdboot
description: Windows-Befehle Thema **Bcdboot** – schnell eine Systempartition einrichten, oder reparieren Sie die Boot-Umgebung, die sich auf der Systempartition befindet.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78838dd6567ad886948df8ac21425a8f9b596d5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825881"
---
# <a name="bcdboot"></a>bcdboot



Ermöglicht es Ihnen, die zum schnellen Einrichten einer Partition oder reparieren die Boot-Umgebung, die sich auf der Systempartition befindet. Die Systempartition wird eingerichtet, von einem einfachen Satz von Startkonfigurationsdaten (Boot Configuration Data, BCD)-Dateien in eine leere Partition kopiert wird.

Weitere Informationen zu BCDboot, einschließlich Informationen zum Aufrufen von BCDboot und Beispiele für diesen Befehl verwenden, finden Sie unter den [BCDboot-Befehlszeilenoptionen](https://technet.microsoft.com/library/hh824874.aspx) Thema.

## <a name="syntax"></a>Syntax

```
bcdboot <source> [/l] [/s]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Quelle|Gibt den Speicherort des Windows-Verzeichnisses, das als Quelle verwenden, zum Kopieren von Startdateien-Umgebung.|
|/l|Gibt das Gebietsschema. Das Standardgebietsschema ist Englisch (USA).|
|/s|Gibt an, dem Volumebuchstaben der Systempartition. Der Standardwert ist die Systempartition von der Firmware identifiziert.|

## <a name="BKMK_examples"></a>Beispiele für

Weitere Beispiele zur Verwendung mit diesem Befehl finden Sie in der [BCDboot-Befehlszeilenoptionen](https://technet.microsoft.com/library/hh824874.aspx) Thema.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)