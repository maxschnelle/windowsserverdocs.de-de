---
title: bitsadmin getfilestransferred
description: Windows-Befehls Thema für **bizadmin getfilestransferred**, das die Anzahl der für den angegebenen Auftrag übertragenen Dateien abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 053b67f5f85066d202b446b31eb1b1698fd735b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850673"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred

Ruft die Anzahl der Dateien ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getfilestransferred <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Anzahl der Dateien abgerufen, die im Auftrag mit dem Namen *mydownloadjob*übertragen wurden.

```
C:\>bitsadmin /getfilestransferred myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)