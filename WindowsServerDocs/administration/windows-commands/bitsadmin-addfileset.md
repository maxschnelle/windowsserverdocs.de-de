---
title: bitsadmin addfileset
description: Referenz Artikel für den bizadmin-Befehl ADDFILESET, mit dem dem angegebenen Auftrag eine oder mehrere Dateien hinzugefügt werden.
ms.topic: reference
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e3e736fe6dcc96b7f81b3b249257f0d23dd78c9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632716"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

Fügt dem angegebenen Auftrag eine oder mehrere Dateien hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /addfileset <job> <textfile>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| Textfile | Eine Textdatei, in der jede Zeile einen Remote-und einen lokalen Dateinamen enthält. **Hinweis:** Namen müssen durch Leerzeichen getrennt werden. Zeilen, die mit einem Zeichen beginnen, `#` werden als Kommentar behandelt. |

## <a name="examples"></a>Beispiele

```
bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
