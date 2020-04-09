---
title: jetpack
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 008e9dd4d41fe270d775b1c44d799dd16429046f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841973"
---
# <a name="jetpack"></a>jetpack

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

komprimiert eine Windows Internet Name Service (WINS)-oder DHCP-Datenbank (Dynamic Host Configuration-Protokoll). Microsoft empfiehlt, dass Sie die WINS-Datenbank immer dann komprimieren, wenn Sie 30 MB erreicht. 

## <a name="syntax"></a>Syntax
```
jetpack.EXE <database name> <temp database name>
```

#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<database name>|Gibt die ursprüngliche Datenbankdatei an.|
|<temp database name>|Gibt die temporäre Datenbankdatei an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
So komprimieren Sie die WINS-Datenbank:
```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack WINS.MDB TMP.MDB
NET start WINS
```
So komprimieren Sie die DHCP-Datenbank:
```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERver
jetpack DHCP.MDB TMP.MDB
NET start DHCPSERver
```
In den obigen Beispielen ist **tmp. mdb** eine temporäre Datenbank, die von Jetpack. exe verwendet wird. **WINS. mdb** ist die WINS-Datenbank. **DHCP. mdb** ist die DHCP-Datenbank.
Jetpack. exe komprimiert die WINS-oder DHCP-Datenbank wie folgt:
1.  Kopiert Datenbankinformationen in eine temporäre Datenbankdatei mit dem Namen " **tmp. mdb**".
2.  Löscht die ursprüngliche Datenbankdatei **WINS. mdb** oder **DHCP. mdb**.
3.  benennt die temporären Datenbankdateien in den ursprünglichen Dateinamen um.

> [!NOTE]
> Während des Compact-Prozesses erstellt Jetpack. exe eine temporäre Datei mit dem Namen, der durch den Parameter " *Temp Database Name* " angegeben wird. Die temporäre Datei wird entfernt, wenn der Compact-Prozess beendet ist. Stellen Sie sicher, dass keine Datei bereits im WINS-oder DHCP-Ordner mit dem Namen vorhanden ist, der im Parameter " *Temp Database Name* " angegeben ist.

## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
