---
title: BI-admin getclientcertificate
description: Windows-Befehls Thema für **bigsadmin getclientcertificate** -Ruft das Client Zertifikat aus dem Auftrag ab.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 613feafb442f63513d34e9038647c4dbeb278630
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381716"
---
# <a name="bitsadmin-getclientcertificate"></a>BI-admin getclientcertificate



Ruft das Client Zertifikat aus dem Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetClientCertificate <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird das Client Zertifikat für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin / GetClientCertificate myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)