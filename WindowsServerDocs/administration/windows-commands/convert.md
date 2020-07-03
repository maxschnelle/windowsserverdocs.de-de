---
title: convert
description: Referenz Artikel für den Convert-Befehl, der einen Datenträger von einem Datenträger Datenträger in einen anderen konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f93f2b16838a6f54af3f28b7e0883808a6cd013a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928907"
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

| Parameter | Beschreibung |
| --------- | ----------- |
| [Befehl "Basic konvertieren"](convert-basic.md) | Konvertiert einen leeren dynamischen Datenträger in eine Basisfestplatte. |
| [dynamischen Befehl konvertieren](convert-dynamic.md) | Konvertiert einen Basis Datenträger in einen dynamischen Datenträger. |
| [GPT-Befehl konvertieren](convert-gpt.md) | Konvertiert einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle). |
| [Befehl "MBR konvertieren"](convert-mbr.md) | Konvertiert einen leeren Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle) in einen Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR). |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
