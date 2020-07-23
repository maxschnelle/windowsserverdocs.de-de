---
title: ftp open
description: Referenz Artikel für den Befehl FTP Open, der eine Verbindung mit dem angegebenen FTP-Server herstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 265668809040d7644d698c8b9bc0da5371fb5499
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957632"
---
# <a name="ftp-open"></a>ftp open

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit dem angegebenen FTP-Server her.

## <a name="syntax"></a>Syntax

```
open <computer> [<port>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<computer>` | Gibt den Remote Computer an, mit dem Sie eine Verbindung herstellen möchten. Sie können eine IP-Adresse oder einen Computernamen verwenden (in diesem Fall muss ein DNS-Server oder eine Datei mit Hosts verfügbar sein). |
| `[<port>]` | Gibt eine TCP-Portnummer an, die für die Verbindung mit einem FTP-Server verwendet wird. Standardmäßig wird TCP-Port 21 verwendet. |

### <a name="examples"></a>Beispiele

Zum Herstellen einer Verbindung mit dem FTP-Server unter *FTP.Microsoft.com*geben Sie Folgendes ein:

```
open ftp.microsoft.com
```

Zum Herstellen einer Verbindung mit dem FTP-Server unter *FTP.Microsoft.com* , der TCP-Port *755*überwacht, geben Sie Folgendes ein:

```
open ftp.microsoft.com 755
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
