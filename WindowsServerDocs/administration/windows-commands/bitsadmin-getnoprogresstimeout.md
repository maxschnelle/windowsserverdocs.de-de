---
title: bitsadmin getnoprogresstimeout
description: Windows-Befehle Thema **Bitsadmin Getnoprogresstimeout** -Ruft die Zeitdauer in Sekunden, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler auftritt.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9563b68b8012a49471b56e3b8f2fbd60d1c69756
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850801"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout



Ruft die Zeitdauer in Sekunden, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler auftritt.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetNoProgressTimeout <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Status-Timeoutwert für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetNoProgressTimeout myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)