---
title: ftp send
description: Referenz Artikel zum Befehl FTP Send, bei dem eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer kopiert wird.
ms.topic: reference
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 300b73bdcaeaa7854980698fad100b5b4f1d58b8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035708"
---
# <a name="ftp-send"></a>ftp send

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl [FTP PUT](ftp-put.md)identisch.

## <a name="syntax"></a>Syntax

```
send <localfile> [<remotefile>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<localfile>` | Gibt die zu Kopier lokale Datei an. |
| `<remotefile>` | Gibt den Namen an, der auf dem Remote Computer verwendet werden soll. Wenn Sie keine *remotefile*-Datei angeben, erhält die Datei den *LocalFile* -Namen. |

### <a name="examples"></a>Beispiele

Wenn Sie die lokale Datei *test.txt* kopieren und *test1.txt* auf dem Remote Computer benennen möchten, geben Sie Folgendes ein:

```
send test.txt test1.txt
```

Wenn Sie die lokale Datei *program.exe* auf den Remote Computer kopieren möchten, geben Sie Folgendes ein:

```
send program.exe
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
