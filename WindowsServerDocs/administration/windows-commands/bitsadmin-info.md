---
title: bitsadmin info
description: Referenz Thema für den Befehl bizadmin Info, mit dem zusammenfassende Informationen zum angegebenen Auftrag angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 904f70c82ab4bcc4fb25f759898674cc719b1954
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717441"
---
# <a name="bitsadmin-info"></a>bitsadmin info

Zeigt zusammenfassende Informationen zum angegebenen Auftrag an.

## <a name="syntax"></a>Syntax

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| /verbose | Optional. Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a>Beispiele

So rufen Sie Informationen zum Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
