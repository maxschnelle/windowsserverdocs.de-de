---
title: ftp binary
description: Referenz Artikel zum binären FTP-Befehl, mit dem der Datei Übertragungstyp auf Binary festgelegt wird.
ms.topic: reference
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 725dc41eaa8800372b438e85fbb430edcbf04832
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638546"
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
