---
title: Kontext festlegen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6f24e795f2d7c92d462cf822e70e4830b53827e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845851"
---
# <a name="set-contex"></a>Set-Kontextmenü



Legt den Kontext für die Erstellung von Schattenkopien fest. Wenn Sie ohne Angabe von Parametern **Kontext festlegen** zeigt die Hilfe an der Eingabeaufforderung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|ClientAccessible|Gibt an, dass die Schattenkopie von Clientversionen von Windows verwendet werden kann.|
|persistente|Gibt an, dass die Schattenkopie bei Beenden des Programms, zurücksetzen oder bei Neustart erhalten bleibt.|
|volatile|Löscht die Schattenkopie zu kopieren, auf Beenden oder zurücksetzen.|
|NoWriters|Gibt an, dass alle Writer ausgeschlossen werden.|

## <a name="remarks"></a>Hinweise

-   Die *Clientaccessible* Kontext ist persistent in der Standardeinstellung.

## <a name="BKMK_examples"></a>Beispiele für

Um zu verhindern, dass Schattenkopien gelöscht wird, wenn Sie DiskShadow beenden, geben Sie Folgendes ein:
```
set context persistent
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)