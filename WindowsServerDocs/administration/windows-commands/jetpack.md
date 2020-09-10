---
title: jetpack
description: Referenz Artikel für den Jetpack-Befehl, der eine Windows Internet Name Service (WINS)-oder DHCP-Datenbank (Dynamic Host Configuration Protocol) komprimiert.
ms.topic: reference
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 300218e6eb98e2cf5ab7adeda1b31bc0da0b026b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634405"
---
# <a name="jetpack"></a>jetpack

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Komprimiert eine Windows Internet Name Service (WINS)-oder DHCP-Datenbank (Dynamic Host Configuration-Protokoll). Es wird empfohlen, die WINS-Datenbank zu komprimieren, wenn Sie 30 MB erreicht.

Jetpack.exe komprimiert die Datenbank wie folgt:

1. Kopieren der Datenbankinformationen in eine temporäre Datenbankdatei.

2. Löschen der ursprünglichen Datenbankdatei, entweder WINS oder DHCP.

3. Benennt die temporären Datenbankdateien in den ursprünglichen Dateinamen um.

## <a name="syntax"></a>Syntax

```
jetpack.exe <database_name> <temp_database_name>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ------- | -------- |
| `<database_name>` | Gibt den Namen der ursprünglichen Datenbankdatei an. |
| `<temp_database_name>` | Gibt den Namen der temporären Datenbankdatei an, die von jetpack.exe erstellt werden soll.<p>Hinweis: Diese temporäre Datei wird entfernt, wenn der Compact-Prozess beendet ist. Damit dieser Befehl ordnungsgemäß funktioniert, müssen Sie sicherstellen, dass der temporäre Dateiname eindeutig ist und dass eine Datei mit diesem Namen nicht bereits vorhanden ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Komprimieren der WINS-Datenbank, wobei " **tmp. mdb** " eine temporäre Datenbank ist und " **WINS. mdb** " die WINS-Datenbank ist, geben Sie Folgendes ein:

```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack Wins.mdb Tmp.mdb
NET start WINS
```

Zum Komprimieren der DHCP-Datenbank, wobei **tmp. mdb** eine temporäre Datenbank und **DHCP. mdb** die DHCP-Datenbank ist, geben Sie Folgendes ein:

```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERVER
jetpack Dhcp.mdb Tmp.mdb
NET start DHCPSERVER
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
