---
title: ksetup dumpstate
description: Referenz Artikel für den Ksetup-dumpstate-Befehl, der den aktuellen Status der Bereichs Einstellungen für alle auf dem Computer definierten Bereiche anzeigt.
ms.topic: reference
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5f9d16a094dd3d3bbcdd5e9cb740e1bca5203a6d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639666"
---
# <a name="ksetup-dumpstate"></a>ksetup dumpstate

Zeigt den aktuellen Status der Bereichs Einstellungen für alle Bereiche an, die auf dem Computer definiert sind. Dieser Befehl zeigt dieselbe Ausgabe an wie der **Ksetup** -Befehl.

## <a name="syntax"></a>Syntax

```
ksetup /dumpstate
```

### <a name="remarks"></a>Hinweise

- Die Ausgabe dieses Befehls enthält den Standardbereich (die Domäne, in der der Computer Mitglied ist) und alle Bereiche, die auf diesem Computer definiert sind. Folgendes ist für jeden Bereich enthalten:

  - Alle Schlüssel Verteilungs Center (KDCs), die diesem Bereich zugeordnet sind.

  - Alle **Set** -bereichflags für diesen Bereich.

  - Das KDC-Kennwort.

- Mit diesem Befehl wird der von der DNS-Erkennung oder dem-Befehl angegebene Domänen Name nicht angezeigt `ksetup /domain` .

- Mit diesem Befehl wird das festgelegte Computer Kennwort nicht mit dem Befehl angezeigt `ksetup /setcomputerpassword` .

## <a name="examples"></a>Beispiele

Um die Kerberos-Bereichs Konfigurationen auf einem Computer zu suchen, geben Sie Folgendes ein:

```
ksetup /dumpstate
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)