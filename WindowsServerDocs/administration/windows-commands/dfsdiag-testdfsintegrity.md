---
title: dfsdiag testdfsintegrity
description: Referenz Artikel für den Dfsdiag testdfsintegrity-Befehl, der die Integrität des DFS-Namespace (verteiltes Dateisystem) überprüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7896174bb58c957e4c24b1c3f7e1b2bacc9f95f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930635"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag testdfsintegrity

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Integrität des DFS-Namespace (verteiltes Dateisystem) durch Ausführen der folgenden Tests:

- Sucht nach DFS-metadatenbeschädigungen

- Überprüft die Konfiguration der Zugriffs basierten Enumeration, um sicherzustellen, dass Sie zwischen den DFS-Metadaten und der Namespace-Server Freigabe konsistent ist.

- Erkennt überlappende DFS-Ordner (Verknüpfungen), doppelte Ordner und Ordner mit überlappenden Ordner Zielen.

## <a name="syntax"></a>Syntax

```
dfsdiag /testdfsintegrity /DFSroot: <DFS root path> [/recurse] [/full]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /DFSroot:`<DFS root path>` | Der zu diagnostizieren DFS-Namespace. |
| /recurse | Führt die Tests aus, einschließlich aller Namespace-Interlinks. |
| /full | Überprüft die Konsistenz der Freigabe und NTFS-ACLs sowie die Client seitige Konfiguration für alle Ordner Ziele. Außerdem wird überprüft, ob die Online-Eigenschaft festgelegt ist. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Integrität und Konsistenz verteiltes Dateisystem der DFS-Namespaces (DFS-Namespaces *) in "* Configuration Manager" (einschließlich aller Links) zu überprüfen:

```
dfsdiag /testdfsintegrity /DFSRoot:\contoso.com\MyNamespace /recurse /full
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Dfsdiag-Befehl](dfsdiag.md)
