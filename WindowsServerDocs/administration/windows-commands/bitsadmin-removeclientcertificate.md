---
title: bitsadmin removeclientcertificate
description: Referenz Artikel für den Befehl "bizadmin removeclientcertificate", der das Client Zertifikat aus dem Auftrag entfernt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3659f830b9462469762fcd4c7690295073400b1e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927989"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate

Entfernt das Client Zertifikat aus dem Auftrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /removeclientcertificate <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So entfernen Sie das Client Zertifikat aus dem Auftrag *mydownloadjob*:

```
bitsadmin /removeclientcertificate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
