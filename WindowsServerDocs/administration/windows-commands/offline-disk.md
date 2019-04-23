---
title: Offline-Datenträger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 617371583a3f0cb3d0cb739845208e4216573d9c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834621"
---
# <a name="offline-disk"></a>Offline-Datenträger



Der online-Datenträger mit dem Fokus dauert im Offlinezustand.

> [!IMPORTANT]
> Dieser DiskPart-Befehl ist nicht in jeder Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
offline disk [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|

## <a name="remarks"></a>Hinweise

-   Dieser Befehl funktioniert auf Datenträgern, die im SAN-online-Modus befinden. Es ändert ihre SAN-Modus in den Offlinemodus.
-   Wenn Sie ein dynamischer Datenträger in einer Datenträgergruppe offline geschaltet wird, ändert sich der Status des Datenträgers **fehlende** und die Gruppe wird einen Datenträger, der offline ist. Der fehlende Datenträger wird in der Gruppe "ungültig" verschoben. Wenn der dynamische Datenträger den letzten Datenträger in der Gruppe, wird der Status des Datenträgers wird nun **offline**, und die leere Gruppe entfernt werden.
-   Ein Datenträger muss ausgewählt werden, für die **Offlinedatenträger** Befehl erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um den Datenträger mit dem Fokus offline zu schalten:
```
offline disk
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

