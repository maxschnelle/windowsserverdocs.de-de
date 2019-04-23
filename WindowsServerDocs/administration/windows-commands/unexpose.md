---
title: Heben Sie die Verfügbarkeit
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe9cb5dfd8ae6c71fdc72ddc1e8421229f98f5d0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837471"
---
# <a name="unexpose"></a>Heben Sie die Verfügbarkeit



Unexposes eine Schattenkopie, die verfügbar gemacht wurde die **verfügbar zu machen** Befehl. Die verfügbar gemachten Schattenkopie kann anhand der Schattenkopie-ID, Laufwerkbuchstaben, Freigabe oder Bereitstellungspunkt angegeben werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<ShadowID>|Die Schattenkopie anhand der angegebenen Schattenkopien-ID angegebene unexposes|
|\<Drive:>|Unexposes die Schattenkopie der angegebene Laufwerkbuchstabe (z. B. Laufwerk P) zugeordnet.|
|\<Share>|Die Schattenkopie der angegebenen Freigabe unexposes (z. B. \\ \\ *"MachineName"*\).|
|\<MountPoint>|Die Schattenkopie der angegebene Bereitstellungspunkt zugeordneten unexposes (z. B. C:\shadowcopy\).|

## <a name="remarks"></a>Hinweise

-   Sie können einen vorhandenen Alias oder eine Umgebungsvariable anstelle von *ShadowID*. Verwendung **hinzufügen** ohne Parameter, um die vorhandenen Aliase finden Sie unter.

## <a name="BKMK_examples"></a>Beispiele für

Um die Schattenkopie zugeordnete Laufwerk P zu schließen, geben Sie Folgendes ein:
```
unexpose P:
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)