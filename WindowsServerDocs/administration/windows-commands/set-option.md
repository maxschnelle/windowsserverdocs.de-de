---
title: Set-Option
description: Windows-Befehls Thema für die Set-Option, die die Optionen für die Erstellung von Schatten Kopien festlegt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4d8d4921-9fdd-4a3c-bb0f-9df5458c4b84
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a956c74619f3a6c33dfcaa62ee4c810cd93b21f1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834493"
---
# <a name="set-option"></a>Set-Option

Legt die Optionen für die Erstellung von Schatten Kopien fest. Bei Verwendung ohne Parameter zeigt die **Option Set die Option** Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

### <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                  Beschreibung                                                                                                  |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [differenziell   |                                                                                                     Plex                                                                                                     |
|  austauschen  |                       Gibt an, dass die Schatten Kopie noch nicht importiert werden soll. Die Datei "Metadata. cab" kann später verwendet werden, um die Schatten Kopie auf denselben oder einen anderen Computer zu importieren.                       |
| [rollbackrecovery] |                     Signalisiert Writer, während des **PostSnapshot** -Ereignisses *Auto Wiederherstellen* zu verwenden. Dies ist hilfreich, wenn die Schatten Kopie für das Rollback verwendet wird (z. b. mit Data Mining).                      |
|   [txfrecover]    |                                                               Fordert VSS auf, die schattenkopiekonsistenz während der Erstellung Transaktions konsistent zu machen.                                                                |
|  [noautorecover]  | Hindert Writer und das Dateisystem daran, Wiederherstellungs Änderungen an der Schatten Kopie in einem Transaktions konsistenten Zustand auszuführen. **Noautorecover** kann nicht mit **txfrecover** oder **rollbackrecover**verwendet werden. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)