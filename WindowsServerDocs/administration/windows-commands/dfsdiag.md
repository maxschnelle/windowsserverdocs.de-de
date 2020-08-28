---
title: dfsdiag
description: Referenz Artikel für den Dfsdiag-Befehl, der Diagnoseinformationen für DFS-Namespaces bereitstellt.
ms.topic: reference
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da34cc9b4c2cfcb30d2f8ff3161d6777ae9d0275
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034148"
---
# <a name="dfsdiag"></a>dfsdiag

Stellt Diagnoseinformationen für DFS-Namespaces bereit.

## <a name="syntax"></a>Syntax

```
dfsdiag /testdcs [/domain:<domain name>]
dfsdiag /testsites </machine:<server name>| /DFSPath:<namespace root or DFS folder> [/recurse]> [/full]
dfsdiag /testdfsconfig /DFSRoot:<namespace>
dfsdiag /testdfsintegrity /DFSRoot:<DFS root path> [/recurse] [/full]
dfsdiag /testreferral /DFSpath:<DFS path to get referrals> [/full]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| [dfsdiag testdcs](dfsdiag-testdcs.md) | Überprüft die Konfiguration des Domänen Controllers. |
| [dfsdiag testsites](dfsdiag-testsites.md) | Überprüft Site Zuordnungen. |
| [dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md) | Überprüft die DFS-Namespace Konfiguration. |
| [dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md) | Überprüft die Integrität des DFS-Namespace. |
| [dfsdiag testreferral](dfsdiag-testreferral.md) | Überprüft Verweis Antworten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
