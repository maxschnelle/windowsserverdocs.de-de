---
title: dispdiag
description: Referenz Artikel für den dispdiag-Befehl, der Anzeigeinformationen in einer Datei protokolliert.
ms.topic: reference
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d2171aae18601f3783389335ea1cfa592a5c7f23
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627150"
---
# <a name="dispdiag"></a>dispdiag

Protokolliert Anzeigeinformationen in einer Datei.

## <a name="syntax"></a>Syntax

```
dispdiag [-testacpi] [-d] [-delay <seconds>] [-out <filepath>]
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -testacpi | Führt einen Hotkey-Diagnosetest aus. Zeigt den Schlüsselnamen, den Code und den Überprüfungs Code für alle während des Tests gedrückten Schlüssel an. |
| -d | Generiert eine Dumpdatei mit Testergebnissen. |
| -Verzögerung `<seconds>` | Verzögert die Erfassung von Daten nach der angegebenen Zeit in *Sekunden*. |
| -Out `<filepath>`  | Gibt den Pfad und den Dateinamen zum Speichern der gesammelten Daten an. Dies muss der letzte Parameter sein. |
| -? | Zeigt verfügbare Befehlsparameter an und bietet Hilfe zur Verwendung. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
