---
title: Scwcmd-Rollback
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3f089ea3e6e5d5b95080356dd239272b95a76b37
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371215"
---
# <a name="scwcmd-rollback"></a>scwcmd: rollback

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Wendet die neueste Rollback-Richtlinie an und löscht dann diese Rollback-Richtlinie.

## <a name="syntax"></a>Syntax

```
scwcmd rollback /m:<ComputerName> [/u:<UserName>] [/pw:<Password>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/m: \<computername >|Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse eines Computers an, auf dem der Rollback-Vorgang ausgeführt werden soll.|
|/u: \<username >|Gibt ein alternatives Benutzerkonto an, das beim Ausführen eines Remote Rollbacks verwendet werden soll. Der Standardwert ist der angemeldete Benutzer.|
|/PW: \<password >|Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen eines Remote Rollbacks verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd. exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="BKMK_Examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Rollback der Sicherheitsrichtlinie auf einem Computer unter IP-Adresse 172.16.0.0 auszuführen:
```
scwcmd rollback /m:172.16.0.0
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)