---
title: dfsdiag testdcs
description: Referenz Artikel für den Dfsdiag testdcs-Befehl, der die Konfiguration von Domänen Controllern in der angegebenen Domäne überprüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1eca75d233661d51a36b52b79230ad36b704e203
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930662"
---
# <a name="dfsdiag-testdcs"></a>dfsdiag testdcs

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Konfiguration von Domänen Controllern, indem die folgenden Tests auf den einzelnen Domänen Controllern in der angegebenen Domäne durchgeführt werden:

- Überprüft, ob der verteiltes Dateisystem (DFS)-Namespace-Dienst ausgeführt wird und der Starttyp auf " **automatisch**" festgelegt ist.

- Hiermit wird die Unterstützung von für die Website costeten verweisen für "Netlogon" und "SYSVOL" überprüft.

- Überprüft die Konsistenz der Site Zuordnung nach Hostname und IP-Adresse.

## <a name="syntax"></a>Syntax

```
dfsdiag /testdcs [/domain:<domain_name>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /Domain`<domain_name>` | Der Name der zu Überprüfung enden Domäne. Dieser Parameter ist optional. Der Standardwert ist die lokale Domäne, der der lokale Host hinzugefügt wird. |

## <a name="examples"></a>Beispiele

Zum Überprüfen der Konfiguration von Domänen Controllern in der Domäne *contoso.com* geben Sie Folgendes ein:

```
dfsdiag /testdcs /domain:contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Dfsdiag-Befehl](dfsdiag.md)
