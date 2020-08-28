---
title: bitsadmin setdisplayname
description: Referenz Artikel für den Befehl "bitadmin setdisplayname", mit dem der Anzeige Name des angegebenen Auftrags festgelegt wird.
ms.topic: reference
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4726d4d1dec867e72ab542222a71289994ed12fd
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028538"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

Legt den anzeigen Amen für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| display_name | Text, der als angezeigter Name für den jeweiligen Auftrag verwendet wird. |

## <a name="examples"></a>Beispiele

So legen Sie den anzeigen Amen für den Auftrag auf *mydownloadjob*fest

```
bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
