---
title: bitsadmin anhalten
description: Windows-Befehls Thema für bigsadmin Suspend, wodurch der angegebene Auftrag angehalten wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0419f4cdf59d04539b8b4c6d47cec886197d412b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849053"
---
# <a name="bitsadmin-suspend"></a>bitsadmin anhalten

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hält den angegebenen Auftrag an.

## <a name="syntax"></a>Syntax

```
bitsadmin /Suspend <Job>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Verwenden Sie den Schalter [bigsadmin Resume](bitsadmin-resume.md) , um den Auftrag neu zu starten.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Auftrag mit dem Namen *mydownloadjob*angehalten.

```
C:\>bitsadmin /Suspend myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
