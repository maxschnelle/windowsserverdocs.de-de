---
title: tpmtool
description: Referenz Artikel für das tpmtool, das Informationen zum Trusted Platform Module abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: a6b092f9242f76092cb45e484ef59d8bb29147dc
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936905"
---
# <a name="tpmtool"></a>tpmtool

Dieses Hilfsprogramm kann verwendet werden, um Informationen zum [Trusted Platform Module (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview)zu erhalten.

>[!IMPORTANT]
>Einige Informationen beziehen sich auf die Vorabversion, an der bis zur kommerziellen Veröffentlichung unter Umständen noch grundsätzliche Änderungen vorgenommen werden. Microsoft übernimmt bezüglich der hier bereitgestellten Informationen keine Gewährleistungen, weder ausdrücklich noch konkludent.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#tpmtool_examples).

## <a name="syntax"></a>Syntax

```
tpmtool /parameter [<arguments>]
```
### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|getde viceinformation|Zeigt die grundlegenden Informationen für das TPM an. Die Bedeutung der informationsflagwerte finden Sie [hier](https://docs.microsoft.com/windows/desktop/SecProv/win32-tpm-isreadyinformation#parameters).|
|GatherLogs [Ausgabeverzeichnis Pfad]|Sammelt TPM-Protokolle und platziert Sie im angegebenen Verzeichnis. Wenn dieses Verzeichnis nicht vorhanden ist, wird es erstellt. Standardmäßig werden Sie im aktuellen Verzeichnis abgelegt. Die folgenden Dateien können generiert werden: </br>-Tpmevents. evtx</br>-TpmInformation.txt</br>-Srtmboot. dat</br>-Srtmresume. dat</br>-Drtmboot. dat</br>-Drtmresume. dat</br>|
|drivertracing [starten/Abbrechen]|Startet/beendet die Erfassung von TPM-Treiber-Ablauf Verfolgungen. Das Ablauf Verfolgungs Protokoll "tpmtrace. ETL" wird generiert und im aktuellen Verzeichnis abgelegt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=tpmtool_examples></a>Beispiele

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

## <a name="decoding-error-codes"></a>Decodieren von Fehler Codes

TPM-spezifische Fehlercodes werden [hier](https://docs.microsoft.com/windows/desktop/com/com-error-codes-6)dokumentiert.
