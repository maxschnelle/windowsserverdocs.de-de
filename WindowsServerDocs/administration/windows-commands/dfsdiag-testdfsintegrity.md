---
title: Dfsdiag testdfsintegrity
description: Windows-Befehls Thema für **Dfsdiag testdfsintegrity**, das die Integrität des verteiltes Dateisystem (DFS)-Namespace überprüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 714b79369898338a4e4a6e4fad8487709ab4fc60
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846273"
---
# <a name="dfsdiag-testdfsintegrity"></a>Dfsdiag testdfsintegrity

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Integrität des DFS-Namespace (verteiltes Dateisystem) durch Ausführen der folgenden Tests:

- Sucht nach DFS-metadatenbeschädigungen

- Überprüft die Konfiguration der Zugriffs basierten Enumeration, um sicherzustellen, dass Sie zwischen den DFS-Metadaten und der Namespace-Server Freigabe konsistent ist.

- Erkennt überlappende DFS-Ordner (Verknüpfungen), doppelte Ordner und Ordner mit überlappenden Ordner Zielen.

## <a name="syntax"></a>Syntax

```
dfsdiag /TestDFSIntegrity /DFSRoot: <DFS root path> [/Recurse] [/Full]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|-------|--------|
| /DFSRoot: `<DFS root path>`| Der zu diagnostizieren DFS-Namespace. |
| /Recurse | Führt die Tests einschließlich der Namespace-Interlinks aus. |
| /Full | Überprüft die Konsistenz von Freigabe-und NTFS-ACLs und Client seitiger Konfiguration für alle Ordner Ziele. Außerdem wird überprüft, ob die Online-Eigenschaft festgelegt ist. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

```
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

-   [Dfsdiag](dfsdiag.md)


