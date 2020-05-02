---
title: 'Ksetup: dumpstate'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27a7e3154b9dfa663b88b04857ea7650995613c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724642"
---
# <a name="ksetupdumpstate"></a>Ksetup: dumpstate



Zeigt den aktuellen Status der Bereichs Einstellungen für alle Bereiche an, die auf dem Computer definiert sind.

## <a name="syntax"></a>Syntax

```
ksetup /dumpstate
```

#### <a name="parameters"></a>Parameter

Keine

## <a name="remarks"></a>Bemerkungen

Die Ausgabe dieses Befehls enthält den Standardbereich (die Domäne, in der der Computer Mitglied ist) und alle Bereiche, die auf diesem Computer definiert sind. Folgendes ist für jeden Bereich enthalten:
-   Alle Schlüssel Verteilungs Center (KDCs), die diesem Bereich zugeordnet sind
-   Alle **Set** -bereichflags für diesen Bereich.
-   Das KDC-Kennwort

Mit diesem Befehl wird der von der DNS-Erkennung angegebene Domänen Name oder der Befehl **Ksetup/Domain**nicht angezeigt.

Mit diesem Befehl wird das Computer Kennwort, das mithilfe des Befehls **Ksetup/setcomputerpassword**festgelegt wurde, nicht angezeigt.

**Ksetup** erzeugt dieselbe Ausgabe wie **Ksetup/dumpstate**.

## <a name="examples"></a>Beispiele

Suchen Sie den größten Teil der Kerberos-Bereichs Konfigurationen auf einem Computer:
```
ksetup /dumpstate
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)