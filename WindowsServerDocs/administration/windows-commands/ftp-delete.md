---
title: ftp delete
description: Referenz Artikel für den Befehl FTP DELETE, mit dem Dateien auf Remote Computern gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fa24e8a052d2eb05d180bce2e843e34532a453f8
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957902"
---
# <a name="ftp-delete"></a>ftp delete

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf Remote Computern.

## <a name="syntax"></a>Syntax

```
delete <remotefile>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<remotefile>` | Gibt die Datei an, die gelöscht werden soll. |

### <a name="examples"></a>Beispiele

Um die *test.txt* Datei auf dem Remote Computer zu löschen, geben Sie Folgendes ein:

```
delete test.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
