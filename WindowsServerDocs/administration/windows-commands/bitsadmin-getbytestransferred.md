---
title: bitsadmin getbytestransferred
description: Windows-Befehls Thema für **bizadmin getbytestransferred**, mit dem die Anzahl der für den angegebenen Auftrag übertragenen Bytes abgerufen wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 957b3e60bf8a5e41b3964f4d762633472606654d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850773"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

Ruft die Anzahl der Bytes ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Anzahl der Bytes abgerufen, die für den Auftrag mit dem Namen *mydownloadjob*übertragen werden.

```
C:\>bitsadmin /getbytestransferred myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)