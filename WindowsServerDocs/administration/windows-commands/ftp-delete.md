---
title: ftp delete
description: Referenz Artikel für den Befehl FTP DELETE, mit dem Dateien auf Remote Computern gelöscht werden.
ms.topic: reference
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebf1a770144409dca91ddea0a18a85536e05b926
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038058"
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

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
