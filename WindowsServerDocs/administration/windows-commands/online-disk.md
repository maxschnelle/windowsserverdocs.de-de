---
title: Online-Datenträger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc44a783-eaa4-40ca-be01-5703b5bf4eb3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c30d0853ff0ae065f02c0ee198c8cdcb90c950b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858061"
---
# <a name="online-disk"></a>Online-Datenträger



Bringt Datenträger, die gerade in einen Onlinestatus offline sind.

> [!IMPORTANT]
> Dieser Befehl ist nicht in jeder Edition von Windows Vista verfügbar.

> [!IMPORTANT]
> Dieser Befehl schlägt fehl, wenn es auf einem schreibgeschützten Datenträger verwendet wird.

Anweisungen dazu, wie Sie diesen Befehl verwenden, finden Sie unter [Reaktivieren eines nicht vorhanden oder Offline dynamischer Datenträger](https://go.microsoft.com/fwlink/?LinkId=207046) (https://go.microsoft.com/fwlink/?LinkId=207046).

## <a name="syntax"></a>Syntax

```
online disk [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

-   Bei der Verwendung ohne Parameter in Windows Vista, arbeitet mit diesem Befehl in einer Datenträgergruppe ein. Für basic-Datenträger ist nie mehr als einen Datenträger pro Gruppe. Für dynamische Datenträger enthält die Gruppe alle nicht-fremden dynamischen Datenträgern.
-   Bei Basisdatenträger wird dieser Befehl versucht, den ausgewählten Datenträger und alle Volumes auf diesem Datenträger online zu schalten.
-   Für dynamische Datenträger wird mit diesem Befehl versucht, alle Datenträger wieder online schalten, die nicht als Fremdschlüssel auf dem lokalen Computer gekennzeichnet sind. Es wird auch versuchen, alle Volumes auf dem Satz der dynamischen Datenträger online zu schalten.
-   Wenn Sie ein dynamischer Datenträger in einer Datenträgergruppe online geschaltet wird, und es ist die einzige Festplatte in der Gruppe, die ursprüngliche Gruppe neu erstellt, und der Datenträger wird in dieser Gruppe verschoben. Wenn andere Datenträger in der Gruppe vorhanden sind, und diese online sind, wird der Datenträger einfach wieder in der Gruppe hinzugefügt.
-   Wenn die Gruppe von eines ausgewählten Datenträgers gespiegelten oder RAID-5-Volumes enthält, synchronisiert mit diesem Befehl auch diese Volumes erneut.
-   Ein Datenträger muss ausgewählt werden, damit dieser Befehl erfolgreich ausgeführt werden. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Um den Datenträger mit dem Fokus online zu schalten, geben Sie Folgendes ein:
```
online disk
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

