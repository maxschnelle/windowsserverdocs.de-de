---
title: convert gpt
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 433e30efeecec4e4ec51d67c40c14cacf986d12e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434225"
---
# <a name="convert-gpt"></a>convert gpt



Konvertiert einen leeren Basisdatenträger mit dem Partitionsstil der master Boot Record (MBR) in einen Basisdatenträger mit Partitionsstil der GUID-Partitionstabelle (GPT).

Anweisungen dazu, wie Sie diesen Befehl verwenden, finden Sie unter [ändern Sie einen Datenträger Master Boot Record in eine GUID-Partitionstabelle](https://go.microsoft.com/fwlink/?LinkId=207049) (https://go.microsoft.com/fwlink/?LinkId=207049).

## <a name="syntax"></a>Syntax

```
convert gpt [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

> [!IMPORTANT]
> Der Datenträger muss für die Konvertierung in einen GPT-Datenträger leer sein. Sichern Sie Ihre Daten, und klicken Sie dann löschen Sie alle Partitionen oder Volumes, bevor der Datenträger konvertieren.
> -   Die erforderliche Mindestgröße des Datenträgers für die Konvertierung in GPT beträgt 128 MB.
> -   Ein grundlegende MBR-Datenträger muss ausgewählt werden, für diesen Vorgang erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen Basisdatenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um einen einfachen Datenträger von MBR-Partitionstyp in GPT-Partitionstyp zu konvertieren:
```
convert gpt
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

