---
title: Dfsdiag testdfsintegrity
description: Referenz Thema für **Dfsdiag testdfsintegrity**, das die Integrität des DFS-Namespace (verteiltes Dateisystem) überprüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21aa6ef3d7d4a7b4a9c64fc51aec77f49f1e0a0c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719578"
---
# <a name="dfsdiag-testdfsintegrity"></a>Dfsdiag testdfsintegrity

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Integrität des DFS-Namespace (verteiltes Dateisystem) durch Ausführen der folgenden Tests:

- Sucht nach DFS-metadatenbeschädigungen

- Überprüft die Konfiguration der Zugriffs basierten Enumeration, um sicherzustellen, dass Sie zwischen den DFS-Metadaten und der Namespace-Server Freigabe konsistent ist.

- Erkennt überlappende DFS-Ordner (Verknüpfungen), doppelte Ordner und Ordner mit überlappenden Ordner Zielen.

## <a name="syntax"></a>Syntax

```
dfsdiag /TestDFSIntegrity /DFSRoot: <DFS root path> [/Recurse] [/Full]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|-------|--------|
| /DFSRoot:`<DFS root path>`| Der zu diagnostizieren DFS-Namespace. |
| /Recurse | Führt die Tests einschließlich der Namespace-Interlinks aus. |
| /Full | Überprüft die Konsistenz von Freigabe-und NTFS-ACLs und Client seitiger Konfiguration für alle Ordner Ziele. Außerdem wird überprüft, ob die Online-Eigenschaft festgelegt ist. |

## <a name="examples"></a>Beispiele

```
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

-   [Dfsdiag](dfsdiag.md)


