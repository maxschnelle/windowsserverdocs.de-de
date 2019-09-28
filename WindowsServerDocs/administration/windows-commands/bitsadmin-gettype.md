---
title: bitsadmin gettype
description: 'Thema Windows-Befehle für **bizadmin GetType** : Ruft den Auftragstyp des angegebenen Auftrags ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca46cb813809621f4fa79b3265198206729a392c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381337"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype



Ruft den Auftragstyp des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetType <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Der Typ kann "Download", "Upload", "Upload-Reply" oder "unknown" lauten.

## <a name="BKMK_examples"></a>Beispiele

Das folgende Beispiel ruft den Auftragstyp für den Auftrag mit dem Namen *mydownloadjob*ab.
```
C:\>bitsadmin /GetType myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)