---
title: bitsadmin getclientcertificate
description: Referenz Artikel für den Befehl "bizadmin getclientcertificate", der das Client Zertifikat aus dem Auftrag abruft.
ms.topic: reference
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a2fe63369aab098b012462e063518463047218d
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027828"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate

Ruft das Client Zertifikat aus dem Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie das Client Zertifikat für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getclientcertificate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
