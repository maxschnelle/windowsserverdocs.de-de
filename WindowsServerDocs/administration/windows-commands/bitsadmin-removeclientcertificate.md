---
title: bitsadmin removeclientcertificate
description: Referenz Artikel für den Befehl "bizadmin removeclientcertificate", der das Client Zertifikat aus dem Auftrag entfernt.
ms.topic: reference
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f2c739c1e1b1b3ee31d592adfb17e363dde865bf
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631165"
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
