---
title: bitsadmin removeclientcertificate
description: Referenz Artikel für den Befehl "bizadmin removeclientcertificate", der das Client Zertifikat aus dem Auftrag entfernt.
ms.topic: reference
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a447354a309d16ed75c89c586c8edabd2eadb528
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026428"
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
