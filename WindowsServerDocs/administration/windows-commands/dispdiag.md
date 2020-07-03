---
title: dispdiag
description: Referenz Artikel für den dispdiag-Befehl, der Anzeigeinformationen in einer Datei protokolliert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d95a53f60aa7e51450a640d5ec9c5a5e6ccb41a6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931221"
---
# <a name="dispdiag"></a>dispdiag

Protokolliert Anzeigeinformationen in einer Datei.

## <a name="syntax"></a>Syntax

```
dispdiag [-testacpi] [-d] [-delay <seconds>] [-out <filepath>]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -testacpi | Führt einen Hotkey-Diagnosetest aus. Zeigt den Schlüsselnamen, den Code und den Überprüfungs Code für alle während des Tests gedrückten Schlüssel an. |
| -d | Generiert eine Dumpdatei mit Testergebnissen. |
| -Verzögerung`<seconds>` | Verzögert die Erfassung von Daten nach der angegebenen Zeit in *Sekunden*. |
| -Out`<filepath>`  | Gibt den Pfad und den Dateinamen zum Speichern der gesammelten Daten an. Dies muss der letzte Parameter sein. |
| -? | Zeigt verfügbare Befehlsparameter an und bietet Hilfe zur Verwendung. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
