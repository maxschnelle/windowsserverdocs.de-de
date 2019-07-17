---
title: tpmtool
description: Windows-Befehle Thema Tpmtool - Ruft Informationen über das Trusted Platform Module ab.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: e125dbf6127b92c91e041c431f1e462e1f884168
ms.sourcegitcommit: 0ff812a80f654fa2c35b1632524e27841eca75c7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/16/2019
ms.locfileid: "68230864"
---
# <a name="tpmtool"></a>tpmtool

Dieses Hilfsprogramm kann verwendet werden, um Informationen zu erhalten, über die [Trusted Platform Module (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview).

>[!IMPORTANT]
>Einige Informationen beziehen sich auf die Vorabversion, an der bis zur kommerziellen Veröffentlichung unter Umständen noch grundsätzliche Änderungen vorgenommen werden. Microsoft übernimmt keine Garantie, weder ausdrücklich noch stillschweigend, für die hier bereitgestellten Informationen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#tpmtool_examples).

## <a name="syntax"></a>Syntax

```
tpmtool /parameter [<arguments>]
```
## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|getdeviceinformation|Zeigt die grundlegende Informationen des TPM. Die Bedeutung der Flagwerte Informationen finden Sie [hier](https://docs.microsoft.com/windows/desktop/SecProv/win32-tpm-isreadyinformation#parameters).|
|GatherLogs [Pfad des Ausgabeverzeichnisses]|TPM-Protokolle erfasst und in das angegebene Verzeichnis. Wenn dieses Verzeichnis nicht vorhanden ist, wird es erstellt. Standardmäßig werden sie in das aktuelle Verzeichnis platziert. Die möglichen generierten Dateien werden zu können: </br>-TpmEvents.evtx</br>-TpmInformation.txt</br>-SRTMBoot.dat</br>-SRTMResume.dat</br>-DRTMBoot.dat</br>-DRTMResume.dat</br>|
|Drivertracing [starten / beenden]|Starten Sie / beenden Sie Sammeln von ablaufverfolgungen der TPM-Treiber. Das Ablaufverfolgungsprotokoll, TPMTRACE.etl, generiert und im aktuellen Verzeichnis abgelegt.|
|Parsetcglogs [-überprüfen (-V)]|Zeigt die analysierte TCG-Protokoll, auch bekannt als die Windows Boot Configuration Log (WBCL). Die aktuellen ereignisbeschreibungen finden Sie auf die [TCG-Website](https://trustedcomputinggroup.org/resource/pc-client-specific-platform-firmware-profile-specification/)unter **Ereignisbeschreibungen**. Wenn die `-validate` flag so festgelegt, überprüft, ob die Werte (Platform Configuration registrieren, PCR) des TPM Werte in das Protokoll übereinstimmen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="tpmtool_examples"></a>Beispiele für

Um die grundlegenden Informationen für das TPM anzuzeigen, geben Sie Folgendes ein:
```
tpmtool getdeviceinformation
```
Um TPM-Protokolle sammeln und im aktuellen Verzeichnis platzieren, geben Sie Folgendes ein:
```
tpmtool gatherlogs
```
TPM-Protokolle erfassen und speichern Sie sie im `C:\Users\Public`, Typ:
```
tpmtool gatherlogs C:\Users\Public
```
Um TPM-Treiber ablaufverfolgungen zu erfassen, geben Sie Folgendes ein:
```
tpmtool drivertracing start
# Run scenario
tpmtool drivertracing stop
```
TCG-Protokoll zu analysieren:
```
tpmtool parsetcglogs
```
So analysieren TCG-Protokoll, und überprüfen die PCRs:
```
tpmtool parsetcglogs -validate
```

## <a name="decoding-error-codes"></a>Decodieren von Fehlercodes

TPM-spezifischen Fehlercodes werden dokumentiert [hier](https://docs.microsoft.com/windows/desktop/com/com-error-codes-6).
