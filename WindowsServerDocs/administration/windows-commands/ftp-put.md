---
title: FTP-PUT
description: Windows-Befehls Thema für FTP-PUT
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: ecd579a313fe1cad1b8a5b4a622aaaec2d6a6d63
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843133"
---
# <a name="ftp-put"></a>FTP: Put

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.
## <a name="syntax"></a>Syntax
```
put <LocalFile> [<remoteFile>]
```
#### <a name="parameters"></a>Parameter

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
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
