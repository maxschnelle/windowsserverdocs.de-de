---
title: ftp remotehelp
description: Referenz Artikel für den ftp-remotehelp-Befehl, der Hilfe zu Remote Befehlen anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7edfcdadf777dbff062665831fdc2aee3139ec6e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957485"
---
# <a name="ftp-remotehelp"></a>ftp remotehelp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Hilfe für Remote Befehle an.

## <a name="syntax"></a>Syntax

```
remotehelp [<command>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

- [ftp quote](ftp-quote.md)

- [ftp literal](ftp-literal_1.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
