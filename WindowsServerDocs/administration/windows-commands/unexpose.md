---
title: Heben des
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4e10126739ef82b060e271e9b804a77658b5ec82
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392263"
---
# <a name="unexpose"></a>Heben des



Macht eine Schatten Kopie verfügbar **, die mit dem verfügbar** gemachten Befehl verfügbar gemacht wurde. Die verfügbar gemachte Schatten Kopie kann durch die Schatten-ID, den Laufwerk Buchstaben, die Freigabe oder den Einfügepunkt angegeben werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<shadowid >|Macht die von der angegebenen Schatten-ID angegebene Schatten Kopie nicht verfügbar.|
|\<Laufwerk: >|Macht die Schatten Kopie verfügbar, die dem angegebenen Laufwerk Buchstaben zugeordnet ist (z. b. Laufwerk P).|
|\<Freigabe >|Macht die der angegebenen Freigabe zugeordnete Schatten Kopie (z. b. \\\\*MachineName*\)nicht verfügbar.|
|\<Mountpoint >|Macht die für den angegebenen Einstellungspunkt zugeordnete Schatten Kopie (z. b. c:\shadowcopy\)nicht verfügbar.|

## <a name="remarks"></a>Hinweise

-   Anstelle von *shadowid*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die verfügbar machung der dem Laufwerk P zugeordneten Schatten Kopie anzuzeigen:
```
unexpose P:
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)