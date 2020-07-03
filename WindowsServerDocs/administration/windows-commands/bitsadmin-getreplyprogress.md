---
title: bitsadmin getreplyprogress
description: Referenz Artikel für den Befehl "BITSAdmin getreplyprogress", der die Größe und den Fortschritt des Servers "Upload-Reply" abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 728a6ba9c63f31403da59dc392cff581ec0e5c83
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926713"
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

| Parameter | Beschreibung |
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
