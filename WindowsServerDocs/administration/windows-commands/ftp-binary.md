---
title: ftp binary
description: Referenz Artikel zum binären FTP-Befehl, mit dem der Datei Übertragungstyp auf Binary festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: daf300598f8a31fc35d5702b5bd42507dd9e8211
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925952"
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

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
