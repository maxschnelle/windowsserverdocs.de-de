---
title: bitsadmin getdescription
description: Referenz Artikel für den bizadmin GetDescription-Befehl, der die Beschreibung des angegebenen Auftrags abruft.
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5023a0a4114796fa3a492de4fddaa0d5ddb0187
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894404"
---
# <a name="bitsadmin-getdescription"></a>bitsadmin getdescription

Ruft die Beschreibung des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getdescription <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Beschreibung für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getdescription myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
