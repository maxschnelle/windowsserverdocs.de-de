---
title: reset
description: Referenz Artikel für den Reset-Befehl, der DiskShadow.exe auf den Standardzustand zurücksetzt.
ms.topic: reference
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ca1b0574fae1e0d00bc1f2cbec17ff9572ed253
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038338"
---
# <a name="reset"></a>reset

Setzt DiskShadow.exe auf den Standardzustand zurück. Dieser Befehl ist besonders nützlich bei der Trennung von zusammengesetzten DiskShadow-Vorgängen, wie z. b. **Erstellen**, **importieren**, **sichern**oder **Wiederherstellen**.

> [! Wichtig: Nachdem Sie diesen Befehl ausgeführt haben, verlieren Sie Statusinformationen von Befehlen, z. b. **Hinzufügen**, **festlegen**, **Laden**oder **Writer**. Dieser Befehl gibt auch ivssbackupcomponent-Schnittstellen frei und verliert nicht persistente Schatten Kopien.

## <a name="syntax"></a>Syntax

```
reset
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)

- [Import Befehl](import_1.md)

- [Backup-Befehl](begin-backup.md)

- [Restore-Befehl](begin-restore.md)

- [Befehl hinzufügen](add.md)

- [SET-Befehl](set_2.md)

- [Befehl "Laden"](reg-load.md)

- [Writer-Befehl](writer.md)
