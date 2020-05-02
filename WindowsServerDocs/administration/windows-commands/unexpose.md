---
title: Heben des
description: Referenz Thema zur nicht verfügbar machung, das eine Schatten Kopie zurückgibt, die mit dem verfügbar gemachten Befehl verfügbar gemacht wurde.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0caa412e5ff7de149f0a2bd8806f7141c368306
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721188"
---
# <a name="unexpose"></a>Heben des

Macht eine Schatten Kopie verfügbar **, die mit dem verfügbar** gemachten Befehl verfügbar gemacht wurde. Die verfügbar gemachte Schatten Kopie kann durch die Schatten-ID, den Laufwerk Buchstaben, die Freigabe oder den Einfügepunkt angegeben werden.



## <a name="syntax"></a>Syntax

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Shadowid->|Macht die von der angegebenen Schatten-ID angegebene Schatten Kopie nicht verfügbar.|
|\<Laufwerk: >|Macht die Schatten Kopie verfügbar, die dem angegebenen Laufwerk Buchstaben zugeordnet ist (z. b. Laufwerk P).|
|\<Freigabe>|Macht die der angegebenen Freigabe zugeordnete Schatten Kopie \\ \\(z. b. *MachineName*\)) nicht verfügbar.|
|\<Bereitstellungspunkt->|Macht die für den angegebenen Einstellungspunkt zugeordnete Schatten Kopie (z. b. c:\shadowcopy\)) nicht verfügbar.|

## <a name="remarks"></a>Bemerkungen

-   Anstelle von *shadowid*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die verfügbar machung der dem Laufwerk P zugeordneten Schatten Kopie anzuzeigen:
```
unexpose P:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)