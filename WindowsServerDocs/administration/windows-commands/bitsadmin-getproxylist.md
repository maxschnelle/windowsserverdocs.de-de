---
title: 'BI-admin getproxylist: Ruft die Proxy Liste für den angegebenen Auftrag ab.'
description: Referenz Artikel für den bizadmin getproxylist-Befehl, der die Proxy Liste für den angegebenen Auftrag abruft.
ms.topic: reference
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4d4cefcb27a9aa18b06bc588d08aba2f2f810636
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631744"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
