---
title: bdehdcfg-Neustart
description: Windows-Befehls Thema für **bdehdcfg Restart**, das bdehdcfg anweist, dass der Computer nach Abschluss der Laufwerks Vorbereitung neu gestartet werden soll.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ae6f8d31c09feddf8f994c28d34e4e1b08cc322
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851033"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: neu starten

Informiert das Befehlszeilen Tool bdehdcfg darüber, dass der Computer nach Abschluss der Laufwerks Vorbereitung neu gestartet werden soll. Ein Beispiel für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```

#### <a name="parameters"></a>Parameter

Dieser Befehl erfordert keine zusätzlichen Parameter.

## <a name="remarks"></a>Hinweise

Wenn andere Benutzer auf dem Computer angemeldet sind und der Befehl **quiet** nicht angegeben ist, wird eine Eingabeaufforderung angezeigt, um zu bestätigen, dass der Computer neu gestartet werden muss.

## <a name="examples"></a><a name="BKMK_Examples"></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls **Restart** .

```
bdehdcfg -target default -restart
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)