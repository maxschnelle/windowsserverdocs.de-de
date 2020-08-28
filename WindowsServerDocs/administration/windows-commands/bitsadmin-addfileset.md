---
title: bitsadmin addfileset
description: Referenz Artikel für den bizadmin-Befehl ADDFILESET, mit dem dem angegebenen Auftrag eine oder mehrere Dateien hinzugefügt werden.
ms.topic: reference
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b9b93f38f3604c4f0a9fcaf886d74356d355086
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033708"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

Fügt dem angegebenen Auftrag eine oder mehrere Dateien hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /addfileset <job> <textfile>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
