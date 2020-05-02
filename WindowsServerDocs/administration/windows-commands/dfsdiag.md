---
title: Dfsdiag
description: Referenz Thema für Dfsdiag, das Diagnoseinformationen für DFS-Namespaces bereitstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d5a9b147994628ccad6a723311decbccbe82ec6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719543"
---
# <a name="dfsdiag"></a>Dfsdiag

Stellt Diagnoseinformationen für DFS-Namespaces bereit.

## <a name="syntax"></a>Syntax

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[Dfsdiag-testdcs](dfsdiag-testdcs.md)|Überprüft die Konfiguration des Domänen Controllers.|
|[Dfsdiag Testsites](dfsdiag-testsites.md)|Überprüft Site Zuordnungen.|
|[Dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md)|Überprüft die DFS-Namespace Konfiguration.|
|[Dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md)|Überprüft die Integrität des DFS-Namespace.|
|[Dfsdiag testreferral](dfsdiag-testreferral.md)|Überprüft Verweis Antworten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)