---
title: ftp put
description: Referenz Artikel für den Befehl FTP PUT, bei dem eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer kopiert wird.
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: e0794c12d7e613f92546903586fe14d23319185a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889120"
---
# <a name="ftp-put"></a>ftp put

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert eine lokale Datei mit dem aktuellen Datei Übertragungstyp auf den Remote Computer.

> [!NOTE]
> Dieser Befehl ist mit dem Befehl [FTP Send](ftp-send_1.md)identisch.

## <a name="syntax"></a>Syntax

```
put <localfile> [<remotefile>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<localfile>` | Gibt die zu Kopier lokale Datei an. |
| `[<remotefile>]` | Gibt den Namen an, der auf dem Remote Computer verwendet werden soll. Wenn Sie keine *remotefile*-Datei angeben, gibt die Datei den Namen der *LocalFile* an.|

### <a name="examples"></a>Beispiele

Wenn Sie die lokale Datei *test.txt* kopieren und *test1.txt* auf dem Remote Computer benennen möchten, geben Sie Folgendes ein:

```
put test.txt test1.txt
```

Wenn Sie die lokale Datei *program.exe* auf den Remote Computer kopieren möchten, geben Sie Folgendes ein:

```
put program.exe
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-ASCII-Befehl](ftp-ascii.md)

- [FTP-Binär Befehl](ftp-binary.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
