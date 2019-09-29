---
title: 'BI-admin getproxylist: Ruft die Proxy Liste für den angegebenen Auftrag ab.'
description: 'Windows-Befehls Thema für **bigsadmin getproxylist** : Ruft die Proxy Liste für den angegebenen Auftrag ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6f176d268c816725b183da0a948afcb25272b2fb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381312"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

Ruft die Proxy Liste für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetProxyList <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Die Proxy Liste ist die Liste der zu verwendenden Proxy Server. Die Liste ist durch Kommas getrennt.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Proxy Liste für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetProxyList myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)