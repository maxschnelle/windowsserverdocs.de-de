---
title: ftp mdelete
description: Referenz Artikel für den ftp-mdelete-Befehl, mit dem Dateien auf dem Remote Computer gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 720ae8b5ebb0ef380f6547a85913cd84c6d98c7e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931168"
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

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
