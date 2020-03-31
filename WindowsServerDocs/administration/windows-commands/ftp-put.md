---
title: FTP-PUT
description: Windows-Befehls Thema für FTP-PUT
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: 019a81364dbedb443a3a23d5c5a6f8db1496d83d
ms.sourcegitcommit: 479ad84a0d6c7c7b8308122b8bac8308cb36fe9b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2020
ms.locfileid: "80391718"
---
# <a name="ftp-put"></a>FTP: Put

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.
## <a name="syntax"></a>Syntax
```
put <LocalFile> [<remoteFile>]
```
### <a name="parameters"></a>Parameter

|    Parameter     |                    Beschreibung                    |
|------------------|---------------------------------------------------|
|   `<LocalFile>`  |         Gibt die zu Kopier lokale Datei an.         |
| `[<remoteFile>]` | Gibt den Namen an, der auf dem Remote Computer verwendet werden soll. |

## <a name="remarks"></a>Hinweise
- Der **Put** -Befehl ist mit dem **Send** -Befehl identisch.
- Wenn *remotefile* nicht angegeben wird, erhält die Datei den Namen *LocalFile* .
  ## <a name="examples"></a><a name="BKMK_Examples"></a>Beispiele
  Kopieren Sie die lokale Datei " **Test. txt** ", und nennen Sie Sie " **test1. txt** " auf dem Remote Computer.
  ```
  put test.txt test1.txt
  ```
  Kopieren Sie die lokale Datei **Programm. exe** auf den Remote Computer.
  ```
  put program.exe
  ```
  ## <a name="additional-references"></a>Weitere Verweise
- [FTP: ASCII](ftp-ascii.md)
- [FTP: binär](ftp-binary.md)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
