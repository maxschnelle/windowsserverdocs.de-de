---
title: ftp open
description: Referenz Artikel für den Befehl FTP Open, der eine Verbindung mit dem angegebenen FTP-Server herstellt.
ms.topic: reference
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 24fabf61e57a0dda00837a15702dfe9ef5ee6862
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635280"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
