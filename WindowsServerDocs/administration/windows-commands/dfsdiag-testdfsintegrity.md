---
title: dfsdiag testdfsintegrity
description: Referenz Artikel für den Dfsdiag testdfsintegrity-Befehl, der die Integrität des DFS-Namespace (verteiltes Dateisystem) überprüft.
ms.topic: reference
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4aa6eb44084ec939ebed708982e527b237d407c7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634155"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /DFSroot: `<DFS root path>` | Der zu diagnostizieren DFS-Namespace. |
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
