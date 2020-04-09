---
title: bdehdcfg newdriveletter
description: Windows-Befehls Thema für **bdehdcfg newdriveletter**, der einen neuen Laufwerk Buchstaben zum Teil eines Laufwerks zuweist, das als Systemlaufwerk verwendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a8757e7d0684912525817708fbe34953b049582
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851053"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter

Weist dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zu. Ein Beispiel für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -newdriveletter <DriveLetter>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------| ----------- |
|`<DriveLetter>`|Definiert den Laufwerk Buchstaben, der dem angegebenen Ziellaufwerk zugewiesen wird.|

## <a name="remarks"></a>Hinweise

Als bewährte Vorgehensweise wird empfohlen, dem Systemlaufwerk keinen Laufwerk Buchstaben zuzuweisen.

## <a name="examples"></a><a name="BKMK_Examples"></a>Beispiele

Im folgenden Beispiel wird gezeigt, wie dem Standard Laufwerk der Laufwerk Buchstabe P zugewiesen wird.

```
bdehdcfg -target default -newdriveletter P:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)