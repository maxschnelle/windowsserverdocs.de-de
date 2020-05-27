---
title: ftp-mdelete
description: Referenz Thema für den ftp-mdelete-Befehl, mit dem Dateien auf dem Remote Computer gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8ee1882878ce06a16bd6ff6f0dcaa512d6d8b56a
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820230"
---
# <a name="ftp-mdelete"></a>ftp-mdelete

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

Geben Sie Folgendes ein, um Remote Dateien " *exe* " und " *b. exe*" zu löschen:

```
mdelete a.exe b.exe
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
