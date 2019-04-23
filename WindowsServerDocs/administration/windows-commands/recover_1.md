---
title: recover
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc3a73d-9456-41a0-b375-2b4cc37c3992
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 261bfd79d74323ad324246e21b84a5eb798ebcdf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867181"
---
# <a name="recover"></a>recover



Aktualisiert den Zustand aller Datenträger in einer Datenträgergruppe versuchen, in einem ungültigen Datenträgergruppe wiederherzustellen und synchronisiert die gespiegelte Volumes und RAID-5-Volumes, die veraltete Daten erneut.

> [!IMPORTANT]
> Dieser DiskPart-Befehl ist nicht in jeder Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
recover [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

-   Mit diesem Befehl wird mit einer Datenträgergruppe ausgeführt.
-   Dieser Befehl gilt nur für Gruppen von dynamischen Datenträgern. Wenn Sie diesen Befehl für eine Gruppe mit einem einfachen Datenträger verwendet wird, es wird kein Fehler zurückgegeben, jedoch wird keine Aktion ausgeführt werden.
-   Dieser Befehl wirkt sich auf Datenträger, die durchgeführt werden bzw. ein Fehler auftritt. Er arbeitet auch auf Volumes, die fehlerhaft sind, fehlschlägt, oder im Zustand Fehlerhafte Redundanz.
-   Ein Datenträger, die Teil einer Datenträgergruppe muss ausgewählt werden, für diesen Befehl erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Um die Datenträgergruppe wiederherzustellen, die der Datenträger mit dem Fokus enthält, geben Sie Folgendes ein:
```
recover
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

