---
title: Set-option
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d8d4921-9fdd-4a3c-bb0f-9df5458c4b84
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81678768bb2b5fcfd7f2f2d067562e78e93dc549
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848851"
---
# <a name="set-option"></a>Set-option



Legt die Optionen für die Erstellung von Schattenkopien fest. Wenn Sie ohne Angabe von Parametern **legen Option** zeigt die Hilfe an der Eingabeaufforderung.

## <a name="syntax"></a>Syntax

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[differenziellen | plexer]|Gibt den Typ der Schattenkopie zu erstellen, mit dem Anbieter an.|
|[übertragbarer]|Gibt an, dass die Schattenkopie nicht noch importiert werden. Die Metadaten-CAB-Datei kann später verwendet werden, um die Schattenkopie auf demselben oder einem anderen Computer zu importieren.|
|[rollbackrecover]|Signalisiert der Writer mit *AutoWiederherstellen* während der **PostSnapshot** Ereignis. Dies ist nützlich, wenn die Schattenkopie für Rollback (z. B. mit Datamining) verwendet wird.|
|[Txfrecover]|Fordert Sie VSS, um die Schattenkopie während der Erstellung im Hinblick auf Transaktionen konsistent zu machen.|
|[noautorecover]|-Writer beendet und das Dateisystem, von der Durchführung der Wiederherstellung Änderungen an der Schattenkopie auf einen transaktionskonsistenten Zustand. **Noautorecover** kann nicht verwendet werden, mit **Txfrecover** oder **Rollbackrecover**.|

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)