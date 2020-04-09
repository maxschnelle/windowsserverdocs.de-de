---
title: convert
description: Windows-Befehls Thema für Convert, bei dem ein Datenträger von einem Datenträger in einen anderen konvertiert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1b5c62b7e51b497faac77a13185f844de230d67
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847183"
---
# <a name="convert"></a>convert

Konvertiert einen Datenträger von einem Datenträger in einen anderen.

## <a name="syntax"></a>Syntax

```
convert basic
convert dynamic
convert gpt
convert mbr
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Standard konvertieren](convert-basic.md)|Konvertiert einen leeren dynamischen Datenträger in eine Basisfestplatte.|
|[Dynamisch konvertieren](convert-dynamic.md)|Konvertiert einen Basis Datenträger in einen dynamischen Datenträger.|
|[GPT konvertieren](convert-gpt.md)|Konvertiert einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle).|
|[MBR konvertieren](convert-mbr.md)|Konvertiert einen leeren Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle) in einen Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR).|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

