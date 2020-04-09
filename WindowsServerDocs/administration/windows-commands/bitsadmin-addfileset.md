---
title: bitsadmin addfileset
description: Windows-Befehls Thema für **bitadmin ADDFILESET**, mit dem dem angegebenen Auftrag eine oder mehrere Dateien hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c4cff7dc8439fe8e1c54d1f5d231d1b487dc70c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850973"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

Fügt dem angegebenen Auftrag eine oder mehrere Dateien hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /addfileset <Job> <TextFile>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| Textfile | Eine Textdatei, in der jede Zeile einen Remote-und einen lokalen Dateinamen enthält. **Hinweis:** Die Namen sind durch Leerzeichen getrennt. Zeilen, die mit einem `#` Zeichen beginnen, werden als Kommentar behandelt. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

```
C:\>bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)