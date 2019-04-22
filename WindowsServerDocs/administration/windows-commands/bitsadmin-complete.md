---
title: bitsadmin complete
description: Windows-Befehle Thema **Bitsadmin vollständige** -wird der Auftrag abgeschlossen. Die heruntergeladenen Dateien sind nicht verfügbar, bis Sie diesen Schalter verwenden.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 561585da370f7e69aa3b83b3ddd7579bfc658a21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817321"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

Wird der Auftrag abgeschlossen. Die heruntergeladenen Dateien sind nicht verfügbar, bis Sie diesen Schalter verwenden. Verwenden Sie diese Option aus, nachdem der Auftrag in den übertragenen Zustand verschoben. Andernfalls stehen nur die Dateien, die erfolgreich übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /complete <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Wenn der Status des Auftrags übertragen wird, BITS wurde erfolgreich übertragen alle Dateien im Auftrag. Die Dateien sind jedoch nicht verfügbar, bis Sie verwenden die **/ vollständige** wechseln. Wenn mehrere Aufträge verwenden *MyDownloadJob* als Name, ersetzen Sie *MyDownloadJob* durch die Auftrags GUID zur eindeutigen Identifizierung des Auftrags.
```
C:\>bitsadmin /complete myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)