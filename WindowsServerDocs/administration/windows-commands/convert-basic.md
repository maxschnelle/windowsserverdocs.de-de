---
title: Basisdatenträger konvertieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: df1f999499154366304d59e0573ba921ab1af83d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434241"
---
# <a name="convert-basic"></a>Basisdatenträger konvertieren



Konvertiert einen leeren dynamischen Datenträger in einen Basisdatenträger konvertieren.

Anweisungen dazu, wie Sie diesen Befehl verwenden, finden Sie unter [ändern Sie einen dynamischen Datenträger zurück in einen Basisdatenträger](https://go.microsoft.com/fwlink/?LinkId=207048) (https://go.microsoft.com/fwlink/?LinkId=207048).

## <a name="syntax"></a>Syntax

```
convert basic [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

> [!IMPORTANT]
> Der Datenträger muss für die Konvertierung in einen Basisdatenträger leer sein. Sichern Sie Ihre Daten, und klicken Sie dann löschen Sie alle Partitionen oder Volumes, bevor der Datenträger konvertieren.
> -   Ein dynamischer Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **select Disk** Befehl aus, wählen Sie einen dynamischen Datenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um den ausgewählten dynamischen Datenträger in Basic zu konvertieren:
```
convert basic
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

