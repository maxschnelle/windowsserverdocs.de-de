---
title: 'BI-admin getproxylist: Ruft die Proxy Liste für den angegebenen Auftrag ab.'
description: Referenz Thema für den bizadmin getproxylist-Befehl, der die Proxy Liste für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a92703d83cc872204d3dc488c15d703dfd50a780
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717658"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

Ruft die durch Trennzeichen getrennte Liste der Proxy Server ab, die für den angegebenen Auftrag verwendet werden sollen.

## <a name="syntax"></a>Syntax

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen der Proxy Liste für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
