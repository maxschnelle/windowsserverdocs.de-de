---
title: Dfsdiag testdfsconfig
description: Referenz Thema für Dfsdiag testdfsconfig, das die Konfiguration eines verteiltes Dateisystem-Namespace (DFS) prüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d9490f35c2d509c83d9008aa87627bd3c55a875
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992994"
---
# <a name="dfsdiag-testdfsconfig"></a>Dfsdiag testdfsconfig

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Konfiguration eines verteiltes Dateisystem-Namespace (DFS), indem die folgenden Aktionen durchgeführt werden:

- Überprüft, ob der DFS-Namespace-Dienst ausgeführt wird und ob der Starttyp auf allen Namespace Servern auf " **automatisch** " festgelegt ist.

- Mit dieser Option wird überprüft, ob die Konfiguration der DFS-Registrierung zwischen den Namespace Servern konsistent ist.

- Überprüft die folgenden Abhängigkeiten auf gruppierten Namespace Servern:

  - Namespace-Stamm Ressourcenabhängigkeit von Netzwerknamen Ressource.

  - Netzwerknamen Ressourcenabhängigkeit von IP-Adress Ressource.

  - Namespace-Stamm Ressourcenabhängigkeit von physischer Datenträger Ressource.

## <a name="syntax"></a>Syntax

```
dfsdiag /testdfsconfig /DFSroot:<namespace>
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /DFSroot:`<namespace>` | Der zu diagnostizieren Namespace (DFS-Stamm). |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Konfiguration von verteiltes Dateisystem-Namespaces (DFS-Namespaces) in "%% amp; quot;" "" *.*

```
dfsdiag /testdfsconfig /DFSroot:\contoso.com\MyNamespace
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Dfsdiag-Befehl](dfsdiag.md)
