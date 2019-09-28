---
title: lodctr
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 96a2818110b766071eb83822abd34d8c0d00132d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374573"
---
# <a name="lodctr"></a>lodctr

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit können Sie den Namen und die Registrierungs Einstellungen des Leistungs Zählers in einer Datei registrieren oder speichern und vertrauenswürdige Dienste festlegen.
## <a name="syntax"></a>Syntax
```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```
### <a name="parameters"></a>Parameter

|    Parameter     |                                                                                                                                         Beschreibung                                                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <filename>    |                                                                                          Registriert die namens Einstellungen des Leistungs Zählers und erläutert den in der Initialisierungsdatei Dateiname angegebenen Text.                                                                                          |
|  /s: <filename>   |                                                                                                       Speichert die Registrierungs Einstellungen des Leistungs Zählers und erläutert Text in Datei <filename>.                                                                                                       |
|        /r        |                                Stellt die Registrierungs Einstellungen für den-Leistungs-und-Text aus aktuellen Registrierungs Einstellungen und zwischengespeicherten Leistungs Dateien für die Registrierung wieder her.<br /><br />Diese Option ist nur im Betriebssystem Windows Server 2003 verfügbar.                                |
|  /r: <filename>   | Stellt die Registrierungs Einstellungen des Leistungs Zählers wieder her und erläutert Text aus der Datei <filename>. **Warnung:** Wenn Sie den Befehl **Lodctr/r** verwenden, überschreiben Sie alle Registrierungs Einstellungen des Leistungs Zählers und erläutern den Text, sodass Sie durch die in der angegebenen Datei definierte Konfiguration ersetzt werden. |
| /t: <servicename> |                                                                                                                       Gibt an, dass der Dienst <servicename> vertrauenswürdig ist.                                                                                                                       |
|        /?        |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="remarks"></a>Hinweise
Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "<filename>").
## <a name="BKMK_Examples"></a>Beispiele
So speichern Sie die aktuellen Registrierungs Einstellungen und den Leistungs Bestellungstext in der Datei **Leistungs Sicherung 1. txt**:
```
lodctr /s:"perf backup1.txt"
```
## <a name="additional-references"></a>Weitere Verweise
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

