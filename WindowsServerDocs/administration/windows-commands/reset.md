---
title: reset
description: Referenz Artikel für den Reset-Befehl, der DiskShadow.exe auf den Standardzustand zurücksetzt.
ms.topic: reference
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 84f4aedee746e642e59a09055c3994160f503afa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626883"
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
