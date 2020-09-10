---
title: retain
description: Referenz Artikel für den Befehl "beibehalten", bei dem ein vorhandenes dynamisches Volume für die Verwendung als Start-oder System Volume vorbereitet wird.
ms.topic: reference
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 201aa8b79f8ac0f89d44be7db3f84c9f3059e206
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626905"
---
# <a name="retain"></a>retain

Bereitet ein vorhandenes einfaches dynamisches Volume für die Verwendung als Start-oder System Volume vor. Wenn Sie einen dynamischen Datenträger mit Master Boot Record (MBR) verwenden, erstellt dieser Befehl einen Partitionseintrag im Master Boot Record. Wenn Sie einen dynamischen GPT-Datenträger (GUID-Partitionstabelle) verwenden, erstellt dieser Befehl einen Partitionseintrag in der GUID-Partitionstabelle.

## <a name="syntax"></a>Syntax

```
retain
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
