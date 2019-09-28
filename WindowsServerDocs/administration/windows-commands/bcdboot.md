---
title: bcdboot
description: 'Windows-Befehle Thema für **BCDboot** : richten Sie schnell eine Systempartition ein, oder reparieren Sie die Start Umgebung, die sich auf der Systempartition befindet.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: a1c0f505180a503617335cc9575fea3d346bbe02
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383437"
---
# <a name="bcdboot"></a>bcdboot



Ermöglicht es Ihnen, schnell eine Systempartition einzurichten oder die Start Umgebung zu reparieren, die sich auf der Systempartition befindet. Die Systempartition wird eingerichtet, indem ein einfacher Satz von Startkonfigurationsdaten Dateien (BCD) in eine vorhandene leere Partition kopiert wird.

Weitere Informationen zu BCDboot, einschließlich Informationen dazu, wo Sie BCDboot finden, sowie Beispiele zur Verwendung dieses Befehls finden Sie im Thema [BCDboot-Befehlszeilenoptionen](https://technet.microsoft.com/library/hh824874.aspx) .

## <a name="syntax"></a>Syntax

```
bcdboot <source> [/l] [/s]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Quelle|Gibt den Speicherort des Windows-Verzeichnisses an, das als Quelle zum Kopieren von Start Umgebungs Dateien verwendet werden soll.|
|/l|Gibt das Gebiets Schema an. Das Standard Gebiets Schema ist US-Englisch.|
|/s|Gibt den volumenbuchstabe der Systempartition an. Der Standardwert ist die von der Firmware identifizierte Systempartition.|

## <a name="BKMK_examples"></a>Beispiele

Weitere Beispiele zur Verwendung dieses Befehls finden Sie im Thema [BCDboot-Befehlszeilenoptionen](https://technet.microsoft.com/library/hh824874.aspx) .

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)