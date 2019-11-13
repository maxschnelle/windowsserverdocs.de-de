---
title: bitsadmin rawreturn
description: 'Windows-Befehls Thema für **bitionadmin rawreturn** : gibt Daten zurück, die für die-Verarbeitung geeignet sind.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86d769de460538acda696194348980de5752d6d8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380876"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

Gibt Daten zurück, die für die-Verarbeitung geeignet sind.

## <a name="syntax"></a>Syntax

```
bitsadmin /RawReturn
```

## <a name="remarks"></a>Hinweise

Entfernt Zeilen mit Zeilen und Formatierungen aus der Ausgabe.

In der Regel verwenden Sie diesen Befehl in Verbindung mit den Switches **Create** und **Get\\** *, um nur den Wert zu erhalten. Dieser Switch muss vor anderen Schaltern angegeben werden.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Rohdaten für den Status des Auftrags mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /RawReturn /GetState myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)