---
title: bitsadmin anhalten
description: Windows-Befehle Thema **Bitsadmin anhalten** -hält an den angegebenen Auftrag.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 87e1bbd1b068d68fb60655043735c6c1aeb07707
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825921"
---
# <a name="bitsadmin-suspend"></a>bitsadmin anhalten

> Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Hält den angegebenen Auftrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /Suspend <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Verwenden Sie zum Neustarten des Auftrags die [Bitsadmin fortsetzen](bitsadmin-resume.md) wechseln.

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel hält den Auftrag mit dem Namen *MyDownloadJob*.

```
C:\>bitsadmin /Suspend myDownloadJob
```

#### <a name="additional-references"></a>Zusätzliche Referenzen

[Befehlszeilensyntax](command-line-syntax-key.md)
