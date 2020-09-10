---
title: dfsdiag testdcs
description: Referenz Artikel für den Dfsdiag testdcs-Befehl, der die Konfiguration von Domänen Controllern in der angegebenen Domäne überprüft.
ms.topic: reference
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0c2796cc149d905abae56bb909d337862c5fd7f2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633852"
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

| Parameter | BESCHREIBUNG |
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
