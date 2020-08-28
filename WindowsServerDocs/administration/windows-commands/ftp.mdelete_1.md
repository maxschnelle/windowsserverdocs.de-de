---
title: ftp mdelete
description: Referenz Artikel für den ftp-mdelete-Befehl, mit dem Dateien auf dem Remote Computer gelöscht werden.
ms.topic: reference
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 647f7aa532f15e5391f68ef2121766e9aa31ff85
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038891"
---
# <a name="ftp-mdelete"></a>ftp mdelete

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf dem Remote Computer.

## <a name="syntax"></a>Syntax
```
mdelete <remotefile>[...]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<remotefile>` | Gibt die zu löschende Remote Datei an. |

### <a name="examples"></a>Beispiele

Zum Löschen von Remote Dateien *a.exe* und *b.exe*geben Sie Folgendes ein:

```
mdelete a.exe b.exe
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
