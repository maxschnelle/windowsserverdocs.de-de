---
title: Bitsadmin setsecurityflags
description: Windows-Befehle Thema **Bitsadmin Setsecurityflags** -legt-flags für HTTP, die zu bestimmen, ob BITS sollte überprüfen Sie die Certificate Revocation List, bestimmte Zertifikatfehler ignoriert und definieren die Richtlinie, um beim verwenden ein Servers leitet die HTTP-Anforderung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a7f74146a26314ddb4fa92f85e5a40267d0f0d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858621"
---
# <a name="bitsadmin-setsecurityflags"></a>Bitsadmin setsecurityflags



Legt die Flags für HTTP, die bestimmen, ob BITS überprüfen Sie die Certificate Revocation List, bestimmte Zertifikatfehler ignoriert und definieren Sie die Richtlinie zu verwenden, wenn ein Server leitet die HTTP-Anforderung sollte fest. Der Wert ist eine Ganzzahl ohne Vorzeichen.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetSecurityFlags <Job> <Value>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Wert|Finden Sie unter "Hinweise"|

## <a name="remarks"></a>Hinweise

Die **Wert** Parameter kann eine oder mehrere der folgenden Benachrichtigungsflags, die enthalten.

|Aktion|Binäre Darstellung|
|------|---------------------|
|Aktivieren der CRL-Prüfung|Legen Sie das unwichtigste bit|
|Ignorieren von ungültiger allgemeinen Namen im Serverzertifikat|Legen Sie das 2. Bit von rechts|
|Ungültiges Datum im Serverzertifikat ignorieren|Legen Sie das 3rd Bit von rechts|
|Ignorieren von ungültiger Zertifizierungsstelle im Serverzertifikat|Legen Sie das 4. Bit von rechts|
|Ungültige Verwendung des Zertifikats ignorieren|Legen Sie das 5. Bit von rechts|
|Richtlinie zur konsolenumleitung|Gesteuert durch die 9., 11. Bits von rechts</br>0,0,0 - umleitungen automatisch zulässig sein werden.</br>0,0,1 - remote-Namen in der Schnittstelle IBackgroundCopyFile wird aktualisiert werden, im Falle eine Umleitung.</br>0,1,0 - BITS schlägt den Auftrag fehl, wenn eine Umleitung erfolgt.|
|Umleitung von HTTPS-auf HTTP zulassen|Legen Sie das am 12. Bit von rechts|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Sicherheitsflags zu einer CRL-Prüfung für den Auftrag mit dem Namen *MyJob*.
```
C:\>bitsadmin /SetSecurityFlags myJob 0x0001
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)