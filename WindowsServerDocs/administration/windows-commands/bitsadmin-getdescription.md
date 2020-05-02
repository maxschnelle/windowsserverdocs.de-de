---
title: bitsadmin getdescription
description: Referenz Thema für den bizadmin GetDescription-Befehl, der die Beschreibung des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec5fa9875ca9f669c2a43d58532d3e5e0770d550
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718079"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
