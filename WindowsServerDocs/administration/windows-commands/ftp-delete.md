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
ms.openlocfilehash: 5e59abdb18104ad23e5e46ffa01b9bfcf015768c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933267"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
