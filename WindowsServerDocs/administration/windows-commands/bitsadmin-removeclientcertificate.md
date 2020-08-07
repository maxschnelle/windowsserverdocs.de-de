---
title: bitsadmin removeclientcertificate
description: Referenz Artikel für den Befehl "bizadmin removeclientcertificate", der das Client Zertifikat aus dem Auftrag entfernt.
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f4b2a17a08f3c2b224d90237975841644ea16ecd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893376"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate

Entfernt das Client Zertifikat aus dem Auftrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /removeclientcertificate <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
