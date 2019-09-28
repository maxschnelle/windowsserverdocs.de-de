---
title: bitsadmin anhalten
description: 'Das Thema Windows-Befehle für **bigsadmin Suspend** : hält den angegebenen Auftrag an.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a3a484df2b50cdc8893512020b835f913793d2c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380371"
---
# <a name="bitsadmin-suspend"></a>bitsadmin anhalten

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hält den angegebenen Auftrag an.

## <a name="syntax"></a>Syntax

```
bitsadmin /Suspend <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Verwenden Sie den Schalter [bigsadmin Resume](bitsadmin-resume.md) , um den Auftrag neu zu starten.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Auftrag mit dem Namen *mydownloadjob*angehalten.

```
C:\>bitsadmin /Suspend myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
