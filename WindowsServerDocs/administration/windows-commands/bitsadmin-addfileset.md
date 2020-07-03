---
title: bitsadmin addfileset
description: Referenz Artikel für den bizadmin-Befehl ADDFILESET, mit dem dem angegebenen Auftrag eine oder mehrere Dateien hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 861186dfc7ba1a230e1df05c98378d27bfff26b1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927089"
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
