---
title: ftp recv
description: Referenz Artikel für den Befehl FTP empfangener, bei dem eine Remote Datei mit dem aktuellen Datei Übertragungstyp auf den lokalen Computer kopiert wird.
ms.topic: reference
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 65acf6bae09d9b1cad1bf89028b4a51232116c60
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624649"
---
# <a name="ftp-recv"></a>ftp recv

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine Remote Datei mithilfe des aktuellen Datei Übertragungs Typs auf den lokalen Computer.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl [FTP Get](ftp-get.md)identisch.

## <a name="syntax"></a>Syntax

```
recv <remotefile> [<localfile>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<remotefile>` | Gibt die zu Kopier-Remote Datei an. |
| `[<localfile>]` | Gibt den Namen der Datei an, die auf dem lokalen Computer verwendet werden soll. Wenn *LocalFile* nicht angegeben wird, erhält die Datei den Namen der *remotefile*. |

### <a name="examples"></a>Beispiele

Wenn Sie *test.txt* mithilfe der aktuellen Dateiübertragung auf den lokalen Computer kopieren möchten, geben Sie Folgendes ein:

```
recv test.txt
```

*test1.txt* Wenn Sie *test.txt* mithilfe der aktuellen Dateiübertragung auf den lokalen Computer kopieren möchten, geben Sie Folgendes ein:

```
recv test.txt test1.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP get-Befehl](ftp-get.md)

- [FTP-ASCII-Befehl](ftp-ascii.md)

- [FTP-Binär Befehl](ftp-binary.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
