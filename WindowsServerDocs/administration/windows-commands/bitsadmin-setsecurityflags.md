---
title: bitadmin setsecurityflags
description: 'Windows-Befehls Thema für **BITSAdmin setsecurityflags** : Legt Flags für http fest, die bestimmen, ob Bits die Zertifikat Sperr Liste überprüfen, bestimmte Zertifikat Fehler ignorieren und die Richtlinie definieren, die verwendet werden soll, wenn ein Server die HTTP-Anforderung umleitet.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: acc5a64ef7c82b14e6815b6d51dda5ea4700dcad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380408"
---
# <a name="bitsadmin-setsecurityflags"></a>bitadmin setsecurityflags



Legt Flags für http fest, die bestimmen, ob Bits die Zertifikat Sperr Liste überprüfen soll, bestimmte Zertifikat Fehler ignorieren und die Richtlinie definieren, die verwendet werden soll, wenn ein Server die HTTP-Anforderung umleitet. Der Wert ist eine ganze Zahl ohne Vorzeichen.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetSecurityFlags <Job> <Value>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Wert|Siehe Hinweise|

## <a name="remarks"></a>Hinweise

Der **value** -Parameter kann eine oder mehrere der folgenden Benachrichtigungs Flags enthalten.

|Aktion|Binäre Darstellung|
|------|---------------------|
|Überprüfung der CRL aktivieren|Legen Sie das unwichtigste Bit fest.|
|Ungültigen allgemeinen Namen im Serverzertifikat ignorieren|Legen Sie das zweite Bit von rechts fest.|
|Ungültiges Datum im Serverzertifikat ignorieren|Legen Sie das dritte Bit von rechts fest.|
|Ungültige Zertifizierungsstelle im Serverzertifikat ignorieren|Legen Sie das 4. Bit von der rechten Seite fest.|
|Ungültige Verwendung des Zertifikats ignorieren|Legen Sie das 5. Bit von der rechten Seite fest.|
|Umleitungs Richtlinie|Gesteuert von den 9. bis 11. Bits von rechts</br>0, 0, 0-Umleitungen werden automatisch zugelassen.</br>0, 0, 1: der Remote Name in der ibackgroundcopyfile-Schnittstelle wird aktualisiert, wenn eine Umleitung erfolgt.</br>0, 1, 0-Bits schlagen den Auftrag fehl, wenn eine Umleitung erfolgt.|
|Umleitung von HTTPS zu http zulassen|Legen Sie das 12. Bit von der rechten Seite fest.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die sicherheitsflags so festgelegt, dass eine CRL-Prüfung für den Auftrag mit dem Namen *MyJob*aktiviert wird.
```
C:\>bitsadmin /SetSecurityFlags myJob 0x0001
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)