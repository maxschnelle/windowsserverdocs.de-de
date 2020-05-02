---
title: bitsadmin setpriority
description: Referenz Thema für den Befehl "bizadmin SetPriority", mit dem die Priorität des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 556a1d94700780ea22acc1e4c2f32961c0e43342
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717252"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
