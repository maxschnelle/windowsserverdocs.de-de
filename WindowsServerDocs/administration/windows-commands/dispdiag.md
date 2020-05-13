---
title: dispdiag
description: Referenz Thema für den dispdiag-Befehl, mit dem Anzeigeinformationen in einer Datei protokolliert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff4e3690ec3b2c9d473f05027d5637eda124d0ba
ms.sourcegitcommit: aed942d11f1a361fc1d17553a4cf190a864d1268
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235220"
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
| -Verzögerung`<seconds>` | Verzögert die Erfassung von Daten nach der angegebenen Zeit in *Sekunden*. |
| -Out`<filepath>`  | Gibt den Pfad und den Dateinamen zum Speichern der gesammelten Daten an. Dies muss der letzte Parameter sein. |
| -? | Zeigt verfügbare Befehlsparameter an und bietet Hilfe zur Verwendung. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
