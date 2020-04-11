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
ms.openlocfilehash: e81bd80232cd4ec8fbba70c86cd97bb9695680f8
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123071"
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

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird der Auftrag mit dem Namen *mydownloadjob*fortgesetzt.

```
C:\>bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)