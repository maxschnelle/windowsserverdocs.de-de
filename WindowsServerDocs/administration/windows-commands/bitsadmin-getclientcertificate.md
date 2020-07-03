---
title: bitsadmin getclientcertificate
description: Referenz Artikel für den Befehl "bizadmin getclientcertificate", der das Client Zertifikat aus dem Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5113214f106aea21b1b13f08cc08002237730daf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928517"
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
