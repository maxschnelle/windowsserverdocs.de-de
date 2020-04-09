---
title: bitsadmin getdescription
description: Windows-Befehls Thema für **bigsadmin GetDescription**, das die Beschreibung des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ff1638cf634d76001042691fd890dfe41f9ae0b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850723"
---
# <a name="bitsadmin-getdescription"></a>bitsadmin getdescription

Ruft die Beschreibung des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getdescription <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Beschreibung für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getdescription myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)