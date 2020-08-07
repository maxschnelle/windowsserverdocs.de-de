---
title: bitsadmin setdescription
description: Referenz Artikel für den Befehl "bizadmin setDescription", mit dem die Beschreibung des angegebenen Auftrags festgelegt wird.
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d499b152f5cb3a846cc1de6ec65f07903421cf49
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893174"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

Legt die Beschreibung für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| description | Der Text, der zur Beschreibung des Auftrags verwendet wird. |

## <a name="examples"></a>Beispiele

So rufen Sie die Beschreibung für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
