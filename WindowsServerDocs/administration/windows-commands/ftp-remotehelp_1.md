---
title: ftp-remotehelp
description: Referenz Thema für den ftp-remotehelp-Befehl, der Hilfe zu Remote Befehlen anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 659de5487890b50aab9004f650e4584085e7306c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820320"
---
# <a name="ftp-remotehelp"></a>ftp-remotehelp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Hilfe für Remote Befehle an.

## <a name="syntax"></a>Syntax

```
remotehelp [<command>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ------- | -------- |
| `[<command>]` | Gibt den Namen des Befehls an, zu dem Sie Hilfe benötigen. Wenn `<command>` nicht angegeben ist, zeigt dieser Befehl eine Liste aller Remote Befehle an. Sie können Remote Befehle auch über [FTP-Anführungs](ftp-quote.md) Zeichen oder [FTP-Literale](ftp-literal_1.md)ausführen. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Liste der Remote Befehle anzuzeigen:

```
remotehelp
```

Um die Syntax für den Befehl " *feat* Remote" anzuzeigen, geben Sie Folgendes ein:

```
remotehelp feat
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-Anführungszeichen](ftp-quote.md)

- [FTP-Literale](ftp-literal_1.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
