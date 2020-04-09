---
title: biout admin getcustomheaders
description: Windows-Befehls Thema für **BI-admin getcustomheaders**, das die benutzerdefinierten HTTP-Header aus dem Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80a3d1230fd541f0b986434ce373da4c8bb0c761
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850733"
---
# <a name="bitsadmin-getcustomheaders"></a>biout admin getcustomheaders

Ruft die benutzerdefinierten HTTP-Header aus dem Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die benutzerdefinierten Header für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getcustomheaders myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)