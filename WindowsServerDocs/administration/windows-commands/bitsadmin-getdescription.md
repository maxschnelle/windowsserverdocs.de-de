---
title: bitsadmin getdescription
description: Referenz Artikel für den bizadmin GetDescription-Befehl, der die Beschreibung des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 74e54f963325c0b7222dbd0f9bdccd44d0efc5e1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923062"
---
# <a name="bitsadmin-getdescription"></a>bitsadmin getdescription

Ruft die Beschreibung des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getdescription <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
