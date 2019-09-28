---
title: BI-admin-Cache und ' abtexpirationtime '
description: 'Windows-Befehle-Thema für den **bitadmin-Cache und setexpirationtime** : legt die Ablaufzeit für den Cache fest.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 386c6659e4410b41669ade39d8af97829d81a1cb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381918"
---
>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="bitsadmin-cache-and-setexpirationtime"></a>BI-admin-Cache und ' abtexpirationtime '
Legt die Ablaufzeit für den Cache fest.
## <a name="syntax"></a>Syntax
```
bitsadmin /Cache /SetExpirationtime secs
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Sekunden|Die Anzahl der Sekunden bis zum Ablauf des Caches.|
## <a name="BKMK_examples"></a>Beispiele
Im folgenden Beispiel läuft der Cache in 60 Sekunden ab.
```
C:\>bitsadmin /Cache / SetExpirationtime 60
```
## <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
