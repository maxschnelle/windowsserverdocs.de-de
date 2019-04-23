---
title: jetpack
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a3bffc29519df139921bdb1de53e67acd558b306
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858011"
---
# <a name="jetpack"></a>jetpack

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

komprimiert eine Datenbank für Windows Internet Name Service (WINS) "oder" Dynamic Host Configuration-Protokoll (DHCP). Microsoft empfiehlt, dass die WINS-Datenbank komprimieren, wenn es sich um 30 MB nähert. 

## <a name="syntax"></a>Syntax
```
jetpack.EXE <database name> <temp database name>
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<database name>|Gibt die ursprüngliche Datenbankdatei an.|
|<temp database name>|Gibt die temporäre Datenbank an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele für
Die WINS-Datenbank komprimiert:
```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack WINS.MDB TMP.MDB
NET start WINS
```
Die DHCP-Datenbank komprimiert:
```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERver
jetpack DHCP.MDB TMP.MDB
NET start DHCPSERver
```
In den obigen Beispielen **Tmp.mdb** ist eine temporäre Datenbank, die mit jetpack.exe verwendet wird. **WINS.mdb** ist die WINS-Datenbank. **DHCP.mdb** ist die DHCP-Datenbank.
Jetpack.exe komprimiert das WINS oder DHCP-Datenbank wie folgt:
1.  Datenbank kopiert Daten in eine temporäre Datenbank-Datei namens **Tmp.mdb**.
2.  Löscht die ursprüngliche Datenbankdatei **Wins.mdb** oder **Dhcp.mdb**.
3.  Benennt die temporäre Datenbankdateien auf den ursprünglichen Dateinamen an.

> [!NOTE]
> Während der Komprimierung, jetpack.exe erstellt eine temporäre Datei mit dem angegebenen Namen, durch die *Name der temporären Datenbank* Parameter. Die temporäre Datei wird entfernt, wenn der compact-Vorgang abgeschlossen ist. Stellen Sie sicher, Sie verfügen nicht über eine Datei, die bereits in WINS oder DHCP-Ordner mit dem gleichen Namen wie die der *Name der temporären Datenbank* Parameter.

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)
