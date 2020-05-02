---
title: bitsadmin addfileset
description: Referenz Thema für den bizadmin-Befehl ADDFILESET, mit dem dem angegebenen Auftrag eine oder mehrere Dateien hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d610c1330818cf820923b6d4f2e3555dc477444b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718479"
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
| Textfile | Eine Textdatei, in der jede Zeile einen Remote-und einen lokalen Dateinamen enthält. **Hinweis:** Namen müssen durch Leerzeichen getrennt werden. Zeilen, die mit `#` einem Zeichen beginnen, werden als Kommentar behandelt. |

## <a name="examples"></a>Beispiele

```
bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
