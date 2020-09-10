---
title: bitsadmin getnotifyinterface
description: Referenz Artikel für den bizadmin getnotifyinterface-Befehl, der bestimmt, ob ein anderes Programm eine com-Rückruf Schnittstelle für den angegebenen Auftrag registriert hat.
ms.topic: reference
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 563cdf103ce60fc13f0455caea98e30f9e2e03e4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631890"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

Bestimmt, ob ein anderes Programm eine com-Rückruf Schnittstelle (die Benachrichtigungs Schnittstelle) für den angegebenen Auftrag registriert hat.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

#### <a name="output"></a>Output

Mit der Ausgabe für diesen Befehl wird entweder, **registriert** oder **nicht registriert**angezeigt.

> [!NOTE]
> Das Programm, das die Rückruf Schnittstelle registriert hat, kann nicht bestimmt werden.

## <a name="examples"></a>Beispiele

So rufen Sie die Benachrichtigungs Schnittstelle für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getnotifyinterface myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
