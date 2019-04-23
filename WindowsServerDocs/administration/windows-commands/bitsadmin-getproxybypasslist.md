---
title: bitsadmin getproxybypasslist
description: Windows-Befehle Thema **Bitsadmin Getproxybypasslist** -ruft der Proxyumgehungsliste enthalten für den angegebenen Auftrag ab.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 020b8fc0019eb103a0e469258be8705b80dd45de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854111"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

Ruft die Proxyumgehungsliste für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetProxyBypassList <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Die Bypass-Liste enthält den Hostnamen oder IP-Adressen oder beides, sollen, die nicht über einen Proxy geleitet werden. Die Liste kann enthalten "\<lokalen >" auf allen Servern im selben LAN verweisen. Die Liste kann durch Semikolons oder Leerzeichen als Trennzeichen.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft der Proxyumgehungsliste enthalten für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetProxyBypassList myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)