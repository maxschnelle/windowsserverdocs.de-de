---
title: bitsadmin setpriority
description: Referenz Artikel für den Befehl "bizadmin SetPriority", mit dem die Priorität des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 07afd9c636a5dbcd4e70de71b3a6f515e7e02bae
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927596"
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
