---
title: bitsadmin setnoprogresstimeout
description: Windows-Befehle Thema **Bitsadmin Setnoprogresstimeout** -legt die Zeitspanne in Sekunden, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler auftritt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45dd8a7ddfae877984a98db66c742e0af4d18f0d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873771"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

Legt die Zeitspanne in Sekunden an, die BITS versucht wird, um die Datei zu übertragen, nachdem der erste vorübergehende Fehler tritt auf, fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNoProgressTimeout <Job> <TimeOutvalue>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|TimeOutvalue|Eine Zahl, ausgedrückt in Sekunden.|

## <a name="remarks"></a>Hinweise

-   Das keine Bearbeitung Timeoutintervall beginnt, wenn es sich bei der Auftrag einen vorübergehenden Fehler auftritt.
-   Das Timeoutintervall beendet oder wird zurückgesetzt, wenn ein Byte an Daten erfolgreich übertragen wurde.
-   Wenn kein Status-Timeout-Intervall überschreitet die *TimeOutvalue*, und klicken Sie dann der Auftrag in ein schwerwiegender Fehlerzustand versetzt wird.

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird der kein Fortschritt Timeoutwert für den Auftrag mit dem Namen *MyDownloadJob* auf 20 Sekunden
```
C:\>bitsadmin /SetNoProgressTimeout myDownloadJob 20
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)