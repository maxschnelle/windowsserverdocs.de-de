---
title: Set-Option
description: Referenz Artikel für den Befehl Set Option, mit dem die Optionen für die Erstellung von Schatten Kopien festgelegt werden.
ms.topic: reference
ms.assetid: 4d8d4921-9fdd-4a3c-bb0f-9df5458c4b84
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a37e993700169f0268e68822be3a7fbaf6e58361
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389056"
---
# <a name="set-option"></a>Set-Option

Legt die Optionen für die Erstellung von Schatten Kopien fest. Bei Verwendung ohne Parameter zeigt die **Option Set die Option** Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| differenzielle | Gibt an, dass eine Zeit Punkt Momentaufnahme der angegebenen Volumes erstellt werden soll. |
| Plex | Gibt an, dass eine Zeit Punkt Klon Kopie der Daten auf einem angegebenen Volume erstellt werden soll. |
| austauschen | Gibt an, dass die Schatten Kopie noch nicht importiert werden soll. Die Datei "Metadata. cab" kann später verwendet werden, um die Schatten Kopie auf denselben oder einen anderen Computer zu importieren. |
| [rollbackrecovery] | Signalisiert Writer, während des **PostSnapshot** -Ereignisses *Auto Wiederherstellen* zu verwenden. Dies ist hilfreich, wenn die Schatten Kopie für das Rollback verwendet wird (z. b. mit Data Mining). |
| [txfrecover] | Fordert VSS auf, die schattenkopiekonsistenz während der Erstellung Transaktions konsistent zu machen. |
| [noautorecover] | Hindert Writer und das Dateisystem daran, Wiederherstellungs Änderungen an der Schatten Kopie in einem Transaktions konsistenten Zustand auszuführen. **Noautorecover** kann nicht mit **txfrecover** oder **rollbackrecover**verwendet werden. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Kontext Befehl festlegen](set-context.md)

- [Befehl "Metadaten festlegen"](set-metadata.md)

- [Befehl "ausführliche festlegen"](set-verbose.md)
