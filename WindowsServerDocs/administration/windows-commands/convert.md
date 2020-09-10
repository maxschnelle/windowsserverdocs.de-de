---
title: umgebaut
description: Referenz Artikel für den Convert-Befehl, der einen Datenträger von einem Datenträger Datenträger in einen anderen konvertiert.
ms.topic: reference
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 654d5266fff3a3fffadb9d176eb07a792f22fa01
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629273"
---
# <a name="convert"></a>umgebaut

Konvertiert einen Datenträger von einem Datenträger in einen anderen.

## <a name="syntax"></a>Syntax

```
convert basic
convert dynamic
convert gpt
convert mbr
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [Befehl "Basic konvertieren"](convert-basic.md) | Konvertiert einen leeren dynamischen Datenträger in eine Basisfestplatte. |
| [dynamischen Befehl konvertieren](convert-dynamic.md) | Konvertiert einen Basis Datenträger in einen dynamischen Datenträger. |
| [GPT-Befehl konvertieren](convert-gpt.md) | Konvertiert einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle). |
| [Befehl "MBR konvertieren"](convert-mbr.md) | Konvertiert einen leeren Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle) in einen Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR). |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
