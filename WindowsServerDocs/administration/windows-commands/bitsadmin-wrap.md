---
title: bitsadmin Umbruch
description: Windows-Befehle Thema **Bitsadmin Wrap** -dient als Wrapper für jede Zeile der Ausgabe Text erweitern, über die rechte Rand des Befehlsfensters in die nächste Zeile.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4834a8a17c72394b6ee8f051ec76919af9880124
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881671"
---
# <a name="bitsadmin-wrap"></a>bitsadmin Umbruch

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Umschließt die Ausgabe in einem Befehlsfenster passen.

## <a name="syntax"></a>Syntax

```
bitsadmin /Wrap Job
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Geben Sie vor anderen Schaltern. Standardmäßig wird für alle Switches, mit Ausnahme der [Bitsadmin Monitor](bitsadmin-monitor.md) wechseln, und Packen Sie die Ausgabe.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft Informationen für den Auftrag mit dem Namen *MyDownloadJob* und dient als Wrapper für die Ausgabe.

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

#### <a name="additional-references"></a>Zusätzliche Referenzen

[Befehlszeilensyntax](command-line-syntax-key.md)
