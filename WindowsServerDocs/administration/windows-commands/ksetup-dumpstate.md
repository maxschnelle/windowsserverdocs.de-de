---
title: ksetup:dumpstate
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e5e8f20188fc27cc08dfd37c5fdbd811925f476
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863121"
---
# <a name="ksetupdumpstate"></a>ksetup:dumpstate



Zeigt den aktuellen Zustand der Bereich der Einstellungen für alle Bereiche, die auf dem Computer definiert sind. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /dumpstate
```

### <a name="parameters"></a>Parameter

Keine

## <a name="remarks"></a>Hinweise

Die Ausgabe dieses Befehls enthält den Standardbereich (die Domäne, der Computer Mitglied ist) und alle Bereiche, die auf diesem Computer definiert sind. Folgendes ist für jeden Bereich enthalten:
-   Alle der Schlüssel Verteilungscenter (KDCs), die diesem Bereich zugeordnet sind.
-   Alle der **Satz Bereich** Flags für diesen Bereich
-   Das KDC-Kennwort

Dieser Befehl zeigt den Domänennamen, die durch die DNS-Ermittlung oder mit dem Befehl angegeben ist keine **Ksetup/Domain**.

Dieser Befehl zeigt nicht das Kennwort des Computerkontos, der festgelegt wird, mithilfe des Befehls **Ksetup /setcomputerpassword**.

**Ksetup** erzeugt dieselbe Ausgabe wie **Ksetup /dumpstate**.

## <a name="BKMK_Examples"></a>Beispiele für

Finden Sie die meisten der Kerberos-Realm-Konfigurationen auf einem Computer aus:
```
ksetup /dumpstate
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)