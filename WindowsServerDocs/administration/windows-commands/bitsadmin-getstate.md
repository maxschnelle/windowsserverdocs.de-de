---
title: bitsadmin getstate
description: 'Windows-Befehle Thema ****- '
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
ms.openlocfilehash: 55be37a6b1b44b81ed9002e5e3b9eb1fd46bd0dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381233"
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
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Folgende Zustände sind möglich:

|-----|-----| | In Warteschlange | Der Auftrag wartet darauf, ausgeführt zu werden. | | Verbindung wird hergestellt | Bits kontaktiert den Server. | | Übertragen | Bits überträgt Daten. | | Angehalten | Der Auftrag wurde angehalten. | | Fehler | Ein nicht BEHEB barer Fehler ist aufgetreten. die Übertragung wird nicht wiederholt. | TRANSIENT_ERROR | Ein BEHEB barer Fehler ist aufgetreten. der Übertragungs Versuch wird wiederholt, wenn die minimale Wiederholungs Verzögerung abläuft. | Bestätigt | Der Auftrag wurde abgeschlossen. | | Abgebrochen | Der Auftrag wurde abgebrochen. |

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Status für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetState myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)