---
title: FTP-ASCII
description: Referenz Thema für den FTP-ASCII-Befehl, mit dem der Datei Übertragungstyp auf ASCII festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9bf3f278bb478c7244f90533a689f41fd910783
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820040"
---
# <a name="ftp-ascii"></a>FTP-ASCII

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf ASCII fest. Der **FTP** -Befehl unterstützt sowohl ASCII-(Standard) als auch binäre Bilddatei-Übertragungs Typen, aber wir empfehlen die Verwendung von ASCII beim Übertragen von Textdateien. Im ASCII-Modus werden Zeichen Konvertierungen in und aus dem Netzwerkstandard-Zeichensatz ausgeführt. Beispielsweise werden zeitzeiendezeichen nach Bedarf auf Grundlage des Ziel Betriebssystems konvertiert.

## <a name="syntax"></a>Syntax

```
ascii
```

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Datei Übertragungstyp auf ASCII festzulegen:

```
ascii
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-Binär Befehl](ftp-binary.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
