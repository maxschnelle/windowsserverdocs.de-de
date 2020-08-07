---
title: dispdiag
description: Referenz Artikel für den dispdiag-Befehl, der Anzeigeinformationen in einer Datei protokolliert.
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78b8080395fa30a934d1a9380bf86beae7e62dc0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890829"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
