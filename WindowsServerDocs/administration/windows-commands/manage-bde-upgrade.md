---
title: Verwalten von-Bde-upgrade
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23bfa824-6ff0-44cc-9b8b-b199a769fb8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc28dfc98a66a60172c812d12a16d03c078b79e1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822281"
---
# <a name="manage-bde-upgrade"></a>Verwalten von-Bde: Aktualisieren



Die BitLocker-Version aktualisiert. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -upgrade [<Drive>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-computername|Gibt an, dass bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|\<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **-upgrade** Befehl zum Aktualisieren der BitLocker-Verschlüsselung auf Laufwerk C.
```
manage-bde –upgrade C:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Verwalten von-bde](manage-bde.md)
-   [Aktualisieren einen durch BitLocker geschützter Computer von Windows Vista auf Windows 7](https://technet.microsoft.com/library/ee424325(v=ws.10).aspx)