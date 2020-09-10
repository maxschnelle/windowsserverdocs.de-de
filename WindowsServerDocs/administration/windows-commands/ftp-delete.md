---
title: ftp delete
description: Referenz Artikel für den Befehl FTP DELETE, mit dem Dateien auf Remote Computern gelöscht werden.
ms.topic: reference
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7a09e9abbe23582a2b5f2ba197a1877ffc62c7cc
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624794"
---
# <a name="ftp-delete"></a>ftp delete

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf Remote Computern.

## <a name="syntax"></a>Syntax

```
delete <remotefile>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<remotefile>` | Gibt die Datei an, die gelöscht werden soll. |

### <a name="examples"></a>Beispiele

Um die *test.txt* Datei auf dem Remote Computer zu löschen, geben Sie Folgendes ein:

```
delete test.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
