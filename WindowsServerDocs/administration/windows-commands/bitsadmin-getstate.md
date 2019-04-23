---
title: bitsadmin getstate
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7ed7529fda264efaceb6b4b36e36e728c211f3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889621"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate



Ruft den Zustand des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetState <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Die möglichen Statuswerte sind:

|-----|-----| | IN DER WARTESCHLANGE | Der Auftrag wird auf die Ausführung warten. | | EINE VERBINDUNG HERSTELLEN | BITS wird eine Verbindung mit dem Server. | | ÜBERTRAGEN VON | BITS wird übertragen von Daten. | | ANGEHALTEN | Der Auftrag wurde angehalten. | | FEHLER | Ein nicht behebbarer Fehler aufgetreten. die Übertragung wird nicht wiederholt. | | TRANSIENT_ERROR | Ein behebbarer Fehler aufgetreten. die Übertragung wird wiederholt, wenn die minimale wiederholungsverzögerung läuft ab. | | BESTÄTIGT | Der Auftrag abgeschlossen wurde. | | ABGEBROCHEN | Der Auftrag wurde abgebrochen. |

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft den Status des Auftrags namens *MyDownloadJob*.
```
C:\>bitsadmin /GetState myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)