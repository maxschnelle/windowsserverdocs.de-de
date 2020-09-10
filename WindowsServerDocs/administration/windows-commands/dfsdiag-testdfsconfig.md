---
title: dfsdiag testdfsconfig
description: Referenz Artikel für Dfsdiag testdfsconfig, der die Konfiguration eines verteiltes Dateisystem-Namespace (DFS) prüft.
ms.topic: reference
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a95e5df19bfab4a8724d755b4495dc90bcf5f93a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634144"
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

| Parameter | BESCHREIBUNG |
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
