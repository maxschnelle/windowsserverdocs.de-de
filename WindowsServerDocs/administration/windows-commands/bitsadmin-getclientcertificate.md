---
title: BI-admin getclientcertificate
description: Windows-Befehls Thema für **BI-admin getclientcertificate**, das das Client Zertifikat aus dem Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c29d5c64fd172cfdd2d5d93c5ed22d519077806
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850763"
---
# <a name="bitsadmin-getclientcertificate"></a>BI-admin getclientcertificate

Ruft das Client Zertifikat aus dem Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird das Client Zertifikat für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getclientcertificate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)