---
title: bitsadmin getreplyprogress
description: Referenz Artikel für den Befehl "BITSAdmin getreplyprogress", der die Größe und den Fortschritt des Servers "Upload-Reply" abruft.
ms.topic: article
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29a5f5f0023f6241ee70271de865ed14e379aa4c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893871"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

Ruft die Größe und den Fortschritt des Server Uploads-Antwort-Vorgangs ab.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplyprogress <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie den Upload-Antwort-Status für den Auftrag *mydownloadjob*ab:

```
bitsadmin /getreplyprogress myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
