---
title: lodctr
description: Referenz Artikel für den lodctr-Befehl, mit dem Sie den Namen und die Registrierungs Einstellungen des Leistungs Zählers in einer Datei registrieren oder speichern und vertrauenswürdige Dienste festlegen können.
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 428830b06796914e66434c90f7624cc7c64eec5b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887475"
---
# <a name="lodctr"></a>lodctr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit können Sie den Namen und die Registrierungs Einstellungen des Leistungs Zählers in einer Datei registrieren oder speichern und vertrauenswürdige Dienste festlegen.

## <a name="syntax"></a>Syntax

```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<filename>` | Gibt den Namen der Initialisierungsdatei an, in der die Namen Einstellungen und der erklärende Text des Leistungs Zählers registriert werden. |
| /s`<filename>` | Gibt den Namen der Datei an, in der die Registrierungs Einstellungen des Leistungs Zählers und der erklärende Text gespeichert werden. |
| /r | Stellt die Registrierungs Einstellungen und den erläuternden Text aus aktuellen Registrierungs Einstellungen und zwischengespeicherten Leistungs Dateien für die Registrierung wieder her. |
| /r`<filename>` | Gibt den Namen der Datei an, mit der die Registrierungs Einstellungen des Leistungs Zählers und der erklärende Text wieder hergestellt werden<p>**Warnung:** Wenn Sie diesen Befehl verwenden, überschreiben Sie alle Registrierungs Einstellungen des Leistungs Zählers und den erläuternden Text und ersetzen Sie durch die in der angegebenen Datei definierte Konfiguration. |
| /t:`<servicename>` | Gibt an, dass der Dienst `<servicename>` vertrauenswürdig ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Dateiname 1").

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuellen Leistungs Registrierungs Einstellungen und den erläuternden Text in der Datei *"Perf backup1.txt"* zu speichern:

```
lodctr /s:"perf backup1.txt"
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
