---
title: bizadmin getvalidationstate
description: Windows-Befehls Thema für **BITSAdmin getvalidationstate**, das den Status der Inhalts Validierung der angegebenen Datei innerhalb des Auftrags meldet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52d7d983cc7858607c350483ed81223d107cee25
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850433"
---
# <a name="bitsadmin-getvalidationstate"></a>bizadmin getvalidationstate

Meldet den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| file_index | Beginnt bei 0. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Status der Inhalts Überprüfung der Datei 2 innerhalb des Auftrags mit dem Namen *mydownloadjob*abgerufen.

```
C:\>bitsadmin /getvalidationstate myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)