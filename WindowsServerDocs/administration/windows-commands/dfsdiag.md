---
title: Dfsdiag
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61a6ab9a90e4d0220cfe27d2d21120be19b9ff1f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378310"
---
# <a name="dfsdiag"></a>Dfsdiag



Der Befehl "`Dfsdiag`" stellt Diagnoseinformationen für DFS-Namespaces bereit.

## <a name="syntax"></a>Syntax

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Dfsdiag-testdcs](dfsdiag-testdcs.md)|Überprüft die Konfiguration des Domänen Controllers.|
|[Dfsdiag Testsites](dfsdiag-testsites.md)|Überprüft Site Zuordnungen.|
|[Dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md)|Überprüft die DFS-Namespace Konfiguration.|
|[Dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md)|Überprüft die Integrität des DFS-Namespace.|
|[Dfsdiag testreferral](dfsdiag-testreferral.md)|Überprüft Verweis Antworten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)