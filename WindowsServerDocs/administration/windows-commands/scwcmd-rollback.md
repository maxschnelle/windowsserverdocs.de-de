---
title: Scwcmd-Rollback
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2db6e0aa85deb2ab999a50d1f2ed9cb311db9da0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636985"
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

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Rollback der Sicherheitsrichtlinie auf einem Computer unter IP-Adresse 172.16.0.0 auszuführen:
```
scwcmd rollback /m:172.16.0.0
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)