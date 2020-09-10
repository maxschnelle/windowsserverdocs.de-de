---
title: ftp mdelete
description: Referenz Artikel für den ftp-mdelete-Befehl, mit dem Dateien auf dem Remote Computer gelöscht werden.
ms.topic: reference
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4b9ca1843fd405aef2a1c28c8b7f94bbc650f2d4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627626"
---
# <a name="ftp-mdelete"></a>ftp mdelete

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Dateien auf dem Remote Computer.

## <a name="syntax"></a>Syntax
```
mdelete <remotefile>[...]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
