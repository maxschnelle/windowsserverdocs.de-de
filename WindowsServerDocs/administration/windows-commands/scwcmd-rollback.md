---
title: Scwcmd-rollback
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6d6cd79c7068d86915141a37b5a4510bddefc94c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852201"
---
# <a name="scwcmd-rollback"></a>scwcmd: rollback

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Die neueste verfügbare Rollbackrichtlinie gilt, und löscht dann die Rollbackrichtlinie.

## <a name="syntax"></a>Syntax

```
scwcmd rollback /m:<ComputerName> [/u:<UserName>] [/pw:<Password>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/m:\<ComputerName>|Gibt an, den NetBIOS-Namen, die DNS-Namen oder die IP-Adresse eines Computers, in dem der Rollbackvorgang ausgeführt werden soll.|
|/ u:\<Benutzername >|Gibt ein anderes Benutzerkonto beim Ausführen eines Rollbacks remote zu verwendende an. Der Standardwert ist der angemeldete Benutzer.|
|PW:\<Kennwort >|Gibt eine alternative Anmeldeinformationen beim Ausführen eines Rollbacks remote zu verwendende. Der Standardwert ist der angemeldete Benutzer.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern unter Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 verfügbar.

## <a name="BKMK_Examples"></a>Beispiele für

Um die Sicherheitsrichtlinie auf einem Computer mit IP-Adresse 172.16.0.0 zurückzusetzen, geben Sie Folgendes ein:
```
scwcmd rollback /m:172.16.0.0
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)