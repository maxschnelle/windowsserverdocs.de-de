---
title: biout admin Cache und setLimit
description: Windows-Befehls Thema für **bitadmin-Cache und setLimit**, mit dem die Cache Größenbeschränkung festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 746ee0b69da8f5bd22fec2ccbd432126cc25d94d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850873"
---
# <a name="bitsadmin-cache-and-setlimit"></a>biout admin Cache und setLimit

Legt die Cache Größenbeschränkung fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| percent | Der als Prozentsatz des gesamten Festplatten Speichers definierte Cache Limit. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Cache Größe auf 50% beschränkt.

```
C:\>bitsadmin /cache /setlimit 50
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)