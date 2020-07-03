---
title: dfsdiag testdfsconfig
description: Referenz Artikel für Dfsdiag testdfsconfig, der die Konfiguration eines verteiltes Dateisystem-Namespace (DFS) prüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3387b661f454cff089f76f7c9c0d1abe59387010
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930642"
---
# <a name="dfsdiag-testdfsconfig"></a>dfsdiag testdfsconfig

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

| Parameter | Beschreibung |
| --------- | ----------- |
| /DFSroot:`<namespace>` | Der zu diagnostizieren Namespace (DFS-Stamm). |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Konfiguration von verteiltes Dateisystem-Namespaces (DFS-Namespaces) in "%% amp; quot;" "" *.*

```
dfsdiag /testdfsconfig /DFSroot:\contoso.com\MyNamespace
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Dfsdiag-Befehl](dfsdiag.md)
