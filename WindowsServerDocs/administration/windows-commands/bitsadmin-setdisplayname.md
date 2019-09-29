---
title: bitsadmin setdisplayname
description: 'Windows-Befehls Thema für **bitadmin setdisplayname** : legt den anzeigen amen des angegebenen Auftrags fest.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 10a5607eb26f8199ec415a4cec17d03015a26bcd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380631"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname



Legt den anzeigen amen des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|DisplayName|Text, der für den anzeigen amen des angegebenen Auftrags verwendet wird.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Anzeige Name für den Auftrag mit dem Namen *mydownloadjob* auf *myDownloadJob2*festgelegt.
```
C:\>bitsadmin /SetDisplayName myDownloadJob "Download Music Job"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)