---
title: dynamisch konvertieren
description: Windows-Befehls Artikel für Convert Dynamic, bei dem ein Basis Datenträger in einen dynamischen Datenträger konvertiert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ad84cf2ecb6808b68110187b52f3fc13590b491
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847323"
---
# <a name="convert-dynamic"></a>dynamisch konvertieren

Konvertiert einen Basis Datenträger in einen dynamischen Datenträger.

Anweisungen zur Verwendung dieses Befehls finden Sie unter Ändern eines Basis Datenträgers [in einen dynamischen](https://go.microsoft.com/fwlink/?LinkId=207047) Datenträger (https://go.microsoft.com/fwlink/?LinkId=207047).

## <a name="syntax"></a>Syntax

```
convert dynamic [noerr]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Alle vorhandenen Partitionen auf dem Basis Datenträger werden zu einfachen Volumes.
-   Ein Basis Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger **auswählen** , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um einen einfachen Datenträger in einen dynamischen Datenträger zu konvertieren:
```
convert dynamic
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

