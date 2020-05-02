---
title: lodctr
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e20e085e5e2cadcb0684ef57f80137a6043b1e64
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724441"
---
# <a name="lodctr"></a>lodctr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit können Sie den Namen und die Registrierungs Einstellungen des Leistungs Zählers in einer Datei registrieren oder speichern und vertrauenswürdige Dienste festlegen.
## <a name="syntax"></a>Syntax
```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```
#### <a name="parameters"></a>Parameter

|    Parameter     |                                                                                                                                         BESCHREIBUNG                                                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <filename>    |                                                                                          Registriert die namens Einstellungen des Leistungs Zählers und erläutert den in der Initialisierungsdatei Dateiname angegebenen Text.                                                                                          |
|  /s<filename>   |                                                                                                       Speichert die Registrierungs Einstellungen des Leistungs Zählers und erläutert <filename>Text in der Datei.                                                                                                       |
|        /r        |                                Stellt die Registrierungs Einstellungen für den-Leistungs-und-Text aus aktuellen Registrierungs Einstellungen und zwischengespeicherten Leistungs Dateien für die Registrierung wieder her.<p>Diese Option ist nur im Betriebssystem Windows Server 2003 verfügbar.                                |
|  /r<filename>   | Stellt Registrierungs Einstellungen des Leistungs Zählers wieder her und <filename>erläutert Text aus der Datei. **Warnung:** Wenn Sie den Befehl **Lodctr/r** verwenden, überschreiben Sie alle Registrierungs Einstellungen des Leistungs Zählers und erläutern den Text, sodass Sie durch die in der angegebenen Datei definierte Konfiguration ersetzt werden. |
| /t:<servicename> |                                                                                                                       Gibt an, <servicename> dass der Dienst vertrauenswürdig ist.                                                                                                                       |
|        /?        |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="remarks"></a>Bemerkungen
Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen <filename>(z. b.).
## <a name="examples"></a>Beispiele
So speichern Sie die aktuellen Registrierungs Einstellungen und den Leistungs Bestellungstext in der Datei **Leistungs Sicherung 1. txt**:
```
lodctr /s:perf backup1.txt
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

