---
title: dfsdiag
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ab5c86ce7ed4760aef4941de55e8dcf8efe48c8f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819141"
---
# <a name="dfsdiag"></a>dfsdiag



Die `Dfsdiag` Befehl bietet Diagnoseinformationen für DFS-Namespaces.

## <a name="syntax"></a>Syntax

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Dfsdiag TestDCs](dfsdiag-testdcs.md)|Überprüft die Konfiguration des Domänencontrollers.|
|[Dfsdiag TestSites](dfsdiag-testsites.md)|Überprüfungen site Zuordnungen.|
|[Dfsdiag TestDFSConfig](dfsdiag-testdfsconfig.md)|Überprüft die Konfiguration der DFS-Namespace.|
|[Dfsdiag TestDFSIntegrity](dfsdiag-testdfsintegrity.md)|Überprüft die Integrität des DFS-Namespace.|
|[Dfsdiag TestReferral](dfsdiag-testreferral.md)|Überprüft die Weiterleitung von Reaktionen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)