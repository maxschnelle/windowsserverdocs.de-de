---
title: bitsadmin setdisplayname
description: Referenz Artikel für den Befehl "bitadmin setdisplayname", mit dem der Anzeige Name des angegebenen Auftrags festgelegt wird.
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac83fee33703555f1a8ba4b65ae8dc4d0f947916
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893161"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

Legt den anzeigen Amen für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
