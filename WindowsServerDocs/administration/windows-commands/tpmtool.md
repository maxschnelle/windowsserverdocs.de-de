---
title: tpmtool
description: Referenz Artikel für den Befehl "tpmtool", der Informationen zum Trusted Platform Module abruft.
ms.topic: reference
author: ashleytqy
ms.author: asteoh
manager: raigner
ms.date: 05/07/2019
ms.openlocfilehash: bc0aaa4bc4bd9c23e0cf22b0315335287867d8cd
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156432"
---
# <a name="tpmtool"></a>tpmtool

Dieses Hilfsprogramm kann verwendet werden, um Informationen zum [Trusted Platform Module (TPM)](/windows/security/information-protection/tpm/trusted-platform-module-overview)zu erhalten.

>[!IMPORTANT]
>Einige Informationen beziehen sich möglicherweise auf das vorab veröffentlichte Produkt, das im wesentlichen geändert werden kann, bevor es kommerziell veröffentlicht wird. Microsoft übernimmt keine Garantie, weder ausdrücklich noch stillschweigend, für die hier bereitgestellten Informationen.

## <a name="syntax"></a>Syntax

```
tpmtool /parameter [<arguments>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| getde viceinformation | Zeigt die grundlegenden Informationen für das TPM an. Weitere Informationen zu den Werten für das informationsflag finden Sie im Artikel [Win32_Tpm:: isread yinformation-Methoden Parameter](/windows/win32/secprov/win32-tpm-isreadyinformation#parameters) . |
| GatherLogs [Ausgabeverzeichnis Pfad] | Sammelt TPM-Protokolle und platziert Sie im angegebenen Verzeichnis. Wenn dieses Verzeichnis nicht vorhanden ist, wird es erstellt. Standardmäßig werden die Protokolldateien im aktuellen Verzeichnis abgelegt. Die folgenden Dateien können generiert werden:<ul><li>Tpmevents. evtx</li><li>TpmInformation.txt</li><li>Srtmboot. dat</li><li>Srtmresume. dat</li><li>Drtmboot. dat</li><li>Drtmresume. dat</li></ul> |
| drivertrag. `[start | stop]` | Startet oder beendet die Erfassung von TPM-Treiber Ablauf Verfolgungen. Das Ablauf Verfolgungs Protokoll " *tpmtrace. ETL*" wird erstellt und im aktuellen Verzeichnis abgelegt. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die grundlegenden Informationen für das TPM anzuzeigen:

```
tpmtool getdeviceinformation
```

Um TPM-Protokolle zu erfassen und im aktuellen Verzeichnis zu platzieren, geben Sie Folgendes ein:

```
tpmtool gatherlogs
```

Um TPM-Protokolle zu erfassen und in zu platzieren, geben Sie Folgendes ein `C:\Users\Public` :

```
tpmtool gatherlogs C:\Users\Public
```

Geben Sie zum Erfassen von TPM-Treiber Ablauf Verfolgungen Folgendes ein:

```
tpmtool drivertracing start
# Run scenario
tpmtool drivertracing stop
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [COM-Fehler Codes (TPM, Pla, f)](/windows/win32/com/com-error-codes-6)
