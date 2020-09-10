---
title: ftp remotehelp
description: Referenz Artikel für den ftp-remotehelp-Befehl, der Hilfe zu Remote Befehlen anzeigt.
ms.topic: reference
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c91fda83ea988f79237b27f6df6bd6062748e37c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639371"
---
# <a name="ftp-remotehelp"></a>ftp remotehelp

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [ftp quote](ftp-quote.md)

- [ftp literal](ftp-literal_1.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
