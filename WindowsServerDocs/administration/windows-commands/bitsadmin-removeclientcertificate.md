---
title: removeclientcertificate für biout admin
description: Windows-Befehls Thema für **bigsadmin removeclientcertificate**, das das Client Zertifikat aus dem Auftrag entfernt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 312226b73b91385436e15c4afbb49df161258768
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123107"
---
# <a name="bitsadmin-removeclientcertificate"></a>removeclientcertificate für biout admin

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

Im folgenden Beispiel wird das Client Zertifikat aus dem Auftrag mit dem Namen *mydownloadjob*entfernt.

```
C:\>bitsadmin /removeclientcertificate myDownloadJob 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)