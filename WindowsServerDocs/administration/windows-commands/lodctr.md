---
title: lodctr
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 33c14970a669d24f1cc803003e8530712311c564
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840953"
---
# <a name="lodctr"></a>lodctr

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit können Sie den Namen und die Registrierungs Einstellungen des Leistungs Zählers in einer Datei registrieren oder speichern und vertrauenswürdige Dienste festlegen.
## <a name="syntax"></a>Syntax
```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```
#### <a name="parameters"></a>Parameter

|    Parameter     |                                                                                                                                         Beschreibung                                                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <filename>    |                                                                                          Registriert die namens Einstellungen des Leistungs Zählers und erläutert den in der Initialisierungsdatei Dateiname angegebenen Text.                                                                                          |
|  /s:<filename>   |                                                                                                       Speichert Registrierungs Einstellungen des Leistungs Zählers und erläutert Text in Datei <filename>.                                                                                                       |
|        /r        |                                Stellt die Registrierungs Einstellungen für den-Leistungs-und-Text aus aktuellen Registrierungs Einstellungen und zwischengespeicherten Leistungs Dateien für die Registrierung wieder her.<p>Diese Option ist nur im Betriebssystem Windows Server 2003 verfügbar.                                |
|  /r:<filename>   | Stellt die Registrierungs Einstellungen des Leistungs Zählers wieder her und erläutert Text aus dem Datei <filename>. **Warnung:** Wenn Sie den Befehl **Lodctr/r** verwenden, überschreiben Sie alle Registrierungs Einstellungen des Leistungs Zählers und erläutern den Text, sodass Sie durch die in der angegebenen Datei definierte Konfiguration ersetzt werden. |
| /t:<servicename> |                                                                                                                       Gibt an, dass der Dienst <servicename> vertrauenswürdig ist.                                                                                                                       |
|        /?        |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="remarks"></a>Hinweise
Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. <filename>).
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
So speichern Sie die aktuellen Registrierungs Einstellungen und den Leistungs Bestellungstext in der Datei **Leistungs Sicherung 1. txt**:
```
lodctr /s:perf backup1.txt
```
## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

