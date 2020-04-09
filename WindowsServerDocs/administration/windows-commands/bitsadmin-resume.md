---
title: bitsadmin fortsetzen
description: Windows-Befehls Artikel zum Fortsetzen von **bitadmin**, wodurch ein neuer oder angehaltene Auftrag in der Übertragungs Warteschlange aktiviert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a3f464ba00c5cc233c42a40c063372dc0d584e9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849753"
---
# <a name="bitsadmin-resume"></a>bitsadmin fortsetzen

Aktiviert einen neuen oder angehaltenen Auftrag in der Übertragungs Warteschlange.

## <a name="syntax"></a>Syntax

```
bitsadmin /resume <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Auftrag mit dem Namen *mydownloadjob*fortgesetzt.

```
C:\>bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)