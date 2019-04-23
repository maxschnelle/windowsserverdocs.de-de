---
title: bitsadmin takeownership
description: Windows-Befehle Thema **Bitsadmin Takeownership** -ermöglicht es einem Benutzer mit Administratorrechten den Besitz des angegebenen Auftrags zu übernehmen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aedca49e43588ab51f84477cf8690cf58486c3cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827841"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership



Ermöglicht Benutzern mit Administratorrechten den Besitz des angegebenen Auftrags zu übernehmen.

## <a name="syntax"></a>Syntax

```
bitsadmin /TakeOwnership <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel übernimmt den Besitz des Auftrags mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /TakeOwnership myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)