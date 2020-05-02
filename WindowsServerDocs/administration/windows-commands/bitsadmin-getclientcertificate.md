---
title: bitsadmin getclientcertificate
description: Referenz Thema für den bizadmin getclientcertificate-Befehl, mit dem das Client Zertifikat aus dem Auftrag abgerufen wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d2582950dd02ca1880e4765fb974c83c423b22bb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718123"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate

Ruft das Client Zertifikat aus dem Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie das Client Zertifikat für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getclientcertificate myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
