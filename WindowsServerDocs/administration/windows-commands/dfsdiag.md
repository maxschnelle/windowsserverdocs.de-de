---
title: dfsdiag
description: Referenz Artikel für den Dfsdiag-Befehl, der Diagnoseinformationen für DFS-Namespaces bereitstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97f39d740bc321ebcece69ff0690dfac7aab6567
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928662"
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
