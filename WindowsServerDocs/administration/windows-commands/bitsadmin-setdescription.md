---
title: bitsadmin setdescription
description: Referenz Artikel für den Befehl "bizadmin setDescription", mit dem die Beschreibung des angegebenen Auftrags festgelegt wird.
ms.topic: reference
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86f63a553b9d308ef3e8bfe5bfc2a2334b5d28e8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031258"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

Legt die Beschreibung für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
