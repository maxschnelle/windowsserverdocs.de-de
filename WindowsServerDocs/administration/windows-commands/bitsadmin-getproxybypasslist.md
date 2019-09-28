---
title: bitsadmin getproxybypasslist
description: 'Windows-Befehls Thema für **bigsadmin getproxybypasslist** : Ruft die Proxy Umgehungs Liste für den angegebenen Auftrag ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87cc131402707eac40329750e98218ec52083b94
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381417"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

Ruft die Proxy Umgehungs Liste für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetProxyBypassList <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Die Umgehungs Liste enthält die Hostnamen oder IP-Adressen, die nicht über einen Proxy weitergeleitet werden sollen. Die Liste kann "\<local >" enthalten, um auf alle Server im gleichen LAN zu verweisen. Die Liste kann ein Semikolon oder ein Leerzeichen sein.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Proxy Umgehungs Liste für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetProxyBypassList myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)