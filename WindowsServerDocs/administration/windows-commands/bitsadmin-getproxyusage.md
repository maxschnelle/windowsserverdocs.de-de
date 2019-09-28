---
title: bitsadmin getproxyusage
description: 'Windows-Befehls Thema für **bitionadmin getproxyusage** : Ruft die Einstellung für die Proxy Verwendung für den angegebenen Auftrag ab.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ea9a22f4fb35af3436d02d9f23b62ce0888a26b0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381287"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage



Ruft die Proxy Verwendungs Einstellung für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetProxyUsage <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Mögliche Werte sind:
-   Preconfig – verwenden Sie die Internet Explorer-Standardeinstellungen des Besitzers.
-   NO_PROXY – keinen Proxy Server verwenden.
-   Überschreiben – verwenden Sie eine explizite Proxy Liste.
-   Autodetect – die Proxy Einstellungen werden automatisch erkannt.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Proxy Verwendung für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetProxyUsage myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)