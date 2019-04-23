---
title: Bdehdcfg newdriveletter
description: Windows-Befehle Thema Bdehdcfg Newdriveletter - weist einen neuen Laufwerksbuchstaben zu den Teil eines Laufwerks als Systemlaufwerk verwendet.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd40942dfb724d46c0fa9a43c4646e1db09d2a76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887141"
---
# <a name="bdehdcfg-newdriveletter"></a>Bdehdcfg: Newdriveletter



Weist einen neuen Laufwerksbuchstaben, der Teil eines Laufwerks als Systemlaufwerk verwendet. Ein Beispiel, wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -newdriveletter <DriveLetter>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<DriveLetter>|Definiert den Laufwerkbuchstaben, der für das angegebene Ziellaufwerk zugewiesen wird.|

## <a name="remarks"></a>Hinweise

Als bewährte Methode empfiehlt es sich, dass Sie auf das Systemlaufwerk keinen Laufwerkbuchstaben zuweisen.

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel zeigt das Standardlaufwerk gruppenzuweisung für den Laufwerkbuchstaben P.
```
bdehdcfg -target default -newdriveletter P:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)