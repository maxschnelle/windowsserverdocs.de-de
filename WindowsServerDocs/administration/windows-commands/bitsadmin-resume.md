---
title: bitsadmin resume
description: Referenz Artikel für den Befehl bizadmin Resume, der einen neuen oder angehaltenen Auftrag in der Übertragungs Warteschlange aktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd2a8dcb486c584ef4adaf96a5288a9db32d4553
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927965"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume

Aktiviert einen neuen oder angehaltenen Auftrag in der Übertragungs Warteschlange. Wenn Sie Ihren Auftrag versehentlich fortsetzen oder den Auftrag einfach aussetzen müssen, können Sie den Schalter [bigsadmin Suspend](bitsadmin-suspend.md) zum Aussetzen des Auftrags verwenden.

## <a name="syntax"></a>Syntax

```
bitsadmin /resume <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So setzen Sie den Auftrag mit dem Namen " *mydownloadjob*" fort

```
bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Suspend"](bitsadmin-suspend.md)

- [Bider admin-Befehl](bitsadmin.md)
