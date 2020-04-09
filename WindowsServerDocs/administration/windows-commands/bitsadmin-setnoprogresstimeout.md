---
title: bitsadmin setnoprogresstimeout
description: Windows-Befehls Thema für bistiadmin setnoprogresstimeout, mit dem die Zeitspanne (in Sekunden) festgelegt wird, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 544a6c73f29684bc4091ec05fa28016fbc718bb2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849353"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

Legt die Zeitspanne (in Sekunden) fest, die Bits versucht, die Datei zu übertragen, nachdem der erste vorübergehende Fehler aufgetreten ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNoProgressTimeout <Job> <TimeOutvalue>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|TimeOutValue|Eine Zahl, die in Sekunden dargestellt wird.|

## <a name="remarks"></a>Hinweise

-   Das No Progress Timeout Interval beginnt, wenn beim Auftrag ein vorübergehender Fehler auftritt.
-   Das Timeout Intervall wird beendet oder zurückgesetzt, wenn ein Byte mit Daten erfolgreich übertragen wird.
-   Wenn kein Status Timeout Intervall den Timeout *Wert*überschreitet, wird der Auftrag in einen schwerwiegenden Fehlerzustand versetzt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Wert No Progress Timeout für den Auftrag *mydownloadjob* auf 20 Sekunden festgelegt.
```
C:\>bitsadmin /SetNoProgressTimeout myDownloadJob 20
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)