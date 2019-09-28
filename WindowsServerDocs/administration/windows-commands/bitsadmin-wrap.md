---
title: bitsadmin Umbruch
description: Das Thema Windows-Befehle für **bizadmin** umschließt eine beliebige Zeile von Ausgabetext, die über den rechten Rand des Befehls Fensters zur nächsten Zeile hinaus erweitert wird.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5609fb6f38716795a545e0c7fe3939f893a8c8d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380680"
---
# <a name="bitsadmin-wrap"></a>bitsadmin Umbruch

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Umschließt die Ausgabe so, dass Sie in ein Befehlsfenster passt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Wrap Job
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Geben Sie vor anderen Switches an. Standardmäßig wrappen alle Switches, außer dem Schalter [bizadmin Monitor](bitsadmin-monitor.md) , die Ausgabe.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden Informationen für den Auftrag mit dem Namen *mydownloadjob* abgerufen und die Ausgabe umschlossen.

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
