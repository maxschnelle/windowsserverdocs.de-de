---
title: Scwcmd-Rollback
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9679f8a8ef2e62f451d7ee01c3c5718825b5cbeb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835143"
---
# <a name="scwcmd-rollback"></a>scwcmd: rollback

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Wendet die neueste Rollback-Richtlinie an und löscht dann diese Rollback-Richtlinie.

## <a name="syntax"></a>Syntax

```
scwcmd rollback /m:<ComputerName> [/u:<UserName>] [/pw:<Password>]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/m:\<Computername >|Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse eines Computers an, auf dem der Rollback-Vorgang ausgeführt werden soll.|
|/u:\<Benutzername >|Gibt ein alternatives Benutzerkonto an, das beim Ausführen eines Remote Rollbacks verwendet werden soll. Der Standardwert ist der angemeldete Benutzer.|
|/PW:\<Kennwort >|Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen eines Remote Rollbacks verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd. exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Geben Sie Folgendes ein, um ein Rollback der Sicherheitsrichtlinie auf einem Computer unter IP-Adresse 172.16.0.0 auszuführen:
```
scwcmd rollback /m:172.16.0.0
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)