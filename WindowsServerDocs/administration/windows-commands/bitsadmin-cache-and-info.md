---
title: bizadmin-Cache und Info
description: Windows-Befehls Artikel für den **bistiadmin-Cache und Informationen**, der einen bestimmten Cache Eintrag absichert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e9c6ce1eb972a76408483b8a27a3abca5500e56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850893"
---
# <a name="bitsadmin-cache-and-info"></a>bizadmin-Cache und Info

Sichert einen bestimmten Cache Eintrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>Parameter

| Paramreter | Beschreibung |
| -------------- | -------------- |
| Datensatz | Die GUID, die dem Cache Eintrag zugeordnet ist. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Cache Eintrag mit dem RecordID-Wert {6511sb02-E195-40A2-B595-e8e2f 8F 47702} Abbilder.

```
C:\>bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)