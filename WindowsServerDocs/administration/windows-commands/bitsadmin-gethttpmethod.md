---
title: bitsadmin gethttpmethod
description: Referenz Artikel für den bizadmin gethttpmethod-Befehl, der das HTTP-Verb abruft, das mit dem Auftrag verwendet wird.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 0d96c85aa99330b133954a77ca5584fe2d02cd43
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632031"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

Ruft das HTTP-Verb ab, das mit dem Auftrag verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie das HTTP-Verb für die Verwendung mit dem Auftrag *mydownloadjob*ab:

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
