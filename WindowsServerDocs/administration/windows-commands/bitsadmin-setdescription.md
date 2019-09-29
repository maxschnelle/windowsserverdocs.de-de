---
title: bitsadmin Beschreibung
description: 'Windows-Befehls Thema für **bitadmin setDescription** : legt die Beschreibung des angegebenen Auftrags fest.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d140ee9d575828a1a4d536073e468c9b4e56799f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380929"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin Beschreibung



Legt die Beschreibung des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetDescription <Job> <Description>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Beschreibung|Der Text, der zur Beschreibung des Auftrags verwendet wird.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Beschreibung für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /SetDescription myDownloadJob "Music Downloads"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)