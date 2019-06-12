---
title: lodctr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b67c11b24013adb911309ab2ea9bdbfdfc3408da
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437892"
---
# <a name="lodctr"></a>lodctr

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Lässt Sie sich registrieren oder Performance Counter-Namen und die Registrierung konfiguriert in einer Datei speichern und vertrauenswürdigen Dienste festlegen.
## <a name="syntax"></a>Syntax
```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```
### <a name="parameters"></a>Parameter

|    Parameter     |                                                                                                                                         Beschreibung                                                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <filename>    |                                                                                          Registriert die leistungsindikatoreinstellungen Name und erläuternden Texts in der FileName-Initialisierungsdatei bereitgestellt.                                                                                          |
|  /s:<filename>   |                                                                                                       Speichert Leistungsindikator-registrierungseinstellungen, und Erläutern Sie Text in Datei <filename>.                                                                                                       |
|        /r        |                                Wird von Leistungsindikator-registrierungseinstellungen und eine erläuternden Texts aus aktuellen registrierungseinstellungen und zwischengespeicherte Leistung-Dateien, die im Zusammenhang mit der Registrierung.<br /><br />Diese Option ist nur in das Betriebssystem Windows Server 2003 verfügbar.                                |
|  /r:<filename>   | Wiederherstellungen Leistungsindikator-registrierungseinstellungen, und Erläutern Sie Text aus Datei <filename>. **Warnung:** bei Verwendung der **Lodctr/r** können Sie alle Leistungsindikator-registrierungseinstellungen überschrieben und Erklärungstext, ersetzt sie durch die Konfiguration, die in der angegebenen Datei definiert. |
| /t:<servicename> |                                                                                                                       Gibt an, diesen Dienst <servicename> ist vertrauenswürdig.                                                                                                                       |
|        /?        |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="remarks"></a>Hinweise
Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. "<filename>").
## <a name="BKMK_Examples"></a>Beispiele für
Speichern die aktuellen registrierungseinstellungen für die Leistung und erläuternden Text in Datei Leistungsindikator **Perf backup1.txt**:
```
lodctr /s:"perf backup1.txt"
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

