---
title: bitsadmin getdisplayname
description: 'Windows-Befehls Thema für **bizadmin GetDisplayName** : Ruft den anzeigen amen des angegebenen Auftrags ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 229bd245f9e810fc6aeb856bbfba253b9ab8a9f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381630"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname



Ruft den anzeigen amen des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetDisplayName <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Anzeige Name für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetDisplayName myDownloadJob
```
Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)