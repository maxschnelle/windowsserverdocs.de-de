---
title: Ksetup dumpstate
description: Referenz Thema für die Ksetup-dumpstate-Kommas, die den aktuellen Status der Bereichs Einstellungen für alle auf dem Computer definierten Bereiche anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4ccb75ac143239d97b823fb7030f9a8020b4b4f6
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817740"
---
# <a name="ksetup-dumpstate"></a>Ksetup dumpstate

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)