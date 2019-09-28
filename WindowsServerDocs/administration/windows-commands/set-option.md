---
title: Set-Option
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9b9174f219654e99eb9441abe3342c31b5089ef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384049"
---
# <a name="set-option"></a>Set-Option



Legt die Optionen für die Erstellung von Schatten Kopien fest. Bei Verwendung ohne Parameter zeigt die **Option Set die Option** Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

## <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                  Beschreibung                                                                                                  |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [differenziell   |                                                                                                     Plex                                                                                                     |
|  austauschen  |                       Gibt an, dass die Schatten Kopie noch nicht importiert werden soll. Die Datei "Metadata. cab" kann später verwendet werden, um die Schatten Kopie auf denselben oder einen anderen Computer zu importieren.                       |
| [rollbackrecovery] |                     Signalisiert Writer, während des **PostSnapshot** -Ereignisses *Auto Wiederherstellen* zu verwenden. Dies ist hilfreich, wenn die Schatten Kopie für das Rollback verwendet wird (z. b. mit Data Mining).                      |
|   [txfrecover]    |                                                               Fordert VSS auf, die schattenkopiekonsistenz während der Erstellung Transaktions konsistent zu machen.                                                                |
|  [noautorecover]  | Hindert Writer und das Dateisystem daran, Wiederherstellungs Änderungen an der Schatten Kopie in einem Transaktions konsistenten Zustand auszuführen. **Noautorecover** kann nicht mit **txfrecover** oder **rollbackrecover**verwendet werden. |

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)