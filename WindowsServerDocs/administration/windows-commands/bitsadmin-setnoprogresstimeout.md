---
title: bitsadmin setnoprogresstimeout
description: 'Windows-Befehls Thema für **bitadmin setnoprogresstimeout** : legt die Zeitspanne (in Sekunden) fest, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 761d0d76a2c70af9d4ad68aa564c1a9816691d0d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380499"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

Legt die Zeitspanne (in Sekunden) fest, die Bits versucht, die Datei zu übertragen, nachdem der erste vorübergehende Fehler aufgetreten ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetNoProgressTimeout <Job> <TimeOutvalue>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|TimeOutValue|Eine Zahl, die in Sekunden dargestellt wird.|

## <a name="remarks"></a>Hinweise

-   Das No Progress Timeout Interval beginnt, wenn beim Auftrag ein vorübergehender Fehler auftritt.
-   Das Timeout Intervall wird beendet oder zurückgesetzt, wenn ein Byte mit Daten erfolgreich übertragen wird.
-   Wenn kein Status Timeout Intervall den Timeout *Wert*überschreitet, wird der Auftrag in einen schwerwiegenden Fehlerzustand versetzt.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Wert No Progress Timeout für den Auftrag *mydownloadjob* auf 20 Sekunden festgelegt.
```
C:\>bitsadmin /SetNoProgressTimeout myDownloadJob 20
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)