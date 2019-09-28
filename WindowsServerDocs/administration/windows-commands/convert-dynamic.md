---
title: dynamisch konvertieren
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 15c15d14aeb440c5d7862f0a304f223988f52bbe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379100"
---
# <a name="convert-dynamic"></a>dynamisch konvertieren



Konvertiert einen Basis Datenträger in einen dynamischen Datenträger.

Anweisungen zur Verwendung dieses Befehls finden Sie unter Ändern eines Basis Datenträgers [in einen dynamischen](https://go.microsoft.com/fwlink/?LinkId=207047) Datenträger (https://go.microsoft.com/fwlink/?LinkId=207047).

## <a name="syntax"></a>Syntax

```
convert dynamic [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Alle vorhandenen Partitionen auf dem Basis Datenträger werden zu einfachen Volumes.
-   Ein Basis Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger **auswählen** , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um einen einfachen Datenträger in einen dynamischen Datenträger zu konvertieren:
```
convert dynamic
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

