---
title: bitsadmin getcreationtime
description: 'Thema Windows-Befehle für **bigsadmin getkreationtime** : Ruft die Erstellungszeit für den angegebenen Auftrag ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ea92133c90e20e37e5d281116e91bf1f109e83f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381688"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime



Ruft die Erstellungszeit für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetCreationTime <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Erstellungszeit für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetCreationTime myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)