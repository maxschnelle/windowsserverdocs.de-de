---
title: convert
description: Referenz Thema für den Convert-Befehl, der einen Datenträger von einem Datenträger Datenträger in einen anderen konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab7189ea774750f8de2ceaecd9511fc8c3a71a97
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720738"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [Befehl "Basic konvertieren"](convert-basic.md) | Konvertiert einen leeren dynamischen Datenträger in eine Basisfestplatte. |
| [dynamischen Befehl konvertieren](convert-dynamic.md) | Konvertiert einen Basis Datenträger in einen dynamischen Datenträger. |
| [GPT-Befehl konvertieren](convert-gpt.md) | Konvertiert einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle). |
| [Befehl "MBR konvertieren"](convert-mbr.md) | Konvertiert einen leeren Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle) in einen Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR). |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
