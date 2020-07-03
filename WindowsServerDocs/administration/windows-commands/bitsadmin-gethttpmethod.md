---
title: bitsadmin gethttpmethod
description: Referenz Artikel für den bizadmin gethttpmethod-Befehl, der das HTTP-Verb abruft, das mit dem Auftrag verwendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 3a963eb275c6e635849094906c52fedf90dccd0d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927023"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

Ruft das HTTP-Verb ab, das mit dem Auftrag verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie das HTTP-Verb für die Verwendung mit dem Auftrag *mydownloadjob*ab:

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
