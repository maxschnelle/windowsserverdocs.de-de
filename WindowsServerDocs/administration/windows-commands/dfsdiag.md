---
title: dfsdiag
description: Referenz Artikel für den Dfsdiag-Befehl, der Diagnoseinformationen für DFS-Namespaces bereitstellt.
ms.topic: reference
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 05ca89a2ad2984ec7e47002489f26968e7d2d69b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635032"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [dfsdiag testdcs](dfsdiag-testdcs.md) | Überprüft die Konfiguration des Domänen Controllers. |
| [dfsdiag testsites](dfsdiag-testsites.md) | Überprüft Site Zuordnungen. |
| [dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md) | Überprüft die DFS-Namespace Konfiguration. |
| [dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md) | Überprüft die Integrität des DFS-Namespace. |
| [dfsdiag testreferral](dfsdiag-testreferral.md) | Überprüft Verweis Antworten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
