---
title: biout admin Cache und DELETE
description: Windows-Befehls Thema für **bistiadmin Cache und DELETE**, wodurch ein bestimmter Cache Eintrag gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0fd7f1db83a62dd9c1085d6afdcf509c1c3ac8cf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850943"
---
# <a name="bitsadmin-cache-and-delete"></a>biout admin Cache und DELETE

Löscht einen bestimmten Cache Eintrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /delete recordID
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Datensatz | Die GUID, die dem Cache Eintrag zugeordnet ist. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Cache Eintrag mit dem Datensatz did {6511b595-E195-40A2-b47702 e8e2f 8F} gelöscht.

```
C:\>bitsadmin /cache /delete {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)