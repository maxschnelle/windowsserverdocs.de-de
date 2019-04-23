---
title: bitsadmin getproxyusage
description: Windows-Befehle Thema **Bitsadmin Getproxyusage** -Ruft die Proxy-Verwendung-Einstellung für den angegebenen Auftrag ab.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20ba418b8dfcf3d96d9b20b22e53797a232a13f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863881"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage



Ruft die Einstellung für den Proxy für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetProxyUsage <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Die möglichen Werte sind:
-   VORKONFIGURIERTE – des Besitzers der Standardeinstellungen von Internet Explorer verwenden.
-   "No_proxy" – verwenden Sie einen Proxyserver nicht.
-   Außer Kraft setzen, verwenden Sie eine explizite Proxyliste.
-   AUTOERMITTLUNG – die Proxyeinstellungen automatisch erkennen.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Proxyverwendung für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetProxyUsage myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)