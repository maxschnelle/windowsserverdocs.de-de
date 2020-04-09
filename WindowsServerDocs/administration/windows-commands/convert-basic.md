---
title: Basisdatenträger konvertieren
description: Windows-Befehle-Thema für Convert Basic, das einen leeren dynamischen Datenträger in einen Basis Datenträger konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e0f6f5f04373042956d83bc9136c884c268e591
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847313"
---
# <a name="convert-basic"></a>Basisdatenträger konvertieren

Konvertiert einen leeren dynamischen Datenträger in einen Basis Datenträger.

Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines dynamischen Datenträgers zurück auf einen Basis](https://go.microsoft.com/fwlink/?LinkId=207048) Datenträger (https://go.microsoft.com/fwlink/?LinkId=207048).

## <a name="syntax"></a>Syntax

```
convert basic [noerr]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

> [!IMPORTANT]
> Der Datenträger muss leer sein, um ihn in einen Basis Datenträger zu konvertieren. Sichern Sie Ihre Daten, und löschen Sie dann alle Partitionen oder Volumes, bevor Sie den Datenträger umstellen.

-   Ein dynamischer Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen dynamischen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um den ausgewählten dynamischen Datenträger in Basic zu konvertieren:
```
convert basic
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

