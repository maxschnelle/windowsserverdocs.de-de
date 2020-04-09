---
title: 'Ksetup: dumpstate'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46f827d26d867392db4cbef92cf5be496aee8d74
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841513"
---
# <a name="ksetupdumpstate"></a>Ksetup: dumpstate



Zeigt den aktuellen Status der Bereichs Einstellungen für alle Bereiche an, die auf dem Computer definiert sind. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /dumpstate
```

#### <a name="parameters"></a>Parameter

Keine

## <a name="remarks"></a>Hinweise

Die Ausgabe dieses Befehls enthält den Standardbereich (die Domäne, in der der Computer Mitglied ist) und alle Bereiche, die auf diesem Computer definiert sind. Folgendes ist für jeden Bereich enthalten:
-   Alle Schlüssel Verteilungs Center (KDCs), die diesem Bereich zugeordnet sind
-   Alle **Set** -bereichflags für diesen Bereich.
-   Das KDC-Kennwort

Mit diesem Befehl wird der von der DNS-Erkennung angegebene Domänen Name oder der Befehl **Ksetup/Domain**nicht angezeigt.

Mit diesem Befehl wird das Computer Kennwort, das mithilfe des Befehls **Ksetup/setcomputerpassword**festgelegt wurde, nicht angezeigt.

**Ksetup** erzeugt dieselbe Ausgabe wie **Ksetup/dumpstate**.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Suchen Sie den größten Teil der Kerberos-Bereichs Konfigurationen auf einem Computer:
```
ksetup /dumpstate
```

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)