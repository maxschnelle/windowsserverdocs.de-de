---
title: bitsadmin setpriority
description: Referenz Artikel für den Befehl "bizadmin SetPriority", mit dem die Priorität des angegebenen Auftrags festgelegt wird.
ms.topic: reference
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1fe6a2b3981697a4a8c287fe4fb49c31a4f4244
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028468"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority

Legt die Priorität des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setpriority <job> <priority>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
