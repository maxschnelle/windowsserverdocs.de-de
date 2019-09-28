---
title: jetpack
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b011658c6a745d62707cf88404379b17b0e05eef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375320"
---
# <a name="jetpack"></a>jetpack

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

komprimiert eine Windows Internet Name Service (WINS)-oder DHCP-Datenbank (Dynamic Host Configuration-Protokoll). Microsoft empfiehlt, dass Sie die WINS-Datenbank immer dann komprimieren, wenn Sie 30 MB erreicht. 

## <a name="syntax"></a>Syntax
```
jetpack.EXE <database name> <temp database name>
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<database name>|Gibt die ursprüngliche Datenbankdatei an.|
|<temp database name>|Gibt die temporäre Datenbankdatei an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele
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
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
