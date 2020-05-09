---
title: Dfsdiag
description: Referenz Thema für den Dfsdiag-Befehl, der Diagnoseinformationen für DFS-Namespaces bereitstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e9e0de18b48a4233b950ad6aa8f1e450a99da62
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992828"
---
# <a name="dfsdiag"></a>Dfsdiag

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
| [Dfsdiag-testdcs](dfsdiag-testdcs.md) | Überprüft die Konfiguration des Domänen Controllers. |
| [Dfsdiag Testsites](dfsdiag-testsites.md) | Überprüft Site Zuordnungen. |
| [Dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md) | Überprüft die DFS-Namespace Konfiguration. |
| [Dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md) | Überprüft die Integrität des DFS-Namespace. |
| [Dfsdiag testreferral](dfsdiag-testreferral.md) | Überprüft Verweis Antworten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
