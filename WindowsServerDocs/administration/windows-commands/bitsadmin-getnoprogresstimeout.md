---
title: bitsadmin getnoprogresstimeout
description: 'Thema Windows-Befehle für **bizadmin getnoprogresstimeout** : Ruft die Zeitspanne (in Sekunden) ab, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7dcc0e445f4cae25c27f5ff70c73f4f2f23975aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381504"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout



Ruft die Zeitdauer in Sekunden ab, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetNoProgressTimeout <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Wert für den Status Timeout für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetNoProgressTimeout myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)