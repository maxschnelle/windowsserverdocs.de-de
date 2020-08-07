---
title: ftp binary
description: Referenz Artikel zum binären FTP-Befehl, mit dem der Datei Übertragungstyp auf Binary festgelegt wird.
ms.topic: article
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 95415a2e41e26f54430671f7c2d84cee087081dd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889615"
---
# <a name="ftp-binary"></a>ftp binary

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf Binary fest. Der **FTP** -Befehl unterstützt sowohl ASCII-(Standard) als auch Binärdatei-Übertragungs Typen, aber wir empfehlen die Verwendung von Binary beim Übertragen von ausführbaren Dateien. Im Binärmodus werden Dateien in 1-Byte-Einheiten übertragen.

## <a name="syntax"></a>Syntax

```
binary
```

### <a name="examples"></a>Beispiele

Um den Datei Übertragungstyp auf Binär festzulegen, geben Sie Folgendes ein:

```
binary
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-ASCII-Befehl](ftp-ascii.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
