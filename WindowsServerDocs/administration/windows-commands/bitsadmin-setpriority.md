---
title: bitsadmin setpriority
description: Referenz Artikel für den Befehl "bizadmin SetPriority", mit dem die Priorität des angegebenen Auftrags festgelegt wird.
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1326d4d5eb8a488dde542c33fa886482e753a790
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892990"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority

Legt die Priorität des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setpriority <job> <priority>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| priority | Legt die Priorität des Auftrags fest, einschließlich:<ul><li>FOREGROUND (Vordergrund)</li><li>HIGH</li><li>NORMAL</li><li>LOW</li></ul> |

## <a name="examples"></a>Beispiele

So legen Sie die Priorität des Auftrags mit dem Namen *mydownloadjob* auf Normal fest:

```
bitsadmin /setpriority myDownloadJob NORMAL
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
