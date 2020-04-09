---
title: bitsadmin takeownership
description: Windows-Befehls Thema für bigsadmin TakeOwnership, mit dem ein Benutzer mit Administratorrechten den Besitz des angegebenen Auftrags übernimmt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a2c0bfc1fcb1606102aece76129c49aad701ead
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849023"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

Ermöglicht einem Benutzer mit Administratorrechten, den Besitz des angegebenen Auftrags zu übernehmen.

## <a name="syntax"></a>Syntax

```
bitsadmin /TakeOwnership <Job>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Besitz des Auftrags mit dem Namen *mydownloadjob*angenommen.
```
C:\>bitsadmin /TakeOwnership myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)