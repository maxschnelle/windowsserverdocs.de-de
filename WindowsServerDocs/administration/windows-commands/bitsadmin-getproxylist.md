---
title: Bitsadmin Getproxylist - Ruft die Liste der Proxy für den angegebenen Auftrag ab.
description: Windows-Befehle Thema **Bitsadmin Getproxylist** -Ruft die Proxyliste für den angegebenen Auftrag ab.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: e8c3ffb1e425552cda5b14a00287817ace77a90f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840511"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

Ruft die Liste der Proxy für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetProxyList <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Die Proxyliste ist die Liste der zu verwendenden Proxyserver an. Die Liste ist durch Kommas getrennt.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Liste der Proxy für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetProxyList myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)