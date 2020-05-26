---
title: FTP-Get
description: Referenz Thema für den Befehl FTP Get, bei dem eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer kopiert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7254cac15afc446695f22ee1a63f2f4573d3565
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819710"
---
# <a name="ftp-get"></a>FTP-Get

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl [FTP empfangener](ftp-recv.md)identisch.

## <a name="syntax"></a>Syntax

```
get <remotefile> [<localfile>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<remotefile>` | Gibt die zu Kopier-Remote Datei an. |
| `[<localfile>]` | Gibt den Namen der Datei an, die auf dem lokalen Computer verwendet werden soll. Wenn *LocalFile* nicht angegeben wird, erhält die Datei den Namen der *remotefile*. |

### <a name="examples"></a>Beispiele

Wenn Sie " *Test. txt* " mithilfe der aktuellen Dateiübertragung auf den lokalen Computer kopieren möchten, geben Sie Folgendes ein:

```
get test.txt
```

Zum Kopieren von " *Test. txt* " auf den lokalen Computer als " *test1. txt* " mithilfe der aktuellen Dateiübertragung geben Sie Folgendes ein:

```
get test.txt test1.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl FTP empfangener](ftp-recv.md)

- [FTP-ASCII-Befehl](ftp-ascii.md)

- [FTP-Binär Befehl](ftp-binary.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
