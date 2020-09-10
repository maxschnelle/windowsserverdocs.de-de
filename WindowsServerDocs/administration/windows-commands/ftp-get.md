---
title: ftp get
description: Referenz Artikel für den Befehl FTP Get, bei dem eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer kopiert wird.
ms.topic: reference
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 749c32160c58e2d59563b2355fa0b4c6e6a4c82a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621775"
---
# <a name="ftp-get"></a>ftp get

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

Wenn Sie *test.txt* mithilfe der aktuellen Dateiübertragung auf den lokalen Computer kopieren möchten, geben Sie Folgendes ein:

```
get test.txt
```

*test1.txt* Wenn Sie *test.txt* mithilfe der aktuellen Dateiübertragung auf den lokalen Computer kopieren möchten, geben Sie Folgendes ein:

```
get test.txt test1.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl FTP empfangener](ftp-recv.md)

- [FTP-ASCII-Befehl](ftp-ascii.md)

- [FTP-Binär Befehl](ftp-binary.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
