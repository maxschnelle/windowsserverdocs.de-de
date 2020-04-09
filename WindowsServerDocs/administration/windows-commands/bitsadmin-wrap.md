---
title: bitsadmin Umbruch
description: Windows-Befehls Thema für bizadmin Wrap, das jede Zeile von Ausgabetext umschließt, die über den rechten Rand des Befehls Fensters zur nächsten Zeile hinausgeht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 009a0452f44c4944ae110ca6b9e0570793c32a72
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848753"
---
# <a name="bitsadmin-wrap"></a>bitsadmin Umbruch

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Umschließt eine beliebige Zeile von Ausgabetext, der über den rechten Rand des Befehls Fensters zur nächsten Zeile erweitert wird.

## <a name="syntax"></a>Syntax

```
bitsadmin /Wrap Job
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Geben Sie vor anderen Switches an. Standardmäßig wrappen alle Switches, außer dem Schalter [bizadmin Monitor](bitsadmin-monitor.md) , die Ausgabe.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden Informationen für den Auftrag mit dem Namen *mydownloadjob* abgerufen und die Ausgabe umschlossen.

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
