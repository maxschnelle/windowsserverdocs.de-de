---
title: bitsadmin getstate
description: Windows-Befehls Thema für bizadmin GetState
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 2cff790c8787b1514e8523a4583184d6f6a59efc
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259105"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate


Ruft den Zustand des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetState <Job>
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
|    Auftrag    | Der Anzeige Name oder GUID des Auftrags. |

## <a name="remarks"></a>Hinweise

Mögliche Zustandswerte:

|      Bundesland/Kanton      | Beschreibung |
| --------------- | ----------- |
| Warteschlange          | Der Auftrag wartet darauf, ausgeführt zu werden. |
| VERBINDUNG WIRD HERGESTELLT      | Bits kontaktiert den Server. |
| Tra    | Bits überträgt Daten. |
| Gegangen     | Bits hat erfolgreich alle Dateien im Auftrag übertragen. |
| SUSPENDED (ANGEHALTEN)       | Der Auftrag wurde angehalten. |
| FEHLER           | Ein nicht BEHEB barer Fehler ist aufgetreten. die Übertragung wird nicht wiederholt. |
| TRANSIENT_ERROR | Ein BEHEB barer Fehler ist aufgetreten. der Übertragungs Versuch wird wiederholt, wenn die minimale Wiederholungs Verzögerung abläuft. |
| BESTÄTIGT    | Der Auftrag wurde abgeschlossen. |
| Hob        | Der Auftrag wurde abgebrochen. |

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Status für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /GetState myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
