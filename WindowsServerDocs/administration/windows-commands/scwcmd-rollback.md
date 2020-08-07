---
title: Scwcmd-Rollback
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e0fc158584c15c021b14c96829fe0266c3193be
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883126"
---
# <a name="scwcmd-rollback"></a>Scwcmd: Rollback

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Wendet die neueste Rollback-Richtlinie an und löscht dann diese Rollback-Richtlinie.

## <a name="syntax"></a>Syntax

```
scwcmd rollback /m:<ComputerName> [/u:<UserName>] [/pw:<Password>]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/m\<ComputerName>|Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse eines Computers an, auf dem der Rollback-Vorgang ausgeführt werden soll.|
|/u\<UserName>|Gibt ein alternatives Benutzerkonto an, das beim Ausführen eines Remote Rollbacks verwendet werden soll. Der Standardwert ist der angemeldete Benutzer.|
|/PW\<Password>|Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen eines Remote Rollbacks verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

Scwcmd.exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Rollback der Sicherheitsrichtlinie auf einem Computer unter IP-Adresse 172.16.0.0 auszuführen:
```
scwcmd rollback /m:172.16.0.0
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)